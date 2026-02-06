# 우선순위 큐(Priority Queue)
- **우선순위가 가장 높은 데이터를 가장 먼저 삭제**하는 자료구조이다.

- 예를 들어 여러 개의 물건 데이터를 자료구조에 넣었다가 가치가 높은 물건 데이터부터 꺼내서 확인해야 하는 경우에 우선순위 큐를 이용할 수 있다.

- python, C++, JAVA를 포함한 대부분의 프로그래밍 언어에서 **표준 라이브러리 형태로 지원**한다.

    ![priority_queue_1](./img/priority_queue_1.png)

## 힙(Heap)
- 우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나이다.
  - 내부적으로 트리 구조를 활용하여 삽입과 삭제를 함

- **최소 힙**(**Min Heap**)과 **최대 힙**(**Max Heap**)이 있다.
  - **최소 힙**(**Min Heap**) : 값이 낮은 데이터부터 꺼내는 방식으로 동작
  - **최대 힙**(**Max Heap**) : 값이 높은 데이터부터 꺼내는 방식으로 동작

- 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용된다.

    ![priority_queue_2](./img/priority_queue_2.png)

### 힙 라이브러리 사용 예제: 최소 힙
```
inport heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    redult = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    for i in range(len, h):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 8, 2, 4, 6, 8, 0])
print(result)
```
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
- 데이터를 넣을 때 가장 작은 값이 항상 인덱스 0이 되도록 알아서 위치를 조정해서 h 리스트에 넣는다.

- 데이터를 뺄 때 즉 heappop할 때 그냥 인덱스 0에서부터 순서대로 꺼내는 것이다.

- 힙에 데이터를 하나 넣을 때 $O(logN)$의 시간 복잡도가 걸리므로 n개의 데이터를 넣은 뒤 빼는 경우 $O(NlogN)$의 시간 복잡도가 소요된다. -> 퀵 정렬 알고리즘과 동일한 시간 복잡도

### 힙 라이브러리 사용 예제: 최대 힙
```
inport heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    redult = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    for i in range(len, h):
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 8, 2, 4, 6, 8, 0])
print(result)
```
```
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```
- 기본적으로 파이썬에서는 최대 힙을 따로 제공하지 않는다.

- 따라서 데이터를 힙에 넣기 전에 데이터의 부호를 반대로 바꿔 넣고 꺼낼때도 데이터 부호를 반대로 바꾸면 된다.