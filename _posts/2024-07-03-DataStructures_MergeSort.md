---
# layout : single
title: "MergeSort (병합정렬)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### MergeSort 

<!-- <hr/> -->
n 개를 반씩 나눠서 분할 후 합치면서 정렬   

{: .notice}
시간 복잡도: n 개를 반씩 나눠서 분할 정복하기 때문에 최악, 최선, 평균 모두 O(n log n)   
공간 복잡도: 추가 메모리가 필요하기 때문에 O(n)   

1. 재귀를 써서 분할 
2. 분할 후 희소 다항식을 사용하여 정렬 후 병합

<img src="/assets/images/Sort/MergeSort.png" width="60%" height="60%" title="Tree" alt="Tree"/> 

### 결과 

```cpp
void MergeSort(int arr[], int merged[], int left, int right)
{
	int mid;
	if (left < right)
	{
		mid = (left + right) / 2;

		MergeSort(arr, merged, left, mid);
		MergeSort(arr, merged, mid + 1, right);

		Merge(arr, merged, left, mid, right);
	}
}

void Merge(int init[], int merged[], int left, int mid, int right)
{
	int i, j, k, l;
	i = left;
	j = mid + 1;
	k = left;

	cout << "  Left : ";
	Print(init, left, mid);
	cout << " Right : ";
	Print(init, mid + 1, right);

	// 희소 다항식 
	// 인덱스를 2개 이용해서 정렬하면서 merge
	while(i <= mid && j <= right)
	{
		// 1. 값이 같을때
		// 2. i가 클경우 i++
		// 3. j가 클경우 j++
		if(init[i] == init[j])
		{
			merged[k] = init[j];
			i++;
			j++;
			k++;
		}
		else if(init[i] < init[j])
		{
			merged[k] = init[i];
			i++;
			k++;
		}
		else if(init[i] > init[j])
		{
			merged[k] = init[j];
			j++;
			k++;
		}
	}

	// 남은 내용들 복사
	for(; i <= mid; i++)
	{
		merged[k] = init[i];
		k++;
	}
	for(; j <= right; j++)
	{
		merged[k] = init[j];
		k++;
	}

	// merged -> init 복사
	for (l = left; l <= right; l++)
		init[l] = merged[l];

	cout << "Merged : ";
	Print(init, left, right);
	cout << endl;
}
```
