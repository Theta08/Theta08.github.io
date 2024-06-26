---
# layout : single
title: "Tree (트리)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### Tree (트리)

비선형 자료구조로 되어 있으며 연결노드로 구성되어있다.
양뱡향 연결 구조를 살작 변경한 형태이다. 

<img src="/assets/images/Tree/Tree.png" width="60%" height="60%" title="Tree" alt="Tree"/> 

- 선형 자료구조 vs 비선형 자료구조
- 트리(tree), 서브트리(subtree)
- 노드(node), 루트(root) 노드,
- 부모 노드, 자식 노드, 형제(sibling) 노드, 조상(ancestor) 노드, 후손(descendent) 노드
- 단말 노드(terminal node, leaf node), 비단말 노드(nonterminal node)
- 노드의 차수(degree): 자식 노드의 개수
- 트리의 차수: 노드들의 차수 중 가장 큰 차수
- 레벨(루트의 레벨은 1), 깊이, 높이
- 높이: 최대 레벨
- 간선(edge)
- 이진 트리: 모든 노드의 차수가 2 이하 (최대 2개의 자식 노드)
- 포화 이진 트리(full binary tree): 모든 노드가 가득 차 있는 트리
- 완전 이진 트리(complete binary tree): 마지막 레벨 외에는 모두 다 차있고 마지막 레벨은 왼쪽부터 차있는 트리 (중간 빈곳 X)

### 이진트리 

```cpp
class BinaryTree
{
public:
	struct Node
	{
		T item = T();
		Node* left = nullptr; // Left child
		Node* right = nullptr; // Right child
	};

	BinaryTree(Node* root)
	{
		root_ = root; //  root 설정
	}
}

int main()
{
	// 트리 생성
	using Node = BinaryTree<int>::Node;

	Node* n1 = new Node{ 1, nullptr, nullptr }; 
	Node* n2 = new Node{ 2, n1, nullptr };
	Node* n3 = new Node{ 3, nullptr, nullptr };
	Node* n4 = new Node{ 4, nullptr, nullptr };
	Node* n5 = new Node{ 5, nullptr, n4 };
	Node* n6 = new Node{ 6, n2, n5 };
}
```
### 합 높이

## 합
재귀사용해서 값을 탐색해서 넣음

```cpp
	int Sum()
	{
		return Sum(root_);
	}

	int Sum(Node* node)
	{
		int sum = node->item;
		
		if(node->left)
			sum += Sum(node->left);
		if(node->right)
			sum += Sum(node->right);

		return sum; 
	}
```

## LevelOrder

Queue를 이용하여 레벨순회

 ``` cpp
		Queue<Node*> q;
		Node* current = root_;

		while (current)
		{
			Visit(current);

			
			if (current->left)
				q.Enqueue(current->left);
			if (current->right)
				q.Enqueue(current->right);
			if (q.IsEmpty())
				return;

			// q.Print();
			current = q.Front();
			q.Dequeue();
			
		}
```


### 순회
 - 기본적으로 재귀합수를 사용하여 탑색함
 - 재귀함수 순서를 어떻게 작동하는지 알면 쉽게 할수있다.

## 전위(Preorder)

- 재귀사용

```cpp
	void Preorder() { Preorder(root_); }
	void Preorder(Node* node)
	{
		if(!node)
			return;

		Visit(node);	// node->item
		
		Preorder(node->left);
		Preorder(node->right);
	}
```

- 스택 사용

```cpp
	void IterPreorder()
	{
		if (!root_) return;

		Stack<Node*> s;

		s.Push(root_);
		while (!s.IsEmpty())
		{

			Node* temp = s.Top();
			Visit(temp);
			
			s.Pop();

			if(temp->right)
				s.Push(temp->right);
			if(temp->left)
				s.Push(temp->left);
		}
	}
```
## 중위(Inorder)

- 재귀를 사용

```cpp
	void Inorder() { Inorder(root_); }
	void Inorder(Node* node)
	{
		if(!node)
			return;
		
		Inorder(node->left);
		
		Visit(node);	// node->item

		Inorder(node->right);
	}
```
- 스택 사용

왼쪽부터 조회하고 오른쪽을 조회하는데   
왼쪽 부분들만 조회를 어떻게 만들어야 하는지 생각이 안 나서 시간이 걸렸다.

```cpp
	void IterInorder()
	{
		if (!root_) return;

		Stack<Node*> s;
		Node* current = root_;
		using namespace std;
		while (current || !s.IsEmpty())
		{
			// 여기 생각이 잘 안 났음
			while (current)
			{
				s.Push(current);
				current = current->left;
			}

			current = s.Top();
			s.Pop();
			
			Visit(current);

			current = current->right;
		}
	}
```

## 후위(Postorder)

- 재귀사용

```cpp
	void Postorder() { Postorder(root_); }
	void Postorder(Node* node)
	{
		if(!node)
			return;
		
		Postorder(node->left);
		Postorder(node->right);

		Visit(node);	// node->item
	}
```
- 스택 사용 (어려웠음)

스택 2개를 사용해야 함
하나는 찾기용 하나는 그리는 용도로 사용한다는 생각을 못 했음

```cpp
	// stack 범위 찾기용 1개 그리는 용도 1개 
	void IterPostorder()
	{
		if (!root_) return;

		Stack<Node*> s1, s2;
		s1.Push(root_);

		while (!s1.IsEmpty())
		{
			Node* node =  s1.Top();
			s1.Pop();

			s2.Push(node);
			
			
			if(node->left)
				s1.Push(node->left);
			if(node->right)
				s1.Push(node->right);

		}
	}
```

결과값   
<img src="/assets/images/Tree/BinaryTree.png" width="30%" height="30%" title="BinaryTree" alt="BinaryTree"/> 

