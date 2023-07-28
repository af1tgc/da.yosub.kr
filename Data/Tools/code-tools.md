---
title: Code Tools
description: 
published: true
date: 2023-07-28T01:49:32.204Z
tags: python, pandas, tool, code-sample
editor: markdown
dateCreated: 2023-07-14T01:43:38.430Z
---

# DataFrame
## Delete Columns
```python
cols = ['A', 'B', 'C', 'D']
df = df.drop(columns=cols)
```

## Get 'NaN' (included or exclude) Data
````python
ndf = df[~df['cs1'].isna()]
ndf = df[df['cs1'].isna()]
````

## Expands Field Limit Size
````python
import sys
import csv

csv.field_size_limit(sys.maxsize)
````

## df.apply
````python
def replace_func(x):
    x = str(x)
    x = x.replace('txt', ' ')
    x = re.sub(r"\n\r\t.+", '', x)
    
    return x

df['ncol'] = df.apply(lambda x : replace_func(x['col']), axis = 1)
````

## Drop Columns if Exists
```python
df = pd.DataFrame({'row_num':[1,2], 'w':[3,4]})
df = df.drop(['row_num','start_date','end_date','symbol'], axis=1, errors='ignore')
print (df)
   w
0  3
1  4
```

## Read All csv Files as 1 DF
```python
import pandas as pd
import glob
import os

path = r'C:\DRO\DCL_rawdata_files' # use your path
all_files = glob.glob(os.path.join(path , "/*.csv"))

li = []

for filename in all_files:
    df = pd.read_csv(filename, index_col=None, header=0)
    li.append(df)

frame = pd.concat(li, axis=0, ignore_index=True)
```

Or, with attribution to a comment from Sid.

```
all_files = glob.glob(os.path.join(path, "*.csv"))

df = pd.concat((pd.read_csv(f) for f in all_files), ignore_index=True)
```

## Get Rows with Conditional
```python
df_diff = df[df['sim'] < 0.1 ]
```

# scipy
## np.array to csr_matrix
```python
from scipy import sparse
csr = sparse.csr_matrix(nparr)
```


# Natives
## Get Files
````python
dir = f'{os.path.dirname(os.getcwd())}/data'

for _, _, files in os.walk(dir):
    for f in files:
        tmp = pd.read_csv(f'{dir}/{f}', encoding='utf-8-sig', sep=',', engine='python')
        df = df.append(tmp)
````

# Regex
## IP
````regex
[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}
````

## Special Chars
````regex
[!@#$%^&*+()\{\};:,./_<>?\|`~=\[\]-]
````

## Non-Eng Chars
````regex
[^A-Za-z0-9]+
````

# ML
## TF-IDF
```python
from sklearn.feature_extraction.text import TfidfVectorizer

nl_utf8 = [str(x).encode('utf-8-sig') for x in nl_raw]
# nl_utf8

vectorizer_tn = TfidfVectorizer(lowercase=False, encoding='utf-8-sig', min_df=0.0001, max_df=0.9999) # token_pattern='(?u)\\b\\w+\\b', min_df=0.001, max_df=0.985)

# fit model & feature_names (version dependency)
TNX = vectorizer_tn.fit_transform(nl_utf8)
TN_feature_names = vectorizer_tn.get_feature_names_out()

# use model
targe_nl = df['c'].to_list()
NX = vectorizer_tn.transform([str(x).encode('utf-8-sig') for x in target_nl])
# -> csr matrix
```

```python
# result -> df
pd.DataFrame(NX.toarray(), columns=vectorizer_tn.get_feature_names_out())
```

## KMeans
### elbow
```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

def elbow(vector):
    sse = []

    for i in range(1, 25):
        kmeans = KMeans(n_clusters=i).fit(vector)
        sse.append(kmeans.inertia_)

    return sse

sse = elbow(NX) # TF-IDF Results

plt.plot(range(1, 25), sse, marker='o')
plt.show()
```

## Word2Vec
```python
from nltk.tokenize import sent_tokenize, word_tokenize
from gensim.models import Word2Vec
from gensim.models import KeyedVectors

result = [word_tokenize(sentence) for sentence in df['real_name'].tolist()]
model = Word2Vec(sentences=result, vector_size=100, window=5, min_count=5, workers=4, sg=0)

# w2v result with sentense (average)
embedded_vector = []
for r in result:
    svector = []
    for r in result[0]:
        svector.append(model.wv[r])

    embedded_vector.append(np.average(svector, axis=0))

embedded_vector[0]
```














