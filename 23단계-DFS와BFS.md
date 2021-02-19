##### 단계 1 - DFS와 BFS (1260)

```python
import sys
from collections import deque
answer = []

n, m, v = map(int, sys.stdin.readline().rstrip().split())
arr = []
d_visited = [1]*(n+1)
for i in range(m):
    a, b = map(int, sys.stdin.readline().rstrip().split())
    d_visited[a] = 0
    d_visited[b] = 0
    arr.append([a, b])
    arr.append([b, a])

arr = sorted(arr, key=lambda x:(x[0], x[1]))

def dfs_sol(d_arr, d_visited, d_v):
    def dfs(index):
        d_visited[index] = 1
        print(index, end=' ')
        for i in range(len(d_arr)):
            if index == d_arr[i][0] and d_visited[d_arr[i][1]] == 0:
                dfs(d_arr[i][1])

    index = d_v
    dfs(index)

def bfs_sol(b_arr, b_v):
    b_dict = {}
    visited = []
    for i in range(1, n+1):
        b_dict[i] = set()
    for line in b_arr:
        b_dict[line[0]].add(line[1])
        b_dict[line[1]].add(line[0])
    queue = deque([b_v])

    while queue:
        i = queue.popleft()
        if i not in visited:
            visited.append(i)
            print(i, end=' ')
            tmp = b_dict[i] - set(visited)
            tmp = sorted(tmp)
            queue += tmp

dfs_sol(arr, d_visited, v)
print()
bfs_sol(arr, v)
```

##### 단계 2 - 바이러스 (2606)

```python
import sys
computers = int(sys.stdin.readline().rstrip())
n = int(sys.stdin.readline().rstrip())
lines = []
visited = [0]*(computers+1)
visited[0] = 1
answer = -1

for _ in range(n):
    a, b = map(int, sys.stdin.readline().rstrip().split())
    lines.append([a, b])
    lines.append([b, a])

lines = sorted(lines, key=lambda x:x[0])

def dfs(index):
    visited[index] = 1
    global answer
    answer += 1
    for line in lines:
        if line[0] == index and visited[line[1]] == 0:
            dfs(line[1])
    
    return answer

index = visited.index(0)
print(dfs(index))
```

##### 단계 3 - 단지번호붙이기 (2667)

```python
n = int(input())
apart = []
visited = [[0]*n for _ in range(n)]
answer = []

for _ in range(n):
    apart.append(list(map(int, list(input()))))    

def dfs(i, j, count):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    visited[i][j] = 1
    for pos in range(4):
        nx, ny = i+dx[pos], j+dy[pos]
        if 0 <= nx < n and 0 <= ny < n and visited[nx][ny] == 0 and apart[nx][ny] == 1:
            count = dfs(nx, ny, count+1)
    
    return count

for i in range(n):
    for j in range(n):
        if apart[i][j] == 1 and visited[i][j] == 0:
            c = dfs(i, j, 1)
            answer.append(c)

print(len(answer))
for ans in sorted(answer):
    print(ans)
```

1이 나올 때 까지 크게 단지를 돌며 1이 나온 순간 dfs탐색을 시작한다.

해당 위치에서 상하좌우를 체크해 방문하지 않은 지역이고 1인 지역이라면 해당 좌표로 다시 dfs 탐색을 시작한다.

또한 방문하지 않은 1인 좌표를 탐색할 때 마다 count 횟수를 늘린다.

##### 단계 4 - 유기농 배추 (1012)

```python
import sys
sys.setrecursionlimit(10000)
t = int(input())
for _ in range(t):
    m, n, k = map(int, input().split())
    cabbage = [[0]*n for _ in range(m)]
    visited = [[0]*n for _ in range(m)]
    answer = []

    for _ in range(k):
        a, b = map(int, input().split())
        cabbage[a][b] = 1

    def dfs(i, j, count):
        dx = [-1, 1, 0, 0]
        dy = [0, 0, -1, 1]
        visited[i][j] = 1
        for pos in range(4):
            nx, ny = i+dx[pos], j+dy[pos]
            if 0 <= nx < m and 0 <= ny < n and visited[nx][ny] == 0 and cabbage[nx][ny] == 1:
                count = dfs(nx, ny, count+1)
        
        return count

    for i in range(m):
        for j in range(n):
            if cabbage[i][j] == 1 and visited[i][j] == 0:
                c = dfs(i, j, 1)
                answer.append(c)
    print(len(answer))
```

