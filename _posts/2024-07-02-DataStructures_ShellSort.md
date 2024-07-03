---
# layout : single
title: "ShellSort (쉘 정렬)"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### ShellSort 

<!-- <hr/> -->
삽입정렬 응용 큰폭으로 건너 띄어 정렬

{: .notice}
최악 O(n^2), 평균 O(n^1.5)

### 결과 

```cpp
void ShellSort(int arr[], int n)
{
	for (int gap = n / 2; gap > 0; gap /= 2)
	{
		cout << "         ";
		Print(arr, n);

		InsertionSort(arr, n, gap);
	}

	cout << "         ";
	Print(arr, n);
	cout << endl;
}

void InsertionSort(int arr[], int n, int gap) 
{
	cout << "gap = " << gap << endl;

	for (int i = gap; i < n; i += 1)
	{
		cout << "Before : ";
		Print(arr, n, i, gap);

		int key = arr[i];
		int j = i;

		for (; j >= gap && arr[j - gap] > key; j -= gap)
			arr[j] = arr[j - gap];

		arr[j] = key;
		
		cout << " After : ";
		Print(arr, n, i, gap);
	}
}
```
## 결과

```
          99  83  18  66   7  54  95  86  47  69  25  28
gap = 6
Before :  99                      95
 After :  95                      99
Before :      83                      86
 After :      83                      86
Before :          18                      47
 After :          18                      47
Before :              66                      69
 After :              66                      69
Before :                   7                      25
 After :                   7                      25
Before :                      54                      28
 After :                      28                      54
          95  83  18  66   7  28  99  86  47  69  25  54

gap = 3
Before :  95          66          99          69
 After :  66          95          99          69
Before :      83           7          86          25
 After :       7          83          86          25
Before :          18          28          47          54
 After :          18          28          47          54
Before :  66          95          99          69
 After :  66          95          99          69
Before :       7          83          86          25
 After :       7          83          86          25
Before :          18          28          47          54
 After :          18          28          47          54
Before :  66          95          99          69
 After :  66          69          95          99
Before :       7          83          86          25
 After :       7          25          83          86
Before :          18          28          47          54
 After :          18          28          47          54
          66   7  18  69  25  28  95  83  47  99  86  54

gap = 1
Before :  66   7  18  69  25  28  95  83  47  99  86  54
 After :   7  66  18  69  25  28  95  83  47  99  86  54
Before :   7  66  18  69  25  28  95  83  47  99  86  54
 After :   7  18  66  69  25  28  95  83  47  99  86  54
Before :   7  18  66  69  25  28  95  83  47  99  86  54 
 After :   7  18  66  69  25  28  95  83  47  99  86  54
Before :   7  18  66  69  25  28  95  83  47  99  86  54
 After :   7  18  25  66  69  28  95  83  47  99  86  54
Before :   7  18  25  66  69  28  95  83  47  99  86  54
 After :   7  18  25  28  66  69  95  83  47  99  86  54
Before :   7  18  25  28  66  69  95  83  47  99  86  54
 After :   7  18  25  28  66  69  95  83  47  99  86  54
Before :   7  18  25  28  66  69  95  83  47  99  86  54
 After :   7  18  25  28  66  69  83  95  47  99  86  54
Before :   7  18  25  28  66  69  83  95  47  99  86  54
 After :   7  18  25  28  47  66  69  83  95  99  86  54
Before :   7  18  25  28  47  66  69  83  95  99  86  54
 After :   7  18  25  28  47  66  69  83  95  99  86  54
Before :   7  18  25  28  47  66  69  83  95  99  86  54
 After :   7  18  25  28  47  66  69  83  86  95  99  54
Before :   7  18  25  28  47  66  69  83  86  95  99  54
 After :   7  18  25  28  47  54  66  69  83  86  95  99
           7  18  25  28  47  54  66  69  83  86  95  99 
```

