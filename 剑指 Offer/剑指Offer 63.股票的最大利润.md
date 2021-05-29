## 题目

```None
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

示例 1:----------------------------------------------------
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
示例 2:----------------------------------------------------
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
-----------------------------------------------------------
限制：0 <= 数组长度 <= 10^5
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：暴力求解，超出时间限制

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l, profit = len(prices), 0
        for i in range(l):
            for j in range(i + 1,l):
                if prices[j]-prices[i] > profit:
                    profit = prices[j]-prices[i]
        return profit
```

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        ans, num = 0, len(prices)
        for i in range(num):
            for j in range(i + 1, num):
                ans = max(ans, prices[j] - prices[i])
        return ans
```

复杂度分析

```
时间复杂度：O(n^2) 循环运行 n(n-1)/2 次
空间复杂度：O(1) 使用常数个变量
```

方法2：动态规划，一次遍历，假设股票买在历史最低价

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        inf = int(1e9)
        minprice = inf
        maxprofit = 0
        for price in prices:
            maxprofit = max(price - minprice, maxprofit)
            minprice = min(price, minprice)
        return maxprofit
```

复杂度分析

```
时间复杂度：O(n) 只需要遍历一次
空间复杂度：O(1) 只使用了常数个变量
```