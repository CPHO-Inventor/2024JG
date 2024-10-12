## assignment3

### 1.题目

#### E28674:《黑神话：悟空》之加密

代码以及AC截图

源代码

```
k = int(input())
s = input()
str0 = 'abcdefghijklmnopqrstuvwxyz'
str1 = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
str2 = ''
for i in s:
    if i in str0:
        n = str0.index(i)
        m = (n + 130000 - k) % 26
        str2 += str0[m]
    else:
        n = str1.index(i)
        m = (n + 130000 - k) % 26
        str2 += str1[m]
print(str2)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122145331.png)

思路： 通过取余数来来使得每个字符对应的数字固定，便于计算。

时间：19ms

#### E28691: 字符串中的整数求和

代码以及AC截图

源代码

```
list0 = [x for x in input().split()]
a = int(list0[0][0:2])
b = int(list0[1][0:2])
print(a + b)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122201511.png)

思路：直接找出数字计算

时间：20ms

#### M28664: 验证身份证号

代码以及AC截图

源代码

```
list0 = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
list1 = ['1','0','X','9','8','7','6','5','4','3','2']
n = int(input())
for _ in range(n):
    s = input()
    sum0 = 0
    for i in range(17):
        sum0 += int(s[i]) * list0[i]
    sum1 = sum0 % 11
    if str(list1[sum1]) == s[17]:
        print('YES')
    else:
        print('NO')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122206102.png)

思路：将身份证号对应的数字以及计算结果对应的数字列成列表，计算后与其对应即可。

时间：19ms

#### M28678:角谷猜想

代码以及AC截图

源代码

```
n = int(input())
while n != 1:
    if n % 2 == 0:
        s = n
        n = int(n / 2)
        print(f'{s}/2={n}')
    else:
        s = n
        n = 3 * n + 1
        print(f'{s}*3+1={n}')
print('End')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122219235.png)

思路：按照题目要求一步一步写出过程。

时间：21ms

#### M28700:罗马数字与整数的转换

代码以及AC截图

源代码

```
s = input()
try:
    s0 = int(s)
    s1 = ''
    list1 = ['','I','II','III','IV','V','VI','VII','VIII','IX']
    list2 = ['', 'X', 'XX', 'XXX', 'XL', 'L', 'LX', 'LXX', 'LXXX', 'XC']
    list3 = ['','C','CC','CCC','CD','D','DC','DCC','DCCC','CM']
    list4 = ['','M', 'MM', 'MMM']
    s1 += list1[int(s[-1])]
    try:
        s1 = list2[int(s[-2])] + s1
    except:
        s1 += list2[0]
    try:
        s1 = list3[int(s[-3])] + s1
    except:
        s1 += list3[0]
    try:
        s1 = list4[int(s[-4])] + s1
    except:
        s1 += list4[0]
    print(s1)
except:
    n1 = s.count('I')
    n2 = s.count('V')
    n3 = s.count('X')
    n4 = s.count('L')
    n5 = s.count('C')
    n6 = s.count('D')
    n7 = s.count('M')
    sum0 = n1 + 5 * n2 + 10 * n3 + 50 * n4 + 100 * n5 + 500 * n6 + 1000 * n7
    for i in range(len(s) - 1, 0, -1):
        if s[i] == 'V':
            if s[i - 1] == 'I':
                sum0 -= 2
        if s[i] == 'X':
            if s[i - 1] == 'I':
                sum0 -= 2
        if s[i] == 'L':
            if s[i - 1] == 'X':
                sum0 -= 20
        if s[i] == 'C':
            if s[i - 1] == 'X':
                sum0 -= 20
        if s[i] == 'D':
            if s[i - 1] == 'C':
                sum0 -= 200
        if s[i] == 'M':
            if s[i - 1] == 'C':
                sum0 -= 200
    print(sum0)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122222966.png)

思路：罗马数字变到阿拉伯数字则直接先计算总体，再讨论含4，9的情况。反过来则利用列表每一位数字单独计算。

时间：20ms

#### T25353: 排队 （选做）

代码以及AC截图

源代码

```
N, D = map(int, input().split())
list0 = []
for _ in range(N):
    n = int(input())
    list0.append(n)
list1 = [0] * N
while 0 in list1:
    list2 = []
    min0 = 0
    max0 = 0
    for i in range(N):
        if list1[i]:
            continue
        if not list2:
            min0 = list0[i]
            max0 = list0[i]
        else:
            if list0[i] > max0:
                max0 = list0[i]
            if list0[i] < min0:
                min0 = list0[i]
        if max0 - min0 > 2 * D:
            break
        if list0[i] + D >= max0 and list0[i] - D <= min0:
            list2.append(list0[i])
            list1[i] = 1
    list2.sort()
    for i in list2:
        print(i)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202410122228725.png)

思路：先遍历，看哪个元素可以放到最前面，然后将这些可以放到最前面的元素排列。这样的字典数一定是最小的。

时间：336ms

### 2.学习收获与总结

月考的时候，一个小时左右AC5（第五题想快点做完，就用一堆if写了一坨），感觉这次差不多稳了，然后碰到了排序这个题（   。但当时主要是没理解题目是什么意思，把字典序理解为开始的时候每个数字在列表中对应的序号。最后也是没做出来，但看完答案就基本明白了。

最近还在做OJ上题库里的题，感觉颇有收获。

