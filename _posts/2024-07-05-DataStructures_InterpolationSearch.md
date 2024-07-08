---
# layout : single
title: "InterpolationSearch (보간 탐색)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### QuickSort 

<!-- <hr/> -->
정렬된 상태일때 쓴다. 이진탐색과 유사함   
찾는값(x)가 클경우 뒤쪽 인덱스에서 탐색 x가 작을경우 앞쪽 인덱스부터 탐색한다.    

{: .notice}
low: 배열의 가장 작은 인덱스 (알고 있는 값)   
high: 배열의 가장 큰 인덱스 (알고 있는 값)   
pos: 탐색을 시작하기에 적적한 인덱스 (우리가 결정해야 하는 값)   
arr[low]: 배열에 저장된 가장 작은 값 (알고 있는 값)   
arr[high]: 배열에 저장된 가장 큰 값 (알고 있는 값)   
x: 우리가 찾고 싶은 값 (알고 있는 값)   

- 비례 관계 : (arr[high] - arr[low]) : (x - arr[low]) = (high - low) : (pos - low) 
 pos = low + (high - low ) / (arr[high] - arr[low]) * (x - arr[low]) 

1. pos로 값 탐색   
2. pos 인덱스 탐색값 비교 후 탐색값 != pos 인덱스면 재탐색   

이진탐색 중간값 == pos   
찾는 값들이 가운데 많이 있으면 이진탐색이 더 빠름 끝에 있을경우 보간 탐색이 빠름

### 결과 

```cpp
int InterpolationSearch(int arr[], int low, int high, int x)
{

	if (low <= high && x >= arr[low] && x <= arr[high])
	{
		int pos = (low + high) / 2; // 이진 탐색 (중간)

		// int pos = 보간 탐색으로 수정
		// float 이유 :계산값이 소수점 자리로 감  
		float fPost = float(high - low ) / float(arr[high] - arr[low]);
		pos = low + int(fPost * (x - arr[low]));
		
		if (arr[pos] == x)
			return pos;

		if (arr[pos] < x)
			return InterpolationSearch(arr, pos + 1, high, x);

		if (arr[pos] > x)
			return InterpolationSearch(arr, low, pos - 1, x);
	}

	return -1;
}

int main()
{
	int arr[] = { 10, 12, 13, 16, 18, 19, 20, 21, 22, 23, 24, 33, 35, 42, 47 };
	
	int index = InterpolationSearch(arr, 0, n - 1, 13);

	if (index != -1)
		cout << 13 << " was found at index " << index << endl;
	else
		cout << 13 << " was not found." << endl;
}
```
