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

- 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에 사용된다.

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

- 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복하는 정렬 알고리즘

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

- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입하는 정렬 알고리즘
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

- 기준 데이터를 설정하고 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 정렬 알고리즘
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

  👉 이상적인 경우에 연산해야 할 데이터가 절반씩 줄어들기 때문에 전체 연산 횟수가 O(N log N)이다.

- 시간 복잡도: 표준 라이브러리를 사용할 때 O(N log N). 첫 번째 원소를 피벗으로 하여 직접 퀵 정렬을 구현했을 때 최악의 경우에는 O(N^2)

📌 구현 예제

- 파이썬 일반적인 방식으로 구현

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    if start >= end:	# 원소가 1개인 경우 종료
        return
    pivot = start	# 피벗은 첫 번째 원소
    left = start + 1	# 피벗 바로 오른쪽 원소부터 정렬 시작
    right = end		# 마지막 원소
    while(left <= end and array[left] <= array[pivot]):
        right -= 1
        # 피벗보다 작은 데이터를 찾을 때까지 반복
        while(left <= end and array[left] <= array[pivot]):
            right -= 1
        if(left > right):	# 엇갈렸다면 작은 데이터와 피벗을 교체
            array[right], array[pivot] = array[pivot], array[right]
        else:	# 엇갈리지 않았다면 작은 데이터와 큰 데이터를 교체
            array[left], array[right] = array[right], array[left]
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
    quick_sort(array, start, right - 1)
    quick_sort(array, right + 1, end)

quick_sort(array, 0, len(array) - 1)
print(array)
```

- 파이썬의 장점을 살려서 간결하게 구현

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array):
    # 리스트가 하나 이하의 원소만 담고 있다면 종료
    if len(array) <= 1:
        return array
    pivot = array[0]	# 피벗은 첫 번째 원소
    tail = array[1:]	# 피벗을 제외한 리스트
    
    left_side = [x for x in tail if x <= pivot]	# 분할된 왼쪽 부분
    right_side = [x for x in tail if x > pivot]	# 분할된 오른쪽 부분
    
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬을 수행하고 전체 리스트 반환
    return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

### 6-2. 계수 정렬

- 특정 조건에 부합할 때만 사용 가능하지만 매우 빠르게 동작하는 정렬 알고리즘

  - 특정 조건: **데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때**

- 데이터의 개수가 N, 데이터(양수) 중 최댓값이 K일 때 최악의 경우에도 수행 시간 O(N + K) 보장

- 동작 순서

  1. 가장 작은 데이터부터 가장 큰 데이터까지의 범위가 모두 담길 수 있도록 리스트 생성
  2. 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가
  3. 그 결과, 리스트에는 각 데이터가 몇 번씩 등장했는지 횟수 기록
  4. 결과를 확인할 때에는 리스트의 첫 번째 데이터부터 하나씩 그 값만큼 반복하여 인덱스 출력

- 퀵 정렬에 비해 공간 복잡도는 높으나 조건만 맞으면 훨씬 빠르게 동작한다.

- 복잡도 분석

  - 시간 복잡도: O(N + K). 각 데이터를 일일이 확인해서 이중 for문을 돌기 때문.

  - 공간 복잡도: O(N + K). 데이터의 전체 크기와 데이터의 가장 큰 값 = 리스트 크기가 필요하기 때문.

  - 데이터의 값이 큰 경우에는 비효율적

    예) 0과 999,999 2개의 데이터만 존재할 때

  - 동일한 값을 가지는 데이터가 여러 개 등장할 때 계수 정렬 사용시 효과적

    예) 성적 확인

📌 구현 예제

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
# 모든 범위를 포함하는 리스트 선언(모든 값은 0으로 초기화)
count = [0] * (max(array) + 1)

for i in range(len(array)):
    count[array[i]] += 1	# 각 데이터에 해당하느 인덱스 값 증가

for i in range(len(count)):	# 리스트에 기록된 정렬 정보 확인
    for j in range(count[i]):
        print(i, end=' ')	# 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
```

## 7. 정렬 알고리즘 정리

| 정렬 알고리즘 | 평균 시간 복잡도 | 공간 복잡도 | 특징                                                         |
| ------------- | ---------------- | ----------- | ------------------------------------------------------------ |
| 선택 정렬     | O(N^2)           | O(N)        | 아이디어가 매우 간단해서 구현 쉬운 편                        |
| 삽입 정렬     | O(N^2)           | O(N)        | 데이터가 거의 정렬되어 있을 때에는 가장 빠르게 동작          |
| 퀵 정렬       | O(N log N)       | O(N)        | 대부분의 경우에 가장 적합하며 충분히 빠른 편이나 최악의 경우 시간 복잡도가 O(N^2) |
| 계수 정렬     | O(N + K)         | O(N + K)    | 데이터의 크기가 한정된 경우에만 사용 가능하지만 매우 빠르게 동작 |

- 대부분의 프로그래밍 언어에서 지원하는 **표준 정렬 라이브러리는 최악의 경우에도 O(N log N)을 보장**하도록 설계되어 있다.

### 문제 

동빈이는 두 개의 배열 A와 B를 가지고 있다. 각 배열은 N개의 원소로 구성되어 있고, 배열의 원소는 모두 자연수이다. 동빈이는 최대 K번의 바꿔치기 연산을 구행할 수 있으며, 바꿔치기 연산은 배열 A에 있는 원소 하나와 배열 B에 있는 원소 하나를 골라서 두 원소를 서로 바꾸는 것을 의미한다. 동빈이의 최종 목표는 배열 A의 모든 원소의 합이 최대가 되도록 하는 것이다. N, K, 배열 A와 B의 정보가 주어졌을 때, 최대 K번의 바꿔치기 연산을 수행하며 만들 수 있는 배열 A의 모든 원소의 합의 최댓값을 출력하는 프로그램을 작성하시오.

`입력조건`

- 첫 번째 줄에 N, K가 공백을 기준으로 구분되어 입력된다. (1 <= N <= 100,000, 0 <= K <= N)
- 두 번째 줄에 배열 A의 원소들이 공백을 기준으로 구분되어 입력된다. 모든 원소는 10,000,000보다 작은 자연수이다.
- 세 번째 줄에 배열 B의 원소들이 공백을 기준으로 구분되어 입력된다. 모든 원소는 10,000,000보다 작은 자연수이다.

`출력조건`

- 최대 K번의 바꿔치기 연산을 수행하여 만들 수 있는 배열 A의 모든 원소의 합의 최댓값을 출력한다.

### 답안

```python
n, k = map(int, input().split())
a = list(map(int, input().split()))
b = list(map(int, input().split()))

a.sort()
b.sort(reverse=True)

for i in range(k):
    if a[i] < b[i]:
        # 원소 교체
        a[i], b[i] = b[i], a[i]
    else:
        break

print(sum(a))
```

## 8. 그래프 탐색: DFS & BFS

### 8-1. DFS (Depth-Fisrt Search) = 깊이 우선 탐색

- 깊은 부분을 우선적으로 탐색하는 알고리즘

- 스택 자료구조(or 재귀 함수) 이용

- 동작 순서

  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
  2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있다면 그 노드를 스택에 넣고 방문 처리. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다. (방문 기준: 번호가 낮은 인접 노드부터 방문)
  3. 반복

- 동작 예시

  ![image-20210628111609955](../../md-img/image-20210628111609955.png)

📌 구현 예제

```python
# DFS 메소드 정의
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)
        
# 각 노드가 연결된 정보를 표현한 2차원 리스트
graph = [
    [],	# 보통 1번 노드부터 시작하므로 0번 노드는 비워둔다.
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

# 각 노드가 방문된 정보를 표현한 1차원 리스트
visited = [False] * 9	# 1번 노드부터 시작하므로 1개 더 크게 초기화

# 정의된 DFS 함수 호출
dfs(graph, 1, visited)
```

### 8-2. BFS (Breadth-First Search) = 너비 우선 탐색

- 가까운 노드부터 우선적으로 탐색하는 알고리즘

- 큐 자료구조 이용

- 최단 거리를 구할 때 사용되기도 한다.

- 동작 순서

  1. 탐색 시작 노드를 큐에 삽입하고 방문 처리 (방문 기준: 번호가 낮은 인접 노드부터 방문)
  2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
  3. 반복

- 동작 예시

  ![image-20210628113927571](../../md-img/image-20210628113927571.png)

📌 구현 예제

```python
from collections import deque

# BFS 메소드 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end=' ')
        # 아직 방문하지 않은 인접한 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True
                
# 각 노드가 연결된 정보를 표현한 2차원 리스트
graph = [
    [],	# 보통 1번 노드부터 시작하므로 0번 노드는 비워둔다.
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

# 각 노드가 방문된 정보를 표현한 1차원 리스트
visited = [False] * 9	# 1번 노드부터 시작하므로 1개 더 크게 초기화

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)
```

## 9. DFS & BFS 기초 문제 풀이

### 문제 1. 음료수 얼려 먹기

N x M 크기의 얼음 틀이 있다. 구멍이 뚫린 부분은 0, 칸막이가 존재하는 부분은 1로 표시된다. 구멍이 뚫려 있는 부분끼리 상, 하, 좌, 우로 붙어 있는 경우에 서로 연결되어 있는 것으로 간주한다. 얼음 틀 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을 작성하시오. 다음의 4 x 5 얼음 틀 예시에서는 아이스크림이 총 3개 생성된다.

`입력 조건`

- 첫 번째 줄에 얼음 틀의 세로 길이 N과 가로 길이 M이 주어진다. (1 <= N, M <= 1,000)
- 두 번째 줄부터 N + 1 번째 줄까지 얼음 틀의 형태가 주어진다.
- 이때 구멍이 뚫려있는 부분은 0, 그렇지 않은 부분은 1이다.

`출력 조건`

- 한 번에 만들 수 있는 아이스크림의 개수를 출력한다.

`입력 예시`

```powershell
4 5
00110
00011
11111
00000
```

`출력 예시`

```powershell
3
```

### 답안

```python
n, m = map(int, input().split())
ice = []
for i in range(n):
    ice.append(list(map(int, input())))

def dfs(a, b):
    # 주어진 범위를 벗어나는 경우 즉시 종료
    if a <= -1 or a >= n or b <= -1 or b >= m:
        return False
    # 현재 노드를 아직 방문하지 않았을 때
    if ice[a][b] == 0:
        # 해당 노드 방문 처리
        ice[a][b] = 1
        # 상하좌우 위치들 재귀적으로 호출
        dfs(a-1, b)
        dfs(a, b-1)
        dfs(a+1, b)
        dfs(a, b+1)
        return True
    return False

# 모든 노드(위치)에 음료수 채우기
cream = 0
for i in range(n):
    for j in range(m):
        # 현재 위치에서 dfs 알고리즘 수행
        if dfs(i, j) == True:
            cream += 1

print(cream)
```

### 문제 2. 미로 탈출

동빈이는 N x M 크기의 직사각형 형태의 미로에 갇혔다. 미로에는 여러 마리의 괴물이 있어 이를 피해 탈출해야 한다. 동빈이의 위치는 (1, 1)이며 미로의 출구는 (N, M)의 위치에 존재하며 한 번에 한 칸씩 이동할 수 있다. 이때 괴물이 있는 부분은 0으로, 괴물이 없는 부분은 1로 표시되어 있다. 미로는 반드시 탈출할 수 있는 형태로 제시된다. 동빈이가 탈출하기 위해 움직여야 하는 최소 칸의 개수를 구하라. 칸을 셀 때는 시작 칸과 마지막 칸을 모두 포함해서 계산한다.

`입력 조건`

- 첫째 줄에 두 정수 N, M(4 <= N, M <= 200)이 주어진다. 다음 N개의 줄에는 각각 M개의 정수(0 또는 1)로 미로의 정보가 주어진다. 각각의 수들은 공백 없이 붙어서 입력으로 제시된다. 또한 시작 칸과 마지막 칸은 항상 1이다.

`출력 조건`

- 첫째 줄에 최소 이동 칸의 개수를 출력한다.

`입력 예시`

```powershell
5 6
101010
111111
000001
111111
111111
```

`출력 예시`

```powershell
10
```

### 답안

```python
from collections import deque

n, m = map(int, input().split())
miro = []
for i in range(n):
    miro.append(list(map(int, input())))

# 이동할 네 가지 방향 정의(상하좌우)
da = [-1, 1, 0, 0]
db = [0, 0, -1, 1]

def bfs(a, b):
    # 큐 구현을 위해 deque 라이브러리 사용
    queue = deque()
    queue.append((a, b))
    # 큐가 빌 때까지 반복
    while queue:
        a, b = queue.popleft()
        # 현재 위치에서 4가지 방향으로 위치 확인
        for i in range(4):
            na = a + da[i]
            nb = b + db[i]
            # 미로 찾기 공간을 벗어난 경우 무시
            if na < 0 or na >= n or nb < 0 or nb >= m:
                continue
            # 벽인 경우 무시
            if miro[na][nb] == 0:
                continue
            # 해당 노드를 처음 방문하는 경우에만 최단 거리 기록
            if miro[na][nb] == 1:
                miro[na][nb] = miro[a][b] + 1
                queue.append((na, nb))
    # 가장 오른쪽 아래까지의 최단 거리 반환
    return miro[n-1][m-1]

print(bfs(0, 0))
```

