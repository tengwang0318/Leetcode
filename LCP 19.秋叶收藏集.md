### [LCP 19. 秋叶收藏集](https://leetcode-cn.com/problems/UlBDOe/)

难度中等178

小扣出去秋游，途中收集了一些红叶和黄叶，他利用这些叶子初步整理了一份秋叶收藏集 `leaves`， 字符串 `leaves` 仅包含小写字符 `r` 和 `y`， 其中字符 `r` 表示一片红叶，字符 `y` 表示一片黄叶。
出于美观整齐的考虑，小扣想要将收藏集中树叶的排列调整成「红、黄、红」三部分。每部分树叶数量可以不相等，但均需大于等于 1。每次调整操作，小扣可以将一片红叶替换成黄叶或者将一片黄叶替换成红叶。请问小扣最少需要多少次调整操作才能将秋叶收藏集调整完毕。



方法一：设置一个3*n的数组，

dp[0] [i] 表示的是第i个为第一次出现红色需要的调整次数

dp[1] [i]表示的是第i个为黄色需要调整的次数

dp[2] [i]表示的是第i个为第二次出现红色需要调整的次数

状态转换方程为：

$ dp[0][i] = dp[0][i - 1] + (0 if leaves[i] == "r" else 1)\\
dp[1][i] = min(dp[1][i - 1], dp[0][i - 1]) + (0 if leaves[i] == "y" else 1)\\
dp[2][i] = min(dp[2][i - 1], dp[1][i - 1]) + (0 if leaves[i] == "r" else 1) $

```python
class Solution:
    def minimumOperations(self, leaves: str) -> int:
        dp = [[0] * len(leaves) for _ in range(3)]
        dp[0][0] = 1 if leaves[0] == "y" else 0
        dp[1][0] = dp[2][0] = float('inf')

        for i in range(1, len(leaves)):
            dp[0][i] = dp[0][i - 1] + (0 if leaves[i] == "r" else 1)
            dp[1][i] = min(dp[1][i - 1], dp[0][i - 1]) + (0 if leaves[i] == "y" else 1)
            dp[2][i] = min(dp[2][i - 1], dp[1][i - 1]) + (0 if leaves[i] == "r" else 1)
        return dp[2][-1]

```

方法二：

降低空间复杂度，不难发现这一轮的数值只用到了上一轮的数值。

```python
class Solution:
    def minimumOperations(self, leaves: str) -> int:
        first = 1 if leaves[0] == 'y' else 0
        third = second = float('inf')
        for i in range(1,len(leaves)):
            third = min(third, second) + (0 if leaves[i] == 'r' else 1)
            second = min(first, second) + (0 if leaves[i] == "y" else 1)
            first = first + (0 if leaves[i] == 'r' else 1)
        return third

```

