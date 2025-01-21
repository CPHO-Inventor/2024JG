## assignment6

### 1.题目

#### sy119: 汉诺塔

代码以及AC截图

源代码

```
n = int(input())
def moving(n, a, c, b):
    if n == 0:
       return
    else:
        moving(n - 1, a, b, c)
        print(f'{a}->{c}')
        moving(n - 1, b, c, a)
print(2 ** n - 1)
moving(n, 'A','C','B')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022059207.png)

时间：0ms

#### sy132: 全排列I

代码以及AC截图

源代码

```
def dfs(idx, n, used, temp, result):
    if idx == n + 1:
        result.append(temp[:])
        return

    for i in range(1, n + 1):
        if not used[i]:
            temp.append(i)
            used[i] = True
            dfs(idx + 1, n, used, temp, result)
            used[i] = False
            temp.pop()


def generate_permutations(n):
    result = []
    used = [False] * (n + 1)
    dfs(1, n, used, [], result)

    for perm in result:
        print(" ".join(map(str, perm)))


n = int(input())
generate_permutations(n)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022112391.png)

时间：0ms

#### 02945: 拦截导弹

代码以及AC截图

源代码

```
def find0(k, h):
    dp = [1] * k
    for i in range(1, k):
        for j in range(i):
            if h[i] <= h[j]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)
n = int(input())
h = [int(x) for x in input().split()]
print(find0(n, h))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022117946.png)

时间：23ms

#### 23421: 小偷背包

代码以及AC截图

源代码

```
n, b = map(int, input().split())
money = [int(x) for x in input().split()]
weight = [int(x) for x in input().split()]
dp = [0] * (b + 1)
for i in range(n):
    for j in range(b, weight[i] - 1, -1):
        dp[j] = max(dp[j], dp[j - weight[i]] + money[i])
print(dp[-1])
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022120087.png)

时间：24ms

#### 02754: 八皇后

代码以及AC截图

源代码

```
answer = []

def Queen(s):
    for col in range(1, 9):
        for j in range(len(s)):
            if (str(col) == s[j] or abs(col - int(s[j])) == abs(len(s) - j)):
                break
        else:
            if len(s) == 7:
                answer.append(s + str(col))
            else:
                Queen(s + str(col))

Queen('')

n = int(input())
for _ in range(n):
    a = int(input())
    print(answer[a - 1])
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022123906.png)

时间：46ms

#### 189A. Cut Ribbon

代码以及AC截图

源代码

```
n, a, b, c = map(int, input().split())
dp = [0] + [-10000000] * 4000
for i in range(1, n + 1):
    dp[i] = max(dp[i - a], dp[i - b], dp[i - c]) + 1
print(dp[n])
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411022126719.png)

时间：93ms

### 2.学习收获与总结

感觉强度上来了，而且这两周期中，也就没跟进每日选做。所以是先看了两道题的答案才摸上门的，而且感觉dp比递归的题更好做一些，但是都不太好写思路（感觉语言有点匮乏）。