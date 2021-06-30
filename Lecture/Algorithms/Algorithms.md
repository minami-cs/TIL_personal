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

  ![image-20210628111609955](../../../md-img/image-20210628111609955.png)

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

  ![image-20210628113927571](../../../md-img/image-20210628113927571.png)

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

- 순차 탐색: 리스트 안에 있는 특정 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인하는 방법
- 이진 탐색: 정렬된 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법으로 시작점, 끝점, 중간점을 이용해 탐색 범위를 설정

