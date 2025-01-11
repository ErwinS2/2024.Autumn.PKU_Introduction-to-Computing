## 1. 题目



### LuoguP1255 数楼梯



dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：水

代码：

```
n = int(input())

dp = [1] + [2] + [0] * 5000
for i in range(1, n + 1):
    dp[i] = dp[i - 1] + dp[i - 2]

print(dp[n])

```



代码运行截图

![屏幕截图 2024-11-26 155524](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 155524.png)

### 27528: 跳台阶



dp, http://cs101.openjudge.cn/practice/27528/

思路：水，并且发现新维护一个前缀和甚至不如sum(list)快

代码：

```
n = int(input())

dp = [0] + [1] + [0] * 30
pre_sum = 1
for i in range(2, n + 1):
    dp[i] += pre_sum + 1
    pre_sum += dp[i]

print(dp[n])

```



代码运行截图![屏幕截图 2024-11-26 160127](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 160127.png)

### 474D. Flowers



dp, https://codeforces.com/problemset/problem/474/D

思路：感觉dp转移方程很难想到

代码：

```
# 成组放置问题
MOD = 1000000007

t, k = map(int, input().split())

dp = [0] * 100001
dp[0] = 1
pre_sum = [0] * 100001
for i in range(1, 100001):
    if i >= k:
        dp[i] = (dp[i - 1] + dp[i - k]) % MOD
    else:
        dp[i] = 1

    pre_sum[i] = (pre_sum[i - 1] + dp[i]) % MOD

for _ in range(t):
    a, b = map(int, input().split())
    print((pre_sum[b] - pre_sum[a - 1] + MOD) % MOD)

```



代码运行截图![屏幕截图 2024-11-26 175814](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 175814.png)

### LeetCode5.最长回文子串



dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：从每一个中心扩展到最大

代码：

```
class Solution:
    def expand(self, s, left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return left + 1, right - 1

    def len(self, s: str) -> str:
        start, end = 0, 0
        for i in range(len(s)):
            left1, right1 = self.expand(s, i, i)
            left2, right2 = self.expand(s, i, i + 1)
            if right1 - left1 > end - start:
                start, end = left1, right1
            if right2 - left2 > end - start:
                start, end = left2, right2
        return s[start: end + 1]

```



代码运行截图![屏幕截图 2024-11-26 171129](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 171129.png)

### 12029: 水淹七军



bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：没用sys库读入一直rte，最后照搬了答案

代码：

```
from collections import deque
import sys
input = sys.stdin.read

def is_valid(x, y, m, n):
    return 0 <= x < m and 0 <= y < n

def bfs(start_x, start_y, start_height, m, n, h, water_height):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    q = deque([(start_x, start_y, start_height)])
    water_height[start_x][start_y] = start_height

    while q:
        x, y, height = q.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            if is_valid(nx, ny, m, n) and h[nx][ny] < height:
                if water_height[nx][ny] < height:
                    water_height[nx][ny] = height
                    q.append((nx, ny, height))

def main():
    data = input().split()
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []

    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        h = []
        for i in range(m):
            h.append(list(map(int, data[idx:idx + n])))
            idx += n
        water_height = [[0] * n for _ in range(m)]

        i, j = map(int, data[idx:idx + 2])
        idx += 2
        i, j = i - 1, j - 1

        p = int(data[idx])
        idx += 1

        for _ in range(p):
            x, y = map(int, data[idx:idx + 2])
            idx += 2
            x, y = x - 1, y - 1
            if h[x][y] <= h[i][j]:
                continue
            bfs(x, y, h[x][y], m, n, h, water_height)

        results.append("Yes" if water_height[i][j] > 0 else "No")

    sys.stdout.write("\n".join(results) + "\n")

if __name__ == "__main__":
    main()
```



代码运行截图![屏幕截图 2024-11-26 175128](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 175128.png)

### 02802: 小游戏



bfs, http://cs101.openjudge.cn/practice/02802/

思路：开始想的是用一个方向跑到底的操作，但是容易与终点”擦肩而过“，然后没想到bfs在这里不能保证一定最短了，必须维护一个ans列表，最后取min

代码：

```
from collections import deque
def bfs(start, end, grid, h, w):
    queue = deque([start])
    visited = set()
    dirs = [(0, -1), (-1, 0), (0, 1), (1, 0)]

    ans = []
    while queue:
        x, y, d_i_r, seg = queue.popleft()
        if (x, y) == end:
            ans.append(seg)
            break

        for i, (dx, dy) in enumerate(dirs):
            nx, ny = x + dx, y + dy

            if 0 <= nx < h + 2 and 0 <= ny < w + 2 and ((nx, ny, i) not in visited):
                new_dir = i
                new_seg = seg if new_dir == d_i_r else seg + 1
                if (nx, ny) == end:
                    ans.append(new_seg)
                    continue

                if grid[nx][ny] != 'X':
                    visited.add((nx, ny, i))
                    queue.append((nx, ny, new_dir, new_seg))

    if len(ans) == 0:
        return -1
    else:
        return min(ans)
    
board_num = 1
while True:
    w, h = map(int, input().split())
    if w == h == 0:
        break

    grid = [' ' * (w + 2)] + [' ' + input() + ' ' for _ in range(h)] + [' ' * (w + 2)]
    print(f"Board #{board_num}:")
    pair_num = 1
    while True:
        y1, x1, y2, x2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0:
            break

        start = (x1, y1, -1, 0)
        end = (x2, y2)

        seg = bfs(start, end, grid, h, w)
        if seg == -1:
            print(f"Pair {pair_num}: impossible.")
        else:
            print(f"Pair {pair_num}: {seg} segments.")
        pair_num += 1

    print()
    board_num += 1
```



代码运行截图![屏幕截图 2024-11-26 212712](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-26 212712.png)

## 2. 学习总结和收获



这次作业对我来说挺难的，bfs，dfs如果不是模板题就很难一写到底，代码量太大了

每日选做落后了，尽量赶上