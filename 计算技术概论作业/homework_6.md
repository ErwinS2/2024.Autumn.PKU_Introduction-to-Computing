## 1. 题目



### sy119: 汉诺塔



recursion, https://sunnywhy.com/sfbj/4/3/119

思路：看的答案，递归的时候搞三个变量轮换，就不用想ABC了

代码：

```
def Hanoi(n, from_rod, to_rod, mid_rod):
    if n == 0:
        return
    Hanoi(n - 1, from_rod, mid_rod, to_rod)
    print(f"{from_rod}->{to_rod}")
    Hanoi(n - 1, mid_rod, to_rod, from_rod)

n = int(input())
print(2**n - 1)
Hanoi(n, 'A', 'C', 'B')
```



代码运行截图![屏幕截图 2024-10-31 155204](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-31 155204.png)

### sy132: 全排列I



recursion, https://sunnywhy.com/sfbj/4/3/132

思路：还是看的答案，感觉回溯的想法很神奇，可以轻松搞出树状结构

代码：

```
def P(l, depth):
    if depth == n:
        ans.append(path[:])
        return
    for i, pos in enumerate(l):
        if not used[i]:
            used[i] = 1
            path.append(f"{pos}")
            P(l, depth + 1)
            path.pop()
            used[i] = 0

n = int(input())
l = list(range(1, n + 1))
used = [0 for i in range(n)]
depth = 0
ans, path = [], []
P(l, 0)
for i in ans:
    print(" ".join(i))
```



代码运行截图![屏幕截图 2024-10-31 155204](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-31 155204.png)

### 02945: 拦截导弹



dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：最长单调子序列

代码：

```
k = int(input())
l = [int(_) for _ in input().split()][::-1]
dp = [1] * k
for i in range(k):
    for j in range(i):
        if l[i] >= l[j]:
            dp[i] = max(dp[j] + 1, dp[i])

print(max(dp))
```



代码运行截图![屏幕截图 2024-10-31 162404](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-31 162404.png)

### 23421: 小偷背包



dp, http://cs101.openjudge.cn/practice/23421

思路：物品循环在外面，保证每件只买一次。递减遍历重量，避免购买多个

代码：

```
n, b = map(int, input().split())
prices = [int(_) for _ in input().split()]
weight = [int(_) for _ in input().split()]
dp = [0] * (b + 1)

for i in range(1, n):
    for j in range(b, weight[i] - 1, -1):
        dp[j] = max(dp[j], dp[j - weight[i]] + prices[i])

print(dp[b])
```



代码运行截图![屏幕截图 2024-10-31 162545](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-31 162545.png)

### 02754: 八皇后



dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：类似全排列，递归中带着used可以不用回溯used

代码：

```
l = [0,1,2,3,4,5,6,7]
def Eeight_QUENN(used, path):
    depth = len(path)
    if depth == 8:
        ans.append(path[:])
        return

    for i, pos in enumerate(l):
        if not used[depth][i]:
            used_ = [row[:] for row in used]

            for j in range(depth, 8):
                used_[j][i] = 1
                if 0 <= i + (j - depth) < 8:
                    used_[j][i + (j - depth)] = 1
                if 0 <= i - (j - depth) < 8:
                    used_[j][i - (j - depth)] = 1

            path.append(pos)
            Eeight_QUENN(used_, path)
            path.pop()

used = [[0 for _ in range(8)] for _ in range(8)]
ans = []
Eeight_QUENN(used, [])

n = int(input())
for _ in range(n):
    m = int(input())
    ans_ = [str(int(i) + 1) for i in ans[m - 1]]
    print("".join(ans_))
```



代码运行截图![屏幕截图 2024-10-31 162733](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-31 162733.png)

### 189A. Cut Ribbon



brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：实际上是三个物品，价值只有1的小偷背包

代码：

```
n, a, b, c = map(int, input().split())
dp = [0]+[float('-inf')]*5000
for i in range(1, n+1):
    dp[i] = max(dp[i - a], dp[i - b], dp[i - c]) + 1
print(dp[n])
```



代码运行截图

![屏幕截图 2024-11-01 122657](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-01 122657.png)

## 2. 学习总结和收获



本周线代期中考，每日选做勉强跟进，目前差两题

dp和度规经典题对我来说很阴间，应该是大脑还没被计算机思维雷普透彻导致的。递归的汉诺塔和全排列想了半天只能看答案。不过最后自己搞出八皇后感觉不错。dp的题很烧脑，目前还在模仿学习阶段。
