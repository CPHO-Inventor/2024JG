## assignment4

### 1.题目

#### 34B. Sale

代码以及AC截图

源代码

```
list0 = [int(x) for x in input().split()]
m = list0[1]
list1 = [int(x) for x in input().split() if int(x) < 0]
list1.sort()
sum = 0
if len(list1) < m:
    for i in list1:
        sum -= i
    print(sum)
else:
    for i in range(m):
        sum -= list1[i]
    print(sum)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181340359.png)

思路：找出所有负数，然后计算其加和。

时间：186ms

#### 160A. Twins

代码以及AC截图

源代码

```
n = int(input())
list0 = [int(x) for x in input().split()]
list0.sort()
sum1 = 0
num = 0
sum0 = 0
for i in list0:
    sum0 += i
while sum1 <= sum0 - sum1:
    sum1 += list0.pop()
    num += 1
print(num)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181343593.png)

思路：将硬币金额输入到列表，然后排序，从后往前取。

时间：124ms

#### 1879B. Chips on the Board

代码以及AC截图

源代码

```
t = int(input())
for _ in range(t):
    n = int(input())
    a = [int(x) for x in input().split()]
    b = [int(x) for x in input().split()]
    a.sort()
    b.sort()
    sum1 = 0
    sum2 = 0
    for i in a:
        sum1 += i
    for j in b:
        sum2 += j
    total1 = sum1 + b[0] * n
    total2 = sum2 + a[0] * n
    if total1 > total2:
        print(total2)
    else:
        print(total1)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181347517.png)

思路：取两个列表的和和另一个列表最小值做乘积，再取两个中较小的那一个，这样保证取到的值是最小的，也同时铺满整个空间。

时间：515ms

#### 158B. Taxi

代码以及AC截图

源代码

```
n = int(input())
list0 = [int(x) for x in input().split()]
n1 = list0.count(1)
n2 = list0.count(2)
n3 = list0.count(3)
n4 = list0.count(4)
s = n1 - n3 - 2 * (n2 % 2)
s0 = 0.5 * (abs(s) + s)
print(int(n4 + n3 + (n2 // 2) + n2 % 2 + 1 - (4 - s0 % 4) // 4 + s0 // 4))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181351785.png)

思路：通过数出各种人数的组数，利用绝对值，直接计算出结果。

时间：186ms

#### 230B. T-primes

代码以及AC截图

源代码

```
n = int(input())
list0 = [int(x) for x in input().split()]
l = [1] * 1000001
s = set()
for i in range(2, 1000001):
    if l[i]:
        s.add(i ** 2)
        for j in range(i ** 2 , 1000001, i):
            l[j] = 0
for j in list0:
    if j in s:
        print('YES')
    else:
        print('NO')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181355110.png)

思路：第一次用的筛子不好，学习了欧拉筛和埃及筛就好多了。但其实感觉主要时间来源于print。

时间：1218ms

#### 12559: 最大最小整数

代码以及AC截图

源代码

```
n = int(input())
list0 = [x for x in input().split()]
for i in range(0, n - 1):
    for j in range(i + 1, n):
        if list0[i] + list0[j] < list0[j] + list0[i]:
            s = list0[i]
            p = list0[j]
            list0[i] = p
            list0[j] = s
s1 = ''.join(list0)
list0.reverse()
print(s1 + ' ' + ''.join(list0))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410181429706.png)

思路：找出最大然后将字符串反向就是最小。如何找出最大就是一个位置一个位置的排，通过两两比对找出结果。

时间：165ms

### 2.学习总结与收获

最后一道题原来想也是补全后，是字典序和实际的顺序相同再直接sort，但语法能力有限没能实现。后来还是采用直接两两比较的方法，感觉更直观些。

感觉语法并没有熟悉到那么熟悉，还要再加强一下语法。