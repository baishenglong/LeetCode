## 题目

```None
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
-------------------------------------------
示例 1：

输入：n = 2
输出：1
-------------------------------------------
示例 2：

输入：n = 5
输出：5
```

## 思路

（可选）

## 补充

```
1. python中整型大小限制取决于计算机内存，不考虑大数越界问题，而其他语言则有类型限制(int)

2. 求余运算规则
	(x+y) mod p = (x mod p + y mod p) mod p
```

## 题解

方法1：递归，超时，很多重复计算

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0 or n == 1: return n
        return int((self.fib(n-1) + self.fib(n-2)) % (1e9+7))
```

方法2：迭代，动态规划

```python
class Solution:
    def fib(self, n: int) -> int:
        a, b = 0, 1
        if n == 0 or n == 1: return n
        for _ in range(n - 1):
            a, b = b, a + b
        return b % 1000000007
```

```python
class Solution:
    def fib(self, n: int) -> int:
        a, b = 0, 1
        for _ in range(n):
            a, b = b, (a + b) % 1000000007 # 提前取余，节约空间，提高速度
        return a % 1000000007
```

复杂度分析：

```
时间复杂度O(N)：循环n-1次，每轮循环操作O(1)复杂度
空间复杂度O(1)：常数大小额外空间
```

