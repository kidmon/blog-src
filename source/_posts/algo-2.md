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
title: 알고리즘 공부하기-2(백준 2798번 / 블랙잭 / 파이썬)
date: 2020-04-18 19:00:00
categories: [Algorithm]
tags: [Algorithm, Study, Python]
thumbnail:
---

## 문제
**블랙잭(https://www.acmicpc.net/problem/2798)**
> 카지노에서 제일 인기 있는 게임 블랙잭의 규칙은 상당히 쉽다. 카드의 합이 21을 넘지 않는 한도 내에서, 카드의 합을 최대한 크게 만드는 게임이다. 블랙잭은 카지노마다 다양한 규정이 있다.
<br>한국 최고의 블랙잭 고수 김정인은 새로운 블랙잭 규칙을 만들어 상근, 창영이와 게임하려고 한다.
김정인 버전의 블랙잭에서 각 카드에는 양의 정수가 쓰여 있다. 그 다음, 딜러는 N장의 카드를 모두 숫자가 보이도록 바닥에 놓는다. 그런 후에 딜러는 숫자 M을 크게 외친다.
<br>이제 플레이어는 제한된 시간 안에 N장의 카드 중에서 3장의 카드를 골라야 한다. 블랙잭 변형 게임이기 때문에, 플레이어가 고른 카드의 합은 M을 넘지 않으면서 M과 최대한 가깝게 만들어야 한다.
<br>N장의 카드에 써져 있는 숫자가 주어졌을 때, M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 구해 출력하시오.

<!-- more -->

## 입력
> 첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다. 둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는다.
합이 M을 넘지 않는 카드 3장을 찾을 수 있는 경우만 입력으로 주어진다.

## 출력
> 첫째 줄에 M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 출력한다.

## 코드 1
```python
card_num, target_score = input().split()

cards = input().split()
cards = [int(i) for i in cards]

max = 0

for i in cards:
    for j in cards:
        if j != i:
            for k in cards:
                if k != j and k != i:
                    if max <= i+j+k <= int(target_score):
                        max = i+j+k
                        
print(max)
```

## 풀이 1
### 문제 이해
기본적인 블랙잭의 게임룰과 같다. 주어진 N개의 카드 중 3장을 골라 더했을 때 M을 넘지 않으면서 가장 큰 수를 만들면 된다.
### 제약 조건
주어진 입력 조건 외에 고려해야 할 조건은 없다.
### 해결 과정
주어진 카드의 수와 목표 점수를 받아서 변수로 지정하고 카드 리스트를 받아서 정수로 변환한다. 카드 리스트를 이용해서 3개의 카드의 합으로 얻을 수 있는 모든 경우의 수를 구하고 그 중 가장 큰 값을 반환하였다. `for`문 반복 중에 같은 카드가 1회 이상 중복되지 않도록 `if j != i, if k != j and k != i` 두 가지 조건을 넣어주었다. 너무 단순한 반복 탐색 방법인 것 같아서 아래의 두 번째 풀이 방법을 생각해보았다.

---

문제의 출처는 [Baekjoon Online Judge](https://www.acmicpc.net/)이며 포스팅에 있는 코드 중 출처 표기가 없는 것은 직접 작성한 코드입니다.