---
title: Learning Equality - Curriculum Recommendations
description: Enhance learning by matching K-12 content to target topics
published: true
date: 2023-04-03T09:44:31.005Z
tags: data, data-science, model, recommendation
editor: markdown
dateCreated: 2023-04-03T05:03:33.789Z
---

# Overview
## Goal of the Competition
- `K-12` 교육 라이브러리 데이터로 교육 컨텐츠를 일치시키는 Competitions.
- 다양한 교육 주제가 있음.
  - `과학`, `기술`, `공학`, `수학`, 등

## Context
- 교육 커리큘럼은 국가마다 모두 다르기 때문에 표준을 수립하기 쉽지 않음.
- 새로운 자료가 식별되면, 국가별 커리큘럼에 맞추기 위한 모델이 필요함.
- Learning Equality는 개방형 교육 자료의 생성, 적응 및 배포를 지원하고 인터넷 엑세스가 없는 전 세계 37%의 사람들의 교육 및 학습을 지원하도록 Kolibri를 개발함.
- UNHCR은 파트너이며, 소속 교사 및 난민 학습자에게 디지털 학습 리소스를 제공할 수 있도록 이 문제를 제시함.
- 따라서, 이들에게 더 나은 학습 자료를 제시하는 것이 본 Competition의 목표임.

# Data
## Dataset Description
- 교육 자료는 사용자가 주제 트리를 생성하고, 이후 자료를 업로드하는 방식으로 구성
  - 토픽 분기 트리 예시
  ```
  Secondary Education >> Ordinary Level >> Mathematics >> Further Learning >> Activities >> Trigonometry
  ```
- 이 주제 트리에 가장 fit한 콘텐츠 항목을 예측해야함.
  - 즉, 주제에 포함될 가능성이 있는 컨텐츠 항목을 큐레이터에게 추천하는 것임

## Files and Fields
- `topics.csv` - 데이터 세트의 각 주제에 대한 행을 포함합니다. 이러한 주제는 "채널"로 구성되며 각 채널에는 단일 "주제 트리"("상위" 참조를 통해 이동할 수 있음)가 포함됩니다. 스코어링에 사용되는 숨겨진 데이터 세트에는 공개 버전에 없는 추가 주제가 포함되어 있습니다. sample_submission.csv에 나열된 주제에 대한 예측만 제출해야 합니다.
  - id - 이 주제에 대한 고유 식별자입니다.
  - title - 이 주제에 대한 제목 텍스트입니다.
  - description - 설명 텍스트(비어 있을 수 있음)
  - channel - 이 주제가 속한 채널(즉, 주제 트리)입니다.
  - category - 주제의 출처를 설명합니다.
    - source - 구조는 원본 콘텐츠 작성자가 제공했습니다(예: Khan Academy에서 가져온 주제 트리). 이 카테고리의 테스트 세트에 항목이 없습니다.
    - aligned - 구조는 국가 커리큘럼 또는 기타 대상 분류법에서 가져오며 콘텐츠는 여러 소스에서 정렬됩니다.
    - supplemental - 어느 정도 정렬되었지만 채널과 동일한 수준의 세분성 또는 충실도가 없는 채널입니다 aligned.
  - language - 주제에 대한 언어 코드. 제목이나 설명의 겉보기 언어와 항상 일치하지 않을 수 있지만 연결된 콘텐츠 항목의 언어와 항상 일치합니다.
  - parent - 이 주제를 포함하는 주제의 ID입니다(있는 경우). 주제가 해당 채널의 루트 노드인 경우 이 필드는 비어 있습니다.
  - level - 토픽 트리 내에서 이 토픽의 깊이. 레벨 0은 루트 노드임을 의미합니다(따라서 해당 제목은 채널의 제목임).
  - has_content - 이 주제와 관련된 콘텐츠 항목이 있는지 여부. 대부분의 콘텐츠는 리프 주제와 상관 관계가 있지만 일부 비리프 주제도 콘텐츠 상관 관계가 있습니다.
- `content.csv` - 데이터 세트의 각 콘텐츠 항목에 대한 행을 포함합니다. 스코어링에 사용되는 숨겨진 데이터 세트에는 공개 버전에 없는 추가 콘텐츠 항목이 포함되어 있습니다. 이러한 추가 콘텐츠 항목은 테스트 집합의 항목과만 연관됩니다. 일부 콘텐츠 항목은 주제와 관련이 없을 수 있습니다.
  - id - 이 콘텐츠 항목의 고유 식별자입니다.
  - title - 이 콘텐츠 항목의 제목 텍스트입니다.
  - description - 설명 텍스트. 비어 있을 수 있습니다.
  - language - 이 콘텐츠 항목의 언어를 나타내는 언어 코드입니다.
  - kind - 이 항목이 나타내는 콘텐츠 형식을 다음 중 하나로 설명합니다.
    - document(텍스트는 PDF 또는 EPUB 파일에서 추출됨)
    - video(가능한 경우 자막 파일에서 텍스트가 추출됨)
    - exercise(텍스트는 질문/답변에서 추출됨)
    - audio(텍스트 없음)
    - html5(HTML 소스에서 텍스트 추출)
  - text - 사용 가능한 경우 및 라이선스가 허용된 경우 추출된 텍스트 콘텐츠(콘텐츠 항목의 약 절반에 텍스트 콘텐츠가 있음).
  - copyright_holder - 콘텐츠에서 텍스트를 추출한 경우 해당 콘텐츠의 저작권 소유자를 나타냅니다. 모든 테스트 집합 항목에 대해 비어 있습니다.
  - license - 콘텐츠에서 텍스트를 추출한 경우 해당 콘텐츠를 사용할 수 있게 된 라이선스. 모든 테스트 집합 항목에 대해 비어 있습니다.
