# Assignment #A: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
n = int(input())
dp = [1] * (n + 1)
for i in range(2, n + 1):
    dp[i] = dp[i - 1] + dp[i - 2]
print(dp[n])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011243772.png)

时间：3min

### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：



代码：

```python
n = int(input())
dp = [1] * (n + 1)
for i in range(2, n + 1):
    s = 0
    for j in range(1, i + 1):
        s += dp[i - j]
    dp[i] = s
print(dp[n])
```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011247816.png)

时间：5min

### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：



代码：

```python
t, k = map(int, input().split())
dp = [1] * (10 ** 5 + 1)
s = [1] * (10 ** 5 + 1)
num = 10 ** 9 + 7
for i in range(1, 10 ** 5 + 1):
    if i >= k:
        dp[i] = (dp[i - 1] + dp[i - k]) % num
    else:
        dp[i] = dp[i - 1] % num
    s[i] = (s[i - 1] + dp[i]) % num

for i in range(t):
    a, b = map(int, input().split())
    print((s[b] - s[a - 1] + num) % num)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011249001.png)

时间：30min

### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：



代码：

```python
def longestPalindrome(s):
    n = len(s)
    if n == 1 or s == s[::-1]:
        return s
    else:
        for i in range(1, n - 1):
            for j in range(i + 1):
                substr = s[j:n - i + j]
                if substr == substr[::-1]:

                    return (substr)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011250932.png)

时间：1h



### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：



代码：

```python
from collections import deque
import sys
input = sys.stdin.read
dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]
def bfs(x, y, list0, h, visited):
    q = deque([(x, y)])
    inq_set = set()
    inq_set.add((x, y))
    while q:
        front = q.popleft()
        for i in range(4):
            nx = front[0] + dx[i]
            ny = front[1] + dy[i]
            if list0[nx][ny] < h and visited[nx][ny] and (nx, ny) not in inq_set:
                visited[nx][ny] = False
                inq_set.add((nx, ny))
                q.append((nx, ny))



def main():
    data = input().split()
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []

    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        list0 = []
        list0.append([1001] * (n + 2))
        for i in range(m):
            list0.append([1001] + list(map(int, data[idx:idx + n])) + [1001])
            idx += n
        list0.append([1001] * (n + 2))

        a, b = map(int, data[idx:idx + 2])
        idx += 2
        visited = [[False] * (n + 2)]
        for i in range(m):
            visited.append([False] + [True] * n + [False])
        visited.append([False] * (n + 2))

        p = int(data[idx])
        idx += 1

        for _ in range(p):
            c, d = map(int, data[idx:idx + 2])
            idx += 2
            bfs(c, d, list0, list0[c][d], visited)


        results.append("Yes" if not visited[a][b] else "No")

    sys.stdout.write("\n".join(results) + "\n")
if __name__ == "__main__":
    main()

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011252969.png)

时间：30min

### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：



代码：

```python
from collections import deque

dir = [(1, 0), (-1, 0), (0, 1), (0, -1)]
def bfs(s, e, maze, h, w):
    q = deque([s])
    inq_set = set()
    ans = []
    while q:
        x, y, no_dir, no_num = q.popleft()
        if (x, y) == e:
            ans.append(no_num)
            break
        for i in range(4):
            nx = x + dir[i][0]
            ny = y + dir[i][1]
            if 0 <= nx < (h + 2) and 0 <= ny < (w + 2) and (nx, ny, i) not in inq_set:
                new_dir = i
                if new_dir == no_dir:
                    new_num = no_num
                else:
                    new_num = no_num + 1
                if (nx, ny) == e:
                    ans.append(new_num)
                    continue
                if maze[nx][ny] != 'X':
                    inq_set.add((nx,ny,i))
                    q.append((nx,ny,i,new_num))
    if len(ans) == 0:
        return -1
    else:

        return min(ans)

bnum = 1
while True:
    w, h = map(int, input().split())
    if w == 0 and h == 0:
        break
    else:
        maze = []
        maze.append([' '] * (w + 2))
        for i in range(h):
            maze.append([' '] + [str(x) for x in input()] + [' '])
        maze.append([' '] * (w + 2))
        print(f"Board #{bnum}:")
        pnum = 1
        while True:
            y1, x1, y2, x2 = map(int, input().split())
            if x1 == y1 == x2 == y2 == 0:
                break
            else:
                s = (x1, y1, -1, 0)
                e = (x2, y2)
                total_num = bfs(s, e, maze, h, w)
                if total_num == -1:
                    print(f"Pair {pnum}: impossible.")
                else:
                    print(f"Pair {pnum}: {total_num} segments.")
                pnum += 1
        print()
        bnum += 1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202412011255823.png)

时间：5.5h

## 2. 学习总结和收获

这次作业前面三题还好，就是第三题压缩时间花了点时间，第四题想半天dp没想到直接枚举就过了。第五题水淹七军30分钟速通(感觉答案的bfs方式有点麻烦)。然后就是令人破防的小游戏，从周五写到周日，最后发现是线段定义的问题（。但整体感觉这次作业思维量好一点（好点有限），还是要多加训练。





