# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python
n = int(input())
s = 'ABCDEFGHIJKL'
for _ in range(n):
    num = 0
    list0 = [0] * 12
    list1 = []
    for __ in range(3):
        s0 = [str(x).strip() for x in input().split()]
        list1.append(s0)
    for i in range(12):
        list0[i] = 1
        j = 0
        noun1 = True
        while j <= 2:
            a = 0
            b = 0
            for k in range(len(list1[j][0])):
                a += list0[s.index(list1[j][0][k])]
            for k in range(len(list1[j][1])):
                b += list0[s.index(list1[j][1][k])]
            if a > b:
                if list1[j][2] != 'up':
                    noun1 = False
                    break
            elif a < b:
                if list1[j][2] != 'down':
                    noun1 = False
                    break
            else:
                if list1[j][2] != 'even':
                    noun1 = False
                    break
            j += 1
        if noun1:
            num = i
            break
        list0[i] = -1
        j = 0
        noun2 = True
        while j <= 2:
            a = 0
            b = 0
            for k in range(len(list1[j][0])):
                a += list0[s.index(list1[j][0][k])]
            for k in range(len(list1[j][1])):
                b += list0[s.index(list1[j][1][k])]
            if a > b:
                if list1[j][2] != 'up':
                    noun2 = False
                    break
            elif a < b:
                if list1[j][2] != 'down':
                    noun2 = False
                    break
            else:
                if list1[j][2] != 'even':
                    noun2 = False
                    break
            j += 1
        if noun2:
            num = i
            break
        list0[i] = 0
    if list0[num] == 1:
        print(f'{s[num]} is the counterfeit coin and it is heavy.')
    else:
        print(f'{s[num]} is the counterfeit coin and it is light.')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221103205.png)

时间：20min

### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
r, c = map(int, input().split())
maze = [[int(x) for x in input().split()] for i in range(r)]

dp = [[0 for k in range(c)] for j in range(r)]

dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]
def dfs(maze, x, y):
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < r and 0 <= ny < c and maze[x][y] > maze[nx][ny]:
            if dp[nx][ny] == 0:
                dfs(maze, nx, ny)
            dp[x][y] = max(dp[x][y], dp[nx][ny] + 1)
    if dp[x][y] == 0:
        dp[x][y] = 1

max_num = 0
for a in range(r):
    for b in range(c):
        if dp[a][b] == 0:
            dfs(maze, a, b)
            max_num = max(max_num, dp[a][b])
print(max_num)
```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221105375.png)

时间：40min

### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]
def is_valid(maze, n, x, y, num):
    if num == 1:
        return 0<=x<n and 0<=y<n - 1 and not visited[x][y] and maze[x][y] != 1 and maze[x][y + 1] != 1
    else:
        return 0 <= x < n - 1 and 0 <= y < n and not visited[x][y] and maze[x][y] != 1 and maze[x + 1][y] != 1

def dfs(maze, n, x, y,num):
    global noun
    if num == 1:
        if (maze[x][y] == 9 and maze[x][y + 1] != 1) or (maze[x][y + 1] == 9 and maze[x][y] != 1):
            noun = True
        visited[x][y] = True
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if is_valid(maze, n, nx, ny, num):
                # print(nx,ny)
                dfs(maze, n, nx, ny, num)
        visited[x][y] = False
    else:
        if (maze[x][y] == 9 and maze[x + 1][y] != 1) or (maze[x + 1][y] == 9 and maze[x][y] != 1):
            noun = True
        visited[x][y] = True
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if is_valid(maze, n, nx, ny, num):
                dfs(maze, n, nx, ny, num)
        visited[x][y] = False


n = int(input())
num = 0
list0 = []
a = 0
b = 0
noun = False
for i in range(n):
    list1 = [int(x) for x in input().split()]
    list0.append(list1)
    if 5 in list1:
        num += 1
        if num == 1:
            a = i
            b = list1.index(5)
visited = [[False for i in range(n)] for j in range(n)]
# print(num)
# print(a, b)
dfs(list0, n, a, b, num)
if noun:
    print('yes')
else:
    print('no')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221106889.png)

时间：40min

### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：



代码：

```python
def f(string):
    if string=='':
        return 0
    else:
        return int(string)