단계 3과 완전히 같은 문제.

##### 단계 5 - 미로 탐색 (2178)

```python
import sys
from collections import deque

n, m = map(int, sys.stdin.readline().rstrip().split())
lines = []
visited = [[0]*m for _ in range(n)]
count = [[0]*m for _ in range(n)]
count[0][0] = 1

for _ in range(n):
    lines.append(sys.stdin.readline().rstrip())
queue = deque()
queue.append([0, 0])
dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]

while queue:
    x, y = queue.popleft()
    for i in range(4):
        nx, ny = x+dx[i], y+dy[i]
        if 0 <= nx < n and 0 <= ny < m:
            if visited[nx][ny] == 0 and lines[nx][ny] == '1':
                visited[nx][ny] = 1
                queue.append([nx, ny])
                count[nx][ny] = count[x][y] + 1

print(count[n-1][m-1])
```

##### 단계 6 - 토마토 (7576)

```python
from collections import deque
import sys
m, n = map(int, sys.stdin.readline().rstrip().split())
tomatos = []
for _ in range(n):
    tomatos.append(list(map(int, sys.stdin.readline().rstrip().split())))

queue = deque()
day = 0

for i in range(n):
    for j in range(m):
        if tomatos[i][j] == 1:
            queue.append([i, j])

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

while queue:
    tmp = []
    while queue:
        x, y = queue.popleft()
        for i in range(4):
            nx, ny = x+dx[i], y+dy[i]
            if 0 <= nx < n and 0 <= ny < m and tomatos[nx][ny] == 0:
                tomatos[nx][ny] = 1
                tmp.append([nx, ny])
    queue += tmp
    day += 1

for i in range(n):
    check = True
    for j in range(m):
        if tomatos[i][j] == 0:
            check = False
            break
    if check == False:
        print(-1)
        break
else:
    print(day-1)
```

토마토는 상하좌우를 익히기 때문에 dx와 dy 리스트를 만들어 상하좌우 4 가지 경우를 조작한다.

먼저 반복문을 돌며 익은 토마토를 찾아 queue에 저장한다.

다음 반복문에서는 익은 토마토 전부를 사용하여 인접한 토마토들을 익히기 때문에,

현재 queue에 있는 모든 익은 토마토를 pop 시켜서 인접 토마토를 익힌 후에 다음 익은 토마토를 한번에 queue에 넣는다.

날짜는 토마토들이 인접한 토마토를 전부 익히고 난 후 하루가 지나기 때문에 마지막에 1을 늘린다.

연산이 끝난 후 토마토 리스트에 0이 있다면 (익지 못한 토마토가 존재하면) -1을,  그렇지 않다면 날짜를 출력한다.

##### 단계 7 - 토마토 (7569)

```python
from collections import deque
import sys
m, n, h = map(int, sys.stdin.readline().rstrip().split())
tomatos = [[] for _ in range(h)]
for i in range(h):
    for _ in range(n):
        tomatos[i].append(list(map(int, sys.stdin.readline().rstrip().split())))

queue = deque()

for z in range(h):
    for i in range(n):
        for j in range(m):
            if tomatos[z][i][j] == 1:
                queue.append([z, i, j])

def bfs(queue):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    dz = [-1, 1]
    day = 0
    while queue:
        tmp = []
        while queue:
            z, x, y = queue.popleft()
            for hi in range(2):
                nz = z + dz[hi]
                if  0 <= nz < h and tomatos[nz][x][y] == 0:
                    tomatos[nz][x][y] = 1
                    tmp.append([nz, x, y])
            for i in range(4):
                nx, ny = x+dx[i], y+dy[i]
                if 0 <= nx < n and 0 <= ny < m and tomatos[z][nx][ny] == 0:
                    tomatos[z][nx][ny] = 1
                    tmp.append([z, nx, ny])
        queue += tmp
        day += 1

    for z in range(h):
        check = True
        for i in range(n):
            for j in range(m):
                if tomatos[z][i][j] == 0:
                    check = False
                    return -1
    else:
        return day-1

print(bfs(queue))
```

위 토마토 문제의 3차원 버전이다.

위 아래의 z 좌표 값만 준 뒤 확인을 거치면 간단하게 풀 수 있다.

##### 단계 8 - 숨바꼭질 (1697)

