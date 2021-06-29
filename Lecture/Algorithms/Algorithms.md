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

