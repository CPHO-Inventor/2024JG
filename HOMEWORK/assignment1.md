## assignment1

### 02733:判断闰年

代码以及AC截图

```
a = int(input())
combat = False
if a % 4 == 0:
    combat = True
    if a % 3200 == 0:
        combat = False
    elif a % 100 == 0 and a % 400 != 0:
        combat = False

if combat:
    print("Y")
else:
    print('N')
```

![](C:\Users\18963\Desktop\84c9af72403d0a3ed644457609aa1fb.png

![](C:\Users\18963\Desktop\798820ca316d1141c4ab4b81bc7c23a.png)

思路：分别用if语句列出每个条件即可

时间：24ms



 ### 02750:鸡兔同笼

代码以及AC截图

```
a = int(input())
if a < 32768:
    if a % 2 != 0:
        print('0 0')
    else:
        min_num = a // 4 + (a % 4) // 2
        max_num = a // 2
        print(f'{min_num} {max_num}')
```



![](C:\Users\18963\Desktop\347144b05114a63849685121db79fec.png)

思路：直接计算出最大最小

时间：20ms



### CF50A:Domino piling

代码以及AC截图

```
list0 = [int(x) for x in input().split()]
print((list0[0] * list0[1]) // 2)
```



![](C:\Users\18963\Desktop\2555c21c0d8feb00d1d70edad361647.png)

思路：直接取整

时间：156ms



### CF1A:Theatre Square

代码以及AC截图

```
list0 = [int(x) for x in input().split()]
n = list0[0]
m = list0[1]
a = list0[2]
if n % a == 0:
    num1 = n // a
else:
    num1 = (n // a) + 1
if m % a == 0:
    num2 = m // a
else:
    num2 = (m // a) + 1
print(num1 * num2)
```



![](C:\Users\18963\Desktop\a4a34fecaea8da2b7d0a410a50e2a75.png)

思路：分别计算两边的块数，然后相乘

时间：77ms



### CF112A:Petya and Strings

代码以及AC截图

```
str1 = input().lower()
str2 = input().lower()
if len(str1) == len(str2):
    if str1 > str2:
        print(1)
    elif str1 < str2:
        print(-1)
    else:
        print(0)
```



![](C:\Users\18963\Desktop\6296c9c510c47976b0490a52176cd53.png)

思路：写出全部大写与全部小写的字符串，然后遍历并判断

时间：186ms



### CF231A：Team

代码以及AC截图

```
n = int(input())
num = 0
for i in range(n):
    list0 = [int(x) for x in input().split()]
    sum = 0
    for j in list0:
        sum += j
    if sum >= 2:
        num += 1
print(num)
```



![](C:\Users\18963\Desktop\ba0579b0e5e657b5a0e3cfed4444e31.png)

思路：对每一列求和计算，如果大于等于二则成功，总数加一

时间：124ms



### summary

题目很简单，目前每天跟进每日选做，并且额外在CS上做了12道题

