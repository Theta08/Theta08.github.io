---
# layout : single
title: "DataStructures 준비_C++"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### 구조체

struct 이름{...}
자료형 만든거랑 비슷함

```cpp
struct MyStruct
{
    int first;
    int second;
    // ... 추가 가능

    int Sum()
    {
        return first + second;
    }
    
};

int main()
{
    // member(.) operator
    MyStruct a;
    a.first = 123;
    a.second = 456;

    // 포인터는 member(->) operator가 화살표
    MyStruct *ptr_a = &a;

    cout << ptr_a -> first << " " << ptr_a -> second << " " << ptr_a->Sum() << endl;

    // 배열도 가능
    // pairs 자체가 포인터라서 인덱싱으로 접근해야함
    MyStruct pairs[10];
}
```

### 구조체와 배열 차이

{: .notice}
 배열 : 동일한 자료형   
 구조체 : 다양한 자료형 변수   

 ``` cpp
MyStruct a
{
    int first;
    int second;
};

// 이런 구조체라면 결국 int가 여러개 나열된 형태라서 배열과 똑나??

MyStruct a
{
    int first;
    float second;
};

// 구조체는 다양한 자료형의 변수들도 묶어놓을 수가 있음
```

<!-- ### 구조체의 패딩 -->
