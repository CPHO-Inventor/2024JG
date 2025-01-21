# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>董天泽 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：



代码：

```python
n, m = map(int, input().split())
list0 = [[0] for _ in range(n + 2)]
list1 = []
for j in range(m + 2):
    list1.append(0)
list0[0] = list1
list0[-1] = list1
for i in range(n):
    list2 = [int(x) for x in input().split()]
    list3 = [0] + list2 + [0]
    list0[i + 1] = list3
num0 = 0
total = 0
for i in range(1, n + 1):
    for j in range(1, m + 1):
        if list0[i][j] == 1:
            num0 += 1
            s = list0[i - 1][j] + list0[i + 1][j] + list0[i][j - 1] + list0[i][j + 1]
            total -= s
print(num0 * 4 + total)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172059454.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：



代码：

```python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        m = len(matrix)
        n = len(matrix[0])
        list2 = [[10000] * (n + 2)] + [[10000] + [0] * n + [10000] for i in range(m)] + [[10000] * (n + 2)]
        list0 = []
        list1 = [[10000] * (n + 2)] + [[10000] + matrix[i] + [10000] for i in range(m)] + [[10000] * (n + 2)]
        turn = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        row = 1
        col = 1
        drow, dcol = turn[0]
        N = 0
        for i in range(1, m*n + 1):
            list0.append(list1[row][col])
            list2[row][col] = list1[row][col]
            if list2[row + drow][col + dcol]:
                N += 1
                drow, dcol = turn[N % 4]
            row += drow
            col += dcol
        return list0

```



代码运行截图 ==（至少包含有"Accepted"）==

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172111574.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：



代码：

```python
d = int(input())
n = int(input())
list0 = []
for i in range(1025):
    list1 = []
    for j in range(1025):
        list1.append(0)
    list0.append(list1)
for _ in range(n):
    x, y, i = map(int, input().split())
    r1 = x - d
    r2 = x + d
    d1 = y - d
    d2 = y + d
    for k in range(max(r1, 0), min(r2 + 1, 1025)):
        for m in range(max(d1, 0), min(d2 + 1, 1025)):
            list0[k][m] += i
max0 = 0
num0 = 0
for i in range(1025):
    for j in range(1025):
        if list0[i][j] < max0:
            pass
        elif list0[i][j] > max0:
            num0 = 1
            max0 = list0[i][j]
        else:
            num0 += 1
print(num0, max0)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172108437.png)****



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：



代码：

```python
def sgn(x):
    if x == 0:
        return 0
    elif x > 0:
        return 1
    elif x < 0:
        return -1

n = int(input())
list0 = [int(x) for x in input().split()]
list1 = [sgn(list0[i + 1] - list0[i]) for i in range(n - 1) if list0[i + 1] - list0[i] != 0]
num = len(list1)
s = 0
for i in range(1, len(list1)):
    if list1[i] == list1[i - 1]:
        s += 1
print(num - s + 1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172115582.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：



代码：

```python
n = int(input())
list0 = [int(x) for x in input().split()]
dp = [0] * (max(list0) + 1)
count0 = [0] * (max(list0) + 1)
for i in list0:
    count0[i] += 1
dp[1] = count0[1]
for j in range(1, max(list0) + 1):
    dp[j] = max(dp[j - 1], dp[j - 2] + count0[j] * j)
print(max(dp))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172119450.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：



代码：

```python
while True:
    n = int(input())
    if n == 0:
        break
    else:
        list1 = [int(x) for x in input().split()]
        list2 = [int(x) for x in input().split()]
        list1.sort()
        list2.sort()
        l1 = 0
        r1 = n - 1
        l2 = 0
        r2 = n - 1
        total = 0
        while l1 <= r1:
            if list1[l1] > list2[l2]:
                total += 1
                l1 += 1
                l2 += 1
            elif list1[r1] > list2[r2]:
                total += 1
                r1 -= 1
                r2 -= 1
            else:
                if list1[l1] < list2[r2]:
                    total -= 1
                l1 += 1
                r2 -= 1
        print(total * 200)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411172121363.png)



## 2. 学习总结和收获

前面五道题都感觉还可以，就是dp还不是特别熟练。最后田忌赛马原来是只从一边开始贪心（采取胜利优先），但对于两端存在相等的情况无法解决，看了答案才想到可以两边一起贪心，就解决了。现在在补之前的每日选做。





