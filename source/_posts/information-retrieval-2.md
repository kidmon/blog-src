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
title: Information Retrieval - 2
date: 2019-10-25 02:40:40
categories: [NLP, Information Retrieval]
tags: [NLP, Information Retrieval, 공부정리]
thumbnail: /image/information-retrieval/thumbnail.png
---

이 포스팅은 스탠포드 대학교 강의 [CS276 Information Retrieval](http://web.stanford.edu/class/cs276/)의 참고자료와 [KWANGSIK LEE](http://www.kwangsiklee.com/tag/cs276-information-retrieval/page/2/)님의 포스팅을 참고하여 개인적인 공부를 위해 정리한 글입니다.

<!-- more -->

## Wild-card Queries
- *을 이용하여 대상으로 하는 문자열을 포함하는 문서를 검색
- he*llo와 같이 *가 중간에 위치하는 것은 어떻게 처리할 수 있을까?
    - he*와 *llo를 찾아서 교집합을 구한다 → 비용이 크다
    - Wild-card를 변형하여 단어의 끝에 위치하게 바꿔서 구한다 → Permuterm Index

## Permuterm Index
- $로 Term의 끝을 표시
- hello의  Permuterm 결과
| Permuterm |
| --------- |
| hello$    |
| ello$h    |
| llo$he    |
| lo$hel    |
| o$hell    |
| $hello    |
- he*llo를 찾으려면 llo$he*를 찾으면 된다.

## Spell Correction
- 두 가지 방법이 있음
    - Isolated Word
    - Context Sensitive

## Isolated Word
### Edit Distance
- 문자열 S1, S2가 있을 때, 서로 같아지도록 바꿀 수 있는 최소한의 연산 횟수
- dof → dog : 1
- cat → act : 2
- cat → dog : 3

### Weighted Edit Distance
- Edit Distance 에서 가중치를 적용
- 상대적으로 틀리기 쉽거나(키보드가 가까이 있음) 확률이 높은 것에 가중치를 준다.

### N-gram Overlap
- 쿼리 String의 모든 n-gram을 순회한다.
- n-gram 색인을 통해 사전에 매치되는 n-gram이 있는지 찾는다.
- 매치되는 n-gram에 threshold를 둔다.

### Jaccard Similarity
- A와 B의 유사도
- A와 B의 크기가 같을 필요는 없다.
- 항상 0~1의 값을 가지므로 threshold로 쓰기에 좋다.

## Context Sensitive
> I flew form Heathrow to Narita.
단어에는 오류가 없지만 문맥상의 오류인 form을 고치고 싶다.

### Probability Language Models
- 문장에 확률을 할당
- P(about fifteen minutes from) > P(about fifteen minuets from)
- P(A, B, C, D) = P(A)P(B|A)P(C|A, B)P(D|A, B, C)

## Soundex
- Query를 음성이 같은 것끼리 분류하는 것
- Reduced form으로 색인과 검색 수행
1. 첫 번째 문자를 얻음
2. A, E, I, O, U, W, H, Y → 0
3. B, F, P, V → 1
4. C, G, J, K, Q, S, X, Z → 2
5. D, T → 3
6. L → 4
7. M, N → 5
8. R → 6
9. 연속된 숫자 쌍 제거
10. 모든 0 제거
11. 대문자, 숫자, 숫자, 숫자 형태로 변환
- Herman → H655
- High Recall 작업에서 좋음

## Index Construction
### MapReduce
- 검색 엔진의 분산 환경에서 term으로 분할되어있는 색인을 문서로 분할되어 있는 색인으로 변환
- Schema
    - map : input → list(k, v)
    - reduce : (k, list(v)) → output
- map
    - input : collection
    - output : list(termID, docID)
- reduce
    - input : (termID1, list(docID)), (termID2, list(docID)), …
    - output : posting list1, posting list2, …
    
### MapReduce Example
- map
    - input
    - d1 : C came, C c’ed
    - d2 : C died
    - output
    - <C, d1>, <came, d1>, <C, d1> <C’ed, d1>, <C, d2>, <died, d2>
- reduce
    - input
    - (<C,(d1,d2,d1)>, <died,(d2)>, <came,(d1)>, <c’ed,(d1)>)
    - output
    - (<C,(d1:2,d2:1)>, <died,(d2:1)>, <came,(d1:1)>, <c’ed,(d1:1)>)

## Index Compresssion
- Dictionary Compression
- Postrings Compression

### Dictionary Storage 1 — Fixed width entry
![](http://www.kwangsiklee.com/wp-content/uploads/2017/11/searchengine2_0500.png)
- 40만 term을 관리하기 위해서 11.2MB 소모

### Dictionary Storage 2 — Dictionary-as-a-String
![](http://www.kwangsiklee.com/wp-content/uploads/2017/11/searchengine2_0700.png)
- 4 바이트 : term frequency
- 4 바이트 : term의 포스팅에 대한 포인터
- 3 바이트 : term 포인터
- 평균 8 바이트 : term당 term string
- 400K terms x 19 = 7.6 MB (Fixed width entry 대비 3.6MB 절약)

### Dictionary Storage 3 — Blocking
![](http://www.kwangsiklee.com/wp-content/uploads/2017/11/searchengine2_0800-1.png)
- 블럭 사이즈가 k = 4라고 가정
- 포인터당 3바이트를 Blocking 없이 사용

## Postings file entry
![](http://www.kwangsiklee.com/wp-content/uploads/2017/11/searchengine2_0600.png)
- term을 포함하는 문서를 docId가 증가하는 순서로 저장
    - computer: 33, 47, 154, 159, 202, …
- 개선: 첫 docId만 제대로 기입하고 그다음 docId 부터 값의 차이를 저장
    - computer: 33, 14, 107, 5, 43, …
    - 최초는 33, 그다음부터 (47-33), (154-47), …

---

## 참고한 글
[Stanford CS276 Information Retrieval](http://web.stanford.edu/class/cs276/)
[KWANGSIK LEE’s log](http://www.kwangsiklee.com/tag/cs276-information-retrieval/page/3/)