## 1. 题目



### E22548: 机智的股民老张



http://cs101.openjudge.cn/practice/22548/

思路：维护前缀最小值

代码：

```
a = list(map(int, input().split()))

min, max_ans = float("inf"), 0
for price in a:
    if price < min:
        min = price
    else:
        max_ans = max(max_ans, price - min)

print(max_ans)
```



代码运行截图 ![屏幕截图 2024-12-05 172232](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-12-05 172232.png)

### M28701: 炸鸡排



greedy, http://cs101.openjudge.cn/practice/28701/

思路：审题易错，贪心难想

代码：

```
n, k = map(int, input().split())
times = list(map(int, input().split()))
times.sort()

pre_sum = [0 for i in range(n)]
for i in range(n):
    pre_sum[i] = pre_sum[i - 1] + times[i]

cut = 0
while pre_sum[n - 1 - cut] / (k - cut) < times[n - 1 - cut]:
    cut += 1

ans = pre_sum[n - 1 - cut] / (k - cut)
print("{:.3f}".format(ans))
```



代码运行截图 ![屏幕截图 2024-12-06 120251](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-12-06 120251.png)

### M20744: 土豪购物



dp, http://cs101.openjudge.cn/practice/20744/

思路：dp[i]为终止在i位置的最大连续列表和，dp_rev就是方向反一下，最后对price枚举，正负分别讨论

代码：

```
prices = [int(_) for _ in input().split(",")]
prices_rev = prices[::-1]

len_ = len(prices)

dp, dp_rev = [0 for _ in range(len_)], [0 for _ in range(len_)]
dp[0], dp_rev[0] = prices[0], prices_rev[0]
for i in range(len_ - 1):
    dp[i + 1] = dp[i] + prices[i + 1] if dp[i] >= 0 else prices[i + 1]
    dp_rev[i + 1] = dp_rev[i] + prices_rev[i + 1] if dp_rev[i] >= 0 else prices_rev[i + 1]
dp_rev.reverse()

ans = prices[0]
for i in range(1, len_ - 1):
    if prices[i] >= 0:
        ans = max(ans, dp[i] + dp_rev[i + 1])
    else:
        ans = max(ans, dp[i - 1] + dp_rev[i + 1])

print(ans)
```



代码运行截图![屏幕截图 2024-12-05 221348](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-12-05 221348.png)

### T25561: 2022决战双十一



brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：繁琐的枚举，如果没看到tag绝对会往greedy上想

代码：

```
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
coupons = [input().split() for _ in range(m)]

def dfs(store_prices, coupons, items=0, total_price=0, each_store_price=[0] * m):
    global result
    if items == n:
        coupon_price = 0
        for i in range(m):
            store_p = 0
            for coupon in coupons[i]:
                a, b = map(int, coupon.split('-'))
                if each_store_price[i] >= a:
                    store_p = max(store_p, b)

            coupon_price += store_p

        result = min(result, total_price - (total_price // 300) * 50 - coupon_price)
        return

    for i in store_prices[items]:
        idx, p = map(int, i.split(':'))
        each_store_price[idx - 1] += p
        dfs(store_prices, coupons, items + 1, total_price + p, each_store_price)
        each_store_price[idx - 1] -= p

dfs(store_prices, coupons)
print(result)
```



代码运行截图![屏幕截图 2024-12-06 154310](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-12-06 154310.png)

### T20741: 两座孤岛最短距离



dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：dfs+bfs 简直是体力活

代码：

```
from collections import deque
def dfs(x, y, grid, n, queue, directions):
    grid[x][y] = 2  # Mark as visited
    queue.append((x, y))
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < n and grid[nx][ny] == 1:
            dfs(nx, ny, grid, n, queue, directions)
def bfs(grid, n, queue, directions):
    distance = 0
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    if grid[nx][ny] == 1:
                        return distance
                    elif grid[nx][ny] == 0:
                        grid[nx][ny] = 2  # Mark as visited
                        queue.append((nx, ny))
        distance += 1

n = int(input())
grid = [list(map(int, input())) for _ in range(n)]
directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
queue = deque()

for i in range(n):
    for j in range(n):
        if grid[i][j] == 1:
            dfs(i, j, grid, n, queue, directions)
            print(bfs(grid, n, queue, directions))

```



代码运行截图![屏幕截图 2024-12-06 154307](C:\Users\31507\OneDrive\图片\屏幕快照\屏幕截图 2024-12-06 154307.png)



### T28776: 国王游戏



greedy, http://cs101.openjudge.cn/practice/28776

思路：初见杀贪心，拼尽全力无法战胜（）。直接考虑交换的影响，写出排序的key

代码：

```
n = int(input())
a, b = map(int, input().split())
ministers = [list(map(int, input().split())) for _ in range(n)]
ministers.sort(key = lambda x: (x[0] * x[1]))

ans = 0
for i in range(n):
    ans = max(ans, a // ministers[i][1])
    a *= ministers[i][0]

print(ans)
```



代码运行截图![屏幕截图 2024-12-06 161144](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-12-06 161144.png)

## 2. 学习总结和收获



每日选做跟进至今日

前一天没睡好，果断放弃考试。感觉自己上考场是AC2~3的水平。

贪心题难起来深不见底。dfs，bfs代码巨长，必须多加锻炼。