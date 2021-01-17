### 백준 단계별로 풀어보기 - 4단계 (while문)

##### 단계 1 - A+B - 5 (10952)

```python
A, B = map(int, input().split())

while 1:
    print(A+B)
    A, B = map(int, input().split())
    if A == 0 and B == 0:
        break
```

##### 단계 2 - A+B - 4 (10951)

```python
A, B = map(int, input().split())

while True:
    try:
        print(A+B)
        A, B = map(int, input().split())
    except EOFError:
        break

```

##### 단계 3 - 더하기 사이클 (1110)

```python
N = int(input())
answer = N
count = 0
while True:
    count += 1

    if N < 10:
        N = '0'+str(N)
    
    tmp = int(str(N)[0]) + int(str(N)[1])
    N = int(str(str(N)[-1]) + str(tmp)[-1])
    
    if N == answer:
        break
    else:
        pass

print(count)

```

