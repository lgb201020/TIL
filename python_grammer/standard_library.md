# 실전에서 유용한 표준 라이브러리
- 내장 함수: 기본 입출력 함수부터 정렬 함수까지 기본적인 함수들을 제공
  - 별도의 import 구문 없이 사용 가능
- itertools: 파이썬에서 반복되는 형태의 데이터를 처리하기 위한 유용한 기능들을 제공
  - 특히 순열과 조합 라이브러리는 코딩 테스트에서 자주 사용됨
- heapq: 힙(Heap) 자료구조를 제공함
  - 일반적으로 우선순위 큐 기능을 구현하기 위해 사용됨
- bisect: 이진 탐색(Binary Search) 기능을 제공함
- collections: 덱(deque), 카운터(counter) 등의 유용한 자료구조를 포함한 라이브러리
- math: 필수적인 수학적 기능을 제공
  - 팩토리얼(!), 제곱근, 최대공약수(GCD), 삼각함수 관련 함수부터 파이(pi)와 같은 상수를 포함

## 자주 쓰이는 내장 함수
- sum(): 다수의 데이터를 포함하는 리스트나 튜플 등이 들어왔을 때 각 원소들의 모든 합을 반환함
    ```
    result = sum([1,2,3,4,5])
    print(result)
    ```
    ```
    15
    ```
- min(), max(): 입력으로 들어온 값 중에서 가장 작은 값, 가장 큰 값을 반환함
    ```
    min_result = min(1,2,3,4,5)
    max_result = max(1,2,3,4,5)
    print(min_result, max_result)
    ```
    ```
    1 5
    ``` 

- eval(): 문자열로 표현된 수식을 실제 계산해 수 형태의 결과 값을 반환함
    ```
    result = eval("(3+5)*7")
    print(result)
    ```
    ```
    56
    ```
- sorted(): 내부적으로 리스트와 같은 반복 가능한 객체가 입력으로 들어왔을 때 각 원소를 정렬한 결과를 반환함
  - 그냥 sorted로 쓸 수 있고 정렬 기준을 key 속성을 통해 받을 수 있다. 이때 key 속성은 람다 함수 형태로 넣는 경우가 일반적이다.
  - 기본이 오름차순 정렬이고 reverse 값을 True로 입력하면 내림차순 정렬 결과를 반환한다.
    ```
    # sorted()
    result = sorted([9, 1, 8, 5, 4])
    reverse_result = sorted([9, 1, 8, 5, 4], reverse=True)

    print(result) # [1, 4, 5, 8, 9]
    print(reverse_result) # [9, 8, 5, 4, 1]

    # sorted() with key
    array = [('홍길동', 35), ('이순신', 75), ('아무개', 50)]
    result = sorted(array, key=lambda x: x[1], reverse=True)

    print(result) # [('이순신', 75), ('아무개', 50), ('홍길동', 35)]
    ```
## 순열과 조합
- 모든 경우의 수를 고려해야 할 때 itertools 라이브러리가 효과적인다.

- 순열: 서로 다른 n개에서 서로 다른 r개를 선택하여 일렬로 나열하는 것
  - {A,B,C}에서 3개를 선택하여 나열하는 경우: ABC, ACB, BAC, BCA, CAB, CBA이다.
  - 이때 순열의 수는 $nPr = n*(n-1)*(n-2)*\dots*(n-r+1)$이다.

- 조합: 서로 다른 n개에서 순서에 상관없이 서로 다른 r개를 선택한 것
  - {A,B,C}에서 순서를 고려하지 않고 2개를 선택하는 경우: AB, AC, BC이다.
  - 이때 조합의 수는 $nCr = \frac{n*(n-1)*(n-2)*\dots*(n-r+1)}{r!}=\frac{nPr}{r!}$이다.

### 순열
- 서로 다른 n개에서 서로 다른 r개를 선택하여 나열하는 것
    ```
    from itertools import permutations

    data = ['A', 'B', 'C']

    result = list(permutations(data,3))
    print(result)
    ```
    ```
    [('A', 'B', 'C), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]
    ```
### 조합
- 서로 다른 n개에서 순서에 상관 없이 서로 다른 r개를 선택하는 것
    ```
    from itertools import combinations

    data = ['A', 'B', 'C']

    result = list(combinations(data,2))
    print(result)
    ```
    ```
    [('A', 'B'), ('A', 'C'), ('B', 'C')]
    ```
### 중복 순열과 중복 조합
- 중복 순열(nπr): 서로 다른 n개에서 중복을 허용하여 r개를 선택해 순서대로 나열하는 경우의 수로 $n^r$이다.
    ```
    from itertools import product

    data = ['A', 'B', 'C']

    result = list(product(data,repeat=2))
    print(result)
    ```

- 중복 조합: 서로 다른 n개에서 중복을 허용하여 순서에 상관없이 r개를 선택하는 경우의 수로 ${}_{(n+r-1)}C_{r}$이다.
    ```
    from itertools import combinations_with_replacement

    data = ['A', 'B', 'C']

    result = list(combinations_with_replacement(data,2))
    print(result)
    ```

## Counter
- 파이썬 collections 라이브러리의 Counter는 등장 횟수를 세는 기능을 제공한다.
- <U>리스트와 같은 반복 가능한(iterable) 객체가 주어졌을 때 내부의 원소가 몇 번씩 등장했는지를 알려준다.</U>

    ```
    from collections import Counter

    counter = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])

    print(counter['blue']) # 'blue'가 등장한 횟수 출력
    print(counter['green']) # 'green'이 등장한 횟수 출력
    print(dict(counter)) # 사전 자료형으로 반환
    ```
    ```
    3
    1
    {'red': 2, 'blue': 3, 'green': 1}
    ```
## 최대 공약수와 최소 공배수
- 최대 공약수를 구해야 할 때는 math 라이브러리의 gcd() 함수를 이용할 수 있다.
```
import math

# 최소 공배수(LCM)를 구하는 함수
def lcm(a, b):
    result = a * b // math.gcd(a, b)
    return result
    
a = 21
b = 14

print(math.gcd(21, 14)) # 최대 공약수(GCD) 계산
print(lcm(21, 14)) # 최소 공배수(LCM) 계산
```
```
7
42
```