## 10. 다익스트라 알고리즘: 최단 경로 계산

- 최단 경로 알고리즘 - 문제 상황
  - 한 지점에서 다른 한 지점까지의 최단 경로
  - 한 지점에서 다른 모든 지점까지의 최단 경로
  - 모든 지점에서 다른 모든 지점까지의 최단 경로
- 노드: 각 지점
- 간선: 지점 간 연결된 도로

### 10-1. 다익스트라 최단 경로 알고리즘 - 간단한 구현 방법

> 특정한 노드에서 출발해서 다른 모든 노드로 가는 최단 경로 계산 알고리즘

- 옴의 간선이 없을 때 정상적으로 동작
  - 현실 세계의 도로(간선)는 옴의 간선으로 표현되지 않는다.
- **매 상황에서 가장 비용이 적은 노드를 선택**해서 임의의 과정을 반복하므로 `그리디 알고리즘`으로 분류
  - 최단 경로 알고리즘은 원래 기본적으로는 다이나믹 프로그래밍 알고리즘으로 분류된다.

#### 동작 순서

1. 출발 노드 설정
2. 최단 거리 테이블 초기화
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드 선택
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신
5. 3번과 4번 반복

#### 특징

- 알고리즘 동작 과정에서 최단거리 테이블은 각 노드에 대한 현재까지의 최단거리 정보를 가지고 있다.
- 처리 과정에서 더 짧은 경로를 찾으면 최단거리 테이블 갱신
- 이미 앞선 노드들이 모두 처리되었으므로 마지막 노드는 처리하지 않는다.
- 단계를 거치며 한 번 처리된 노드의 최단거리는 고정되어 더 이상 바뀌지 않는다.
  - 한 단계당 하나의 노드에 대한 최단거리를 확실히 찾는 것
- 다익스트라 알고리즘을 수행한 뒤에 테이블에 각 노드까지의 최단거리 정보가 저장된다.
  - 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가적인 기능을 더 넣어야 한다.

#### 📌 구현 예제 

- 방문하지 않은 노드 중 가장 거리가 짧은 노드를 선택하기 위해 매 단계마다 1차원 테이블의 모든 원소를 확인(순차 탐색)한다.

```python
import sys
input = sys.stdin.readline
INF = int(1e9)	# 무한을 의미하는 값으로 10억 설정

# 노드 개수와 간선 개수 입력받기
n, m = map(int, input().split())
# 시작 노드 번호 입력받기
start = int(input())
# 각 노드에 연결된 노드에 대한 정보를 담는 리스트 만들기
graph = [[] for i in range(n+1)]
# 방문한 적 있는지 체크하는 리스트 만들기
visited = [False] * (n+1)

# 모든 간선 정보 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c이다. 튜플로 리스트에 append해준다.
    graph[a].append((b, c))
                    
# 방문하지 않은 노드 중에서 최단거리 노드의 번호 반환
def get_smallest_node():
    min_value = INF	# 최단거리를 무한으로 초기화
    index = 0	# 최단거리 노드(인덱스)
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = 1
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[i]
    # 시작 노드를 제외한 전체 n-1개의 노드에 대해 반복
    for i in range(n-1):
        # 현재 최단거리가 가장 짧은 노드를 꺼내서 방문 처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른 노드 확인
        for j in graph[now]:
            cost = distance[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost
          
# 다익스트라 알고리즘 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단거리 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우 무한(INFINITY)라고 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

- 시간 복잡도: O(V^2). 총 O(V)번에 걸쳐서 최단거리가 가장 짧은 노드를 매번 선형 탐색해야 하기 때문

- 일반적으로 코딩 테스트 최단 경로 문제에서 전체 노드의 개수가 5,000개 이하일 때에는 다익스트라 알고리즘의 간단한 구현 방식으로 해결 가능

- *만약 노드 개수가 100,000개가 넘어간다면?*

  👉 [**우선순위 큐(Priority Queue)**](#2.-우선순위-큐-(priority-queue))

### 10-2. 다익스트라 최단경로 알고리즘 - 개선된 구현 방법 (우선순위 큐)

- 단계마다 방문하지 않은 노드 중에서 최단거리가 가장 짧은 노드를 선택하기 위해 `힙(Heap)` 자료구조를 이용한다.
- 다익스트라 알고리즘 동작 기본 원리는 동일
  - 현재 가장 가까운 노드를 저장하기 위해 힙 자료구조를 추가적으로 이용
  - 현재의 최단거리가 가장 짧은 노드를 선택해야 하므로 최소 힙 사용

- 최소 힙

```python
import heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

- 최대 힙

```python
import heapq

# 내림차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)	# 최대 힙은 라이브러리가 따로 없으므로 거꾸로 넣어준다
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기 -거꾸로 꺼낸다
    for i in range(len(h)):
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

#### 동작 순서

1. 그래프를 준비하고 출발 노드를 설정하여 우선순위 큐에 삽입
2. 우선순위 큐에서 원소를 꺼낸다. 1번 노드는 아직 방문하지 않았으므로 이를 처리한다.
   - 1번 노드까지의 거리는 0으로 처리
3. 우선순위 큐에서 원소를 꺼낸다. 현재 최단거리가 가장 짧은 노드는 아직 방문하지 않았으므로 이를 처리한다.
4. 반복

#### 📌 구현 예제

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)	# 무한을 의미하는 값으로 10억 설정

# 노드 개수와 간선 개수 입력받기
n, m = map(int, input().split())
# 시작 노드 번호 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 생성
graph = [[] for i in range(n+1)]
# 최단거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보 입력받기
for _ in graph(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용 = c
    graph[a].append((b, c))

def dijkstra(start):
    q = []
    # 시작노드로 가기 위한 최단거리는 0으로 설정해서 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:	# 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        # 따라서 아래 for문이 반복되어봤자 최대 간선 개수만큼만 반복된다.
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접 노드 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
                
# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우 무한(INFINITY) 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

- 시간 복잡도: O(E log V)
  - 노드를 하나씩 꺼내 검사하는 반복문(while문)은 최대 노드의 개수인 V만큼의 횟수로 처리된다.
  - 이미 방문하여 처리된 것은 넘어가도록 구현했기 때문에 우선순위 큐에서 꺼낸 노드와 인접한 노드를 확인하는 총횟수는 최대 간선의 개수(E)이다.
  - 전체 과정은 E개의 원소를 우선순위 큐에 넣었다가 모두 빼내는 연산과 매우 유사하여 시간 복잡도를 O(E log E)로 판단할 수 있으며 중복 간선을 포함하지 않는 경우에는 O(E log V)가 된다.

## 11. 플로이드 워셜(Floyd-Warshall) 알고리즘

> 모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산하는 알고리즘

- 단계별로 거쳐가는 노드를 기준으로 알고리즘을 수행 _but 매 단계마다 방문하지 않은 노드 중에 최단거리를 가진 노드를 찾는 과정 불필요_
- 2차원 테이블에 최단거리 정보 저장
- 다이나믹 프로그래밍 유형

#### 점화식

- 각 단계마다 특정한 노드 k를 거쳐가는 경우 확인
  - a에서 b로 가는 최단거리보다 a에서 k를 거쳐서 b로 가는 거리가 더 짧은지 검사

```
Dab = min(Dab, Dak + Dkb)
```

#### 동작 순서

1. 그래프를 준비하고 최단거리 테이블 초기화
2. 1번 노드를 거쳐가는 경우를 고려하여 테이블 갱신
3. 2번 노드를 거쳐가는 경우를 고려하여 테이블 갱신
4. 반복

#### 📌 구현 예제

```python
INF = int(1e9)	# 무한을 의미하는 값으로 10억 설정

# 노드 개수와 간선 개수 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 치고하
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0
            
# 각 간선에 대한 정보를 입력받아 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c
    
# 점화식에 따라 프롤이드 워셜 알고리즘 수행
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])
            
# 수행된 결과 출력
for a in range(1, n+1):
    for b in range(1, n+1):
        # 도달할 수 없는 경우 무한(INFINITY) 출력
        if graph[a][b] == INF:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리 출력
        else:
            print(graph[a][b], end=" ")
    print()
```

- 시간 복잡도: O(N^3)
  - 노드의 개수가 N개일 때 알고리즘상으로 N번의 단계를 수행하며 각 단계마다 O(N^2)의 연산을 통해 현재 노드를 거쳐가는 모든 경로를 고려한다.

## 12. 벨만 포드 알고리즘

> 비용이 음수인 간선이 있을 때 최단 경로를 구하는 알고리즘

### 문제. 타임머신

> 참조: https://www.acmicpc.net/problem/11657

N개의 도시가 있다. 그리고 한 도시에서 출발하여 다른 도시에 도착하는 버스가 M개 있다. 각 버스는 A, B, C로 나타낼 수 있는데, A는 시작도시, B는 도착도시, C는 버스를 타고 이동하는데 걸리는 시간이다. 시간 C가 양수가 아닌 경우가 있다. C = 0인 경우는 순간 이동을 하는 경우, C < 0인 경우는 타임머신으로 시간을 되돌아가는 경우이다. 1번 도시에서 출발해서 나머지 도시로 가는 가장 빠른 시간을 구하는 프로그램을 작성하시오.

`입력 조건`

- 첫째 줄에 도시의 개수 N (1 ≤ N ≤ 500), 버스 노선의 개수 M (1 ≤ M ≤ 6,000)이 주어진다. 둘째 줄부터 M개의 줄에는 버스 노선의 정보 A, B, C (1 ≤ A, B ≤ N, -10,000 ≤ C ≤ 10,000)가 주어진다.

`출력 조건`

- 만약 1번 도시에서 출발해 어떤 도시로 가는 과정에서 시간을 무한히 오래 전으로 되돌릴 수 있다면 첫째 줄에 -1을 출력한다. 그렇지 않다면 N-1개 줄에 걸쳐 각 줄에 1번 도시에서 출발해 2번 도시, 3번 도시, ..., N번 도시로 가는 가장 빠른 시간을 순서대로 출력한다. 만약 해당 도시로 가는 경로가 없다면 대신 -1을 출력한다.

`입력 예시`

```powershell
3 4
1 2 4
1 3 3
2 3 -1
3 1 -2
```

`출력 예시`

```powershell
4
3
```

- 양수 간선만 있을 때에는 다익스트라 알고리즘을 사용할 수 있지만 음수 간선이 존재하거나 음수 간선의 순환이 포함되었을 떄에는 사용 불가

  👉 음수 간선이 있을 때에는  **벨만 포드 최단 경로 알고리즘** 사용

### 11-1. 벨만 포드 최단 경로 알고리즘

- 최단 경로 문제 분류
  1. 모든 간선이 양수인 경우
  2. **음수 간선**이 존재하는 경우
     1. 음수 간선 순환이 없는 경우
     2. 음수 간선 순환이 있는 경우
- 특징
  - 음수 간선이 포함된 상황에서도 사용 가능
  - ***음수 간선의 순환 감지*** 가능 ❗❗
  - 기본 시간 복잡도는 O(VE)로 다익스트라 알고리즘에 비해 느리다.

#### 동작 순서

1. 출발 노드 설정
2. 최단거리 테이블 초기화
3. 아래 과정을 N-1번 반복
   1. 전체 간선 E개를 하나씩 확인
   2. 각 간선을 거쳐 다른 노드로 가는 비용을 계싼하여 최단거리 테이블 갱신

💡 음수 간선 순환이 발생하는지 확인하고 싶을 때에는 **3번 과정을 한 번 더 수행**하여 최단거리 테이블 갱신 여부를 파악하면 된다.

#### 다익스트라 알고리즘과의 비교

- 다익스트라 알고리즘
  - 매번 방문하지 않은 노드 중에서 최단거리가 가장 짧은 노드를 선택
  - 음수 간선이 없다면 최적의 해를 찾을 수 있다.
- 벨만 포드 알고리즘
  - 매번 모든 간선을 전부 확인하므로 다익스트라 알고리즘의 최적의 해를 항상 포함
  - 다익스트라 알고리즘에 비해서 시간이 오래 걸리지만 음수 간선 순환 탐지 가능

#### 📌 구현 예제

````python
import sys
input = sys.stdin.readline
INF = int(1e9)	# 무한을 의미하는 값으로 10억 설정

def bf(start):
    # 시작노드 초기화
    dist[start] = 0
    # 전체 n번의 라운드(round)를 반복
    for i in range(n):
        # 매 반복마다 모든 간선 확인
        for j in range(m):
            cur = edges[j][0]
            next_node = edges[j][1]
            cost = edges[j][2]
            # 현재 간선을 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if dis[cur] != INF and dist[next_node] > dis[cur] + cost:
                dis[next_node] = dist[cur] + cost
                # n번째 라운드에서도 값이 갱신된다면 음수 순환 존재
                if i == n - 1:
                    return True
    return False

# 노드 개수와 간선 개수 입력받기
n, m = map(int, input().split())
# 모든 간선에 대한 정보를 담는 리스트 생성
edges = []
# 최단거리 테이블을 모두 무한으로 초기화
dist = [INF] * (n + 1)

# 모든 간선 정보 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용 = c
    edges.append((a, b, c))
    
# 벨만 포드 알고리즘 수행
negative_cycle = bf(1)	# 1번 노드가 시작 노드

if negative_cycle:
    print("-1")
else:
    # 1번 노드를 제외한 다른 모든 노드로 가기 위한 최단 거리 출력
    for i in range(2, n + 1):
        # 도달할 수 없는 경우 -1 출력
        if dist[i] == INF:
            print("-1")
        # 도달할 수 있는 경우 거리 출력
        else:
            pritn(dist[i])
````

## 13. 유니온 파인드 자료구조: 서로소 집합 판단

### 13-1. 서로소 집합 (Disjoint Sets) 자료구조

> 서로소 집합: 공통 원소가 없는 두 집합

- 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조
- 두 종류의 연산 지원
  - **합집합(Union)**: 두 개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산
  - **찾기(Find)**: 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산
- **합치기 찾기(Union Find)** 자료구조라고도 불린다.

#### 동작 순서

1. 합집합(Union) 연산을 확인하여 서로 연결된 두 노드 A, B를 확인
   1. A와 B의 루트 노드 A', B'를 각각 찾는다.
   2. A'를 B'의 부모 노드로 설정한다.
2. 모든 합집합(Union) 연산을 처리할 때까지 1번 반복

- 동작 순서 예시

  - 처리할 연산: Union(1, 4), Union(2, 3), Union(2, 4), Union(5, 6)

  1. 노드의 개수 크기의 부모 테이블 초기화
  2. 노드 1과 노드 4의 루트 노드를 각각 찾는다. 현재 루트 노드는 각각 1과 4이므로 더 큰 번호인 노드 4의 부모를 노드 1로 설정
  3. 노드 2와 노드 3의 루트 노드를 각각 찾는다. 현재 루트 노드는 2와 3이므로 더 큰 번호인 노드 3의 부모를 노드 2로 설정
  4. 노드 2와 노드 4의 루트 노드를 각각 찾는다. 현재 루트 노드는 2와 1이므로 더 큰 번호인 노드 2의 부모는 노드 1로 설정
  5. 노드 5와 노드 6의 루트 노드를 각각 찾는다. 현재 루트 노드는 5와 6이므로 더 큰 번호인 노드 6의 부모는 노드 5로 설정

### 13-2. 서로소 집합 자료구조: 연결성

- 서로소 집합 자료구조에서는 연결성을 통해 손쉽게 집합의 형태 확인 가능
- 기본적인 형태의 서로소 집합 자료구조에서는 루트 노드에 즉시 접근할 수 없다.
  - 루트 노드를 찾기 위해 부모 테이블을 계속 확인하며 거슬러 올라가야 하기 때문

#### 📌 구현 예제 - 기본적인 구현 방법

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return x

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
# 노드의 개수와 간선(Union 연산) 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1)	# 부모 테이블 초기화

# 부모 테이블상에서 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
# 각 원소가 속한 집합 출력
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, i), end=' ')
 
print()

# 부모 테이블 내용 출력
print('부모 테이블: ', end='')
for i in range(1, v + 1):
    print(parent[i], end=' ')
```

