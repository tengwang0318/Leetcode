#### [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

难度中等244

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

 

**示例 1：**

```
输入: n = 3
输出: 6
```

**示例 2：**

```
输入: n = 9
输出: 45
```

 

**限制：**

-   `1 <= n <= 10000`



这道题2个点：

1.  不能用for循环
2.  不能用if运算

如何解决：

1.  for用递归实现，这很好理解

2.  if用逻辑运算符的计算特性来解决。即and的短路特性。

    A and function() 如果A是True， 返回的是function 如果A是false，function都不会被执行到就下一句了。

因此我们把递归入口放在function处，那么A表达式就可以起到if的作用，function递归起到for的作用

为了让n能及时停止（数量够的时候，要输出false），我们只能把终点设置成0，因此我们递归中要倒数。

```python
class Solution:
    def sumNums(self, n: int) -> int:
        return n and (n + self.sumNums(n-1))
```