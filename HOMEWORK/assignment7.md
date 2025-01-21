## assignment7

### 1.题目

#### E07618: 病人排队

代码以及AC截图

源代码

```
n = int(input())
list0 = []
list1 = []
for i in range(1, n + 1):
    num, a = map(str, input().split())
    b = int(a)
    if b >= 60:
        list0.append((b, -i, num))
    else:
        list1.append(num)
list0.sort()
for j in range(len(list0)):
    print(list0[~j][2])
for j in range(len(list1)):
    print(list1[j])
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110941188.png)

运行时间：30ms

做题时间：7min

#### E23555: 节省存储的矩阵乘法

代码以及AC截图

源代码

```
list3 = []
for _ in range(m1):
    a, b, c = map(int, input().split())
    dict1[(a, b)] = c
for _ in range(m2):
    a, b, c = map(int, input().split())
    dict2[(a, b)] = c
for i in range(0, n):
    for j in range(0, n):
        s = 0
        for k in range(0, n):
            try:
                s += dict1[(i, k)] * dict2[(k, j)]
            except:
                s += 0
        if s != 0:
            list3.append((str(i), str(j), str(s)))
for m in list3:
    print(' '.join(m))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110944305.png)

运行时间：36ms

做题时间：15min

#### M18182: 打怪兽

代码以及AC截图

源代码

```
nCases = int(input())
for _ in range(nCases):
    n, m, b = map(int, input().split())
    list0 = []
    for __ in range(n):
        t, x = map(int, input().split())
        list0.append((t, -x))
    list0.sort()
    s = 0
    for i in range(n):
        if i == 0:
            s += 1
            if s > m:
                s = 0
                continue
            b += list0[i][1]
            if b <= 0:
                print(list0[i][0])
                break
        else:
             if list0[i][0] == list0[i - 1][0]:
                s += 1
                if s > m:
                    continue
             else:
                 s = 1
                 if s > m:
                     continue
             b += list0[i][1]
             if b <= 0:
                print(list0[i][0])
                break
    if b > 0:
        print('alive')
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110948041.png)

运行时间：80ms

做题时间：20min

#### M28780: 零钱兑换3

代码以及AC截图

源代码

```
n, m = map(int, input().split())
list0 = [int(x) for x in input().split()]
dp = [0] + [10000000] * 1000000
for i in range(1, m + 1):
    s = 10000000
    for j in range(n):
        s = min(s, dp[i - list0[j]])
    dp[i] = s + 1
if dp[m] >= 10000000:
    print(-1)
else:
    print(dp[m])
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110950519.png)

运行时间：12400ms

做题时间：15min

#### T12757: 阿尔法星人翻译官

代码以及AC截图

源代码

```
list0 = [str(x) for x in input().split()]
p = 0
if list0[0] == 'negative':
    p = -1
    del list0[0]
else:
    p = 1
dict1 = {"zero":0, "one":1, "two":2, "three":3, "four":4, "five":5, "six":6,
     "seven":7, "eight":8, "nine":9, "ten":10, "eleven":11, "twelve":12,
     "thirteen":13, "fourteen":14, "fifteen":15, "sixteen":16, "seventeen":17,
     "eighteen":18, "nineteen":19}
list2 = [(' ',0),("one",1),("two",2),("three",3),("four",4),("five",5),
             ("six",6),("seven",7),("eight",8),("nine",9)]
list3 = [("twenty",20),("thirty",30),("forty",40),("fifty",50),("sixty",60),
             ("seventy",70),("eighty",80),("ninety",90)]
for i in range(len(list3)):
    for j in range(len(list2)):
        word = list3[i][0] + ' ' + list2[j][0]
        num = list3[i][1] + list2[j][1]
        dict1[word.strip()] = num
def ten(list1, dict1):
    s = ' '.join(list1)
    return dict1[s]
def hundred(list1, dict1):
    if 'hundred' in list1:
        num0 = list1.index('hundred')
        if num0 != len(list1) - 1:
            list2 = list1[0: num0]
            list3 = list1[num0 + 1:]
            num1 = ten(list2, dict1)
            num2 = ten(list3, dict1)
            return num1 * 100 + num2
        else:
            list2 = list1[0: num0]
            return ten(list2, dict1) * 100
    else:
        return ten(list1, dict1)
def final(list1, dict1):
    if 'thousand' not in list1 and 'million' not in list1:
        return hundred(list1, dict1)
    elif 'thousand' in list1 and 'million' not in list1:
        num0 = list1.index('thousand')
        if num0 != len(list1) - 1:
            list2 = list1[0: num0]
            list3 = list1[num0 + 1:]
            num1 = hundred(list2, dict1)
            num2 = hundred(list3, dict1)
            return num1 * 1000 + num2
        else:
            list2 = list1[0: num0]
            return hundred(list2, dict1) * 1000
    elif 'thousand' not in list1 and 'million' in list1:
        num0 = list1.index('million')
        if num0 != len(list1) - 1:
            list2 = list1[0: num0]
            list3 = list1[num0 + 1:]
            num1 = hundred(list2, dict1)
            num2 = hundred(list3, dict1)
            return num1 * 1000000 + num2
        else:
            list2 = list1[0: num0]
            return hundred(list2, dict1) * 1000000
    elif 'thousand' in list1 and 'million' in list1:
        num1 = list1.index('million')
        num2 = list1.index('thousand')
        if num2 != len(list1) - 1:
            lista = list1[0: num1]
            listb = list1[num1 + 1: num2]
            listc = list1[num2 + 1:]
            num3 = hundred(lista, dict1)
            num4 = hundred(listb, dict1)
            num5 = hundred(listc, dict1)
            return num3 * 1000000 + num4 * 1000 + num5
        else:
            lista = list1[0: num1]
            listb = list1[num1 + 1: num2]
            num3 = hundred(lista, dict1)
            num4 = hundred(listb, dict1)
            return num3 * 1000000 + num4 * 1000


print(p * final(list0, dict1))
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110952239.png)

运行时间：25ms

做题时间：1h15min

#### T16528: 充实的寒假生活

代码以及AC截图

源代码

```
n = int(input())
list0 = []
for _ in range(n):
    a, b = map(int, input().split())
    list0.append((b, a))
list0.sort()
num0 = 1
front = list0[0][0]
for i in range(n):
    if list0[i][1] > front:
        num0 += 1
        front = list0[i][0]
print(num0)
```

AC截图

![](https://raw.githubusercontent.com/CPHO-Inventor/2024JG/main/image/202411110955229.png)

运行时间：33ms

做题时间：25min

### 2.学习总结与收获

经同学告知，作业里的时间是指做题时间不是运行时间（ ，这两周都是期中周，所以每日选做没有跟进，月考是自测的，感觉手感有点下降。期中之后还要多加练习。