- 기본적인 구현 방법의 문제점
  - 합집합(Union) 연산이 편향되게 이루어지는 경우 찾기(Find) 함수가 비효율적으로 동작
  - 최악의 경우에는 찾기(Find) 함수가 모든 노드를 다 확인하게 되어 시간 복잡도가 O(V)가 된다.

### 13-3. 서로소 집합 자료구조: 경로 압축

> 찾기(Find) 함수를 재귀적으로 호출한 뒤에 부모 테이블 값을 바로 갱신하는 방법

#### 📌 구현 예제 - 일부분 수정

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```

- 경로 압축 기법을 적용하면 각 노드에 대해 찾기(Find) 함수를 호출한 이후에 해당 노드의 루트 노드가 바로 부모 노드가 된다.
- **모든 합집합(Union) 함수를 처리한 후 각 원소에 대해 찾기(Find) 함수를 수행하면 부모 테이블이 갱신**되므로 기본적인 방법에 비하여 시간 복잡도가 개선된다.

### 13-4. 서로소 집합을 활용한 사이클 판별 알고리즘

- 무방향 그래프 내에서의 사이클을 판별할 때 사용
  - 방향 그래프에서의 사이클 여부는 DFS를 이용하여 판별한다.

#### 동작 순서

1. 모든 노드에 대해 자기 자신을 부모로 설정하는 형태로 부모 테이블 초기화
2. 각 간선을 하나씩 확인하며 두 노드의 루트 노드를 확인
   1. 루트 노드가 서로 다르면 두 노드에 대해 합집합(Union) 연산 수행
   2. 루트 노드가 서로 같으면 사이클(Cycle) 발생
3. 그래프에 포함된 모든 간서에 대해 1번 반복

#### 📌 구현 예제

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
# 노드의 개수와 간선(Union 연산) 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1)	# 부모 테이블 초기화

# 부모 테이블상에서 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
cycle = False	# 사이클 발생 여부

for i in range(e):
    a, b = map(int, input().split())
    # 사이클이 발생한 경우 종료
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    # 사이클이 발생하지 않으면 합집합(Union) 연산 수행
    else:
        union_parent(parent, a, b)
        
if cycle:
    print("사이클이 발생했습니다.")
else:
    print("사이클이 발생하지 않았습니다.")
```

## 14. 크루스칼 알고리즘: 최소 신장 트리를 찾는 알고리즘

### 14-1. 신장 트리

> 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프

- 트리의 조건: 모든 노드가 포함되어 서로 연결되면서 사이클이 존재하지 않는다

### 14-2. 최소 신장 트리

- 문제 예제
  - 최소한의 비용으로 구성되는 신장 트리 찾기
  - N개의 도시가 존재하는 상황에서 두 도시 사이에 도로를 놓아 전체 도시가 서로 연결될 수 있게 도로 설치하기

### 14-3. 크루스칼 알고리즘

- 대표적인 최소 신장 트리 알고리즘
- 그리디 알고리즘의 한 종류

#### 동작 순서

1. 간선 데이터를 비용을 기준으로 오름차순 정렬
2. 정렬된 순서대로 간선을 하나씩 합집합 연산을 수행하며 현재의 간선이 사이클을 발생시키는지 확인
   1. 사이클이 발생하지 않으면 최소 신장 트리에 포함
   2. 사이클이 발생하면 최소 신장 트리에서 제외
3. 모든 간선에 대해 2번 반복
4. 최소 신장 트리에 포함된 간선의 비용을 모두 더해서 최종 비용 계산

#### 📌 구현 예제

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드 찾을 때까지 재귀 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
       
# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1)	# 부모 테이블 초기화

# 모든 간선을 담을 리스트와 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
# 모든 간선에 대한 정보 입력받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용 순으로 정렬하기 위해 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))
    
# 간선 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
        
print(result)
```

- 시간 복잡도: 표준 라이브러리 사용 시 간선 개수가 E개일 때, O(E log E)
  - 가장 많은 시간을 요구하는 곳은 간선 정렬

## 15. 최소 공통 조상: 트리에서 최소 공통 조상 찾기 알고리즘

#### 문제1. LCA (기초 문제)

> 참조: https://www.acmicpc.net/problem/11437

N(2 ≤ N ≤ 50,000)개의 정점으로 이루어진 트리가 주어진다. 트리의 각 정점은 1번부터 N번까지 번호가 매겨져 있으며, 루트는 1번이다. 두 노드의 쌍 M(1 ≤ M ≤ 10,000)개가 주어졌을 때, 두 노드의 가장 가까운 공통 조상이 몇 번인지 출력한다.

`입력 조건`

- 첫째 줄에 노드의 개수 N이 주어지고, 다음 N-1개 줄에는 트리 상에서 연결된 두 정점이 주어진다.
- 그 다음 줄에는 가장 가까운 공통 조상을 알고싶은 쌍의 개수 M이 주어지고, 다음 M개 줄에는 정점 쌍이 주어진다.

`출력 조건`

- M개의 줄에 차례대로 입력받은 두 정점의 가장 가까운 공통 조상을 출력한다.

`입력 예시`

```powershell
15
1 2
1 3
2 4
3 7
6 2
3 8
4 9
2 5
5 11
7 13
10 4
11 15
12 5
14 7
6
6 11
10 9
2 6
7 6
8 13
8 15
```

`출력 예시`

```powershell
2
4
2
1
3
1
```

- 두 노드의 공통된 조상 중에서 가장 가까운 조상을 찾는 문제
- **최소 공통 조상 찾기 알고리즘** 사용
  1. 모든 노드에 대한 깊이(depth)를 계산한다.
  2. 최소 공통 조상을 찾을 두 노드를 확인한다.
     1. 먼저 두 노드의 깊이(depth)가 동일하도록 거슬러 올라간다.
     2. 이후 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라간다.
  3. 모든 LCA(a, b) 연산에 대해 2번 과정 반복

#### 답안

```python
import sys
sys.setrecursionlimit(int(1e5))	# 런타임 오류 피하기
n = int(input())

parent = [0] * (n + 1)	# 부모 노드 정보
d = [0] * (n + 1)	# 각 노드까지의 깊이
c = [0] * (n + 1)	# 각 노드의 깊이가 계산됐는지 여부
graph = [[] for _ in range(n + 1)]	# 그래프(graph) 정보

for _ in range(n - 1):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)
    
# 루트 노드부터 시작해서 깊이(depth)를 구하는 함수
def dfs(x, depth):
    c[x] = True
    d[x] = depth
    for y in graph[x]:
        if c[y]:	# 이미 깊이를 구했다면 넘기기
            continue
        parent[y] = x
        dfs(y, depth + 1)
        
# A와 B의 최소 공통 조상을 찾는 함수
def lca(a, b):
    # 먼저 깊이(depth)가 동일하도록 설정
    while d[a] != d[b]:
        if d[a] > d[b]:
            a = parent[a]
        else:
            b = parent[b]
    # 노드가 같아지도록 설정
    while a != b:
        a = parent[a]
        b = parent[b]
    return a

dfs(1, 0)	# 루트 노드는 1번 노드

m = int(input())

for i in range(m):
    a, b = map(int, input().split())
    print(lca(a, b))
```

- 시간 복잡도: O(NM)
  - 매 쿼리마다 부모 방향으로 거슬러 올라가기 위해 최악의 경우 O(N)의 시간 복잡도가 요구되므로 모든 쿼리를 처리할 때 시간 복잡도는 O(NM)이 된다.

### 문제2. LCA 2 (심화 문제)

> 참조: https://www.acmicpc.net/problem/11438

N(2 ≤ N ≤ 100,000)개의 정점으로 이루어진 트리가 주어진다. 트리의 각 정점은 1번부터 N번까지 번호가 매겨져 있으며, 루트는 1번이다. 두 노드의 쌍 M(1 ≤ M ≤ 100,000)개가 주어졌을 때, 두 노드의 가장 가까운 공통 조상이 몇 번인지 출력한다.

`입력 조건`

- 첫째 줄에 노드의 개수 N이 주어지고, 다음 N-1개 줄에는 트리 상에서 연결된 두 정점이 주어진다.
- 그 다음 줄에는 가장 가까운 공통 조상을 알고싶은 쌍의 개수 M이 주어지고, 다음 M개 줄에는 정점 쌍이 주어진다.

`출력 조건`

- M개의 줄에 차례대로 입력받은 두 정점의 가장 가까운 공통 조상을 출력한다.

`입력 예시`

```bash
15
1 2
1 3
2 4
3 7
6 2
3 8
4 9
2 5
5 11
7 13
10 4
11 15
12 5
14 7
6
6 11
10 9
2 6
7 6
8 13
8 15
```

`출력 예시`

```bash
2
4
2
1
3
1
```

- LCA 알고리즘 속도 개선
  - 2의 제곱 형태로 거슬러 올라가도록 하면 O(log N)의 시간 복잡도 보장 가능
  - 메모리를 조금 더 사용하여 각 노드에 대해  2^i번째 부모에 대한 정보를 기록
- 개선된 LCA 알고리즘
  1. 모든 노드에 대해 깊이(depth)와 2^i번째 부모에 대한 정보 계산
  2. 두 노드의 깊이 맞추기
  3. 부모를 거슬러 올라가기
- 시간 복잡도: O(M log N)
  - 다이나믹 프로그래밍 or 세그먼트 트리를 이용해서 시간 복잡도 개선 가능
  - 매 쿼리마다 부모를 거슬러 올라가기 위해 O(log N)의 복잡도가 필요하므로 모든 쿼리를 처리할 때의 시간 복잡도가 O(M log N)이 된다.

#### 답안

```python
import sys
input = sys.stdin.readline	# 시간 초과를 피하기 위한 빠른 입력 함수
sys.setrecursionlimit(int(1e5))	# 런타임 오류 피하기
LOG = 21	# 2^20 = 1,000,000

n = int(input())
parent = [[0] * LOG for _ in range(n + 1)]	# 부모 노드 정보
d = [0] * (n + 1)	# 각 노드까지의 깊이
c = [0] * (n + 1)	# 각 노드의 깊이가 계산됐는지 여부
graph = [[] for _ in range(n + 1)]	# 그래프(graph) 정보

for _ in range(n - 1):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)
    
# 루트 노드부터 시작해서 깊이(depth)를 구하는 함수
def dfs(x, depth):
    c[x] = True
    d[x] = depth
    for y in graph[x]:
        if c[y]:	# 이미 깊이를 구했다면 넘기기
            continue
        parent[y] = x
        dfs(y, depth + 1)

