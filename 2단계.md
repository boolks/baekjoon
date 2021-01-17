### 백준 단계별로 풀어보기 - 2단계 (if문)

##### 단계 1 - 두 수 비교하기 (1330)

```python
a, b = map(int, input().split())

if a > b:
    print(">")
elif a < b:
    print("<")
else:
    print("==")
```

##### 단계 2 - 시험 성적 (9498)

```python
score = int(input())

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

##### 단계 3 - 윤년 (2753)

```python
year = int(input())
if (year%4 == 0 and year%100 != 0) or (year%400 == 0):
    print(1)
else:
    print(0)
```

##### 단계 4 - 사분면 고르기 (14681)

```python
x = int(input())
y = int(input())

if x > 0 and y > 0:
    print(1)
elif x < 0 and y > 0:
    print(2)
elif x < 0 and y < 0:
    print(3)
else:
    print(4)
```

##### 단계 5 - 알람 시계 (2884)

```python
h, m = map(int, input().split())

if m < 45:
    if h == 0:
        print(23, m+15)
    else:
        print(h-1, m+15)
else:
    print(h, m-45)
```

