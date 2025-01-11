# 1.题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A

思路：随时找1

```
for i in range(5):
    row = input().split()
    if "1" in row:
    	print(abs(i-2) + abs(row.index("1")-2))
```

代码运行截图：
![](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 152234.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A

思路：可以直接算

##### 代码

```
times = int(input())
for i in range(times):
    a, b = map(int,input().split())
    if a % b == 0:
        print("0")
    else:
        print( b * int(a/b + 1) - a)
```

代码运行截图![屏幕截图 2024-09-24 152720](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 152720.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A

思路：一个一个数，注意在flag小于零时犯人不叠加，表明时间的先后性

##### 代码

```
n = int(input())
list = input().split()
count = 0
flag = 0
for p in list:
    flag += int(p)
    if flag < 0:
        count += 1
        flag = 0
print(count)
```

代码运行截图![屏幕截图 2024-09-24 152720](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 152720.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/

思路：implementation

##### 代码

```
length,n = map(int,input().split())
list = [0 for i in range(length+1)]
for i in range(n):
    a,b = map(int,input().split())
    for i in range(a-1,b):
        list[i] = 1
print(list.count(0))
```

代码运行截图![屏幕截图 2024-09-24 154022](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 154022.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60

思路：inplementation

##### 代码

```
a , b = map(int,input().split())
daffodils_numbers = []
for i in range(a,b+1):
    if i == (i % 10)**3 + ((i//10) % 10)**3 + (i // 100)**3:
        daffodils_numbers.append(str(i))

if daffodils_numbers != []:
    print(" ".join(daffodils_numbers))
else:
    print("NO")
```

代码运行截图 

![屏幕截图 2024-09-24 155530](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 155530.png)



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/

思路：画图有助于理解条件：1.时间尽量短 2.到终点之前能赶上 ==》只有在0时后出发有效

##### 代码

```
while True:
    n = int(input())
    time_min = 10 ** 10
    if n == 0:
        break
    for i in range(n):
        v , t = map(float,input().split("\t"))
        if  t >= 0:
            time_min = min(time_min,t + (4.5/v) * 3600)
    print(int(time_min+1-10**(-9)))
```

代码运行截图![屏幕截图 2024-09-24 163917](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-24 163917.png)



## 2. 学习总结和收获

经过又一段时间的训练，感觉语法更加熟悉了，能够写出比之前更为优雅的代码，比如读入矩阵时成功用一行代码实现而不是狂套for循环。同时感到一些难题更加考验思维能力了，希望之后能更进一步，学到更多更好的计算机思维！