# Algorithms

## 1. 스택 (Stack) & 큐 (Queue)

### 1-1. 스택 자료구조

- 먼저 들어온 데이터가 나중에 나가는 형식(선입후출)

- 입구와 출구가 동일한 형태, 상자쌓기로 시각화 가능

- DFS 등 다양한 알고리즘에서 사용되는 자료구조

- 시간복잡도는 항상 O(1)

- 파이썬에서는 리스트 형식을 그대로 사용

📌 구현 예제

  ```python
  stack = []
  
  # 삽입(5) > 삽입(2) > 삽입(3) > 삽입(7) > 삭제() > 삽입(1) > 삽입(4) > 삭제()
  stack.append(5)
  stack.append(2)
  stack.append(3)
  stack.append(7)
  stack.pop()
  stack.append(1)
  stack.append(4)
  stack.pop()
  
  print(stack[::-1])	# 최상단 원소부터 출력
  print(stack)	# 최하단 원소부터 출력
  ```

### 1-2. 큐 자료 구조 (a.k.a. 공평한 자료구조)

- 먼저 들어온 데이터가 먼저 나가는 형식(선입선출)

- 입구와 출구가 모두 뚫려 있는 터널과 같은 형태, 대기열로 시각화 가능

- 파이썬에서 큐를 구현할 때에는 리스트 형식을 사용하면 시간복잡도가 더 높기 때문에 `deque` 라이브러리 사용

- 데이터 삽입은 `append()` , 데이터 삭제는 `popleft()` 를 사용하므로 해당 메소드의 시간복잡도는 O(n)이지만 관행적으로 사용

📌 구현 예제

  ```python
  from collections import deque
  
  # 큐(Queue) 구현을 위해 deque 라이브러리 사용
  queue = deque()
  
  # 삽입(5) > 삽입(2) > 삽입(3) > 삽입(7) > 삭제() > 삽입(1) > 삽입(4) > 삭제()
  queue.append(5)
  queue.append(2)
  queue.append(3)
  queue.append(7)
  queue.popleft()
  queue.append(1)
  queue.append(4)
  queue.popleft()
  
  print(queue)	# 먼저 들어온 순서대로 출력
  queue.reverse()	# 역순으로 바꾸기
  print(queue)	# 나중에 들어온 원소부터 출력
  ```

## 2. 우선순위 큐 (Priority Queue)

- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조
- 데이터를 우선순위에 따라 처리하고 싶을 때 사용
- 자료구조 비교표

| 자료구조                    | 추출되는 데이터             |
| --------------------------- | --------------------------- |
| 스택(Stack)                 | 가장 나중에 삽입된 데이터   |
| 큐(Queue)                   | 가장 먼저 삽입된 데이터     |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높으 데이터 |

- 구현 방법

  1. 리스트로 구현
  2. 힙(heap)으로 구현

- 시간 복잡도

  | 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
  | --------------------- | --------- | --------- |
  | 리스트                | O(1)      | O(N)      |
  | 힙(Heap)              | O(log N)  | O(log N)  |

  > 단순히 N개의 데이터를 힙에 넣었다가 모두 꺼내는 작업 = 힙 정렬
  >
  > 시간 복잡도: O(N log N)

  👉 따라서 힙의 시간 복잡도가 리스트보다 더 낮음!

### 힙(Heap)의 특징

- **완전 이진 트리 자료구조**

  > 루트노드➡왼쪽 자식 노드➡오른쪽 자식 노드 차례로 데이터가 삽입되는 트리

- 항상 루트 노트(root node) 제거

- 최소 힙(min heap)

  - 루트 노드가 가장 작은 값을 가진다.
  - 값이 가장 작은 데이터가 우선적으로 제거된다.

- 최대 힙(max heap)

  - 루트 노드가 가장 큰 값을 가진다.
  - 값이 큰 데이터가 우선적으로 제거된다.

#### 최소 힙 구성 함수: Min-Heapify()

- 상향식: 부모 노드로 거슬러 올라가며 부모보다 자신의 값이 더 작은 경우에는 부모와 자신의 위치를 교체
- 새 원소가 삽입되었을 때에는 O(log N)의 시간 복잡도로 힙 성질을 유지하도록 할 수 있다.
- 힙에서 원소를 제거할 때에도 O(log N)의 시간 복잡도로 힙 성질 유지가 가능하다.
  1. 가장 마지막 노드가 루트 노드의 위치에 오도록 한다.
  2. 루트 노드에서 하향식으로 `Heapify()` 진행

📌 구현 예제

```python
import sys
import heapq	# 파이썬의 힙 라이브러리
input = sys.stdin.readLine

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입 (-1을 인자에 넣으면 max heap 가능)
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기 (-1을 인자에 넣으면 max heap 가능)
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

n = int(input())
arr = []

for i in range(n):
    arr.append(int(input()))

res = heapsort(arr)

for i in range(n):
    print(res[i])
```

