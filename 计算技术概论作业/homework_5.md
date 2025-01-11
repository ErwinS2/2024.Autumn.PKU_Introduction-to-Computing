## 1. 题目



### 04148: 生理周期



brute force, http://cs101.openjudge.cn/practice/04148

思路：Inplementation

代码：

```
time = 1
while True:
    b, c, d, a = map(int,input().split())
    
    if a == -1:
        break
    else:
        j = min(b, c, d)
        ini, dis = [b, c, d], [23, 28, 33]
        p = 0
        for i in range(3):
            if j == ini[i]:
                p = dis[i]
        while (j - b) % 23 != 0 or (j - c) % 28 != 0 or (j - d) % 33 != 0 or j <= a:
            j += p
            
        print(f'Case {str(time)}: the next triple peak occurs in {str(j-a)} days.')
        time += 1
```



代码运行截图![屏幕截图 2024-10-23 153152](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 153152.png)

### 18211: 军备竞赛



greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：排序，做最便宜的，卖最贵的，同时保证卖了一定能再做

代码：

```
p = int(input())
blueprints = [int(_) for _ in input().split()]
blueprints.sort()

self, enemy = 0, 0
l, r = 0, len(blueprints) - 1
while l <= r:
    if p >= blueprints[l]:
        p -= blueprints[l]
        self += 1
        l += 1
    else:
        if self > enemy and l < r:
            p += blueprints[r]
            enemy += 1
            r -= 1
        else:
            l += 1

print(self - enemy)
```



代码运行截图![屏幕截图 2024-10-23 153903](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 153903.png)

### 21554: 排队做实验



greedy, http://cs101.openjudge.cn/practice/21554

思路：水

代码：

```
n = int(input())
stu = sorted([[int(pos), i + 1] for i, pos in enumerate(input().split())])

t = 0
for i in range(n):
    t += stu[i][0] * (n - 1 - i)
t /= n

ans = [str(_[1]) for _ in stu]
print(' '.join(ans))
print(f'{t:.{2}f}')
```



代码运行截图 ![屏幕截图 2024-10-23 154345](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 154345.png)

### 01008: Maya Calendar



implementation, http://cs101.openjudge.cn/practice/01008/

思路：对我来说是易错题，想到了月份要减1取模，但是没想到年份WA了几次，然后没看清要求要print(n)又WA一次

代码：

```
Haab = ["pop", "no", "zip", "zotz", "tzec", "xul", "yoxkin", "mol", "chen", "yax", "zac", "ceh", "mac", "kankin", "muan", "pax", "koyab", "cumhu", "uayet"]
Tzolkin = ["imix", "ik", "akbal", "kan", "chicchan", "cimi", "manik", "lamat", "muluk", "ok", "chuen", "eb", "ben", "ix", "mem", "cib", "caban", "eznab", "canac", "ahau"]

n = int(input())
print(n)
for i in range(n):
    day, name_of_month, year = input().split()
    sum = int(year) * 365 + Haab.index(name_of_month) * 20 + int(day[:-1]) + 1

    year = str((sum - 1) // 260)
    name_of_day = Tzolkin[sum % 20 - 1]
    month = str((sum - 1) % 13 + 1)
    print(f"{month} {name_of_day} {year}")
```



代码运行截图![屏幕截图 2024-10-23 154744](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 154744.png)

### 545C. Woodcutters



dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：能砍就砍，往左倒优先，特殊情况不影响总棵数

代码：

```
n = int(input())
trees = [list(map(int, input().split())) for i in range(n)]

count = 1
for i in range(1, n - 1):
    if trees[i][1] < trees[i][0] - trees[i - 1][0]:
        count += 1
    elif trees[i][1] < trees[i + 1][0] - trees[i][0]:
        count += 1
        trees[i][0] += trees[i][1]
if n == 1:
    print(1)
else:
    print(count + 1)
```



代码运行截图 ![屏幕截图 2024-10-23 155040](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 155040.png)

### 01328: Radar Installation



greedy, http://cs101.openjudge.cn/practice/01328/

思路：考虑每个岛对应的能放的雷达的范围，然后对n个区间求最小覆盖，对右边界排序，从左向右逐个比较即可

代码：

```
t = 0
while True:
    t += 1
    n, d = map(int, input().split())
    if n == 0:
        break
    loc = [list(map(int, input().split())) for i in range(n)]
    input()

    radar_loc, flag = [], True
    for i in range(n):
        if loc[i][1] > d:
            print(f"Case {t}: {-1}")
            flag = False
            break
        radar_loc.append([loc[i][0] - (d ** 2 - loc[i][1] ** 2) ** 0.5, loc[i][0] + (d ** 2 - loc[i][1] ** 2) ** 0.5])

    radar_loc.sort(key= lambda x: x[1])
    if flag:
        count = 1
        for i in range(1, n):
            if radar_loc[i][0] > radar_loc[i - 1][1]:
                count += 1

        print(f"Case {t}: {count}")
```



代码运行截图![屏幕截图 2024-10-23 155546](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-23 155546.png)

## 2. 学习总结和收获



完成了每日选做至10.24的题目

这周每日选做狠狠上压力，有时候一题要卡两小时，Cipher写了半天实现模拟，结果超时了， Radar Installation是一开始没看清思路直接排序WA了很久。贪心题很难“一眼看到本质”，目前只能尽量搞一个最直接的算法再优化。

希望恶心的过程就是进步的过程。