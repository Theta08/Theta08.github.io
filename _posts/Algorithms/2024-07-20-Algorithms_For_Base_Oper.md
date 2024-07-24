---
# layout : single
title: "사칙연산 (Four basic operations)"

# author_profile: true
categories:
  - Algorithms
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---
### 사칙연산 (Four basic operations)

큰 수 구할려고 하면 기존 사칙연산으로 하면 에러가 걸린다.

값을 하나씩 가져와서 계산해야함
 
1. 구현을 편하게 하기 위해서 두 숫자의 자리수를 맞춰줍니다.
2. 더 짧은 쪽의 높은 자리에 0으로 채워줍니다.
3. str1 = "1234", str2 = "56"인 경우 str2를 "0056"으로 변경
4. 더한 결과가 10보다 클 경우 다음 자리로 넘겨줄 숫자 (carry)로 설정
5. 모든 자리를 다 더한 후에는 carry만 가장 높은 자리에 추가

### 예시
``` cpp
int N = max(str1.size(), str2.size()); 
str1.insert(0, N - str1.size(), '0');
str2.insert(0, N - str2.size(), '0');

string result(N, '0');
int carry = 0; 
for (int i = N - 1; i >= 0; i--) 
{
  int n1 = str1[i] - '0'; 
  int n2 = str2[i] - '0';

  // 사칙연산에 따라 변경해야함
  // 현재 더하기 상태
  int sum = n1 + n2 + carry;
  carry = sum / 10;
  result[i] = char(sum % 10 + '0'); 
}

// 모든 자리를 다 더한 후에는 carry만 가장 높은 자리에 추가
if(carry > 0)
  result.insert(0, to_string(carry));

```