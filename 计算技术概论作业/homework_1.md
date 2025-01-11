# P1 题目

### 02733: 判断闰年

http://cs101.openjudge.cn/practice/02733/

思路：无

##### 代码

```
import calendar

year = int(input())

if calendar.isleap(year) == True:
    print("Y")
else:
    print("N")
```

代码运行截图 

![屏幕截图 2024-09-15 101434](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 101434.png)



### 02750: 鸡兔同笼

http://cs101.openjudge.cn/practice/02750/

思路：直接考虑极端情况

##### 代码

```
a = int(input())

if a % 2 == 0:
    print("{min_r} {max_r}".format( min_r =  (a+2)//4 , max_r = a//2 ))
else:
    print("0 0")
```

代码运行截图 

![屏幕截图 2024-09-15 102036](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 102036.png)



### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A

思路：一眼丁真

##### 代码

```
a,b=map(int,input().split())

print(str(a*b//2))
```

代码运行截图 

![屏幕截图 2024-09-15 102331](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 102331.png)



### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A

思路：先放能塞下的最多的，再补满

##### 代码

```
m,n,a=map(int,input().split())

sum=( m//a + int(m%a != 0) ) * ( n//a + int(n%a != 0) )
print(sum)
```

代码运行截图

![屏幕截图 2024-09-15 102445](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 102445.png)



### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A

思路：implementation

##### 代码

```
a=input().upper()
b=input().upper()

if a > b:
    print(1)
elif a < b:
    print(-1)
else:
    print(0)
```

代码运行截图

![屏幕截图 2024-09-15 102649](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 102649.png)



### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A

思路：implementation

##### 代码

```
n = int(input())
count = 0

for i in range(0,n):
    list = input().split()
    if list.count("1") >= 2:
        count +=1
 
print(count)
```

代码运行截图![屏幕截图 2024-09-15 102854](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-09-15 102854.png)



# P2 总结与感悟

经过这几道题和每日选做的跟进，初步掌握了python语法，掌握了几种简单的算法，可能培养了一点计算机思维