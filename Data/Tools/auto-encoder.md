---
title: Simple Auto-Encoder
description: 
published: true
date: 2023-07-14T02:14:42.272Z
tags: model, deep-learning, tool, code-sample, dl
editor: markdown
dateCreated: 2023-07-14T02:14:42.272Z
---

# Simple Auto-Encoder
## Data Loader
```python
import torch
import matplotlib.pyplot as plt

tn_tensor = tn_train_vector.toarray().tolist()
tn_train = torch.utils.data.TensorDataset(torch.tensor(tn_tensor))
### test dataset 생략 ###

loader = torch.utils.data.DataLoader(tn_train)
```

## Models
```python
class AE(torch.nn.Module):
    def __init__(self):
        super().__init__()
         
        # Building an linear encoder with Linear
        # layer followed by Relu activation function
        # input dim : 125
        self.encoder = torch.nn.Sequential(
            torch.nn.Linear(125, 128),
            torch.nn.ReLU(),
            torch.nn.Linear(128, 64),
            torch.nn.ReLU(),
            torch.nn.Linear(64, 36),
            torch.nn.ReLU(),
            torch.nn.Linear(36, 18),
            torch.nn.ReLU(),
            torch.nn.Linear(18, 9)
        )
         
        # Building an linear decoder with Linear
        # layer followed by Relu activation function
        # The Sigmoid activation function
        # outputs the value between 0 and 1
        self.decoder = torch.nn.Sequential(
            torch.nn.Linear(9, 18),
            torch.nn.ReLU(),
            torch.nn.Linear(18, 36),
            torch.nn.ReLU(),
            torch.nn.Linear(36, 64),
            torch.nn.ReLU(),
            torch.nn.Linear(64, 128),
            torch.nn.ReLU(),
            torch.nn.Linear(128, 125),
            torch.nn.Sigmoid()
        )
    def forward(self, x):
        encoded = self.encoder(x)
        decoded = self.decoder(encoded)
        return decoded
```

## init model & set params
```python
# Model Initialization
model = AE()
 
# Validation using MSE Loss function
loss_function = torch.nn.MSELoss()
 
# Using an Adam Optimizer with lr = 0.1
optimizer = torch.optim.Adam(model.parameters(),
                             lr = 1e-1,
                             weight_decay = 1e-8)
```

## Train Function
```python
def train_one_epoch(epoch_index):
    running_loss = 0.
    last_loss = 0.

    # Here, we use enumerate(training_loader) instead of
    # iter(training_loader) so that we can track the batch
    # index and do some intra-epoch reporting
    for i, data in enumerate(loader):
        # Every data instance is an input + label pair
        vec = data[0]

        # Zero your gradients for every batch!
        optimizer.zero_grad()

        # Make predictions for this batch
        outputs = model(vec)

        # Compute the loss and its gradients
        loss = loss_function(outputs, vec)
        loss.backward()

        # Adjust learning weights
        optimizer.step()

        # Gather data and report
        running_loss += loss.item()
        if i % 1000 == 999:
            last_loss = running_loss / 1000 # loss per batch
            print('  batch {} loss: {}'.format(i + 1, last_loss))
            running_loss = 0.

    return last_loss
```

## RUN
```python
epoch_number = 0
EPOCHS = 2

for epoch in range(EPOCHS):
    print('EPOCH {}:'.format(epoch))

    # Make sure gradient tracking is on, and do a pass over the data
    model.train(True)
    avg_loss = train_one_epoch(epoch)


    running_vloss = 0.0
    # Set the model to evaluation mode, disabling dropout and using population
    # statistics for batch normalization.
    model.eval()

    # Disable gradient computation and reduce memory consumption.
    """
    with torch.no_grad():
        for i, vdata in enumerate(validation_loader):
            vinputs, vlabels = vdata
            voutputs = model(vinputs)
            vloss = loss_function(voutputs, vlabels)
            running_vloss += vloss

    avg_vloss = running_vloss / (i + 1)
    print('LOSS train {} valid {}'.format(avg_loss, avg_vloss))

    # Track best performance, and save the model's state
    if avg_vloss < best_vloss:
        best_vloss = avg_vloss
    """
    #model_path = 'model_{}_{}'.format(timestamp, epoch_number)
    torch.save(model.state_dict(), './model.h5')
```

## Get Embedded Vector
```python
di = next( iter(loader) )
model.encoder(di[0]).tolist()[0]
```

## USE Saved Model
```python
saved_model = AE()
saved_model.load_state_dict(torch.load('./model.h5'))
```