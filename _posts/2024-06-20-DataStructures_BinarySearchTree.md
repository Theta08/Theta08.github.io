---
# layout : single
title: "BinarySearchTree (이진 탐색 트리)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### BinarySearchTree 

<!-- <hr/> -->
`Inorder`를 써서 key에 대해 중위정렬 출력   
key와 value로 이루어져있음   
검색은 key로 찾아 value값을 보여줌   
root_ 값 기준   
왼쪽 노드 값 < root_ 값   
오른쪽 노드 값 > root_ 값   

이진 탐색 트리에서 검색이나 삽입, 삭제의 시간 복잡도는 균형이 잘 맞는 구조라면 O(logN)

자동정렬X 

## 결과 

```cpp
BinarySearchTree<int, char> bst;

for (int i : { 5, 3, 7, 1, 4, 6, 8 })
{
	bst.Insert(Item{ i, char('A' + i) });
	bst.Print2D();
}
```

Insert 6Z
Height = 3
                 5F
         3D               7H
     1B       4E       6Z       8I

### 삽입

1. node가 없으면 노드 생성

```cpp
Node* Insert(Node* node, const Item& item)
{
	if(!node)
		return new Node { item, nullptr, nullptr};
		
	if( item.key < node->item.key)
		node->left = Insert(node->left, item);
	else if( item.key > node->item.key)
		node->right = Insert(node->right, item);
	else
		node->item = item;
	
	return node;
}
```

### 탐색

`root_`기준 내려가며 키값 찾기

```cpp

// main
BinarySearchTree<int, char> bst;

cout << bst.RecurGet(3)->value << endl;

// BinarySearchTree
Item* RecurGet(const K& key)
{
	return RecurGet(root_, key);
}

Item* RecurGet(Node* node, const K& key)
{
	if (!node) return nullptr;

	if (key < node->item.key)
		return RecurGet(node->left, key);
	if (key > node->item.key)
		return RecurGet(node->right, key);

	// if (key == node->item.key)
	return &node->item; 
}
```
### 삭제

```cpp
Node* Remove(Node* node, const K& key)
{
	if (!node) return node;

	if (key < node->item.key)
		node->left = Remove(node->left, key);
	else if (key > node->item.key)
		node->right = Remove(node->right, key);
	else
	{
		// 1. node right, node->left nullptr 유무로 삭제
		// 2. node->right, node->left != nullptr node-right의 가장 왼쪽값을 복사 후
		// 복사한 node 삭제
		
		if(!node->left)
		{
			Node* temp = node->right;
			delete node;
			return temp;
		}
		else if(!node->right)
		{
			Node* temp = node->left;
			delete node;
			return temp;
		}
		
		Node* temp = MinKeyLeft(node->right);
		node->item = temp->item;
		node->right = Remove(node->right, temp->item.key);
		
	}

	return node;
}
```
