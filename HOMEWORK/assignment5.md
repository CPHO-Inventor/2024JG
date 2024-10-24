## assignemnt5

### 1.题目

#### 04148:生理周期

代码以及AC截图

源代码

```
l = 1
while True:
    list0 = [int(x) for x in input().split()]
    if list0 == [-1, -1, -1, -1]:
        break
    else:
        d = list0[3]
        p = list0[0] % 23
        e = list0[1] % 28
        i = list0[2] % 33
        for j in range(d + 1, 21253 + d):
            p0 = j % 23
            e0 = j % 28
            i0 = j % 33
            if p0 == p and e0 == e and i0 == i:
                d0 = j - d
                print(f'Case {l}: the next triple peak occurs in {d0} days.')
                l += 1
                break
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241015786.png)

思路：从之后的每一天挨个枚举，利用取模，得出下一个时间。

时间：39ms

#### 18211: 军备竞赛

代码以及AC截图

源代码

```
p = int(input())
list0 = [int(x) for x in input().split()]
list0.sort()
n = 0
left0 = 0
right0 = len(list0) - 1
while left0 <= right0:
    if list0[left0] <= p:
        n += 1
        p -= list0[left0]
        left0 += 1
    else:
        if right0 == left0:
            break

        p += list0[right0]
        n -= 1
        if n < 0:
            n = 0
            break
        right0 -= 1
print(n)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241021825.png)

思路：先将数据排序，然后利用双指标，分别代表造成和出售，最后直到钱数不够支撑或者军火数比邻国少时停止。

时间：21ms

#### 21554: 排队做实验

代码以及AC截图

源代码

```
n = int(input())
list0 = [int(x) for x in input().split()]
list1 = list0.copy()
list2 = list0.copy()
list3 = []
list2.sort()
for i in range(len(list2)):
    num0 = list1.index(list2[i])
    list3.append(str(num0 + 1))
    list1[num0] = -1
print(' '.join(list3))
t = 0
for i in range(n - 1):
    s = n - 1 - i
    t += s * list2[i]
print("{:.2f}".format(t / n))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241049840.png)

思路：每次优先让时间最小的人先做实验，这样后面人的等待时间（为人数乘以实验学生所需时间）会相对小一些。
时间：22ms

#### 01008: Maya Calendar

代码以及AC截图

源代码

```
n = int(input())
print(n)
list0 = ['pop', 'no', 'zip', 'zotz', 'tzec', 'xul', 'yoxkin', 'mol', 'chen', 'yax',
     'zac', 'ceh', 'mac', 'kankin', 'muan', 'pax', 'koyab', 'cumhu', 'uayet']
list1 = ['imix', 'ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk',
     'ok', 'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban', 'eznab', 'canac', 'ahau']
list2 = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13']
dict0 = {}
for i in range(260):
    dict0[i] = list2[(i) % 13] + ' ' + list1[(i) % 20]
for _ in range(n):
    a, b, c = input().split()
    a = int(a[:-1])
    c = int(c)
    d = c * 365 + list0.index(b) * 20 + a
    print(dict0[d % 260] + ' ' + f'{d // 260}')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241056394.png)

思路：将第二种日历的每一天做成一个字典，然后计算天的总数，最后换到第二种日历。

时间：25ms

#### 545C. Woodcutters

代码以及AC截图

源代码

```
n = int(input())
list0 = []
for _ in range(n):
    list1 = [int(x) for x in input().split()]
    list0.append(list1)
list0.sort()
if n == 1:
    print(1)
else:
    num0 = 2
    for i in range(1, n - 1):
        if list0[i][0] - list0[i - 1][0] > list0[i][1]:
            num0 += 1
        elif list0[i + 1][0] - list0[i][0] > list0[i][1]:
            num0 += 1
            list0[i][0] += list0[i][1]
    print(num0)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241100090.png)

思路：先判断树可不可以砍到，再根据砍倒的方向来决定占用位置的改变。

时间：375ms

#### 01328: Radar Installation

代码以及AC截图

源代码

```
m = 0
while True:
    n, d = map(int, input().split())
    if n == d == 0:
        break
    else:
        m += 1
        list0 = []
        for i in range(n):
            x, y = map(int, input().split())
            if d >= y:
                x1 = x - (d ** 2 - y ** 2) ** 0.5
                x2 = x + (d ** 2 - y ** 2) ** 0.5
                list0.append([x1, x2])
        input()
        if len(list0) < n:
            print(f"Case {m}: -1")
        elif d < 0:
            print(f"Case {m}: -1")
        else:
            list0.sort(reverse = True)
            n0 = len(list0)
            min0 = list0[0][0]
            for j in range(1, len(list0)):
                if list0[j][1] < min0:
                    min0 = list0[j][0]
                else:
                    n0 -= 1
            print(f"Case {m}: {n0} " )
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410241110702.png)

思路：将小岛的二维数据改变为一维数据，从而从后往前直接排序（直接分析）

时间：59ms

### 2.学习收获与总结

感觉作业题目和选做开始难了起来，每天每日选做要做一个多小时，可能期中那周就先停一下。最近感觉自己debug能力有待提升。