## 3. 트리 자료구조 (Tree)

> 가계도처럼 계층적인 구조를 표현할 때 사용할 수 있는 자료구조

- 트리 관련 용어
  - 루트 노드: 부모가 없는 최상위 노드
  - 단말 노드: 자식이 없는 노드
  - 크기: 트리에 포함된 모든 노드의 개수
  - 깊이: 루트 노드부터의 거리
  - 높이: 깊이 중 최댓값
  - 차수: 각 노드의 자식 방향 간선 개수

📌 트리 크기가 N일 때 전체 간선의 개수는 N-1

### 3-1. 이진 탐색 트리(Binary Search Tree)

- 이진 탐색이 동작할 수 있도록 고안된 효율적인 탐색이 가능한 자료구조
- 특징
  - **왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드**
  - 부모 노드보다 왼쪽 자식 노드가 작다.
  - 부모 노드보다 오른쪽 자식 노드가 크다.
- 데이터 조회 과정
  1. 루트 노드부터 방문하여 탐색 진행
  2. 현재 노드와 찾는 원소 값을 비교
  3. 찾는 원소가 더 크면 오른쪽 노드 방문
  4. 현재 노드가 찾는 원소보다 더 크면 왼쪽 노드 방문
  5. 찾는 원소에 다다를 때까지 반복

### 3-2. 트리의 순회

> 트리 자료구조에 포함된 노드를 특정 방법으로 한 번씩 방문하는 방법. 트리의 정보를 시각적으로 확인할 수 있으므로 자주 사용한다.

- 트리 순회 방법
  - 전위 순회: 루트➡왼쪽 자식➡오른쪽 자식
  - 중위 순회: 왼쪽 자식➡루트➡오른쪽 자식
  - 후위 순회: 왼쪽 자식➡오른쪽 자식➡루트

📌 구현 예제

```python
class Node:
    def __init__(self, data, left_node, right_node):
        self.data = data
        self.left_node = left_node
        self.right_node = right_node

# 전위 순회
def pre_order(node):
    print(node.data, end=' ')
    if node.left_node != None:
        in_order(tree[node.left_node])
    print(node.data, end=' ')
    if node.right_node != None:
        in_order(tree[node.right_node])
        
# 중위 순회
def in_dorder(node):
    if node.left_node != None:
        in_order(tree[node.left_node])
    print(node.data, end=' ')
    if node.right_node != Nonde:
        in_order(tree[node.right_node])

# 후위 순회
def post_order(node):
    if node.left_node != None:
        post_order(tree[node.left_node])
    if node.right_node != None:
        post_order(tree[node.right_node])
    print(node.data, end=' ')
    
n = int(input())
tree = []

for i in range(n):
    data, left_node, right_node = input().split()
    if left_node == "None":
        left_node = None
    if right_node == "None":
        right_node = None
    tree[data] = Node(data, left_node, right_node)

pre_order(tree['A'])
print()
in_order(tree['A'])
print()
post_order(tree['A'])
```

## 4. 바이너리 인덱스 트리 (Binary Indexed Tree)

> a.k.a. BIT, 펜윅 트리(Fenwick Tree). 이진법 인덱스 구조를 활용해서 구간 합 문제를 효과적으로 해결해 줄 수 있는 자료구조
>
> 👉 구간 합 알고리즘 문제: https://www.acmicpc.net/problem/2042

- 정수에 따른 이진수 표기 예시

  | 정수 | 이진수 표기                        |
  | ---- | ---------------------------------- |
  | 7    | 00000000 00000000 00000000 0000111 |
  | -7   | 11111111 11111111 11111111 1111001 |

- 0이 아닌 마지막 비트를 찾는 방법

  - 특정 숫자 K의 0이 아닌 마지막 비트 계산: K & -K

  ```python
  n = 8
  for i in range(n+1):
      print(i, "의 마지막 비트:", (i & -i))
  ```

- 바이너리 인덱스 트리 구현 동작 원리

  1. 생성: 0이 아닌 마지막 비트 = 내가 저장하고 있는 값들의 개수

  2. 업데이트

     - 특정 값을 변경하는 경우: 0이 아닌 마지막 비트만큼 더하면서 구간들의 값을 변경

       예) 3번 값 변경: 1~4번 값 변경 ➡ 1~8번 값 변경 ➡ 1~16번값 변경

  3. 누적 합 구하기

     - 1부터 N까지의 누적 합: 0이 아닌 마지막 비트만큼 빼면서 구간들의 값의 합을 계산

       예) 11번까지 누적 합 구하기: 11번 값 + 9~10번 값 + 1~8번 값

