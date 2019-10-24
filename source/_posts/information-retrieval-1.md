---
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: recent_posts
    position: right
sidebar:
  right:
    sticky: true
title: Information Retrieval - 1
date: 2019-10-25 02:40:35
categories: [NLP, Information Retrieval]
tags: [NLP, Information Retrieval, 공부정리]
thumbnail:
---

이 포스팅은 스탠포드 대학교 강의 [CS276 Information Retrieval](http://web.stanford.edu/class/cs276/)의 참고자료와 [KWANGSIK LEE](http://www.kwangsiklee.com/tag/cs276-information-retrieval/page/3/)님의 포스팅을 참고하여 개인적인 공부를 위해 정리한 글입니다.

<!-- more -->

## Precision and Recall
- Precision(정밀도) : 분류 결과가 True인 것 중에서 실제 정답도 True인 것의 비율
- Recall(재현율) : 실제 정답이 True인 것 중에서 분류 결과도 True인 것의 비율

$$precision=\cfrac{TP}{TP + FP}$$
$$recall = \cfrac{TP}{TP + FN}$$

## Boolean Retrieval
- Information Retrieval 시스템 중에서 가장 단순한 모델
- Query는 Boolean으로 표현
- Boolean 표현을 만족하는 모든 결과를 반환

## Inverted Index
- 색인의 기준이  Document가 아니라 Term
- Term과 Term이 등장하는 Document(Posting List) 형태
![Inverted Index](http://www.kwangsiklee.com/wp-content/uploads/direct/bigdata_analysis/border/searchengine0400.png)

- Construction
    1. Index를 만들 문서 수집
    2. Tokenization
    3. Preprocessing
        - Lemmatization : 단어를 원형으로 바꿈
        - Stemming : 단어의 어근만 빼고 날림
        - Stop words : 불용어 제거

## Boolean Query Processing
- AND, OR, NOT의 조합으로 사용
- Query의 Term이 2개 이상일 때, 포스팅 리스트가 짧은 것부터 순서대로 처리

## Normalization
- Numbers
- Case Folding : 모두 소문자로 만드는 것
- Stop Words : 너무 흔하게 등장해서 의미가 없는 단어
- Lemmatization :  원형으로 변형하는 것
- Stemming : 단어의 어근만 남기고 자는 것
- Porter Algorithm
![Porter Algorithm](http://www.kwangsiklee.com/wp-content/uploads/direct/bigdata_analysis/border/searchengine2100.png)

## Skip Pointer
- Query Processing을 할 때, 포스팅 리스트에 포인터를 만들고 이것을 통해 포스팅을 Skip함으로써 불필요한 계산을 줄이고 바르게 처리할 수 있음
![Example](http://www.kwangsiklee.com/wp-content/uploads/direct/bigdata_analysis/border/searchengine2600.png)

- Tradeoff
    - More skips -> skip 성공 가능성 높음, 너무 많은 비교가 일어날 수 있음
    - Fewer skips -> skip 성공 가능성이 낮을 수 있음, 비교가 적어짐
![Tradeoff](http://www.kwangsiklee.com/wp-content/uploads/direct/bigdata_analysis/border/searchengine2801.png)

## Phrase Queries
- Phrase 형태의 쿼리
- 2가지 방법으로 처리할 수 있음
    - Bi-word Index : Bi-gram처럼 순서대로 2개씩 색인
        ex) “stanford university palo alto” → [stanford university], [university palo], [palo alto]
    - Positional Index : 각 Term은 등장하는 DocID와 위치에 대한 리스트를 가지고 있음
![Positional Index](http://www.kwangsiklee.com/wp-content/uploads/direct/bigdata_analysis/border/searchengine2900.png)

---

## 참고한 글
1. [Stanford CS276 Information Retrieval](http://web.stanford.edu/class/cs276/)
2. [KWANGSIK LEE’s log](http://www.kwangsiklee.com/tag/cs276-information-retrieval/page/3/)