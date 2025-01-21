# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：



代码：

```python
dire = [[-1,-1],[-1,0],[-1,1],[0,-1],[0,1],[1,-1],[1,0],[1,1]]

area = 0
def dfs(x,y):
    global area
    if matrix[x][y] == '.':return
    matrix[x][y] = '.'
    area += 1
    for i in range(len(dire)):
        dfs(x+dire[i][0], y+dire[i][1])


for _ in range(int(input())):
    n,m = map(int,input().split())

    matrix = [['.' for _ in range(m+2)] for _ in range(n+2)]
    for i in range(1,n+1):
        matrix[i][1:-1] = input()

    sur = 0
    for i in range(1, n+1):
        for j in range(1, m+1):
            if matrix[i][j] == 'W':
                area = 0
                dfs(i, j)
                sur = max(sur, area)
    print(sur)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251613606.png)

时间：65min

### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：



代码：

```python
from collections import deque

dx = [0, 0, 1, -1]
dy = [1, -1, 0, 0]

def bfs(x, y, m, n,maze):
    q = deque()
    q.append((0, (x, y)))
    inq_set = set()
    inq_set.add((x, y))
    while q:
        step, (x0, y0) = q.popleft()
        if maze[x0][y0] == 1:
            return step
        for i in range(4):
            nx = x0 + dx[i]
            ny = y0 + dy[i]
            if (maze[nx][ny] == 0 or maze[nx][ny] == 1) and (nx, ny) not in inq_set:
                q.append((step + 1, (nx, ny)))
                inq_set.add((nx, ny))
    return 'NO'

m, n = map(int, input().split())
maze = []
maze.append([2 for _ in range(n + 2)])
for i in range(m):
    row = [2] + [int(x) for x in input().split()] + [2]
    maze.append(row)
maze.append([2 for _ in range(n + 2)])

print(bfs(1, 1, m, n, maze))


```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251614462.png)

时间：14min

### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：



代码：

```python
t = int(input())
direction = [(1, 2), (2, 1), (-1, 2), (-2, 1), (-1, -2), (-2, -1), (1, -2), (2, -1)]

cnt = 0
def is_valid(x, y):
    return 0 <= x < n and 0 <= y < m and not visited[x][y]


def dfs(x, y, num, n, m):
    global cnt
    if num == n * m:
        cnt += 1
        return
    visited[x][y] = True
    for i in range(8):
        nx = x + direction[i][0]
        ny = y + direction[i][1]
        if is_valid(nx, ny):
            next_num = num + 1
            dfs(nx, ny, next_num, n, m)
    visited[x][y] = False


for _ in range(t):
    cnt = 0
    n, m, x0, y0 = map(int, input().split())
    visited = [[False for i in range(m)] for j in range(n)]
    dfs(x0, y0, 1, n, m)
    print(cnt)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251616834.png)

时间：20min

### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：



代码：

```python
n, m = map(int, input().split())
maze = []
for _ in range(n):
    row = [int(x) for x in input().split()]
    maze.append(row)
visited = [[False for _ in range(m)] for _ in range(n)]
max_num = -float('inf')
mid_list = []
output_list = []
def is_valid(x, y):
    return 0<=x<n and 0<=y<m and not visited[x][y]

dx = [0, 0, 1, -1]
dy = [1, -1, 0, 0]

def dfs(x, y, now_num):
    global max_num, mid_list, output_list

    if x == n - 1 and y == m - 1:
        if now_num > max_num:
            max_num = now_num
            output_list = list(mid_list)
        return

    visited[x][y] = True
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if is_valid(nx, ny):
            next_num = now_num + maze[nx][ny]
            mid_list = mid_list + [[nx, ny]]
            dfs(nx, ny, next_num)
            mid_list.pop()
    visited[x][y] = False
mid_list.append([0, 0])
dfs(0, 0, maze[0][0])

for i in output_list:
    print(i[0] + 1, i[1] + 1)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251619915.png)

时间：60min



### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：



代码：

```python
class Solution(object):
    def uniquePaths(self, m, n):
        dp = [[0 for __ in range(n)] for _ in range(m)]
        dp[0][0] = 1
        for i in range(m):
            for j in range(n):
                if i == 0 and j == 0:
                    pass
                elif i == 0 and j != 0:
                    dp[i][j] = dp[i][j - 1]
                elif i != 0 and j == 0:
                    dp[i][j] = dp[i - 1][j]
                else:
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[m - 1][n - 1]


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251620634.png)

时间：10min

### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：



代码：

```python
squart = set()
i = 1
while i * i < 10 ** 9:
    squart.add(i * i)
    i += 1
list0 = list(map(int, input()))
def dfs(idx):
    if idx == len(list0):
        return True
    num = 0
    for i in range(idx, len(list0)):
        num = num * 10 + list0[i]
        if num in squart:
            if dfs(i + 1):
                return True
    return False
print('Yes' if dfs(0) else 'No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411251624897.png)

时间：30min

## 2. 学习总结和收获

感觉这次作业有的题如果直接做还是有点难度的，但整体来说还好。目前还在以每天2-3道题的速度补每日选做。





