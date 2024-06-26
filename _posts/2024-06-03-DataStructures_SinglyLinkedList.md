---
# layout : single
title: "SinglyLinkedList (단방향 연결 리스트)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### SinglyLinkedList (단방향 연결 리스트)

링크 리스트가 value, link로 이루어져 있다.
배열과 다르게 1, 2, 3…. 4, 5 순서대로 이루어지지 않고 메모리 주소를 가지고 다음 인덱스를 찾아간다.

배열은 순차적이라 순차적으로 찾을 때 빠르지만, 삽입, 삭제 경우 다시 복사해야 한다.
리스트는 순차적이지 않아 차례대로 찾을 때는 O(n) 배열보다는 시간이 오래 걸리지만 삽입, 삭제는 link만 변경 하므로 O(1)이 걸린다.

```cpp

public:
    struct Node
    {
        T item = T();
        Node* next = nullptr;
    };

protected:
    Node* first_ = nullptr;
```

### 맨앞 맨뒤삽입

{: .notice}

 ``` cpp
void PushFront(T item)
{
    // 새로운 노드 만들기
    Node* newNode = new Node;	//	O(1)
    newNode->item = item;
    
    // 연결 관계 정리
    newNode->next = first_;
    first_ = newNode;
}
void PushBack(T item)
{
    
    if (first_)
    {
        
        Node* temp = first_;
        while(temp->next)
            temp = temp->next;

        Node* backNode = new Node;
        backNode->item = item;
        temp->next = backNode;
    }
    else
    {
        // backNode->next = first_;
        // first_ = backNode;
        PushFront(item);
    }
}
```
### 값 찾기
``` cpp
Node* Find(T item)
{
    // item이 동일한 노드 포인터 반환
    Node* temp = first_;

    while(temp->item != item)
        temp = temp->next;
    
    return temp;
}
```
### 노드 삭제   

## 특정 값을 찾아서 삭제
``` cpp
void Remove(Node* n)
{
    assert(first_);

    if(first_ == n)
    {
        first_ = first_->next;
        delete n;
        return;
    }

    Node* temp = first_;
    
    while(temp->next != n)
        temp = temp->next;
    
    temp->next = n->next;
    
    delete n;
}
```   
   
## 앞, 뒤 삭제
```cpp
	void PopFront()
	{
		if (IsEmpty())
		{
			using namespace std;
			cout << "Nothing to Pop in PopFront()" << endl;
			return;
		}

		assert(first_);

		//메모리 삭제
		Node* temp = first_;
		first_ = temp->next;

		delete temp;
	}

	void PopBack()
	{
		if (IsEmpty())
		{
			using namespace std;
			cout << "Nothing to Pop in PopBack()" << endl;
			return;
		}

		if(first_->next == nullptr)
		{
			delete first_;
			first_ = nullptr;
			return;
		}

		assert(first_);

		//메모리 삭제
		Node* temp = first_;
		
		while(temp->next->next != nullptr)
			temp = temp->next;

		Node* prev = temp;
		temp = prev->next;
		prev->next = nullptr;

		delete temp;
	}
```

### 역순 정렬
노드를 복사해서 새로운 노드에다 값을 넣고 역순 정렬, 스택을 사용하지 않고 노드 링크 순서만 사용 하여 변경을 하였다.   
반복문을 사용하여 마지막 노드까지 반복해야한다.
기존에 노드를 저장하고
새로운 노드를 생성해야한다. 
첫번째 노드는 first_값에 저장을 해야하고 마지막 노드 next는 nullptr로 만들어야 한다.

참조 : <https://www.geeksforgeeks.org/reverse-a-linked-list>
```cpp
void Reverse()
{
    Node* prev = nullptr;
    Node* current = first_;
    
    while(current != nullptr)
    {
        Node* temp = prev;
        prev = current;
        
        current = current->next;
        prev->next = temp;

    }
        first_ = prev;
}
```