# 전체 부모 관계를 설정하는 함수
def set_parent():
    def(1, 0)	# 루트 노드는 1번 노드
    for i in range(1, LOG):
        for j in range(1, n + 1):
            parent[j][i] = parent[parent[j][i - 1]][i-1]
            
# A와 B의 최소 공통 조상을 찾는 함수
def lca(a, b):
    # b가 더 깊도록 설정
    if d[a] > d[b]:
        a, b = b, a
    # 먼저 깊이(depth)가 동일하도록
    for i in range(LOG - 1, -1, -1):
        if d[b] - d[a] >= (1 << i):
            b = parent[b][i]
    # 부모가 같아지도록
    if a == b:
        return a;
    for i in range(LOG - 1, -1, -1):
        # 조상을 향해 거슬러 올라가기
        if parent[a][i] != parent[b][i]:
            a = parent[a][i]
            b = parent[b][i]
    # 이후에 부모가 찾고자 하는 조상
    return parent[a][0]

set_parent()

m = int(input())

for i in range(m):
    a, b = map(int, input().split())
    print(lca(a, b))
```

## 16. 위상 정렬

> **사이클이 없는 방향 그래프(DAG)**의 모든 노드를 방향성에 거스르지 않도록 순서대로 나열하는 것

### 16-1. 진입차수와 진출차수

- 진입차수(Indegree): 특정 노드로 들어오는 간선 개수
- 진출차수(Outdegree): 특정 노드에서 나가는 간선 개수

### 16-2. 위상 정렬 알고리즘

#### 동작 순서

- **큐**를 이용하는 위상 정렬 알고리즘
  1. 진입차수가 0인 모든 노드를 큐에 넣는다.
     1. 처음에는 노드 1로 시작
  2. 큐가 빌 때까지 다음 과정 반복
     1. 큐에서 원소를 꺼내 해당 노드에서 나가는 간선을 그래프에서 제거
     2. 새롭게 진입차수가 0이 된 노드를 큐에 넣는다.
- 각 노드가 큐에 들어온 순서 = 위상 정렬을 수행한 결과

#### 위상 정렬 특징

- 위상 정렬은 DAG (Direct Acyclic Graph)에 대해서만 수행 가능
- 한 단계에서 큐에 새롭게 들어가는 원소가 2개 이상인 경우 여러 가지 답이 존재할 수 있음
- 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재하는 것
  - 사이클에 포함된 원소 중에서 어떤 원소도 큐에 들어가지 못한다.
- 스택을 활용한 DFS로 위상 정렬 수행 가능

#### 📌 구현 예제

```python
from collection import deque

# 노드의 개수와 간선 개수 입력받기
v, e = map(int, input().split())
# 모든 노드에 대한 진입차수는 0으로 초기화
indegree = [0] * (v + 1)
# 각 노드에 연결된 간선 정보를 담을 연결 리스트 초기화
graph = [[] for i in range(v + 1)]

# 방향 그래프의 모든 간선 정보 입력 받기
for _ in range(e):
    a, b = map(int, input().split())
    graph[a].append(b)	# 정점 A에서 B로 이동 가능
    # 진입차수 1씩 증가
    indegree[b] += 1
    
# 위상정렬 함수
def topology_sort():
    result = []	# 알고리즘 수행 결과
    q = deque()	# 큐 기능을 위한 deque 라이브러리 사용
    # 처음 시작할 때 진입차수가 0인 노드를 큐에 삽입
    for i in range(1, v + 1):
        if indegree[i] == 0:
            q.append(i)
    # 큐가 빌 때까지 반복
    while q:
        # 큐에서 원소 꺼내기
        now = q.popleft()
        result.append(now)
        # 해당 원소와 연결된 노드들의 진입차수에서 1 빼기
        for i in graph[now]:
            indegree[i] -= 1
            # 새롭게 진입차수가 0이 되는 노드를 큐에 삽입
            if indegree[i] == 0:
                q.append(i)
    # 위상정렬 수행 결과 출력
    for i in result:
        print(i, end=' ')
        
topology_sort()
```

- 시간 복잡도: O(V + E). 위상정렬을 위해 차례대로 모든 노드를 확인하고 각 노드에서 나가는 간선을 차례대로 제거해야 하기 때문.

## 17. 재귀 함수 (Recursive Function)

> 자기 자신을 다시 호출하는 함수

```python
def recursive_function():
    print('재귀 함수를 호출합니다.')
    recursive_function()
    
recursive_function()
```

- '재귀 함수를 호출합니다.' 문자열을 무한히 출력하다가 최대 재귀 깊이 초과 메시지 출력

### 17- 1. 재귀 함수의 종료 조건

- 재귀 함수를 문제 풀이에서 사용할 때는 재귀 함수의 종료 조건을 반드시 명시해야 한다.

- 종료 조건을 제대로 명시하지 않으면 함수가 무한 호출된다.

```python
def recursive_function(i):
    # 100번째 호출을 했을 때 종료되도록 종료 조건 명시
    if i == 100:
        return
    print(i, '번째 재귀 함수에서', i + 1, '번째 재귀 함수를 호출합니다.')
    recursive_function(i + 1)
    print(i, '번째 재귀함수를 종료합니다.')
    
recursive_function(1)
```

  ### 17-2. 팩토리얼 구현

- n! = 1 x 2 x 3 x ... x (n - 1) x n
- 0!과 1!의 값은 1

```python
# 반복적으로 구현한 n!
def factorial_iterative(n):
    result = 1
    # 1부터 n까지의 수를 차례대로 곱하기
    for i in range(1, n + 1):
        result *= i
    return result

# 재귀적으로 구현한 n!
def factorial_recursive(n):
    if n <= 1:	# n이 1 이하인 경우 1을 반환
        return 1
    # n! = n * (n - 1)!을 그대로 코드로 작성하기
    return n * factorial_recursive(n - 1)

# 각각의 방식으로 구현한 n! 출력(n = 5)
print('반복적으로 구현:', factorial_iterative(5))
print('재귀적으로 구현:', factorial_recursive(5))
```

### 17-3. 최대공약수 계산 (유클리드 호제법)

#### 💡 유클리드 호제법

> 두 자연수 A, B(A > B)에 대해 A를 B로 나눈 나머지는 R일 때, A와 B의 최대공약수는 B와 R의 최대공약수와 같다.

```python
def gcd(a, b):
    if a % b == 0:
        return b
    else:
        return gcd(b, a % b)
    
print(gcd(192, 162))
```

### 17-4. 재귀함수 사용시 유의 사항

- 재귀 함수를 잘 활용하면 복잡한 알고리즘을 간결하게 작성할 수 있지만 다른 사람이 이해하기 어려운 형태의 코드가 될 수 있으므로 신중하게 사용해야 한다.
- 모든 재귀 함수는 반복문을 이용해서 동일한 기능 구현 가능
- 재귀 함수가 반복문보다 유리한 경우도 있고 불리한 경우도 있으므로 잘 선택해서 구현해야 한다.
- 컴퓨터가 함수를 호출하면 컴퓨터 메모리 내부의 스택 프레임에 쌓이므로 스택을 사용해야 할 때 구현상 스택 라이브러리 대신에 재귀 함수를 이용하는 경우가 많다.

## 18. 유용한 표준 라이브러리

- 내장 함수: 기본 입출력 함수부터 정렬 함수까지 기본 함수 제공
  - 파이썬 프로그램 작성 시 필수적인 기능 포함
- itertools: 파이썬에서 반복되는 형태의 데이터를 처리하기 위한 유용한 기능 제공
  - 특히 순열과 조합 라이브러리는 코딩 테스트에서 자주 사용
- heapq: 힙(Heap) 자료구조 제공
  - 보통 우선순위 큐 기능 구현을 위해 사용
- bisect: 이진 탐색(Binary Search) 기능 제공
- collections: 덱(deque), 카운터(Counter) 등의 유용한 자료구조르 포함
- math: 필수적인 수학 기능 제공
  - 팩토리얼, 제곱근, 최대공약수(GCD), 삼각함수 관련 함수부터 파이(pi) 같은 상수 포함

### 18-1. 내장 함수

```python
# sum()
result = sum([1, 2, 3, 4, 5])
print(result)

# min(), max()
min_result = min(7, 3, 5, 2)
max_result = max(7, 3, 5, 2)
print(min_result, max_result)

# eval()
result = eval("(3+5)*7")
print(result)

# sorted(): 기본 오름차순
result = sorted([9, 1, 8, 5, 4])
reverse_result = sorted([9, 1, 8, 5, 4], reverse=True)	# 내림차순 정렬
print(result)
print(reverse_result)

# sorted() with key
array = [('홍길동', 35), ('이순신', 75), ('아무개', 50)]
result = sorted(array, key=lambda x : x[1], reverse=True)
print(result)
```

### 18-2. itertools

#### 순열과 조합

- 순열: 서로 다른 n개에서 서로 다른 r개를 선택하여 일렬로 나열하는 것

  > 순열의 수 공식: nPr = n * (n - 1) * (n - 2) * ... * (n - r + 1)

  ```python
  from itertools import permutations
  
  data = ['A', 'B', 'C']	# 데이터 준비
  
  result = list(permutations(data, 3))	# 모든 순열 구하기
  print(result)
  ```

- 조합: 서로 다른 n개에서 순서에 상관없이 서로 다른 r개를 선택하는 것

  > 조합의 수 공식: nCr =  n * (n - 1) * (n - 2) * ... * (n - r + 1) / r!

  ```python
  from itertools import combinations
  
  data = ['A', 'B', 'C']	# 데이터 준비
  
  result = list(combinations(data, 2))	# 2개를 뽑는 모든 조합 구하기
  print(result)
  ```

#### 중복 순열과 중복 조합

- 중복 순열

  ```python
  from itertools import product
  
  data = ['A', 'B', 'C']	# 데이터 준비
  
  result = list(product(data, repeat=2))	# 2개를 뽑는 모든 순열 구하기 (중복 허용)
  print(result)
  ```

- 중복 조합

  ```python
  from itertools import combinations_with_replacement
  
  data = ['A', 'B', 'C']	# 데이터 준비
  
  result = list(combinations_with_replacement(data, 2))	# 2개를 뽑는 모든 조합 구하기 (중복 허용)
  print(result)
  ```


### 18-3. collections

#### Counter

- 등장 횟수를 세는 기능 제공
- 리스트 같이 반복 가능한(iterable) 객체가 주어졌을 때 내부의 원소가 몇 번씩 등장했는지 알려준다.

```python
from collections import Counter

counter = Count(['red', 'blue', 'red', 'green', 'blue', 'blue'])

print(counter['blue'])	# 'blue'가 등장한 횟수 출력
print(counter['green'])	# 'green'이 등장한 횟수 출력
print(dict(counter))	# 사전 자료형으로 변환
```

### 18-4. math

#### 최대 공약수와 최소 공배수

- 최대 공약수를 구하는 함수: `gcd()`

```python
import math

# 최소 공배수(LCM)을 구하는 함수
def lcm(a, b):
    return a * b // math.gcd(a, b)

a = 21
b = 14

print(math.gcd(21, 14))	# 최대 공약수(GCD) 계산
print(lcm(21, 14))	# 최소 공배수(LCM) 계산
```

## 19. 소수 여부를 빠르게 처리하는 알고리즘들

### 19-1. 소수 (Prime Number)

> 1보다 큰 자연수 중에서 1과 자기 자신을 제외한 자연수로는 나누어 떨어지지 않는 자연수

#### 📌 기본 알고리즘 구현

```python
# 소수 판별 함수 (2이상 자연수에 대해)
def is_prime_number(x):
    # 2부터 (x - 1)까지의 모든 수 확인
    for i in range(2, x):
        # x가 해당 수로 나누어떨어지면
        if x % i == 0:
            return False	# 소수 아님
    return True	# 아니면 소수

print(is_prime_number(4))
print(is_prime_number(7))
```

- 시간 복잡도: 2부터 X-1까지 모든 수를 하나씩 확인하므로 O(X)

### 19-2. 약수의 성질

- 모든 약수가 가운데 약수를 기준으로 곱셈 연산에 대해 대칭을 이루므로 특정 자연수의 모든 약수를 찾을 때 가운데 약수(제곱근)까지만 확인하면 된다.

  예) 16의 약수: 1, 2, 4, 8, 16 (대칭). 16이 2로 나누어떨어지면 8로도 나누어떨어진다는 것을 의미

#### 📌 개선된 알고리즘 구현

```python
import math

# 소수 판별 함수 (2이상의 자연수)
def is_prime_number(x):
    # 2부터 x의 제곱근까지의 모든 수 확인
    for i in range(2, int(math.sqrt(x)) + 1):
        # x가 해당 수로 나누어떨어진다면
        if x % i == 0:
            return False	# 소수가 아님
    return True	# 소수