m = int(input())
n = int(input())
l = input().split()
# 从后往前排序
for i in range(n):
    for j in range(n-1-i):
        if l[j] + l[j+1] > l[j+1] + l[j]:
            l[j],l[j+1] = l[j+1],l[j]

length = []
for num in l:
    length.append(len(num))

dp = [[''] * (m + 1) for i in range(n + 1)]
# for i in range(n + 1):
#     dp[i][0] = ''
# for i in range(m + 1):
#     dp[0][i] = ''

for i in range(1, n + 1):
    for j in range(1, m + 1):
        if length[i - 1] > j:
            dp[i][j] = dp[i - 1][j]
        else:
            dp[i][j] = str(max(f(dp[i - 1][j]), int(l[i - 1] + dp[i - 1][j - length[i - 1]])))
print(dp[n][m])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221107727.png)

时间：40min（看的答案）

### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：



代码：

```python
X = [[0, 0, 0, 0, 0, 0, 0, 0]]
Y = [[0, 0, 0, 0, 0, 0, 0, 0]]
for _ in range(5):
    X.append([0] + [int(x) for x in input().split()] + [0])
    Y.append([0 for x in range(8)])
X.append([0, 0, 0, 0, 0, 0, 0, 0])
Y.append([0, 0, 0, 0, 0, 0, 0, 0])

import copy

for a in range(2):
    Y[1][1] = a
    for b in range(2):
        Y[1][2] = b
        for c in range(2):
            Y[1][3] = c
            for d in range(2):
                Y[1][4] = d
                for e in range(2):
                    Y[1][5] = e
                    for f in range(2):
                        Y[1][6] = f

                        A = copy.deepcopy(X)
                        B = copy.deepcopy(Y)
                        for i in range(1, 7):
                            if B[1][i] == 1:
                                A[1][i] = abs(A[1][i] - 1)
                                A[1][i - 1] = abs(A[1][i - 1] - 1)
                                A[1][i + 1] = abs(A[1][i + 1] - 1)
                                A[2][i] = abs(A[2][i] - 1)
                        for i in range(2, 6):
                            for j in range(1, 7):
                                if A[i - 1][j] == 1:
                                    B[i][j] = 1
                                    A[i][j] = abs(A[i][j] - 1)
                                    A[i - 1][j] = abs(A[i - 1][j] - 1)
                                    A[i + 1][j] = abs(A[i + 1][j] - 1)
                                    A[i][j - 1] = abs(A[i][j - 1] - 1)
                                    A[i][j + 1] = abs(A[i][j + 1] - 1)
                        if A[5][1] == 0 and A[5][2] == 0 and A[5][3] == 0 and A[5][4] == 0 and A[5][5] == 0 and A[5][
                            6] == 0:
                            for i in range(1, 6):
                                print(" ".join(repr(y) for y in [B[i][1], B[i][2], B[i][3], B[i][4], B[i][5], B[i][6]]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221109266.png)

时间：15min

### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：



代码：

```python
l, n, m = map(int, input().split())
list0 = [0]
for i in range(n):
    list0.append(int(input()))
list0.append(l)

def find(d, m):
    num = 0
    a = 0
    for i in range(1, n + 2):
        if list0[i] - a < d:
            num += 1
        else:
            a = list0[i]

    if num > m:
        return True
    else:
        return False


lo, hi = 0, l + 1
ans = -1
while lo < hi:
    mid = (lo + hi) // 2

    if find(mid, m):
        hi = mid
    else:  # 返回False，有可能是num==m
        ans = mid  # 如果num==m, mid可能是答案
        lo = mid + 1
print(ans)



```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412221110394.png)

（看的答案）

## 2. 学习总结和收获

这次作业感觉还是有点复杂的，对于dp感觉还是不熟练，有的greedy还是想不出来。最近每日选做补到12.13号了，争取能做完。





