---
# layout : single
title: "DoublyLinkedList (양방향 연결 리스트)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### DoublyLinkedList (양방향 연결 리스트)

단방향 노드 연결을 이해했으면 조금만 생각하면 이해하기 편했다. 핵심은 단방향 연결리스트와 비슷하지만 노드가 left, right 2개로 양쪽이 이어져 있다.   
```cpp

public:
    struct Node
    {
        T item = T();
        
		Node* left = nullptr;
		Node* right = nullptr;
    };

protected:
    Node* first_ = nullptr;
```

### 맨앞 맨뒤삽입

{: .notice}
노드가 양방향이라 left, right에 방향 설정

 ``` cpp
void PushFront(T item)
{
	// TODO:
	Node* temp = new Node;
	
	temp->item = item;
	temp->right = first_;
	// temp->left = nullptr;
	
	if(first_)
	{
		first_->left = temp;
		first_ = temp;
	}
	else
	{
		first_ = temp;
	}
	
}
void PushBack(T item)
{
	if(first_)
	{
		Node* temp = first_;
		
		while (temp->right)
			temp = temp->right;
		
		Node* temp1 = new Node;
		temp1->item = item;
		
		temp1->left = temp;
		temp->right = temp1;
	}
	else
	{
		Node* temp = new Node;
	
		temp->item = item;
		temp->right = nullptr;
		temp->left = first_;
		first_->right = temp;
	}

}
```

### 노드 삭제   

단반향과 차이점은 양방향이라 노드 삭제시 하나의 주소만 이어지는것이 아니라 left, right 주소를 이어주어야 한다.
   
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


		Node* temp = first_;
		first_ = first_->right;

		if(first_)
			first_->left = nullptr;

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


		assert(first_);

		if(first_-> right == nullptr)
		{
			delete first_;
			first_ = nullptr;
			return;
		}
		
		Node* temp = first_;
		
		while(temp->right->right)
			temp = temp->right;

		delete temp->right;
		
		temp->right = nullptr;
	}
```

### 역순 정렬
<hr/>
right, left로 양방향으로 이어져 있어 2개의 보드 방향만 바꾸면 역순 정렬이 쉽게 된다.

``` cpp
void Reverse()
{
   if(IsEmpty())
        return;
    else
    {
        Node* current = first_;
        Node* prev = nullptr;
        
        while(current)
        {
            prev = current;

            current = current->right;

            std::swap(prev->left, prev->right);
            
        }
        first_ = prev;
    }
}
```