print(is_prime_number(4))
print(is_prime_number(7))
```

- 시간 복잡도: 2부터 X-1까지(소수점 이하 무시) 모든 수를 하나씩 확인하므로 O(N^0.5)

### 19-3. 다수의 소수 판별: 에라토스테네스의 체 알고리즘

- 다수의 자연수에 대해 소수 여부를 판별할 때 사용하는 대표적인 알고리즘
- N보다 작거나 같은 모든 소수를 찾을 때 사용할 수 있다.

#### 동작 순서

1. 2부터 N까지의 모든 자연수  나열
2. 남은 수 중에서 아직 처리하지 않은 가장 작은 수 i를 찾는다.
3. 남은 수 중에서 i의 배수를 모두 제거 (i는 제거하지 않음)
4. 더 이상 반복할 수 없을 때까지 2번과 3번 과정 반복

#### 📌 구현 예제

```python
import math

n = 1000	# 2부터 1,000까지의 모든 수에 대해 소수 판별
# 처음엔 모든 수가 소수(True)인 것으로 초기화(0과 1 제외)
array = [True for i in range(n + 1)]

# 에라토스테네스의 체 알고리즘 수행
# 2부터 n의 제곱근까지의 모든 수 확인
for i in range(2, int(math.sqrt(n)) + 1):
    if array[i] == True:	# i가 소수인 경우(남은 수인 경우)
        # i를 제외한 i의 모든 배수 삭제
        j = 2
        while i * j <= n:
            array[i * j] = False
            j += 1
            
# 모든 소수 출력
for i in range(2, n + 1):
    if array[i]:
        print(i, end=' ')
