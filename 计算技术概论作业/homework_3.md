## 1. 题目



### E28674:《黑神话：悟空》之加密



http://cs101.openjudge.cn/practice/28674/

思路：水

代码

```
k = int(input())
upper = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
lower = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']

s = input()
s_out = ""
for i in range(len(s)):
    if s[i] in upper:
        s_out += upper[(upper.index(s[i]) - k) % 26]
    else:
        s_out += lower[(lower.index(s[i]) - k) % 26]

print(s_out)
```



代码运行截图 ==（至少包含有"Accepted"）![屏幕截图 2024-10-10 181100](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 181100.png)==

### E28691: 字符串中的整数求和



http://cs101.openjudge.cn/practice/28691/

思路：水

代码

```
a, b = input().split()
print(int(a[:2]) + int(b[:2]))
```



代码运行截图 ==（至少包含有"Accepted"）==![屏幕截图 2024-10-10 181132](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 181132.png)

### M28664: 验证身份证号



http://cs101.openjudge.cn/practice/28664/

思路：implementation

代码

```
xishu_list = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
mowei_list = [1,0,"X",9,8,7,6,5,4,3,2]

n = int(input())
for i in range(n):
    s = input()
    count = 0

    for i in range(17):
        count += xishu_list[i] * int(s[i])

    count = count % 11

    if str(mowei_list[count]) == s[-1]:
        print("YES")
    else:
        print("NO")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）![屏幕截图 2024-10-10 181203](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 181203.png)==

### M28678: 角谷猜想



http://cs101.openjudge.cn/practice/28678/

思路：implementation

代码

```
n = int(input())

while n != 1:
    if n % 2 == 0:
        print("{a}/2={b}".format(a=n,b=n//2))
        n = n//2
    else:
        print("{a}*3+1={b}".format(a=n,b=3*n + 1))
        n = 3 * n + 1

print("End")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）![屏幕截图 2024-10-10 181226](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 181226.png)==

### M28700: 罗马数字与整数的转换



http://cs101.openjudge.cn/practice/28700/

思路：只会暴力，字母转数字：先全相加，再减去两倍的多加的

##### 代码



```
# t = ["0","1","2","3","4","5","6","7","8","9"]
s = input()

output_romen = ""
output_int = 0
if s[0] in t:
    s = int(s)
    output_romen += "M" * (s // 1000)
    s = s % 1000
    if s // 100 == 4:
        output_romen += "CD"
    elif s // 100 == 9:
        output_romen += 'CM'
    else:
        output_romen += "D" * (s // 500)
        s = s % 500
        output_romen += "C" * (s // 100)
    s = s % 100
    if s // 10 == 4:
        output_romen += "XL"
    elif s // 10 == 9:
        output_romen += 'XC'
    else:
        output_romen += "L" * (s // 50)
        s = s % 50
        output_romen += "X" * (s // 10)
    s = s % 10
    if s == 4:
        output_romen += "IV"
    elif s == 9:
        output_romen += 'IX'
    else:
        output_romen += "V" * (s // 5)
        s = s % 5
        output_romen += "I" * s

    print(output_romen)
else:
    s += "I"
    for i in range(len(s) - 1):
        if s[i] == "M":
            output_int += 1000
        if s[i] == "D":
            output_int += 500
        if s[i] == "C":
            output_int += 100
            if s[i + 1] == "D" or s[i + 1] == "M":
                output_int -= 200
        if s[i] == "L":
            output_int += 50
        if s[i] == "X":
            output_int += 10
            if s[i + 1] == "C" or s[i + 1] == "L":
                output_int -= 20
        if s[i] == "V":
            output_int += 5
        if s[i] == "I":
            output_int += 1
            if s[i + 1] == "X" or s[i + 1] == "V":
                output_int -= 2

    print(output_int)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）![屏幕截图 2024-10-10 181418](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 181418.png)==

### *T25353: 排队 （选做）



http://cs101.openjudge.cn/practice/25353/

思路：把所有自由的点移动到最前面排序，剩下的递归

​		注意判断方法：统计前$i$个的最大最小值

代码

```
n, d = map(int,input().split())
height = [int(input()) for _ in range(n)]

def restricted_sort(a):
    if len(a) <= 1:
        return a

    movable, rest = [a[0]], []
    maxh, minh = a[0], a[0]
    for i in a[1:]:
        maxh = max(i, maxh)
        minh = min(i, minh)
        if maxh-i <= d and i-minh <= d:
            movable.append(i)
        else:
            rest.append(i)

    movable.sort()
    return movable + restricted_sort(rest)

print("\n".join(list(map(str,restricted_sort(height)))))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）![屏幕截图 2024-10-10 223437](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-10 223437.png)==

## 2. 学习总结和收获

排序这题我想了大概有四小时，最后得出了一个TLE，十分痛苦的选择了看答案，最后答案的单刀直入让我大吃一惊。感觉自己编程能力的沉淀不足，事实上从最基础的排序算法入手可以很快把握这道题的核心，然后线性储存最大最小值的办法应该也是很常见的，没有想到确实不因该。

这道题的特点是在挑选自由点的时候非常挑剔，只有“完全自由”——即是平移到最前面之后还可以互相换顺序的点才会被选择，然后很精妙的利用排序保证了不会出现无效操作，神！

希望通过学习能更进一步！