## 题目

```None
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。
比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
```

```Example
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：

```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        return list(range(1, 10**n))
```

复杂度分析

```
时间复杂度O(10^n)：生成长度为10^n的列表。
空间复杂度O(1)：建立列表需使用O(1)=大小的额外空间(列表作为返回结果，不计入额外空间)
```

方法2：考虑大数，String类型+递归生成全排列+删除高位的0+转为Int类型

```python
class Solution: # 大神解法
    def printNumbers(self, n: int) -> [int]:
        def dfs(x):
            if x == n: # 终止条件：已固定完所有位
                s = ''.join(num[self.start:]) # 拼接(除高位0)
                if s != '0': res.append(int(s)) # 转为int型
                if n - self.start == self.nine: self.start -= 1 # 所有位为9
                return
            for i in range(10):
                if i == 9: self.nine += 1 # 进位
                num[x] = str(i) # 固定第 x 位为 i
                dfs(x + 1) # 开启固定第 x + 1 位
            self.nine -= 1
        
        # num:起始数字定义为 n 个 0 组成的字符列表
        # res:数字字符串列表
        num, res = ['0'] * n, []
        
        # 数字各位中9的数量为 nine，高位0左边界为 start，
        # 所有位都为 99 的判断条件:n−start=nine
        self.nine = 0 
        self.start = n - 1 
        dfs(0) # 开启全排列递归
        return res
```

方法3：首先设置首位的表达范围0--9；然后递归设置后一位0--9；

```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        num, res = ['0'] * n, []

        def recursion(index):
            if index == n - 1:
                for i in range(10):
                    num[index] = str(i)
                    res.append(int(''.join(num)))
                return
            for i in range(10):
                num[index] = str(i)
                recursion(index + 1)

        recursion(0)
        return res[1:]
```

或者这样写：

```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        num, res = ['0'] * n, []

        def recursion(index):
            for i in range(10):
                num[index] = str(i)
                if index != n - 1:
                    recursion(index + 1)
                else:
                    res.append(int(''.join(num)))
            if index == n - 1: return

        recursion(0)
        return res[1:]
```