- `correlations.csv` - 트레이닝 세트의 주제와 관련된 콘텐츠 항목입니다. 단일 콘텐츠 항목이 둘 이상의 주제와 연결될 수 있습니다. 각 행에서 우리는 topic_id관련된 모든 의 목록을 제공합니다 content_ids. 이들은 훈련 세트의 목표를 구성합니다.

# 1st Place Solution 
## Pipeline
```
Candidate Selection (Retriever methods) -> Feature Engineering -> Lightgbm -> Postprocessing
```

## Validation Scheme
- 1 fold validation
- All source topics and random 67% of the other topics are selected for the training set. The rest are validation topics.
- The contents which only match with validation topics are excluded from the training set. For evaluation, validation topics are matched with all the contents and competition metric is calculated.
- While training lightgbm model on the candidates, group4fold on topic_id is used on the validation set. Evaluation is done on the whole validation set afterwards.

At the end of the competition, I had 0.764 validation score and 0.727 LB. While it is a big gap, improvements in my validation score were almost always correlated with LB. And I got my validation score as my Private LB score, which I didnt expect.

Edit: Efficiency model got 0.718 validation, 0.688 Public LB, 0.740 Private LB and around 20 minutes CPU run-time.

## Topic/Content Representation
Each topic is represented as a text using its title, its description and its ancestor titles up to 3 parents above in the tree. Example:

'Triangles and polygons @ Space, shape and measurement @ Form 1 @ Malawi Mathematics Syllabus | Learning outcomes: students must be able to solve problems involving angles, triangles and polygons including: types of triangles, calculate the interior and exterior angles of a triangle, different types of polygons, interior angles and sides of a convex polygon, the size and exterior angle of any convex polygon.'

Each content is represented as a text using its title, its kind and its description (its text if it doesn’t have a description). Example:

'Compare multi-digit numbers | exercise | Use your place value skills to practice comparing whole numbers.'

## Candidate Selection

## TFIDF
Char 4gram TFIDF sparse vectors are created for each language and matched with sparse_dot_topn, which is a package I co-authered (https://github.com/ing-bank/sparse_dot_topn) It works very fast and memory efficient. For each topic, top 20 matches above 1% cosine similarity are retrieved.

## Transformer Models
I used paraphrase-multilingual-MiniLM-L12-v2 for efficiency track and ensemble of bert-base-multilingual-uncased, paraphrase-multilingual-mpnet-base-v2 (it is actually a xlm-roberta-base) and xlm-roberta-large for the actual competition.

- Sequence length: 64. But only the first half of the output is mean pooled for the representation vector. Last half is only fed for context. This worked the best for me.
- Arcface training: Training contents are used as classes. Therefore topics have multiple classes and l1-normalized target vectors. The margin starts with 0.1 and increases linearly to 0.5 at the end of 22 epochs. First 2 and last 2 epochs have significantly lower LR. Arcface class centers are initialized with content vectors extracted from pretrained models.
- Ensemble method: Concatenation after l2 normalization

Edit: Models are re-trained with whole data for submission at the end.

Top 20 matches within the same language contents are retrieved.

In addition, for each topic, its closest train set topic is found and its content matches are retrieved as second degree matches.

## Matches from Same Title Topics
For each topic, train set topics with the same title are found and their matched contents are retrieved.

## Matches from Same Representation Text Topics
For each topic, train set topics with the same representation text are found and their matched contents are retrieved.

## Matches from Same Parent Topics
For each topic, train set topics with the same parent are found and their matched contents are retrieved.

All retrieved topic-content pairs are outer joined.

## Feature Engineering

- tfidf match score
- tfidf match score max by topic id
- tfidf match score min by topic id
- vector cosine distance
- vector cosine distance max by topic id
- vector cosine distance min by topic id
- topic title length
- topic description length
- content title length
- content description length
- content text length
- content same title match count
- content same title match count mean over topic id
- content same representation text match count
- content same representation text match count mean over topic id
- content same parent match count
- content same parent match count mean over topic id
- topic language
- topic category
- topic level
- content kind
- same chapter (number extracted from the text)
- starts same
- is content train
- content max train score
- topic max train score
- is content second degree match

## Lightgbm Model
- Hit or miss classification problem
- Overweight hit (minority) class
- Monotonic constraint and 2x feature contribution on most important feature: vector cosine distance
- 2 diverse lightgbms: Excluded features which will potentially have different distribution on real test set in one of the models, vector cosine distance min by topic id. Also used slightly different parameters and kfold seed.

## Postprocess
Postprocessing was very important. Using relative probabilities (gaps with highest matches) and using different conditions for train and test set contents were the key. While matching train set contents was like a classification problem, matching test set contents was like an assignment problem.

Topic-content pairs are included if they have one of the conditions below:
- Content has the best matching probability among other contents for the given topic.
- Content is among the train set contents and has above 5% probability and has less than 25% gap with the highest matching probability in the given topic.
- Content is among the test set contents and has less than 5% gap with the highest matching probability in the given topic.
- Content is among the test set contents and the topic is its best match and its total gap* is less than 55%.

## Code

- All training notebooks: https://github.com/aerdem4/curriculum-recommendations
- My actual inference notebook (v15 selected): https://www.kaggle.com/code/aerdem4/lecr-ensemble-v03
- My best Efficiency notebook: https://www.kaggle.com/code/aerdem4/lecr-efficiency-minilm
- An alternative Efficiency solution: https://www.kaggle.com/code/aerdem4/lecr-efficiency-nobert