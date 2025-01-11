## 1. 题目



### 12558: 岛屿周⻓



matices, http://cs101.openjudge.cn/practice/12558/

思路：遍历加4，加多了就减2

代码：

```
n, m = map(int, input().split())
map_ = [list(map(int, input().split())) for i in range(n)]

perimeter = 0
for i in range(n):
    for j in range(m):
        if map_[i][j] == 1:
            perimeter += 4
            if i > 0 and map_[i - 1][j] == 1:
                perimeter -= 2
            if j > 0 and map_[i][j - 1] == 1:
                perimeter -= 2

print(perimeter)
```



代码运行截图![屏幕截图 2024-11-13 144836](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-13 144836.png)

### LeetCode54.螺旋矩阵



matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：四种情况，直接implementation，边界条件处理需注意

代码：

```
n = int(input())
m = [[0 for _ in range(n + 1)] for _ in range(n + 1)]

flag = 0
state = 0
step = [[0, 1],[1, 0],[0, -1],[-1, 0]]
row, col = 0, 0

while flag < n * n:
    flag += 1
    m[row][col] = str(flag)
    if (m[row + step[state][0]][col + step[state][1]] != 0
        or not(0 <= row + step[state][0] < n and 0 <= col + step[state][1] < n)):
        state = (state + 1) % 4
    row += step[state][0]
    col += step[state][1]

for i in range(n):
    print(' '.join(m[i][:-1]))
```



代码运行截图![屏幕截图 2024-11-13 151536](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-13 151536.png)

### 04133:垃圾炸弹



matrices, http://cs101.openjudge.cn/practice/04133/

思路：

代码：

```
m = [[0 for i in range(1025)] for j in range(1025)]
d = int(input())
n = int(input())
max_ = 0
for _ in range(n):
    x, y, q = map(int, input().split())
    for i in range(max(x - d, 0), min(x + d + 1, 1025)):
        for j in range(max(y - d, 0), min(y + d + 1, 1025)):
            m[i][j] += q
            max_ = max(max_, m[i][j])

count = 0
for i in range(1025):
    count += m[i].count(max_)

print(count, max_)
```



代码运行截图![屏幕截图 2024-11-13 151900](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-13 151900.png)

### LeetCode376.摆动序列



greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：注意特殊情况，全同时为1

代码：

```
n = int(input())
nums = [int(_) for _ in input().split()]
delta = []
for i in range(n - 1):
    if nums[i + 1] > nums[i]:
        delta.append(1)
    if nums[i + 1] < nums[i]:
        delta.append(-1)
if len(delta) == 0:
    print(1)
else:
    len_ = 2
    for i in range(len(delta) - 1):
        if delta[i + 1] != delta[i]:
            len_ += 1
    print(len_)
```



代码运行截图![屏幕截图 2024-11-13 153552](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-13 153552.png)

### CF455A: Boredom



dp, 1500, https://codeforces.com/contest/455/problem/A

思路：感觉状态转移方程较难想到，最后结果很简洁

代码：

```
import collections
 
n = int(input())
numbers = [int(_) for _ in input().split()]
count = collections.Counter(numbers)
len = max(numbers) + 1
l = [0] * len
dp = [0] * len
for i in range(len):
    if i in count:
        l[i] = i * count[i]
 
for i in range(1, len):
    dp[i] = max(dp[i - 1], dp[i - 2] + l[i])
 
print(dp[len - 1])
```



代码运行截图![屏幕截图 2024-11-13 153926](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-13 153926.png)

### 02287: Tian Ji -- The Horse Racing



greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：

代码：

```
while True:
    n = int(input())
    if n == 0:
        break

    t = list(map(int, input().split()))
    k = list(map(int, input().split()))
    
    t.sort()
    k.sort()
    
    lt, rt = 0, n - 1
    lk, rk = 0, n - 1
    ans = 0
    
    while lt <= rt:
        if t[lt] > k[lk]:
            ans += 1
            lt += 1
            lk += 1
        elif t[rt] > k[rk]:
            ans += 1
            rt -= 1
            rk -= 1
        else:
            if t[lt] < k[rk]:
                ans -= 1
            lt += 1
            rk -= 1
    
    print(ans * 200)
```



代码运行截图![屏幕截图 2024-11-14 124931](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-14 124931.png)

## 2. 学习总结和收获



每日选做出现了好多新模型，感觉不看答案很难想到，比如count lake

本次作业田忌赛马是很复杂的贪心，在平局的点上卡了很久，最后看了答案
