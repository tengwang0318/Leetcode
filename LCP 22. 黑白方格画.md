#### [LCP 22. 黑白方格画](https://leetcode-cn.com/problems/ccw6C7/)

难度简单21

小扣注意到秋日市集上有一个创作黑白方格画的摊位。摊主给每个顾客提供一个固定在墙上的白色画板，画板不能转动。画板上有 `n * n` 的网格。绘画规则为，小扣可以选择任意多行以及任意多列的格子涂成黑色，所选行数、列数均可为 0。

小扣希望最终的成品上需要有 `k` 个黑色格子，请返回小扣共有多少种涂色方案。

注意：两个方案中任意一个相同位置的格子颜色不同，就视为不同的方案。





选择了i行j列的话：格子总数为 $i*n+j*(n-i)$

从而可以从i ： 0->n-1开始遍历，根据上面公式计算出$j=(k-i*n)/(n-i)$

如果j为整数就求其组合数乘积

```python
class Solution:
    def paintingPlan(self, n: int, k: int) -> int:
        def helper(m, n):
            if m == 0: return 1
            if m < 0: return 0
            res = 1
            for i in range(1, n + 1):
                res *= i
            for i in range(1, m + 1):
                res /= i
            for i in range(1, n - m + 1):
                res /= i
            return res

        if k == 0:
            return 1
        elif k < n:
            return 0
        elif k == n ** 2:
            return 1
        res = 0
        for i in range(n):
            if (k - i * n) % (n - i) == 0:
                j = (k - i * n) // (n - i)
                res += helper(i, n) * helper(j, n)
        return int(res)

	
```

