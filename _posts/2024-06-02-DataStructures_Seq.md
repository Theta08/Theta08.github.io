---
# layout : single
title: "Sequential Representation vs Linked Representation"

# author_profile: true
categories:
  - DataStructures
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### 순차 표현 vs 연결표현
<hr/>

순차 표현
* 데이터가 일렬로 나열되어 있다. -> 배열
* 장점 : 순차적으로 나열되어 있어 찾을 때는 편을 하다
* 단점
 * 데이터 삽입, 삭제 시 데이터를 복사해서 옮겨야 함
 * 데이터를 하나하나 훑어볼 때 편함
 데이터를 삭제, 삽입 시 데이터를 복사해서 옮겨야 해서 시간복잡도가 많이 들어간다.

연결표현
* 데이터가 모여있지 않고 흩어져있고 노드가 주소를 가리키면 삽입, 삭제 시 주소만 수정하면 돼서 편하다.
* 순차적이지 않아 차례대로 찾을 때는 O(n) 배열보다는 시간이 오래 걸리지만 삽입, 삭제는 link만 변경 하므로 O(1)이 걸린다.



