---
title: "About Data Structure"
tags:
    - computer science
    - data structure
    - 자료구조
date: "2023-08-07"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# 시간복잡도
---
알고리즘 로직에서 입력값이 전체 연산의 시간에 미치는 영향을 알기 위한 방법

* big-O  
상한 점근법으로 최대 걸리는 시간을 알 수 있다. 아래는 대표적인 시간이다.
> $O(1)$ - 단일 작업  
> $O(n)$ - 입력에 대한 모든 작업  
> $O(n^2)$ - 입력에 대한 모든 작업의 재반복  
> $O(log(n))$ - 입력에서 이진 탐색하는 방법  

* big-omega  
하한 점근법으로 최선의 경우에서 시간을 알 수 있다.

* big-theta  
상*하한 점근법의 평균

# list
---
LIFO(last in first out) 모델
## static list
---
일반적인 정적 리스트 범위를 미리 지정하고 넘어가면 추가 할당함

## linked list
---
리스트 요소마다 연결되는 형식 처럼 제작한 리스트

{% highlight python %}
from collections import deque

queue = deque()
{% endhighlight %}

# stack
---
LIFO(last in first out) 모델

* push()  
데이터 입력 
* pop()  
데이터 출력(+삭제)
* top(), peek()  
데이터 출력

# Queue
---
FIFO(first in first out) 모델

* push(), offer(), add()  
데이터 입력
* pop(), poll()  
데이터 출력(+삭제)
* peek()  
데이터 출력

# hash(Dictionary,Set in python)
---
데이터를 빠르게 저장하고 가져오는 기법으로 key를 연산을 통해 value를 알 수 있다

# sorting
---
정렬을 하는방법으로 동일한 값이 기존서순대로 나열 되는 stable sort와 그렇지 않은 unstable sort로 나뉘어진다.

* binary search  
정렬된 값에서 중앙값을 찾고 중앙을 기준으로 나눠서 유사한값이 해당하는 집합에서 다시 중앙값을 찾아 나가는 방법
* bubble sort(stable)  
순서대로 다음값과의 순서를 비교하여 정렬하는법 $O(n^2)$
* insert sort(stable)  
순서대로 다음값을 포함하여 포함한 집합에서 순서를 비교하여 정렬하는법 $O(n^2)$
* merge sort(stable)  
각 개별로 분할하고 다시 짝찌어 돌아가면서 정렬하는법 $O(n log(n))$
* quick sort(unstable)  
임의의 pivot값을 정하고 pivot보다 크거나 작은 값을 재배치하는것을 반복함 $O(n log(n))$ ~ $O(n^2)$

# 재귀함수
---
자기 자신을 재호출하여 사용하는 함수의 방식, 시스템 자원의 효율이 조금 떨어짐  
base case, recurrence relation으로 이루어지며 base case로 모든 문제가 해결이 되어야한다.

# tree
---
데이터의 계층적 구조를 나타내며 하나의 노드가 여러 노드들을 가르킬 수있습니다.

* binary tree  
트리 구조에서 자식 노드를 최대 두개까지 가지는 구조
* tree search
    * preorder 방식  
루트를 방문 후 왼쪽 자식 노드, 오른쪽 자식 노드 순으로 진행되며 자식 노드를 루트 노드화 하며 심층적 탐색을 한다.  
    * inorder 방식  
왼쪽 자식 노드를 가고 루트를 방문한 후 오른쪽 자식 노드로 이동하는 방법으로 자식 노드를 루트 노드화 하며 심층적 탐색을 한다.  
    * postorder 방식  
왼쪽 자식 노드를 가고 오른쪽 자식 노드로 이동한 다음 루트를 방문하는 방법으로 자식 노드를 루트 노드화 하며 심층적 탐색을 한다.
* binary tree search  
중복된 값이 없이 루트의 왼쪽에는 루트보다 작은값 오른쪽에는 루트보다 큰값으로 구성이된다.(중위 탐색 기법으로 구성)  
데이터 삭제시 왼쪽의 최대값 또는 오른쪽의 최소값과 교체한다.  

# heap
---
완전 이진트리의 구조를 가지며 데이터 찾기$O(1)$와 추가,삭제$O(log(n))$가 빠르다.

* max heap  
루트 노드가 자식 노드보다 크거나 같음
* min heap  
루트 노드가 자식 노드보다 작거나 같음
* priority queue  
들어온 순서와 상관없이 우선 순위가 높은 데이터 순으로 처리
* heapify(O(n))  
데이터가 추가(O(logn)) 및 삭제(O(logn))될때 힙 구조를 유지하기 위한 로직

{% highlight python %}
import heapq

min_heap=[1,4,6,3,7,8,2]
heapq.heapify(min_heap)
heapq.heappop(min_heap)
heapq.heappush(min_heap)
{% endhighlight %}

# graph
---
vertex(노드)와 edge(연결선)으로 구성이되며 2차원 행렬 관계도 또는 인접 리스트 관계도로 표현이 가능하다.

* 방향 그래프  
edge에 방향성을 추가한 그래프
* 가중치 그래프  
edge에 가중치를 추가한 그래프
* 순환 그래프  
vertex에서 edge를 거쳐 되돌아 올 수 있는 방향 그래프

* adjacency matrix(인접 행렬)  
연결된 vertex는 1 연결이 안된 vertex는 0으로 나타내는 행렬(메모리 비효율)  
* adjacency list(인접 리스트)  
연결된 vertex를 나열한 리스트를 모은 dictinary  
* implicit graph(암시적 그래프)  

* 그래프 탐색
    * DFS(depth-first-search)  
    깊이 우선 탐색법으로 stack을 이용하거나 preorder inorder postorder를 사용 가능하다.
    * BFS(breadth-first-search)  
    너비 우선 탐색법으로 queue사용가능, 가까운것을 먼저 검색한다고 볼 수 있다.(이미 방문한 노드는 재진입 하지 않는다.)

* 위상정렬
비순환 그래프를 순서대로 출력하는 방법
    * Queue(진입 차수) 활용
    진입 차수는 노드에 들어오는 edge의 수를 의미하며 진입 차수가 0인 노드들을 queue에 넣고 순차적으로 빼면서 연결된 edge를 제거하며 해당 노드를 넣는것을 반복한다.
    * stack(DFS) 활용  
    깊이가 깊은 곳부터 순차적으로 stack을 쌓고 모든 데이터가 전부 쌓이고 나면 추출하는 방식.

* 그래프의 최단거리
    * 다익스트라(Dijkstra)  
    노드에서 노드끼리 최단 경로를 찾는 방법으로 edge의 가중치는 양수로 이루어 진다.

# DP
---
동적 계산법으로 재귀함수에서 하위의 함수가 중복될때 사용  
피보나치의 경우 $O(2^n)$에서 $O(n)$으로 감소  
구하려는것부터 시작하는 top-down, 아는것 부터 시작하는 bottom-up방식이 있다.


# cache
---
데이터를 임시로 저장하는 저장소

* LRU(Least Recently Used)
가장 예전에 사용한 데이터를 삭제하는 방법
* LFU(Least Frequently Used)
가장 사용빈도가 작은 데이터를 삭제하는 방법