📌 구현 예시

```python
import sys
input = sys.stdin.readline

# 데이터의 개수(n), 변경 횟수(m), 구간 합 계산 횟수(k)
n, m, k = map(int, input().split())

# 전체 데이터의 개수는 최대 1,000,000개
arr = [0] * (n + 1)
tree = [0] * (n + 1)

# i번째 수까지의 누적 합을 계산하는 함수
def prefix_sum(i):
    result = 0
    while i > 0:
        result += tree[i]
        # 0이 아닌 마지막 비트만큼 빼가면서 이동
        i -= (i & -i)
    return result

# i번째 수를 dif만큼 더하는 함수
def update(i, dif):
    while i <= n:
        tree[i] += dif
        i += (i & -i)

# start부터 end까지의 구간 합을 계산하는 함수
def interval_sum(start, end):
    return prefix_sum(end) - prefix_sum(start - 1)

for i in range(1, n + 1):
    x = int(input())
    arr[i] = x
    update(i, x)

for i in range(m + k):
    a, b, c = map(int, input().split())
    # 업데이트 연산인 경우
    if a == 1:
        update(b, c - arr[b])	# 바뀐 크기(dif)만큼 적용
    else:
        print(interval_sum(b, c))
```

## 5. 정렬 알고리즘: 선택 정렬과 삽입 정렬

> 정렬(Sorting): 데이터를 특정한 기준에 따라 순서대로 나열하는 것

### 5-1. 선택 정렬

- 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복하는 정렬법

- 동작 순서

  1. 처리되지 않은 데이터 중 가장 작은 데이터를 선택해서 가장 앞의 데이터와 바꾼다.
  2. 처리되지 않은 데이터 중 가장 작은 데이터를 선택해서 앞에서 두 번째 데이터와 바꾼다.
  3. 정렬이 완료될 때까지 반복

  👉 탐색 범위는 반복할 때마다 줄어들고, 처리되지 않은 데이터 구간에서 가장 값이 작은 데이터를 찾기 위해 또 반복을 수행하므로 **이중 반복문**으로 구현 가능

- 시간 복잡도: O(N^2)

  - N + (N - 1) + (N - 2) + ... + 2 = (N^2 + N - 2) 2

📌 구현 예시

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
    min_index = i	# 가장 작은 원소의 인덱스
    for j in range(i + 1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i]	# 스와프

print(array)
```

### 5-2. 삽입 정렬

- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입하는 정렬 방법
- 선택 정렬에 비해 구현 난이도는 높으나 더 효율적
- 동작 순서 (오름차순)
  1. 첫 번째 데이터를 기준으로 두 번째 데이터가 첫 번째 데이터의 왼쪽 또는 오른쪽 중 어디로 삽입되어야 할지 판단
  2. 세 번째 데이터가 어디로 삽입되어야 할지 첫 번째 데이터부터 순서대로 두 번째 데이터까지 값의 크기를 비교 판단
  3. 반복
- 시간 복잡도: O(N^2). 단, 현재 리스트의 데이터가 거의 정렬된 상태라면 O(N)

📌 구현 예제

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
    for j in range(i, 0, -1):	# 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
        if array[j] < array[j - 1]:	# 한 칸씩 왼쪽으로 이동
            array[j], array[j - 1] = array[j - 1], array[j]
        else:	# 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
            break
print(array)
```

## 6. 빠른 정렬 알고리즘: 퀵 정렬과 계수 정렬

### 6-1. 퀵 정렬

- 기준 데이터를 설정하고 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 정렬 방법
  - 기본적으로 첫 번째 데이터를 기준 데이터(`pivot`)로 설정
- 일반적으로 가장 많이 사용되는 정렬 알고리즘
- 병합 정렬과 함께 C, 파이썬, Java 등의 정렬 라이브러리의 근간이 되는 알고리즘
- 동작 순서
  1. 첫 번째 데이터를 현재 피벗으로 설정 후 왼쪽에서부터 피벗보다 큰 데이터 선택 후 오른쪽에서부터 피벗보다 작은 데이터 선택
  2. 선택된 2개의 데이터 위치를 교체
  3. 반복
  4. 만약 왼쪽에서부터 선택한 데이터와 오른쪽에서부터 선택한 데이터의 위치가 엇갈리는 경우에는 피벗과 값이 작은 데이터의 위치를 서로 변경
  5. 피벗의 위치를 기준으로 왼쪽에는 피벗보다 작은 값을 가진 데이터, 오른쪽에는 피벗보다 큰 값을 가진 데이터의 묶음으로 분할 완료
  6. 각각의 데이터 묶음에 대해 퀵 정렬 실시
- 퀵 정렬이 빠른 이유
- 