```python
from collections import deque
import sys
n, k = map(int, sys.stdin.readline().rstrip().split())
queue = deque()
visited = [0]*100001
visited[n] = 1
queue.append([n, 0])

def bfs():
    while queue:
        pos, count = queue.popleft()
        
        if pos-1 >= 0 and visited[pos-1] != 1:
            if pos-1 == k:
                break
            else:
                visited[pos-1] = 1
                queue.append([pos-1, count+1])
        if pos+1 <= 100000 and visited[pos+1] != 1:
            if pos+1 == k:
                break
            else:
                visited[pos+1] = 1
                queue.append([pos+1, count+1])
        if pos*2 <= 100000 and visited[pos*2] != 1:
            if pos*2 == k:
                break
            else:
                visited[pos*2] = 1
                queue.append([pos*2, count+1])
    return count

if n == k:
    print(0)
else:
    c = bfs()
    print(c+1)
```

수빈이가 움직이게 되는 경우는 -1, +1, *2 총 세 가지이다.

초기 설정 시 visited는 수빈이가 움직일 수 있는 최대 범위인 100,000 이하로 잡아준다.

각각의 경우를 계산한 값을 visited에 저장해주고, 후에 그 값이 다시 나올 경우에는 건너뛴다.

queue에 저장할 때는 위치 값과 더불어 count 즉, 몇 초 후에 움직인 값 인지에 대한 시간을 저장한다.

##### 단계 9 - 벽 부수고 이동하기 (2206)

```python

```

##### 단계 10 - 나이트의 이동 (7562)

```python
from collections import deque
import sys
t = int(sys.stdin.readline().rstrip())
for _ in range(t):
    l = int(sys.stdin.readline().rstrip())
    visited = [[0]*l for _ in range(l)]
    a, b = map(int, sys.stdin.readline().rstrip().split())
    knight = deque()
    knight.append([a, b, 0])
    ans_x, ans_y = map(int, sys.stdin.readline().rstrip().split())

    if a == ans_x and b == ans_y:
        print(0)
        continue

    while knight:
        x, y, c = knight.popleft()
        if x-2 >= 0 and y+1 < l and visited[x-2][y+1] == 0:
            if x-2 == ans_x and y+1 == ans_y:
                break
            else:
                visited[x-2][y+1] = 1
                knight.append([x-2, y+1, c+1])

        if x-2 >= 0 and y-1 >= 0 and visited[x-2][y-1] == 0:
            if x-2 == ans_x and y-1 == ans_y:
                break
            else:
                visited[x-2][y-1] = 1
                knight.append([x-2, y-1, c+1])

        if x+2 < l and y+1 < l and visited[x+2][y+1] == 0:
            if x+2 == ans_x and y+1 == ans_y:
                break
            else:
                visited[x+2][y+1] = 1
                knight.append([x+2, y+1, c+1])

        if x+2 < l and y-1 >= 0 and visited[x+2][y-1] == 0:
            if x+2 == ans_x and y-1 == ans_y:
                break
            else:
                visited[x+2][y-1] = 1
                knight.append([x+2, y-1, c+1])

        if x+1 < l and y-2 >= 0 and visited[x+1][y-2] == 0:
            if x+1 == ans_x and y-2 == ans_y:
                break
            else:
                visited[x+1][y-2] = 1
                knight.append([x+1, y-2, c+1])
        
        if x+1 < l and y+2 < l and visited[x+1][y+2] == 0:
            if x+1 == ans_x and y+2 == ans_y:
                break
            else:
                visited[x+1][y+2] = 1
                knight.append([x+1, y+2, c+1])
        
        if x-1 >= 0 and y-2 >= 0 and visited[x-1][y-2] == 0:
            if x-1 == ans_x and y-2 == ans_y:
                break
            else:
                visited[x-1][y-2] = 1
                knight.append([x-1, y-2, c+1])

        if x-1 >= 0 and y+2 < l and visited[x-1][y+2] == 0:
            if x-1 == ans_x and y+2 == ans_y:
                break
            else:
                visited[x-1][y+2] = 1
                knight.append([x-1, y+2, c+1])
    
    print(c+1)
```

나이트가 이동할 수 있는 경우의 수는

[[-2, 1], [-2, -1], [2, 1], [2, -1], [1, -2], [1, 2], [-1, -2], [-1, 2]] 로 총 8가지 이다.

각각의 경우에서 해당 좌표의 방문 여부와 정답 여부를 체크해준 후 일치하지 않으면 queue에 추가해준다.

##### 단계 11 - 이분 그래프 (1707)

```python

```

