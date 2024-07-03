---
# layout : single
title: "Heap"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### Heap 

<!-- <hr/> -->
트리인데 구현은 배열로 구현가능	  
배열로 구현할대 처음 인덱스 값을 0이 아니라 1로 시작을 한다.   
이유: 완전이진트리를 만들고 부모와 자식 인덱스를 쉽게 구분 하기위해 root 인덱스를 1로 잡음   
`root`를 기준으로 최소 또는 최대를 빠르게 찾을 수 있다.	
반만 순자적으로 정렬하여 순차적으로 찾을 때보다 더 빠르게 찾을 수 있다.  

완전 이진트리를 사용한다.   
비교는 부모와 자식만 비교하고 자식들끼리는 비교x

{: .notice}
부모 인덱스 * 2 = 왼쪽 자식 인덱스   
부모 인덱스 * 2 + 1 = 오른쪽 자식 인덱스   
자식인덱스 / 2 = 부모 인덱스   

삽입: 일단 맨 마지막에 삽입한 후에 부모 노드로 올린다.   
삭제: 가장 마지막 값을 루트로 옮긴 후에 내려 보낸다.

### 삽입 

```cpp
void Push(const T& item)
{

	// 삽입: 일단 맨 마지막에 삽입한 후에 부모 노드로 올린다.
	size_ += 1;
	int current = size_; // 마지막에 추가가될 위치 (인덱스)

	// 부모 위치의 값이 추가하려는 값보다 작다면
	while (current != 1 && heap_[current / 2] < item) 
	{
		// 부모 위치의 값을 자식 위치로 복사해서 내린다.
		heap_[current] = heap_[current / 2];
		current = current / 2;
	}

	heap_[current] = item; // 최종적으로 결정된 위치에 복사
}
```
### 삭제

1. root에 배열 마지막 인덱스를 넣는다.
2. 내려보내면서 부모와 자식을 비교하며 정렬 시킨다.

```cpp
void Pop()
{

	// 삭제: 가장 마지막 값을 루트로 옮긴 후에 내려 보낸다.
	T last_item = heap_[size_];	// 마지막 아이템 복사
	size_--;				// 크기 줄이기

	int current = 1;		// 루트 노드에서 시작
	int child = 2;			// current * 2 (루트의 왼쪽 자식 인덱스)
	while (child <= size_)
	{
		// left, right 중에서 더 큰 자식의 인덱스를 찾는다. 
		// 이때 자식이 하나라면 찾을 필요 없음
		if(heap_[child + 1] != 0 && heap_[child] < heap_[child + 1])
			child++;
		
		// 마지막 값이 더 큰 자식의 값 이상이면 더이상 적절한
		//  위치를 찾을 필요가 없기 때문에 루프 중단
		if(current > child)
			break;
		
		// 자식 값을 부모 위치로 복사, 
		// heap_[child / 2] = heap_[child];
		heap_[current] = heap_[child];
		
		// 그 자식 위치로 current 인덱스 변경,
		//  child 인덱스도 그 다음 자식 위치로 변경
		current = child;
		child *= 2;
	}

	heap_[current] = last_item;
}
```

### 결과

## 삽입

```cpp
MaxHeap<int> h;

for (auto i : { 2, 8, 5, 3, 2, 1, 9, 3, 7 })
{
	h.Push(i);
	h.Print();
}
```
```
Index:   1
Value:   2

Index:   1  2
Value:   8  2

Index:   1  2  3
Value:   8  2  5

Index:   1  2  3  4
Value:   8  3  5  2

Index:   1  2  3  4  5
Value:   8  3  5  2  2

Index:   1  2  3  4  5  6
Value:   8  3  5  2  2  1

Index:   1  2  3  4  5  6  7
Value:   9  3  8  2  2  1  5

Index:   1  2  3  4  5  6  7  8
Value:   9  3  8  3  2  1  5  2

Index:   1  2  3  4  5  6  7  8  9
Value:   9  7  8  3  2  1  5  2  3
```

## 삭제

```cpp
MaxHeap<int> h;

while (!h.IsEmpty())
{
	cout << h.Top() << " ";
	h.Pop();
	h.Print();
}
```

```
Index:   1  2  3  4  5  6  7  8
Value:   8  7  5  3  2  1  3  2

Index:   1  2  3  4  5  6  7
Value:   7  3  5  2  2  1  3

Index:   1  2  3  4  5  6
Value:   5  3  1  2  2  3

Index:   1  2  3  4  5
Value:   3  2  1  3  2

Index:   1  2  3  4
Value:   2  3  1  2

Index:   1  2  3
Value:   3  2  1

Index:   1  2
Value:   2  1

Index:   1
Value:   1

Index:
Value:

h.Top : 9 8 7 5 3 2 3 2 1
```

