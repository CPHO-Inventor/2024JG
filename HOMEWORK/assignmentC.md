# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：



代码：

```python
while True:
    a, b = map(int, input().split())
    noun = True
    if a == b == 0:
        break
    else:
        a, b = max(a, b), min(a, b)
        while b > 0 and a // b < 2:
            if a == b:
                break
            a, b = b, a - b
            noun = not noun
        print('win' if noun else 'lose')

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131445401.png)

时间：10min

### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
n = int(input())
list0 = [[0] * (n + 2)]
for _ in range(n):
    list0 += [[0] + [int(x) for x in input().split()] + [0]]
list0 += [[0] * (n + 2)]
num = 0
if n % 2 == 0:
    for i in range(n // 2):
        sum = 0
        for k in range(n // 2 - i, n // 2 + i + 2):
            sum += list0[n // 2 - i][k] + list0[n // 2 + i + 1][k]
        for j in range(n // 2 - i + 1, n // 2 + i + 1):
            sum += list0[j][n // 2 - i] + list0[j][n // 2 + i + 1]
        num = max(num, sum)
    print(num)
else:
    for i in range((n + 1)// 2):
        sum = 0
        for k in range((n + 1) // 2 - i, (n + 1) // 2 + i + 1):
            if i != 0:
                sum += list0[(n + 1) // 2 - i][k] + list0[(n + 1) // 2 + i][k]
            else:
                sum += list0[(n + 1) // 2][k]
        for j in range((n + 1) // 2 - i + 1, (n + 1) // 2 + i):
            sum += list0[j][(n + 1) // 2 - i] + list0[j][(n + 1) // 2 + i]
        num = max(num, sum)
    print(num)
```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131446137.png)

时间：20min

### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
n = int(input())
a = [int(x) for x in input().split()]
a0 = [0] + a
dp = [-float('inf')] * (n + 1)
dp[0] = 0
for i in range(1, n + 1): # 对每一瓶药水分析
    for j in range(i, 0, -1):
        num = max(dp[j], dp[j - 1] + a0[i]) # 使得喝了j瓶后血量最高
        if num >= 0:
            dp[j] = num

for i in range(n, -1, -1):
    if dp[i] >= 0:
        print(i)
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131447271.png)

时间：25min

### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
list0 = []
list1 = []
while True:
    try:
        s = input().split()
        if s[0] == 'pop':
            if list0:
                list0.pop()
                if list1:
                    list1.pop()
        elif s[0] == 'min':
            if list1:
                print(list1[-1])
        else:
            num = int(s[1])
            list0.append(num)
            if not list1:
                list1.append(num)
            else:
                list1.append(min(list1[-1], num))
    except:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131450704.png)

时间：30min

### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python
from collections import deque
dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]
def bfs(maze, x, y, m, n):
    q = deque([(x, y)])
    distances = {(x, y): 0}

    while q:
        cx, cy = q.popleft()
        for i in range(4):
            nx = cx + dx[i]
            ny = cy + dy[i]
            if 0 <= nx < m and 0 <= ny < n:
                if maze[nx][ny] != '#':
                    nd = distances[(cx, cy)] + abs(int(maze[nx][ny]) - int(maze[cx][cy]))
                    if (nx, ny) not in distances or nd < distances[(nx, ny)]:
                        distances[(nx, ny)] = nd
                        q.append((nx, ny))
    return distances

m ,n, p = map(int, input().split())
maze = [[x for x in input().split()] for _ in range(m)]
for _ in range(p):
    a, b, c, d = map(int, input().split())
    if maze[a][b] == "#" or maze[c][d] == "#":
        print('NO')
        continue
    distances = bfs(maze, a, b, m, n)
    if (c, d) in distances:
        print(distances[(c, d)])
    else:
        print('NO')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131452301.png)

时间：1h

### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
from collections import deque

dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]
def bfs(maze, x, y, m, n, k):
    visited = {(0, x, y)}
    q = deque([(0, x, y)])
    while q:
        t, cx, cy = q.popleft()
        for i in range(4):
            nx = cx + dx[i]
            ny = cy + dy[i]
            t0 = (t + 1) % k
            if 0<=nx< m and 0<=ny < n and (t0, nx, ny) not in visited:
                if maze[nx][ny] == 'E':
                    return t + 1
                elif maze[nx][ny] != '#' or t0 == 0:
                    q.append((t + 1, nx, ny))
                    visited.add((t0, nx, ny))
    return 'Oop!'

T = int(input())
for _ in range(T):
    m, n, k = map(int, input().split())
    x = 0
    y = 0
    list0 = []
    for i in range(m):
        list1 = [x for x in input()]
        if 'S' in list1:
            x = i
            y = list1.index('S')
        list0.append(list1)
    print(bfs(list0, x, y, m, n, k))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412131453379.png)

时间：30min

## 2. 学习总结和收获

这次作业只自己出来前三道，其他都是看了答案才会的。倒数第二题用dfs写完发现时间超了。最后一题发现还可以在visited里多加一个维度，涨知识了。





