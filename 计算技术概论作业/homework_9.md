## 1. 题目



### 18160: 最大连通域面积



dfs similar, http://cs101.openjudge.cn/practice/18160

思路：跟Lake Counting类似，典型dfs

代码：

```
directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]

def dfs(i, j, m):
    stack = [(i, j)]
    count = 0
    while stack:
        i_, j_ = stack.pop()
        m[i_][j_] = '.'
        count += 1
        for d, r in directions:
            if m[i_ + d][j_ + r] == 'W':
                m[i_ + d][j_ + r] = '.'
                stack.append((i_ + d, j_ + r))
    return count

t = int(input())
for _ in range(t):
    n, l = map(int, input().split())
    m = [["."] + list(input()) + ["."] for _ in range(n)]
    m.insert(0, ["." for i in range(l + 2)])
    m.append(["." for i in range(l + 2)])

    max_ = 0
    for i in range(1, n + 1):
        for j in range(1, l + 1):
            if m[i][j] == 'W':
                max_ = max(max_, dfs(i, j, m))

    print(max_)
```



代码运行截图![屏幕截图 2024-11-20 104416](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 104416.png)

### 19930: 寻宝



bfs, http://cs101.openjudge.cn/practice/19930

思路：看的AI，bfs用deque实现，先进先出，保证了路径最短

代码：

```
from collections import deque
def can_reach_treasure(m, n, grid):
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    start = (0, 0)
    visited = [[False] * n for _ in range(m)]
    queue = deque([(start, 0)])  # (位置, 步数)
    visited[0][0] = True

    while queue:
        (x, y), steps = queue.popleft()
        if grid[x][y] == 1:
            return steps

        for dx, dy in directions:
            nx, ny = x + dx, y + dy

            if 0 <= nx < m and 0 <= ny < n and not visited[nx][ny] and grid[nx][ny] != 2:
                visited[nx][ny] = True
                queue.append(((nx, ny), steps + 1))

    return "NO"

m, n = map(int, input().split())
grid = [list(map(int, input().split())) for _ in range(m)]

print(can_reach_treasure(m, n, grid))
```



代码运行截图![屏幕截图 2024-11-20 111722](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 111722.png)

### 04123: 马走日



dfs, http://cs101.openjudge.cn/practice/04123

思路：又见回溯算法，考虑答案计数的时候本来写的走完一次，ans += 1，因为全局变量用的不明白编译错误很久，最后问了AI把答案封装在递归里就行了

​	另外不知道这题能不能用栈实现？

代码：

```
def dfs(x, y, n, m, count, visited):
    if count == n * m:
        return 1

    directions = [(1, 2), (1, -2), (-1, 2), (-1, -2), (2, 1), (2, -1), (-2, 1), (-2, -1)]
    total_paths = 0

    for l, r in directions:
        nx, ny = x + l, y + r
        if 0 <= nx < n and 0 <= ny < m and not visited[nx][ny]:
            visited[nx][ny] = True
            total_paths += dfs(nx, ny, n, m, count + 1, visited)
            visited[nx][ny] = False

    return total_paths


t = int(input())
for _ in range(t):
    n, m, x, y = map(int, input().split())
    visited = [[False for _ in range(m)] for _ in range(n)]
    visited[x][y] = True
    result = dfs(x, y, n, m, 1, visited)
    print(result)
```



代码运行截图![屏幕截图 2024-11-20 122659](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 122659.png)

### sy316: 矩阵最大权值路径



dfs, https://sunnywhy.com/sfbj/8/1/316

思路：典型dfs，回溯

代码：

```
def dfs(x, y, sum_, path, visited):
    global max_, ans
    if x == n - 1 and y == m - 1:
        if sum_ > max_:
            max_ = sum_
            ans = path[:]
        return

    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

    for l, r in directions:
        nx, ny = x + l, y + r
        if 0 <= nx < n and 0 <= ny < m and not visited[nx][ny]:
            visited[nx][ny] = True
            path.append(f"{nx + 1} {ny + 1}")
            dfs(nx, ny, sum_ + matrix[nx][ny], path, visited)
            path.pop()
            visited[nx][ny] = False

n, m = map(int, input().split())
matrix = [list(map(int, input().split())) for i in range(n)]
visited = [[False for _ in range(m)] for _ in range(n)]
visited[0][0] = True

ans = []
max_ = float("-inf")
dfs(0, 0, matrix[0][0], ["1 1"], visited)
print("\n".join(ans))
```



代码运行截图![屏幕截图 2024-11-20 161508](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 161508.png)

### LeetCode62.不同路径



dp, https://leetcode.cn/problems/unique-paths/

思路：简单dp，可以直接用组合数学公式

代码：

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        return dp[m - 1][n - 1]
```



代码运行截图![屏幕截图 2024-11-20 104613](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 104613.png)

### sy358: 受到祝福的平方



dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：递归

代码：

```
from math import sqrt
def is_square(n):
    return sqrt(n) % 1 == 0 and n > 0
def cut(s):
    if len(s) == 0:
        return True
    for i in range(1, len(s) + 1):
        if not is_square(int(s[:i])):
            continue
        if cut(s[i:]) == True:
            return True
    return False

if cut(input()):
    print("Yes")
else:
    print("No")


```



代码运行截图![屏幕截图 2024-11-20 182655](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-20 182655.png)

## 2. 学习总结和收获



每日选做有跟进

这次的题目以dfs，bfs模板题为主，另外从中复习了递归，回溯。从寻宝学会了bfs，通过dfs，bfs两种算法的对比学到了很多。