## 题目

```None
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
```

示例 1：

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

## 思路

（可选）

## 补充

Python 字符串一旦创建之后，里面的元素是不可以修改的。只能整体重新赋值。

## 题解

方法1：python内置replace函数

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        return s.replace(' ',"%20")
```

方法2：遍历逐个替换

```python
class Solution: # 错误写法
    def replaceSpace(self, s: str) -> str:
        for c in s:
            if c == ' ' : c == '%20' # 只改变c，不改变s
        return s
```

```python
class Solution: # 错误写法
    def replaceSpace(self, s: str) -> str:
        l = len(s)
        for i in range(l):
            # 'str' object does not support item assignment
            if s[i] == ' ' : s[i] = '%20' 
        return s
```

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        l,length = list(s),len(s)
        for i in range(length):
            if l[i] == ' ' : l[i] = '%20'
        return ''.join(l)
```

