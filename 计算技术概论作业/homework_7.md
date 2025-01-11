## 1. 题目



### E07618: 病人排队



sorttings, http://cs101.openjudge.cn/practice/07618/

思路：水

代码：

```
n = int(input())
p_ = [input().split() for _ in range(n)]
old = []
young = []

for i, p in enumerate(p_):
    if int(p[1]) >= 60:
        old.append(p + [i])
    else:
        young.append(p[0])

old.sort(key=lambda x:(-int(x[1]), x[2]))
for p in old:
    print(p[0])
for p in young:
    print(p)
```



代码运行截图![屏幕截图 2024-11-07 171711](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 171711.png)

### E23555: 节省存储的矩阵乘法



implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：水

代码：

```
n, n_m1, n_m2 = map(int, input().split())
m1 = [list(map(int, input().split())) for _ in range(n_m1)]
m2 = [list(map(int, input().split())) for _ in range(n_m2)]
m_1 = [[0 for i in range(n)] for i in range(n)]
m_2 = [[0 for i in range(n)] for i in range(n)]
for p in m1:
    m_1[p[0]][p[1]] = p[2]
for p in m2:
    m_2[p[0]][p[1]] = p[2]

for row in range(n):
    for col in range(n):
        sum = 0
        for i in range(n):
            sum += m_1[row][i] * m_2[i][col]

        if sum:
            print(f"{row} {col} {sum}")
```



代码运行截图![屏幕截图 2024-11-07 171756](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 171756.png)

### M18182: 打怪兽



implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：贪

代码：

```
n_cases = int(input())
for _ in range(n_cases):
    n, m, b = map(int, input().split())
    skills = [list(map(int, input().split())) for _ in range(n)]
    skills.sort(key=lambda x:(x[0], -x[1]))

    flag = "嘻嘻"
    alive = True
    for s in skills:
        if s[0] != flag:
            flag = s[0]
            t = 1
        if t <= m:
            b -= s[1]
            t += 1
        if b <= 0:
            alive = False
            break

    if alive:
        print("alive")
    else:
        print(flag)
```



代码运行截图![屏幕截图 2024-11-07 171840](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 171840.png)

### M28780: 零钱兑换3



dp, http://cs101.openjudge.cn/practice/28780/

思路：典型dp

代码：

```
n, m = map(int, input().split())
coins = [int(_) for _ in input().split()]
dp = [0] + [float("inf") for _ in range(m)]

for i in range(1, m + 1):
    for j in coins:
        dp[i] = min(dp[i], dp[i - j] + 1)

if dp[m] != float("inf"):
    print(dp[m])
else:
    print(-1)
```



代码运行截图![屏幕截图 2024-11-07 171917](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 171917.png)

### T12757: 阿尔法星人翻译官



implementation, http://cs101.openjudge.cn/practice/12757

思路：thousand， million 只能出现一次，线性从左到右输入

代码：

```
def convert_to_number(s):
    num_words = {'zero': 0, 'one': 1, 'two': 2, 'three': 3, 'four': 4,'five': 5, 'six': 6, 'seven': 7, 'eight': 8, 'nine': 9,'ten': 10, 'eleven': 11, 'twelve': 12, 'thirteen': 13, 'fourteen': 14,'fifteen': 15, 'sixteen': 16, 'seventeen': 17, 'eighteen': 18, 'nineteen': 19,'twenty': 20, 'thirty': 30, 'forty': 40, 'fifty': 50, 'sixty': 60,'seventy': 70, 'eighty': 80, 'ninety': 90,'hundred': 100, 'thousand': 1000, 'million': 1000000}
    negative = False
    current_number, result = 0, 0
    for word in s.split():
        if word == 'negative':
            negative = True
        elif word in num_words:
            value = num_words[word]
            if value == 100:
                current_number *= value
            elif value >= 1000:
                result += current_number * value
                current_number = 0
            else:
                current_number += value
    result += current_number
    return -result if negative else result

print(convert_to_number(input()))

```



代码运行截图![屏幕截图 2024-11-07 172045](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 172045.png)

### T16528: 充实的寒假生活



greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：类似区间覆盖问题（雷达安装），从左到右贪就行

代码：

```
n = int(input())
activities = [list(map(int, input().split())) for _ in range(n)]
activities.sort()

l, r = -1, -1
count = 0
for a in activities:
    if a[0] > r:
        count += 1
        l, r = a[0], a[1]
    else:
        if a[1] < r:
            r = a[1]

print(count)
```



代码运行截图![屏幕截图 2024-11-07 172249](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-11-07 172249.png)

## 2. 学习总结和收获



一个半小时AC5，然后在第五题卡了，没有意识到thousand和million是分水岭，就很难把思路代码实现。

问问老师如果期末能AC5加作业全写能拿多少分？（

每日选做至11.6