### 백준 단계별로 풀어보기 - 3단계 (for문)

##### 단계 1 - 구구단 (2739)

```python
n = int(input())
for i in range(1, 10):
    print(f'{n} * {i} = {n*i}')
```

##### 단계 2 - A+B - 3 (10950)

```python
T = int(input())

for i in range(T):
    A, B = map(int, input().split())
    print(A+B)
```

##### 단계 3 - 합 (8393)

```python
n = int(input())
sum = 0
for i in range(1, n+1):
    sum += i
print(sum)
```

##### 단계 4 - 빠른 A+B (15552)

```python
import sys

T = int(input())

for i in range(T):
    A, B = map(int, sys.stdin.readline().rstrip().split())
    print(A+B)
```

##### 단계 5 - N 찍기 (2741)

```python
N = int(input())
for i in range(1, N+1):
    print(i)
```

##### 단계 6 기찍 N (2742)

```python
N = int(input())
for i in range(N, 0, -1):
    print(i)
```

##### 단계 7 A+B - 7 (11021)

```python
import sys
T = int(input())

for i in range(1, T+1):
    A, B = map(int, sys.stdin.readline().rstrip().split())
    print(f'Case #{i}: {A+B}')
```

##### 단계 8 A+B - 8 (11022)

```python
import sys
T = int(input())

for i in range(1, T+1):
    A, B = map(int, sys.stdin.readline().rstrip().split())
    print(f'Case #{i}: {A} + {B} = {A+B}')
```

##### 단계 9 별 찍기 - 1 (2438)

```python
N = int(input())

for i in range(1, N+1):
    print("*"*i)
```

##### 단계 10 별 찍기 - 2 (2439)

```python
N = int(input())

for i in range(1, N+1):
    print(" "*(N-i) + "*"*i)
```

##### 단계 11 - X보다 작은 수 (10871)

```python
N, X = map(int, input().split())
A = map(int, input().split())
A = list(A)

answer = []
for i in range(N):
    if A[i] < X:
        answer.append(str(A[i]))

print(" ".join(answer))
```