```

- 시간 복잡도: O(N loglogN)
- 에라토스테네스의 체는 사실상 선형 시간에 가까울 정도로 매우 빠르지만 각 자연수에 대한 소수 여부를 저장하기 때문에 메모리가 많이 필요해서 수가 클 때에는 효과적으로 사용하기 힘들다.

## 20. 이진 탐색: 정렬된 데이터에서 빠르게 데이터 찾기

### 20-1. 순차 탐색과 이진 탐색 비교

- 순차 탐색: 리스트 안에 있는 특정 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인하는 방법

- 이진 탐색: 정렬된 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법으로 시작점, 끝점, 중간점을 이용해 탐색 범위를 설정

  👉 단계마다 탐색 범위가 반으로 줄어들기 때문에 이미 정렬된 데이터에 대한 탐색은 이진 탐색이 훨씬 빠르다. 또한 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 연산 횟수는 log2 N에 비례한다.

- 이진 탐색 시간 복잡도는 O(log N)

#### 📌 구현 예제 - 재귀적 구현

```python
# 이진 탐색 소스코드 구현 (재귀 함수)
def binary_search(array, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 주악ㄴ점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    elif array[mid] > target:
        return binary_search(array, target, start, mid - 1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else:
        return binary_search(array, target, mid + 1, end)
    
# n(원소의 개수)과 target(찾고자 하는 값)을 입력받기
n, target = list(map(int, input().split()))
#전체 원소 입력 받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result = None:
    print('원소가 존재하지 않습니다.')
else:
    print(result + 1)
```

#### 📌 구현 예제 - 반복문 구현

```python
# 이진 탐색 소스코드 구현 (반복문)
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # 찾은 경우 중간점 인덱스 반환
        if array[mid] == target:
            return mid
        # 중간점 값보다 찾고자 하는 값이 적은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid - 1
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid + 1
    return None

# n(원소의 개수)과 target(찾고자 하는 값)을 입력 받기
n, target = list(map(int, input().split()))
# 전체 원소 입력받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print('원소가 존재하지 않습니다.')
else:
    print(result + 1)
```

### 20-2. 파이썬 이진 탐색 라이브러리

- `bisect_left(a, x)`: 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 왼쪽 인덱스 반환
- `bisect_right(a, x)`: 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 오른쪽 인덱스 반환

#### 📌 구현 예제

```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 배열 선언
a = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9]

# 값이 4인 데이터 개수 출력
print(count_by_range(a, 4, 4))	# 2

# 값이 [-1, 3] 범위에 있는 데이터 개수 출력
print(count_by_range(a, -1, 3))	# 6
```

### 20-3. 파라메트릭 서치(Parametric Search)

> 최적화 문제를 결정 문제(예/아니오)로 바꾸어 해결하는 기법

- 이진 탐색을 이용해서 해결 가능

  예) 특정한 조건을 만족하는 가장 알맞은 값을 빠르게 찾는 최적화 문제

#### 문제 1. 떡볶이 떡 만들기

오늘 동빈이는 여행 가신 부모님을 대신해서 떡집 일을 하기로 했습니다. 오늘은 떡볶이 떡을 만드는 날입니다. 동빈이네 떡볶이 떡은 재밌게도 떡볶이 떡의 길이가 일정하지 않습니다. 대신에 한 봉지 안에 들어가는 떡의 총 길이는 절단기로 잘라서 맞춰줍니다. 절단기에 높이(H)를 지정하면 줄지어진 떡을 한 번에 절단합니다. 높이가 H보다 긴 떡은 H 위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않습니다. 예를 들어 높이가 19, 14, 10, 17cm인 떡이 나란히 있고 절단기 높이를 15cm로 지정하면 잘느 뒤 떡의 높이는 15, 14, 10, 15cm가 될 것입니다. 잘린 떡의 길이는 차례대로 4, 0, 0, 2cm입니다. 손님은 6cm 만큼의 길이를 가져갑니다. 손님이 왔을 때 요청한 총 길이가 M일 때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하세요.

`입력 조건`

- 첫째 줄에 떡의 개수 N과 요청한 떡의 길이 M이 주어진다. (1 <= N <= 1,000,000, 1 <= M <= 2,000,000,000)
- 둘째 줄에는 떡의 개별 높이가 주어진다. 떡 높이의 총합은 항상 M 이상이므로 손님은 필요한 양만큼 떡을 사갈 수 있다. 높이는 10억보다 작거나 같은 양의 정수 또는 0이다.

`출력 조건`

- 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력한다.

`입력 예시`

```bash
4 6
19 15 10 17
```

`출력 예시`

```bash
15
```

#### 답안

- 적절한 높이를 찾을 때까지 이진 탐색을 수행하여 높이 H를 반복해서 조정
- '현재 이 높이로 자르면 조건을 만족할 수 있는가?'를 확인하고 조건의 만족 여부에 따라 탐색 범위를 좁혀서 해결
- 절단기의 높이는 0부터 10억까지의 정수 중 하나이므로 이진 탐색 사용
- 중간점의 값은 시간이 지날수록 '최적화된 값'이 되므로 과정을 반복하며 얻을 수 있는 떡의 길이 합이 필요한 떡의 길이보다 크거나 같을 때마다 중간점의 값을 기록

```python
# 떡의 개수(N)와 요청한 떡의 길이(M) 입력
n, m = list(map(int, input().split()))
# 각 떡의 개별 높이 정보 입력
array = list(map(int, input().split()))

# 이진 탐색을 위한 시작점과 끝점 설정
start = 0
end = max(array)

# 이진 탐색 수행(반복적)
result = 0
while(start <= end):
    total = 0
    mid = (start + end) // 2
    for x in array:
        # 잘랐을 때의 떡의 양 계산
        if x > mid:
            total += x - mid
    # 떡의 양이 부족한 경우 더 많이 자르기 (왼쪽 부분 탐색)
    if total < m:
        end = mid - 1
    # 떡의 양이 충분한 경우 덜 자르기 (오른쪽 부분 탐색)
    else:
        result = mid	# 최대한 덜 잘랐을 때가 정답이므로 여기에서 result에 기록
        start = mid + 1
        
# 정답 출력
print(result)
```

#### 문제 2. 정렬된 배열에서 특정 수의 개수 구하기

N개의 원소를 포함하고 있는 수열이 오름차순으로 정렬되어 있다. 이때 이 수열에서 x가 등장하는 횟수를 계산하라. 예를 들어 수열 {1, 1, 2, 2, 2, 2, 3}이 있을 때 x = 2라면, 현재 수열에서 값이 2인 원소가 4개이므로 4를 출력한다. 단, 이 문제는 시간 복잡도 O(log N)으로 알고리즘을 설계하지 않으면 시간 초과 판정을 받는다.

`입력 조건`

- 첫째 줄에 N과 x가 정수 형태로 공백으로 구분되어 입력된다. (1 <= N <= 1,000,000), (-10^9 <= x 10^9)
- 둘째 줄에 N개의 원소가 정수 형태로 공백으로 구분되어 입력된다. (-10^9 <= 각 원소의 값 <= 10^9)

`출력 조건`

- 수열의 원소 중에서 값이 x인 원소의 개수를 출력한다. 단, 값이 x인 원소가 하나도 없다면 -1을 출력한다.

`입력 예시`

```bash
7 2
1 1 2 2 2 2 3
```

`출력 예시`

```bash
4
```

#### 답안

- 시간 복잡도 O(log N)으로 동작하는 알고리즘을 요구하고 있고 데이터가 정렬되어 있으므로 이진 탐색 수행
- 특정 값이 등장하는 첫 번째 위치와 마지막 위치를 찾아 위치 차이를 계산해서 문제 해결 가능

```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(array, left_value, right_value):
    right_index = bisect_right(array, right_value)
    left_index = bisect_left(array, left_value)
    return right_index - left_index

n, x = map(int, input().split())
array = list(map(int, input().split()))

# 값이 [x, x] 범위에 있는 데이터의 개수 계산
count = count_by_range(array, x, x)

# 값이 x인 원소가 존재하지 않는다면
if count == 0:
    print(-1)
# 값이 x인 원소가 존재한다면
else:
    print(count)
```

## 21. 다이나믹 프로그래밍

> a.k.a. 동적 계획법. 메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법

- 이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 하므로 효율성이 증대
- 다이나믹 프로그래밍의 구현은 일반적으로 **탑다운**(하향식)과 **보텀업**(상향식) 2가지 방식으로 구성
  - 탑다운(하향식: 재귀함수 이용
  - 보텀업(상향식): 반복문 이용 - 다이나믹 프로그래밍의 전형적인 형태
#### 동적(Dynamic)의 의미
- 일반적인 프로그래밍 분야 중 특히 자료구조에서는 동적 할당(Dynamic Allocation)을 '프로그램이 실행되는 도중에 실행에 필요한 메모리를 할당하는 기법'이라는 의미로 사용
- **다이나믹 프로그래밍에서 다이나믹은 별다른 의미 없음**

### 21-1. 다이나믹 프로그래밍의 조건

- 다이나믹 프로그래밍은 문제가 다음 조건을 만족할 때에 사용할 수 있다.
  1. 최적 부분 구조 (Optimal Substructure)
     - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있을 때
  2. 중복되는 부분 문제 (Overlapping Subproblem)
     - 동일한 작은 문제를 반복적으로 해결해야 할 때

#### 예시 - 피보나치 수열

> 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

- 점화식: 인접한 항들 사이의 관계식

  - An = An-1 + An-2, A1 = 1, A2 = 1

- 트리로 표현 가능

  ![image-20210701113408910](../../md-img/image-20210701113408910.png)

#### 📌 구현 예제 - 재귀 함수 사용

```python
# 피보나치 수열(Fibonacci Function)을 재귀함수로 표현
def fibo(x):
    if x == 1 or x == 2:
        return 1
    return fibo(x - 1) + fibo(x - 2)

print(fibo(4))
```

- 시간 복잡도

  - 세타 표기법: θ(1.618...^N)
  - 빅오 표기법: O(2^N)

- 단순 재귀 함수로 피보나치 수열을 해결하면 전체 수열의 값이 커질수록 시간 복잡도가 높아진다. 중복으로 여러 번 호출되는 부분이 생기기 때문

  👉 **다이나믹 프로그래밍**으로 효율적인 해결 가능

  1. 최적 부분 구조: 큰 문제를 작은 문제로 나눌 수 있음

     - 4번째 수를 구하려면 3번째와 2번째 수를 구해야 한다.

  2. 중복되는 부분 문제: 동일한 작은 문제를 반복적으로 해결

     - 4번째 수를 구하려면 2번째 수를 2번 구해야 한다.

       예) f(4) = f(3) + f(2), f(3) = f(2) + f(1)

### 21-2. 메모이제이션 (Memoization)

- 다이나믹 프로그래밍을 하향식으로 구현
- 한 번 계산한 결과를 메모리 공간에 메모하는 기법
  - 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져온다.
  - 값을 기록하므로 **캐싱(Caching)**이라고도 한다.
  - 결과 저장용 리스트: **DP 테이블**
- 메모이제이션은 이전에 계산된 결과를 일시적으로 기록해 놓는 넓은 개념을 의미하므로 다이나믹 프로그래밍에 국한된 개념은 아니며, 한 번 계산된 결과를 담아 놓기만 하고 다이나믹 프로그래밍에 활용하지 않을 수도 있다.

#### 📌 구현 예제 - 하향식 다이나믹 프로그래밍: 피보나치 수열

```python
# 한 번 계산된 결과를 메모이제이션하기 위한 리스트 초기화
d = [0] * 100

# 피보나치 함수를 재귀함수로 구현(탑다운 다이나믹 프로그래밍)
def fibo(x):
    # 종료 조건(1 혹은 2일 때 1을 반환)
    if x == 1 or x == 2:
        return 1
    # 이미 계산한 적 있는 문제라면 그대로 반환
    if d[x] != 0:
        return d[x]
    # 아직 계산하지 않은 문제라면 점화식에 따라서 피보나치 결과 반환
    d[x] = fibo(x - 1) + fibo(x - 2)
    return d[x]

print(fibo(99))
```

#### 📌 구현 예제 - 상향식 다이나믹 프로그래밍: 피보나치 수열

```python
# 앞서 계산된 결과를 저장하기 위한 DP 테이블 초기화
d = [0] * 100

# 첫 번째 피보나치 수와 두 번째 피보나치 수는 1
d[1] = 1
d[2] = 1
n = 99

# 피보나치 함수 반복문으로 구현(보텀업 다이나믹 프로그래밍)
for i in range(3, n + 1):
    d[i] = d[i - 1] + d[i - 2]
    
print(d[n])
```

- 메모이제이션 방식으로 구현한 코드를 실행하면 실제로 호출되는 함수가 다음과 같다.

  ![image-20210701132742123](../../md-img/image-20210701132742123.png)

- 시간 복잡도: O(N)

### 21-3. 다이나믹 프로그래밍 VS 분할 정복

- 공통점
  - 다이나믹 프로그래밍과 분할 정복은 모두 **최적 부분 구조**를 가질 때 사용할 수 있다.
- 차이점
  - 다이나믹 프로그래밍 문제에서는 각 부분 문제들이 서로 영향을 미치며 부분 문제가 중복된다.
  - 분할 정복 문제에서는 동일한 부분 문제가 반복적으로 계산되지 않는다.

#### 분할 정복 예시

- 퀵 정렬
  - 한 번 기준 원소(Pivot)가 자리를 변경해서 자리를 잡으면 그 기준 원소의 위치는 바뀌지 않는다.
  - 분할 이후에 해당 피벗을 다시 처리하는 부분 문제는 호출하지 않는다.

### 21-4. 다이나믹 프로그래밍 문제 접근 방법

- 주어진 문제가 다이나믹 프로그래밍 유형임을 파악하는 것이 중요
- 가장 먼저 그리디, 구현, 완전 탐색 등의 아이디어로 문제를 해결할 수 있는지 검토한다.
  - 다른 알고리즘으로 풀이 방법이 떠오르지 않으면 다이나믹 프로그래밍을 고려
- 일단 재귀 함수로 비효율적인 완전 탐색 프로그램을 작성한 뒤에 (탑다운) 작은 문제에서 구한 답이 큰 문제에서 그대로 사용될 수 있으면 코드를 개선하는 방법을 사용할 수 있다.
- 일반적인 코딩 테스트 수준에서는 기본 유형의 다이나믹 프로그래밍 문제가 출제되는 경우가 많다.

## 22. 동적 계획법 문제 풀이

### 문제1. 개미 전사

개미 전사는 부족한 식량을 충당하고자 메뚜기 마을의 식량창고를 몰래 공격하려고 한다. 메뚜기 마을에는 여러 개의 식량창고가 있는데 식량창고는 일직선으로 이어져 있다. 각 식량창고에는 정해진 수의 식량을 저장하고 있으며 개미 전사는 식량창고를 선택적으로 약탈하여 식량을 빼앗을 예정이다. 이때 메뚜기 정찰병들은 일직선상에 존재하는 식량창고 중에서 서로 인접한 식량창고가 공격받으면 바로 알아챌 수 있다. 따라서 개미 전사가 정찰병에게 들키지 않고 식량창고를 약탈하기 위해서는 최소한 한 칸 이상 떨어진 식량창고를 약탈해야 한다. 예를 들어 식량창고 4개가 다음과 같이 존재할 때 개미 전사는 두 번째 식량창고와 네 번째 식량창고를 선택해야 최댓값인 총 8개의 식량을 빼앗을 수 있다.

![image-20210702090839574](../../md-img/image-20210702090839574.png)

개미 전사는 식량창고가 이렇게 일직선상일 때 최대한 많은 식량을 얻기를 원한다. 개미 전사를 위해 식량창고 N개에 대한 정보가 주어졌을 때 얻을 수 있는 식량의 최댓값을 구하는 프로그램을 작성하시오.

`입력 조건`

- 첫째 줄에 식량창고의 개수 N이 주어진다. (3 <= N <= 100)
- 둘째 줄에 공백을 기준으로 각 식량창고에 저장된 식량의 개수 K가 주어진다. (0 <= K <=  1,000)

`출력 조건`

- 첫째 줄에 개미 전사가 얻을 수 있는 식량의 최댓값을 출력하라.

`입력 예시`

```bash
4
1 3 1 5
```

`출력 예시`

```bash
8
```

#### 답안

- Ai = i번째 식량창고까지의 최적의 해 (얻을 수 있는 식량의 최댓값)
  - DP 테이블의 값을 갱신하면서 최적의 해를 계산
- 왼쪽부터 차례대로 식량창고를 턴다고 했을 때, 특정한 i번째 식량창고에 대해 털지 안 털지의 여부를 결정하면 i - 1 또는 i - 2번째 식량창고까지 털 수 있음
- Ai = i번째 식량창고까지의 최적의 해 (얻을 수 있는 식량의 최댓값)
- Ki = i번째 식량창고에 있는 식량의 양
- 점화식: Ai = max(Ai-1, Ai-2 + Ki)

```python
n = int(input())
arrayk = list(map(int, input().split()))

# DP 테이블 초기화
d = [0] * 100

# 다이나믹 프로그래밍 (보텀업)
d[0] = arrayk[0]
d[1] = max(arrayk[0], arrayk[1])
for i in range(2, n):
    d[i] = max(d[i - 1], d[i - 2] + arrayk[i])
    
# 계산 결과
print(d[n - 1])
```

### 문제 2. 1로 만들기

정수 X가 주어졌을 때, 정수 X에 사용할 수 있는 연산은 다음과 같이 4가지이다.

1. X가 5로 나누어 떨어지면 5로 나눈다.
2. X가 3으로 나누어 떨어지면 3으로 나눈다.
3. X가 2로 나누어 떨어지면 2로 나눈다.
4. X에서 1을 뺀다.

정수 X가 주어졌을 때 연산 4개를 적절히 사용해서 값을 1로 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하라. 예를 들어 정수가 26이면 다음과 같이 계산해서 3번의 연산이 최솟값이다.

26 ➡ 25 ➡ 5 ➡ 1

`입력 조건`

- 첫째 줄에 정수 X가 주어진다. (1 <= X <= 30,000)

`출력 조건`

- 첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

`입력 예시`

```bash
26
```

`출력 예시`

```bash
3
```

#### 답안

- 피보나치 수열 문제를 도식화한 것처럼 함수가 호출되는 과정을 그림으로 그려보면 **최적 부분 구조**와 **중복되는 부분 문제**를 만족한다.

  ![](../../md-img/dd.png)

- Ai = i를 1로 만들기 위한 최소 연산 횟수

- 점화식: Ai = min(Ai-1, Ai/2, Ai/3, Ai/5) + 1

- 단, 1을 빼는 연산을 제외하고는 해당 수로 나누어떨어질 때에 한해 점화식 적용 가능

```python
x = int(input())

count = [] * 30001

# 다이나믹 프로그래밍 (보텀업)
for i in range(2, x + 1):
    # 현재 수에서 1을 빼는 경우
    count[i] = count[i - 1] + 1
    # 현재 수가 2로 나누어 떨어지는 경우
    if x % 2 == 0:
        count[i] = min(count[i], count[i // 2] + 1)
    # 현재 수가 3으로 나누어 떨어지는 경우
    if x % 3 == 0:
        count[i] = min(count[i], count[i // 3] + 1)
    # 현재 수가 5로 나누어 떨어지는 경우
    if x % 5 == 0:
       count[i] = min(count[i], count[i // 5] + 1)
   
print(count[x])
```

### 문제 3. 효율적인 화폐 구성

N가지 종류의 화폐가 있다. 이 화폐들의 개수를 최소한으로 이용해서 그 가치의 합이 M원이 되도록하려고 한다. 이때 각 종류의 화폐는 몇 개라도 사용할 수 있다. 예를 들어 2원, 3원 단위의 화폐가 있을 때는 15원을 만들기 위해 3원을 5개 사용하는 것이 가장 최소한의 화폐 개수이다. M원을 만들기 위한 최소한의 화폐 개수를 출력하는 프로그램을 작성하라.

`입력 조건`

- 첫째 줄에 N, M이 주어진다. (1 <= N <= 100, 1 <= M <= 10,000)
- 이후의 N개의 줄에는 각 화폐의 가치가 주어진다. 화폐의 가치는 10,000보다 작거나 같은 자연수이다.

`출력 조건`

- 첫째 줄에 최소 화폐 개수를 출력한다.
- 불가능할 때는 -1을 출력한다.

`입력예시 1`

```bash
2 15
2
3
```

`출력예시 1`

```bash
5
```

`입력예시 2`

```bash
3 4
3
5
7
```

`출력예시 2`

```bash
-1
```

#### 답안

- Ai = 금액 i를 만들 수 있는 최소한의 화폐 개수
- k = 각 화폐의 단위
- 점화식: 각 화폐 단위인 K를 하나씩 확인하며
  - Ai-k를 만드는 방법이 존재하는 경우: Ai = min(Ai, Ai-k + 1)
  - Ai-k를 만드는 방법이 존재하지 않는 경우: Ai = INF
- 최대 입력조건이 10,000이므로 INF값을 10,001로 설정하고 각 인덱스를 INF로 초기화

```python
n, m = map(int, input().split())
moneylist = []

for i in range(n):
    moneylist.append(int(input()))

# DP 테이블 초기화
d = [10001] * (m + 1)

# 다이나믹 프로그래밍 진행 (보텀업)
d[0] = 0
for i in range(n):
    for j in range(moneylist[i], m + 1):
        if d[j - moneylist[i]] != 10001:	# (i - k)원을 만드는 방법이 존재하는 경우
            d[j] = min(d[j], d[j - moneylist[i] + 1])
            
# 계산된 결과 출력
if d[m] == 10001:	# 최종적으로 M원을 만들 방법이 없는 경우
    print(-1)
else:
    print(d[m])
        
```

### 문제4. 금광

n x m 크기의 금광이 있다. 금광은 1 x 1 크기의 칸으로 나누어져 있으며, 각 칸은 특정한 크기의 금이 들어 있다. 채굴자는 첫 번째 열부터 출발하여 금을 캐기 시작한다. 맨 처음에는 첫 번째 열의 어느 행에서든 출발할 수 있다. 이후에 m - 1번에 걸쳐 매번 오른쪽 위, 오른쪽, 오른쪽 아래 3가지 중 하나의 위치로 이동해야 한다. 결과적으로 채굴자가 얻을 수 있는 금의 최대 크기를 출력하는 프로그램을 작성하시오.

![image-20210702113858533](../../md-img/image-20210702113858533.png)

`입력 조건`

- 첫째 줄에 테스트 케이스 T가 입력된다. (1 <= T <= 1,000)
- 매 테스트 케이스 첫째 줄에 n과 m이 공백으로 구분되어 입력된다. (1 <= n, m <= 20)
- 둘째 줄에 n x m개의 위치에 매장된 금의 개수가 공백으로 구분되어 입력된다. (1 <= 각 위치에 매장된 금의 개수 <= 100)

`출력 조건`

- 테스트 케이스마다 채굴자가 얻을 수 있는 금의 최대 크기를 출력한다.
- 각 테스트 케이스는 줄 바꿈을 이용해 구분한다.

`입력 예시`

```bash
2
3 4
1 3 3 2 2 1 4 1 0 6 4 7
4 4
1 3 1 5 2 2 4 1 5 0 2 3 0 6 1 2
```

`출력 예시`

```bash
19
16
```

#### 답안

- 금광의 모든 위치에 대해 고려할 3가지
  1. 왼쪽 위에서 오는 경우
  2. 왼쪽 아래에서 오는 경우
  3. 왼쪽에서 오는 경우
- 3가지 중 가장 많은 금을 가지고 있는 경우를 테이블에 갱신해준다.
- array[i][j] = i행 j열에 존재하는 금의 양
- dp[i][j] = i행 j열까지의 최적의 해 (얻을 수 있는 금의 최댓값)
- 점화식: `dp[i][j] = array[i][j] + max(dp[i - 1][j - 1], dp[i][j - 1], dp[i + 1][j - 1])`
- 테이블에 접근할 때마다 리스트의 범위를 벗어나지 않는지 체크
- 편의상 초기 데이터를 담는 변수 array를 사용하지 않고 바로 DP 테이블에 초기 데이터를 담아서 다이나믹 프로그래밍을 적용할 수 있다.

```python
for i in range(int(input())):
    n, m = map(int, input().split())
    golds = list(map(int, input().split()))
    # DP 테이블 초기화
    dp = []
    index = 0
    for j in range(n):
        dp.append(golds[index:index + m])
        index += m
    # 다이나믹 프로그래밍 진행
    for k in range(1, m):
        for l in range(n):
            # 왼쪽 위에서 오는 경우
            if l == 0: left_up = 0
            else: left_up = dp[l - 1][k - 1]
            # 왼쪽 아래에서 오는 경우
            if l == n - 1: left_down = 0
            else: left_down = dp[l + 1][k - 1]
            # 왼쪽에서 오는 경우
            left = dp[l][k - 1]
            dp[l][k] = dp[l][k] + max(left_up, left_down, left)
    result = 0
    for i in range(n):
        result = max(result, dp[i][m - 1])
    print(result)
```

### 문제 5. 병사 배치하기

N명의 병사가 무작위로 나열되어 있다. 각 병사는 특정한 값의 전투력을 보유하고 있다. 병사를 배치할 때는 전투력이 높은 병사가 앞쪽에 오도록 내림차순으로 배치하고자 한다. 다시 말해 앞쪽에 있는 병사의 전투력이 항상 뒤쪽에 있는 병사보다 높아야 한다. 또한 배치 과정에서 특정한 위치에 있는 병사를 열외시키는 방법을 이용한다. 그러면서도 남아 있는 병사의 수가 최대가 되도록 하고 싶다. 예를 들어, N = 7일 때 나열된 병사들의 전투력이 다음과 같다고 가정할 때 3번 병사와 6번 병사를 열외시킨다.

![image-20210702133541828](../../md-img/image-20210702133541828.png)

그때 남아 있는 병사의 수가 내림차순의 형태가 되어 5명이 된다. 이는 남아 있는 병사의 수가 최대가 되도록 하는 방법이다.

![image-20210702133659844](../../md-img/image-20210702133659844.png)

병사에 대한 정보가 주어졌을 때 남은 병사의 수가 최대가 되도록 하기 위해서 열외시켜야 하는 병사의 수를 출력하는 프로그램을 작성하라.

`입력 조건`

- 첫째 줄에 N이 주어진다. (1 <= N <= 2,000)
- 둘째 줄에 각 병사의 전투력이 공백으로 구분되어 차례대로 주어진다. 각 병사의 전투력은 10,000,000보다 작거나 같은 자연수이다.

`출력 조건`

- 첫째 줄에 남아 있는 병사의 수가 최대가 되도록 하기 위해서 열외시켜야 하는 병사의 수를 출력한다.

`입력 예시`

```bash
7
15 11 4 8 5 2 4
```

`출력 예시`

```bash
2
```

#### 답안

- **가장 긴 증가하는 부분 수열(Longest Increasing Subsequence, LIS)**로 알려진 전형적인 다이나믹 프로그래밍 문제의 아이디어와 같다.
- 하나의 수열 array = {4, 2, 5, 8, 4, 11, 15}에서 가장 긴 증가하는 부분 수열은 {4, 5, 8, 11, 15}이다.
- D[I] = array[i]를 마지막 원소로 가지는 부분 수열의 최대 길이
- 점화식: 모든 0 <= j < i에 대하여, D[I] = max(D[i], D[j] + 1 if array[j] < array[i])
- 입력받은 수열의 순서를 뒤집어서 LIS 적용

```python
n = int(input())
array = list(map(int, input().split()))
# 순서 뒤집기
array.reverse()

# 다이나믹 프로그래밍을 위한 1차원 DP 테이블 초기화
dp = [1] * n

# LIS 알고리즘 수행
for i in range(1, n):
    for j in range(0, i):
        if array[j] < array[i]:
            dp[i] = max(dp[i], dp[j] + 1)
            
# 열외해야 하는 병사의 최소 수 출력
print(n - max(dp))
```

## 23. 그리디 알고리즘 (Greedy Algorithm)

> a.k.a. 탐욕법. 현재 상황에서 지금 당장 좋은 것만 고르는 방법

- 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력을 요구한다.
- 정당성 분석이 중요
  - 단순히 가장 좋아 보이는 것을 반복적으로 선택해도 최적의 해를 구할 수 있는지 검토
- 일반적인 상황에서 그리디 알고리즘은 최적의 해를 보장할 수 없을 때가 많다.
- 코딩 테스트에서는 **탐욕법으로 얻은 해가 최적의 해가 되는 상황에서 이를 추론**할 수 있어야 풀리도록 출제

### 문제 1. 거스름 돈

당신은 음식점의 계산을 도와주는 점원이다. 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원짜리 동전이 무한히 존재한다고 가정한다. 손님에게 거슬러 주어야 할 돈이 N원일 때 거슬러 주어야 할 동전의 최소 개수를 구하라. 단, 거슬러 줘야 할 돈 N은 항상 10의 배수이다.

#### 답안

- 최적의 해를 빠르게 구하기 위해서는 가장 큰 화폐 단위부터 돈을 거슬러 준다.
- N원을 거슬러 줘야 할 때, 가장 먼저 500원으로 거슬러 줄 수 있을 만큼 거슬러 준 후에 차례로 100원, 50원, 10원을 거슬러 줄 수 있는 만큼 거슬러 준다.
- N = 1,260일 때의 예시

  - 500원: 2개
  - 100원: 2개
  - 50원: 1개
  - 10원: 1개

- 정당성 분석
  - 가장 큰 화폐 단위부터 돈을 거슬러 주는 것이 최적의 해를 보장하는 이유는 가지고 있는 동전 중에서 **큰 단위가 항상 작은 단위의 배수이므로 작은 단위의 동전들을 종합해 다른 해가 나올 수 없기 때문**
  - 그리디 알고리즘에서는 문제 풀이를 위한 최소한의 아이디어를 떠올리고 이것이 정당한지 검토할 수 있어야 한다.

```python
n = 1260
count = 0

# 큰 단위의 화폐부터 차례대로 확인
array = [500, 100, 50, 10]

for coin in array:
    count += n // coin	# 해당 화폐로 거슬러 줄 수 있는 동전의 개수 세기
    n %= coin
    
print(count)
```

- 시간 복잡도: 화폐의 종류가 K일 때 O(K)
  - 거슬러줘야 하는 금액과 시간 복잡도는 무관하며, 동전의 총 종류에만 영향을 받는다.

### 문제 2. 1이 될 때까지

어떤 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 한다. 단, 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있다.

1. N에서 1을 뺀다.
2. N을 K로 나눈다.

예를 들어 N이 17, K가 4일 때 1번 고정을 한 번 수행하면 N은 16이 된다. 이후 2번으 ㅣ과정을 수행하면 N은 1이 된다. 결과적으로 전체 과정을 실행한 횟수는 3이 되고, 이는 N을 1로 만드는 최소 횟수이다. N과 K가 주어질 때 N이 1이 될 때까지 1번 혹은 2번의 과정을 **수행해야 하는 최소 횟수**를 구하는 프로그램을 작성하라.

`입력 조건`

- 첫째 줄에 N(1 <= N <= 100,000)과 K(2 <= K <= 100,000)가 공백을 기준으로 하여 각각 자연수로 주어진다.

`출력 조건`

- 첫째 줄에 N이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최솟값을 출력한다.

`입력 예시`

```bash
25 5
```

`출력 예시`

```bash
2
```

#### 답안

- 주어진 N에 대하여 최대한 많이 나누기를 수행한다.
- N의 값을 줄일 때 2 이상의 수로 나누는 작업이 1을 빼는 작업보다 수를 훨씬 많이 줄일 수 있다.
- 정당성 분석
  - N이 아무리 큰 수여도, K로 계속 나눈다면 기하급수적으로 빠르게 줄일 수 있다.
  - K가 2 이상이기만 하면, K로 나누는 것이 1을 빼는 것보다 항상 빠르게 N을 줄일 수 있으며 N은 항상 1에 도달한다. (최적의 해 성립)

```python
n, k = map(int, input().split())
count = 0
# n과 k의 수가 커졌을 때 아래와 같이 반복문을 작성하면 시간 복잡도가 높아진다.
# while n > 1:
#     if n % k == 0:
#         n /= k
#         count += 1
#     else:
#         n -= 1
#         count += 1
# 따라서 아래처럼 반복문에서 한 번에 계산하도록 하면 N과 K의 수가 커져도 시간 복잡도가 더 낮다.
while True:
    # n이 k로 나누어 떨어지는 수가 될 때까지 빼기
    target = (n // k) * k
    count += (n - target)	# 1을 빼는 연산 횟수를 한 번에 더해준다.
    n = target
    # n이 k보다 작을 때 (더 이상 나눌 수 없을 때) 반복문 탈출
    if n < k:
        break
    # k로 나누기
    count += 1
    n //= k
    
# 마지막으로 남은 수에 대해 1씩 빼기
count += (n - 1)
print(count)
```

### 문제 3. 곱하기 혹은 더 하기

각 자리가 숫자(0 - 9)로만 이루어진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자 사이세 'x' 혹은 '+' 연산자를 넣어 결과적으로 만들어질 수 있는 가장 큰 수를 구하는 프로그램을 작성하라. 단, +보다 x를 먼저 계산하는 일반적인 방식과는 달리, 모든 연산은 왼쪽에서부터 순서대로 이루어진다고 가정한다. 예를 들어 02984라는 문자열로 만들 수 있는 가장 큰 수는 ((((0 + 2) x 9) x 8) x 4) = 576이다. 또한 만들어질 수 있는 가장 큰 수는 항상 20억 이하의 정수가 되도록 입력이 주어진다.

`입력 조건`

- 첫째 줄에 여러 개의 숫자로 구성된 하나의 문자열 S가 주어진다. (1 <= S의 길이 <= 20)

`출력 조건`

- 첫째 줄에 만들어질 수 있는 가장 큰 수를 출력한다.

`입력 예시1`

```bash
02984
```

`출력 예시1`

```bash
576
```

`입력 예시2`

```bash
567
```

`출력 예시2`

```bash
210
```

#### 답안

- 대부분의 경우 '+'보다는 'x'가 더 값을 크게 만든다.
  - 예를 들어 5 + 6 = 11이고, 5 x 6 = 30
- 다만 두 수 중에서 하나라도 '0' 혹은 '1'인 경우, 곱하기보다는 더하기를 수행하는 것이 효율적

```python
s = input()
    
result = int(s[0])
for i in range(1, len(s)):
    n = int(s[i])
    if (n <= 1) or (result <= 1):
        result += n
    else:
        result *= n
print(result)
```

### 문제 4. 모험가 길드

한 마을에 모험가가 N명 있다. 모험가 길드에서는 N명의 모험가를 대상으로 '공포도'를 측정했는데, '공포도'가 높은 모험가는 쉽게 공포를 느껴 위험 상황에서 제대로 대처할 능력이 떨어진다. 모험가 길드장인 동빈이는 모험가 그룹을 안전하게 구성하고자 공포도가 X인 모험가는 반드시 X명 이상으로 구성한 모험가 그룹에 참여해야 여행을 떠날 수 있도록 규정했다. 동빈이는 최대 몇 개의 모 험가 그룹을 만들 수 있는 궁금하다. N명의  모험가에 대한 정보가 주어졌을 때, 여행을 떠날 수 있는 그룹 수의 최댓값을 구하는 프로그램을 작성하라. 예를 들어 N = 5이고, 각 모험가의 공포도가 다음과 같다면

```bash
2 3 1 2 2
```

이 경우 그룹 1에 공포도가 1, 2, 3인 모험가를 한 명씩 넣고, 그룹 2에 공포도가 2인 남은 두 명을 넣으면 총 2개의 그룹을 만들 수 있다. 또한 몇 명의 모험가는 마을에 그대로 남아 있어도 되기 때문에 모든 모험가를 특정 그룹에 넣을 필요는 없다.

`입력 조건`

- 첫째 줄에 모험가의 수  N이 주어진다.(1 <= N <= 100,000)
- 둘째 줄에 각 모험가의 공포도의 값이 N 이하의 자연수로 주어지며, 각 자연수는 공백으로 구분한다.

`출력 조건`

- 여행을 떠날 수 있는 그룹 수의 최댓값을 출력하라.

`입력 예시`

```bash
5
2 3 1 2 2
```

`출력 예시`

```bash
2
```

#### 답안

- 오름차순 정렬 이후 공포도가 가장 낮은 모험가부터 하나씩 확인
- 앞에서부터 공포도를 하나씩 확인하며 '현재 그룹에 포함된 모험가의 수'가 '현재 확인하고 있는 공포도보다 크거나 같다면 이를 그룹으로 설정'
- 공포도가 오름차순으로 정렬되어 있다는 점에서 항상 최소한의 모험가의 수만 포함하여 그룹을 결성

```python
n = int(input())
a = list(map(int, input().split()))

a.sort()
result = 0	# 총 그룹의 수
count = 0	# 현재 그룹에 포함된 모험가의 수

for i in a:	# 공포도를 낮은 것부터 하나씩 확인
    count += 1	# 현재 그룹에 해당 모험가 포함
    if count >= i:	# 현재 그룹에 포함된 모험가의 수가 현재의 공포도 이상이라면 그룹 결성
        result += 1	# 총 그룹의 수 증가
        count = 0	# 현재 그룹에 포함된 모험가의 수 초기화
        
print(result)	# 총 그룹 수 출력
```

## 24. 구현: 시뮬레이션과 완전 탐색

### 구현 (Implementation)

> 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정

![image-20210705141400283](../../md-img/image-20210705141400283.png)

- 알고리즘 대회나 테스트에서 구현 유형의 문제는 **풀이를 떠올리는 것은 쉽지만 소스코드로 옮기기 어려운 문제**를 지칭

- 예시 - 언어별로 차이 있음

  - 알고리즘은 간단한데 코드가 지나칠 만큼 길어지는 문제
  - 실수 연산을 다루고, 특정 소수점 자리까지 출력해야 하는 문제
  - 문자열을 특정한 기준에 따라서 끊어 처리해야 하는 문제
  - 적절한 라이브러리를 찾아서 사용해야 하는 문제

- 일반적으로 알고리즘 문제에서의 2차원 공간은 **행렬(Matrix)**의 의미로 사용된다.

  ![image-20210705141908701](../../md-img/image-20210705141908701.png)

  ```python
  for i in range(5):
      for j in range(5):
          print('(', i, ',', j, ')', end=' ')
      print()
  ```

- 시뮬레이션 및 완전 탐색 문제에서는 2차원 공간에서의 **방향 벡터**가 자주 활용된다.

  ![image-20210705142307255](../../md-img/image-20210705142307255.png)

  ```python
  # 동, 북, 서, 남
  dx = [0, -1, 0, 1]
  dy = [1, 0, -1, 0]
  
  # 현재 위치
  x, y = 2, 2
  
  for i in range(4):
      # 다음 위치
      nx = x + dx[i]
      ny = y + dy[i]
      print(nx, ny)
  ```

### 문제 1. 상하좌우

여행가 A는 N x N 크기의 정사각형 공간 위에 서 있다. 이 공간은 1 x 1 크기의 정사각형으로 나누어져 있다. 가장 왼쪽 위 좌표는 (1, 1)이며, 가장 오른쪽 아래 좌표는 (N, N)에 해당한다. 여행가 A는 상, 하, 좌, 우 방향으로 이동할 수 있으며 시작 좌표는 항상 (1, 1)이다. 우리 앞에는 여행가 A가 이동할 계획이 적힌 계획서가 놓여 있다. 계획서에는 하나의 줄에 띄어쓰기를 기준으로 하여 L, R, U, D 중 하나의 문자가 반복적으로 적혀 있다. 각 문자의 의미는 다음과 같다.

- L: 왼쪽으로 한 칸 이동
- R: 오른쪽으로 한 칸 이동
- U: 위로 한 칸 이동
- D: 아래로 한 칸 이동

이때 여행가 A가 N x N 크기의 정사각형 공간을 벗어나는 움직임은 무시된다. 예를 들어 (1, 1)의 위치에서 L 혹은 U를 만나면 무시된다. 다음은 N = 5인 지도와 계획서이다.

![image-20210705142824075](../../md-img/image-20210705142824075.png)

`입력 조건`

- 첫째 줄에 공간의 크기를 나타내는 N이 주어진다. (1 <= N <= 100)
- 둘째 줄에 여행가 A가 이동할 계획서 내용이 주어진다. (1 <= 이동 횟수 <= 100)

`출력 조건`

- 첫째 줄에 여행가 A가 최종적으로 도착할 지점의 좌표 (X, Y)를 공백을 기준으로 구분하여 출력

`입력 예시`

```bash
5
R R R U D D
```

`출력 예시`

```bash
3 4
```

#### 답안

- 요구사항대로 충실히 구현하면 되는 문제이다.
- 일련의 명령에 따라서 개체를 차례대로 이동시킨다는 점에서 시뮬레이션(Simulation) 유형으로도 분류되며 구현이 중요한 대표적인 문제 유형이다.
  - 알고리즘 교재나 문제 풀이 사이트에 따라 다르게 일컬을 수 있으나 코딩 테스트에서의 시뮬레이션 유 형, 구현 유형, 완전 탐색 유형은 서로 유사한 점이 많다.

```python
n = int(input())
a = input().split()
x = 1
y = 1

# L, R, U, D에 따른 이동 방향
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]
move_types = ['L', 'R', 'U', 'D']

# 이동 계획을 하나씩 확인
for plan in a:
    for i in range(len(move_types)):
        if plan == move_types[i]:
            nx = x + dx[i]
            ny = y + dy[i]
    # 공간을 벗어나는 경우 무시
    if nx < 1 or ny < 1 or nx > n or ny > n:
        continue
    # 이동 수행
    x, y = nx, ny
print(x, y)
```

### 문제 2. 시각

정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 구하는 프로그램을 작성하세요. 예를 들어 1을 입력했을 때 다음은 3이 하나라도 포함되어 있으므로 세어야 하는 시각이다.

- 00시 00분 03초
- 00시 13분 30초

반면에 다음은 3이 하나도 포함되어 있지 않으므로 세면 안 되는 시각이다.

- 00시 02분 55초
- 01시 27분 45초

`입력 조건`

- 첫째 줄에 정수 N이 입력된다. (0 <= N <= 23)

`출력 조건`

- 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 출력한다.

`입력 예시`

```bash
5
```

`출력 예시`

```bash
11475
```

#### 답안

- 가능한 모든 시각의 경우를 하나씩 모두 세서 풀 수 있는 문제
- 하루는 86,400초이므로, 00시 00분 00초부터 23시 59분 59초까지의 모든 경우는 86,400가지이다.
  - 24 * 60 * 60 = 86,400
- 단순히 시각을 1씩 증가시키면서 3이 하나라도 포함되어 있는지 확인 하는 방법을 사용
- **완전 탐색(Brute Forcing)**: 가능한 경우의 수를 모두 검사해보는 탐색 방법

```python
n = int(input())
count = 0
for i in range(n+1):
    for j in range(60):
        for k in range(60):
            # 매 시각 안에 '3'이 포함되어 있다면 카운트 증가
            if '3' in str(i) + str(j) + str(k):
                count += 1
                
print(count)
```

### 문제 3. 왕실의 나이트

행복 왕국의 왕실 정원은 체스판과 같은 8 x 8 좌표 평면이다. 왕실 정원의 특정한 한 칸에 나이트가 서 있다. 나이트는 매우 충성스러운 신하로서 매일 무술을 연마한다. 나이트는 말을 타고 있기 때문에 이동을 할 때는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없다. 나이트는 특정 위치에서 다음과 같은 2가지 경우로 이동할 수 있다.

1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
2. 수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동하기

이처럼 8 x 8 좌표 평면상에서 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 출력하는 프로그램을 작성하라. 왕실의 정원에서 행 위치를 표현할 때는 1부터 8로 표현하며, 열 위치를 표현할 때는 a부터 h로 표현한다.

- c2에 있을 때 이동할 수 있는 경우의 수: 6가지

  ![image-20210705152431356](../../md-img/image-20210705152431356.png)

- a1에 있을 때 이동할 수 있는 경우의 수: 2가지

  ![image-20210705152445241](../../md-img/image-20210705152445241.png)

`입력 조건`

- 첫째 줄에 8 x 8 좌표 평면상에서 현재 나이트가 위치한 곳의 좌표를 나타내는 두 문자로 구성된 문자열이 입력된다. 입력 문자는 a1처럼 열과 행으로 이뤄진다.

`출력 조건`

- 첫째 줄에 나이트가 이동할 수 있는 경우의 수를 출력

`입력 예시`

```bash
a1
```

`출력 예시`

```bash
2
```

#### 답안

- 요구사항대로 충실히 구현하면 되는 문제
- 나이트의 8가지 경로를 하나씩 확인하며 각 위치로 이동이 가능한지 확인
- 리스트를 이용하여 8가지 방향에 대한 방향 벡터 정의

```python
n = input()
x = int(n[1])
y = int(ord(n[0])) - 96

# 나이트가 이동할 수 있는 8가지 방향 정의
steps = [(-2, -1), (-1, -2), (1, -2), (2, -1), (2, 1), (1, 2), (-1, 2), (-2, 1)]

# 8가지 방향에 대해 각 위치로 이동 가능한지 확인
result = 0
for step in steps:
    # 이동하고자 하는 위치 확인
    next_x = x + step[0]
    next_y = y + step[1]
    # 해당 위치로 이동 가능하면 카운트 증가
    if next_x >= 1 and next_x <= 8 and next_y >= 1 and next_y <= 8:
        result += 1
        
print(result)
```

### 문제 4. 문자열 재정렬

알파벳 대문자와 숫자(0 - 9)로만 구성된 문자열이 입력으로 주어진다. 이때 모든 알파벳을 오름차순으로 정렬하여 이어서 출력한 뒤에 그 뒤에 모든 숫자를 더한 값을 이어서 출력한다. 예를 들어 K1KA5CB7이라는 값이 들어오면 ABCKK13을 출력한다.

`입력 조건`

- 첫째 줄에 하나의 문자열 S가 주어진다. (1 <= S의 길이 <= 10,000)

`출력 조건`

- 첫째 줄에 문제에서 요구하는 정답 출력

`입력 예시1`

```bash
K1KA5CB7
```

`출력 예시1`

```bash
ABCKK13
```

`입력 예시2`

```bash
AJKDLSI412K4JSJ9D
```

`출력 예시2`

```bash
ADDIJJJKKLSS20
```

#### 답안

- 요구사항대로 충실히 구현하면 되는 문제
- 문자열이 입력되었을 때 문자를 하나씩 확인
  - 숫자인 경우 따로 합계 계싼
  - 알파벳은 별도의 리스트에 저장
- 리스트에 저장된 알파벳을 정렬해 출력하고 합계를 뒤에 붙여 출력하면 정답

```python
# 내 소스
s = input()
ss = []

n = 0
for i in s:
    if ord(i) >= 48 and ord(i) <= 57:
        n += int(i)
    else:
        ss.append(i)
ss.sort()

sss = ''
for i in ss:
    sss += i
print(sss+str(n))

# 답안 소스
data = input()
result = []
value = 0

# 문자를 하나씩 확인하며
for x in data:
    # 알파벳인 경우 리스트에 삽입
    if x.isalpha():
        result.append(x)
    # 숫자는 따로 더하기
    else:
        value += int(x)
        
# 알파벳 오름차순 정렬
result.sort()

# 숫자가 하나라도 존재하면 가장 뒤에 삽입
if value != 0:
    result.append(str(value))
    
# 최종 결과 출력(리스트를 문자열로 변환 출력)
print(''.join(result))
```

## 25. 투 포인터와 구간 합

### 25-1. 투 포인터 (Two Pointers) 알고리즘

> 리스트에 순차적으로 접근해야 할 때 두 개의 점의 위치를 기록하면서 처리하는 알고리즘

- 흔히 2, 3, 4, 5, 6, 7번 학생을 지목해야 할 때 간단히 '2번부터 7번까지의 학생'이라고 부르듯이 리스트에 담긴 데이터에 순차적으로 접근해야 할 때는 **시작점**과 **끝점**이라는 2개의 점으로 접근할 데이터의 범위를 표현할 수 있다.

### 문제 1. 특정한 합을 가지는 부분 연속 수열 찾기

N개의 자연수로 구성된 수열이 있다. 합이 M인 부분 연속 수열의 개수를 구하라. 수행 시간 제한은 O(N)이다.

![image-20210705160147819](../../md-img/image-20210705160147819.png)

#### 답안

- 투 포인터 활용
  1. 시작점(start)과 끝점(end)이 첫 번째 원소의 인덱스(0)를 가리키도록 한다.
  2. 현재 부분 합이 M과 같다면 카운트한다.
  3. 현재 부분 합이 M보다 작다면 end를 1 증가시킨다.
  4. 현재 부분 합이 M보다 크거나 같다면 start를 1 증가시킨다.
  5. 모든 경우를 확인할 때까지 2번부터 4번까지의 과정을 반복한다.

```python
n = 5	# 데이터의 개수
m = 5	# 찾고자 하는 부분합
data = [1, 2, 3, 2, 5]	# 전체 수열

count = 0
interval_sum = 0
end = 0

# start를 차례대로 증가시키며 반복
for start in range(n):
    # end를 가능한 만큼 이동
    while interval_sum < m and end < n:
        interval_sum += data[end]
        end += 1
    # 부분합이 m일 때 카운트 증가
    if interval_sum == m:
        count += 1
    interval_sum -= data[start]
    
print(count)
```

### 25-2. 구간 합 (Interval Sum) 문제

> 연속적으로 나열된 N개의 수가 있을 때 특정 구간의 모든 수를 합한 값을 계산하는 문제

- 예를 들어 5개의 데이터로 구성된 수열 {10, 20, 30, 40, 50}이 있을 때 두 번째 수부터 네 번째 수까지의 합은 20 + 30 + 40 = 90이다.

### 문제 2. 구간 합 빠르게 계산하기

N개의 정수로 구성된 수열이 있다. M개의 쿼리(Query) 정보가 주어진다. 각 쿼리는 Left와 Right로 구성며, 각 쿼리에 대해 [Left, Right] 구간에 포함된 데이터들의 합을 출력해야 한다. 수행 시간 제한은 O(N + M)이다.

#### 답안

- 접두사 합(Prefix Sum): 배열의 맨 앞부터 특정 위치까지의 합을 미리 구해 놓은 것
- 접두사 합을 활용한 알고리즘
  - N개의 수 위치 각각에 대해 접두사 합을 계산하여 P에 저장한다.
  - 매 M개의 쿼리 정보를 확인할 때 구간 합은 P[Right] - P[Left - 1]이다.

![image-20210705161636940](../../md-img/image-20210705161636940.png)

```python
# 데이터의 개수 N과 데이터 입력받기
n = 5
data = [10, 20, 30, 40, 50]

# 접두사 합(Prefix Sum) 배열 계산
sum_value = 0
prefix_sum = [0]
for i in data:
    sum_value += i
    prefix_sum.append(sum_value)
    
# 구간 합 계산(세 번째 수부터 네 번째 수까지)
left = 3
right = 4
print(prefix_sum[right] - prefix_sum[left - 1])
```

