---
# layout : single
title: "분할 정복 (Divide & Conquer)"

# author_profile: true
categories:
  - Algorithms
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---
### Karatsuba 알고리듬

여러 자리수의 곱하기를 더 빠르게 하는 방법
분할 정복
 어려운 일을 쉬운 일 여러개로 쪼개어 실행
 분할 -> .. -> 정복 -> .. -> 병합
 
 
 1. 문제를 점점 작게 쪼개들어가는 분할 단계 (더이상 쪼갤수 없는 단계까지 - 재귀)
 2. 다 쪼갠 후에 실제로 계산을 수행하는 정복 단계
 3. 나눠서 정복한 결과들을 합쳐서 최종 결과를 만드는 병합 단계
 
그냥 쪼갰다가 합친다고 무조건 빠름x
차수가 낮아진다는 것이 중요

분할식을 이해하고 사칙연산 구현해야함

## 느낀점
Karatsuba 알고리듬을 하면서 왜 알고리듬을 써서 구현 해야하는지 알수있었다.

작은 수를 곱하면 기존 초등학교 곱하기 방식이 빠르지만 값이 커질수록 Karatsuba 알고리듬이 속도가 더 빠르다.

### 분할식 만들기
예시)  1234 * 5678 
```
x * y = ( a * 100 + b ) * ( c * 100 + d)
	= ac * 10000 + ( (a + b) * ( c + d) - ( ac + bd ) ) * 100 + db


1234 * 5678 = 7006652
Level 0 : 1234 x 5678
Level 1 : 12 x 56
Level 2 : 1 x 5
Level 2 : 2 x 6
Level 2 : 3 x 11
Level 3 : 0 x 1
Level 3 : 3 x 1
Level 3 : 3 x 2
Level 1 : 34 x 78
Level 2 : 3 x 7
Level 2 : 4 x 8
Level 2 : 7 x 15
Level 3 : 0 x 1
Level 3 : 7 x 5
Level 3 : 7 x 6
Level 1 : 46 x 134
Level 2 : 0 x 1
Level 2 : 46 x 34
Level 3 : 4 x 3
Level 3 : 6 x 4
Level 3 : 10 x 7
Level 4 : 1 x 0
Level 4 : 0 x 7
Level 4 : 1 x 7
Level 2 : 46 x 35
Level 3 : 4 x 3
Level 3 : 6 x 5
Level 3 : 10 x 8
Level 4 : 1 x 0
Level 4 : 0 x 8
Level 4 : 1 x 8

7006652 7006652 OK

```