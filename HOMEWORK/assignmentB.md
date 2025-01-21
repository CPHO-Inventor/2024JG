# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）⽉考： AC1。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：



代码：

```python
a = [int(x) for x in input().split()]
list0 = [0] * (len(a))
for i in range(1, len(a)):
    num = list0[i - 1] + a[i] - a[i - 1]
    if num <= 0:
        list0[i] = 0
    else:
        list0[i] = num
print(max(list0))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081135096.png)

时间：15min

### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：



代码：

```python
n, k = map(int, input().split())
t = [int(x) for x in input().split()]
t.sort()
while k:
    num = sum(t) / k
    if t[-1] > num:
        k -= 1
        t.pop()
    else:
        print('{:.3f}'.format(sum(t) / k))
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081136626.png)

时间：20min

### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：



代码：

```python
a = [int(x) for x in input().split(',')]
n = len(a)
dp1 = [0] * n
dp2 = [0] * n
dp1[0] = a[0]
dp2[0] = a[0]
for i in range(1, n):
    dp1[i] = max(dp1[i - 1] + a[i], a[i])
    dp2[i] = max(dp2[i - 1] + a[i], a[i], dp1[i - 1], dp1[i - 1] + a[i])
print(max(dp2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081138807.png)

时间：1h

### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：



代码：

```python
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
you= [input().split() for _ in range(m)]
la=[0]*m
def dfs(i,sum1):
    global result
    if i==n:
        jian=0
        for i2 in range(m):
            store_j=0
            for k in you[i2]:
                a,b=map(int,k.split('-'))
                if la[i2]>=a:
                    store_j=max(store_j,b)
            jian+=store_j
        result=min(result,sum1-(sum1//300)*50-jian)
        return
    for i1 in store_prices[i]:
        idx,p=map(int,i1.split(':'))
        la[idx-1]+=p
        dfs(i+1,sum1+p)
        la[idx-1]-=p
dfs(0,0)
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081140064.png)

时间：1h

### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：



代码：

```python
from collections import deque
dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]

def dfs(x, y, maze, n, queue):
    maze[x][y] = 2
    queue.append((x, y))
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < n and 0 <= ny < n and maze[nx][ny] == 1:
            dfs(nx, ny, maze, n, queue)

def bfs(maze, n, queue):
    distance = 0
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if 0 <= nx < n and 0 <= ny < n:
                    if maze[nx][ny] == 1:
                        return distance
                    elif maze[nx][ny] == 0:
                        maze[nx][ny] = 2
                        queue.append((nx, ny))
        distance += 1
    return distance

n = int(input())
maze = [list(map(int, input())) for _ in range(n)]
queue = deque()
for i in range(n):
    noun = True
    for j in range(n):
        if maze[i][j] == 1:
            dfs(i, j, maze, n, queue)
            noun = False
            break
    if not noun:
        break
print(bfs(maze, n, queue))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081143723.png)

时间:1h

### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：



代码：

```python
n = int(input())
a, b = map(int, input().split())
list0 = []
for _ in range(n):
    c, d = map(int, input().split())
    list0.append((c, d))
list0.sort(key=lambda x: (x[0] * x[1]))
max_num = 0
c = a
for i in range(n):
    c *= list0[i][0]
    max_num = max(max_num, c // (list0[i][1] * list0[i][0]))
print(max_num)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412081144738.png)

时间：30min

## 2. 学习总结和收获

虽然感觉这次考试难度有点超标，但还是对自己的发挥不太满意。两岛那道题考试时dfs染色和bfs几乎和答案完全一样，然后是两个循环都要break，当时只break了一个，考试时本地一直没过也没检查出来，一直卡在这就没做出来。还有炸鸡排理解错题意了，以为是计算炸完全部鸡排的时间，就一直wa。然后国王游戏这个题题都没看，感觉是这4到T里相对简单的，回去想了一会也出来了。感觉如果考试时状态好点，觉得可以再多出来1-2道。





