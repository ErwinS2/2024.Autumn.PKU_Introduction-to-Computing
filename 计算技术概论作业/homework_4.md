## 1. 题目



### 34B. Sale



greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B

思路：尽量多卖，排序

代码

```
a,b = map(int,input().split())
sum = 0
list = [int(_) for _ in input().split()]
list.sort()
for i in range(0,b):
    if list[i] < 0:
        sum -= list[i]
 
print(sum)
```



代码运行截图 ![屏幕截图 2024-10-17 122844](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 122844.png)

### 160A. Twins



greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：从最大开始拿

代码

```
n = int(input())
list = input().split()
sum = 0
count = 0
for i in range(0,n):
    list[i] = int(list[i])
    sum += int(list[i])
list = sorted(list)
for i in range (n-1,-1,-1):
    count += int(list[i])
    if 2*count > sum:
        print(n-i)
        break
```



代码运行截图 ![屏幕截图 2024-10-17 123043](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 123043.png)

### 1879B. Chips on the Board



constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：

代码

```
times = int(input())
for j in range(0,times):
    n = int(input())
    list_1 = [int(_) for _ in input().split()]
    list_2 = [int(_) for _ in input().split()]
    flag_1, flag_2 = 3*10**9, 3*10**9
    sum_1, sum_2 = 0, 0
    
    for i in range(0,n):
        sum_1 += list_1[i]
        sum_2 += list_2[i]
        if list_1[i] <= flag_1:
            flag_1 = list_1[i]
        if list_2[i] <= flag_2:
            flag_2 = list_2[i]
    print(min((sum_1 + n*flag_2),(sum_2 + n*flag_1)))
```



代码运行截图![屏幕截图 2024-10-17 134416](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 134416.png)

### 158B. Taxi



*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：先大后小，分类讨论

代码

```
n = int(input())
s = input().split()
count = {"1":0,"2":0,"3":0,"4":0}
for i in s:
    count[i] += 1

sum = count["3"] + count["4"] + count["2"] // 2
l2 = count["2"] % 2
l1 = count["1"] - count["3"] - 2 * l2
if l1 <= 0:
    print(sum + l2)
else:
    print(sum + l1 // 4 + int(l1 % 4 != 0) + l2)
 
```



代码运行截图 ![屏幕截图 2024-10-17 123420](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 123420.png)

### *230B. T-primes（选做）



binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：我先用筛法跑了1到1000所有的质数（

代码

```
prime_list = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701, 709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997]
def is_prime(x):
    for i in prime_list:
        if x % i == 0 and i < x:
            return False
    return True

n = int(input())
nums = map(int,input().split())
output = [None for i in range(n)]

for num in nums:
    if num == 1:
        output.append('NO')
        continue
    if num**0.5 == int(num**0.5) and is_prime(int(num**0.5)) == True:
        output.append('YES')
    else:
        output.append('YES')

print("\n".join(output))
```



代码运行截图![屏幕截图 2024-10-17 123845](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 123845.png)

### *12559: 最大最小整数 （选做）



greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：其实很直接粗暴的一题，可以直接写冒泡排序，不过用cmp_to_key最快，这样就变成语法题了

代码

```
from functools import cmp_to_key
n = int(input())
numbers = input().split()
def custom_cmp_max(x, y):
    if x + y > y + x:
        return -1
    elif x + y < y + x:
        return 1
    else:
        return 0
numbers.sort(key=cmp_to_key(custom_cmp_max))
print("".join(numbers), "".join(numbers[::-1]))
```



代码运行截图![屏幕截图 2024-10-17 124133](C:\Users\31507\OneDrive\桌面\屏幕截图 2024-10-17 124133.png)

## 2. 学习总结和收获



每日选做一直在跟进，这一周的题在A.XXXXX卡的最久，把自己的TLE交给AI，结果AI给了给又复杂又错的代码，让我想了很久没有结果，之后福至心灵想出来了，之后不敢无条件相信AI了（

总体感觉自己有在进步，1400的题也没有想象的难