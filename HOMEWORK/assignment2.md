## assignment2

### 1.题目

#### 263A. Beautiful Matrix

代码以及AC截图

源代码

```
num = 0
for i in range(5):
    list0 = [int(x) for x in input().split()]
    if 1 in list0:
        num = abs(i - 2) + abs(list0.index(1) - 2)
print(num)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409251914653.png)

思路：直接标定1的位置，带入公式计算即可

时间：124ms

#### 1328A. Divisibility Problem

代码以及AC截图

源代码

```
t = int(input())
for i in range(t):
    list0 = [int(x) for x in input().split()]
    c = list0[0] % list0[1]
    if c != 0:
        print(list0[1] - c)
    else:
        print(0)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409251925785.png)

思路：通过取余数得出到最近倍数的距离，然后计算步长。

时间：109ms

#### 427A. Police Recruits

代码以及AC截图

源代码

```
n = int(input())
list0 = [int(x) for x in input().split()]
sum = 0
output_num  =0
for i in list0:
    sum += i
    if sum < 0:
        sum = 0
        output_num += 1
print(output_num)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409251948492.png)

思路：一直求和，直到出现负数，意味着警察不够用了，有未完成的任务。

时间：93ms

#### 02808: 校门外的树

代码以及AC截图

源代码

```
road_list = []
list0 = input().split()
l = int(list0[0])
m = int(list0[1])
n3 = 0
total = 0
while n3 <= l:
    road_list.append(0)
    n3 += 1
for x in range(1, m + 1):
    list1 = input().split()
    a1 = int(list1[0])
    a2 = int(list1[1])
    for num in range(a1, a2 + 1):
        road_list[num] = 1

for y in road_list:
    if y % 2 == 0:
        total += 1
print(total)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409251959581.png)

思路：创建一个列表，将覆盖的位置填入1，其他位置填入0，从而得出结果。

时间：51ms

#### sy60: 水仙花数II

代码以及AC截图

源代码

```
list0 = [int(x) for x in input().split()]
list1 = []
for i in range(list0[0], list0[1] + 1):
    n = str(i)
    if int(n) == int(n[0]) ** 3 + int(n[1]) ** 3 + int(n[2]) ** 3:
        list1.append(n)
if list1:
    print(' '.join(list1))
else:
    print('NO')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409252003317.png)

思路：直接拆分数字，计算验证结果。

时间：0ms ???

#### 01922: Ride to School

代码以及AC截图

源代码

```
while True:
    try:
        n = int(input())
        time_list = []
        for i in range(n):
            list0 = [int(x) for x in input().split()]
            if list0[1] < 0:
                continue
            else:
                if 4.5 * 3600 % list0[0] == 0:
                    t1 = float((4.5 * 3600) / list0[0])
                else:
                    t1 = float((4.5 * 3600) // list0[0] + 1)
                t2 = float(list0[1])
                time_list.append(t1 + t2)
        time_list.sort()
        print(int(time_list[0]))
    except:
        break
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202409252012703.png)

思路：考虑到这个人肯定跟着一个人到学校，而他总是跟着最快的，因此计算每个路人到达的时间（排除提前出发的，因为如果提前出发最快到达，永远不会遇上，如果中途遇见了，就说明提前出发的不是最快的）。然后对所有人的时间排序，得出到达时间。

时间：47ms

### 2.总结

感觉每日选做增加了难度，但还可以接受，目前在找一些算法题，来练习一下算法。

