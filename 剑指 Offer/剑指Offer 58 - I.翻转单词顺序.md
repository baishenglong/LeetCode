## 题目

```None
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。
为简单起见，标点符号和普通字母一样处理。
例如输入字符串"I am a student. "，则输出"student. a am I"。
```

示例 1：

```
输入: "the sky is blue"
输出: "blue is sky the"
```


示例 2：

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```


示例 3：

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

## 思路

（可选）

## 补充

join：

```python
语法：  'sep'.join(seq)   ： 以sep作为分隔符，将seq所有的元素合并成一个新的字符串

参数说明
sep：分隔符。可以为空
seq：要连接的元素序列、字符串、元组、字典

返回值：返回一个以分隔符sep连接各个元素后生成的字符串
```

split：

```python
split() ：将多个空格看做一个空格
split(' ') ：空间间也要分开 

s1 = "we   are   family" # 中间三个空格
s1.split(' ') # ['we', '', '', 'are', '', '', 'family']
s1.split() # ['we', 'are', 'family']
```

## 题解

方法1：分割 + 倒序

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # return " ".join(s.strip().split()[::-1])
        return ' '.join(list(reversed(s.split())))
```

复杂度分析：

```
时间复杂度O(N)： 总体为线性时间复杂度，各函数时间复杂度和参考资料链接如下
	- split() 方法： 为 O(N) 
	- trim() 和 strip() 方法： 最差情况下（当字符串全为空格时），为 O(N)
	- join() 方法： 为 O(N)
	- reverse() 方法： 为 O(N)
空间复杂度 O(N)： 单词列表 words 占用线性大小的额外空间
```

方法2：双指针

```python
算法解析：
	1.倒序遍历字符串 s ，记录单词左右索引边界 i , j ；
	2.每确定一个单词的边界，则将其添加至单词列表 res ；
	3.最终，将单词列表拼接为字符串，并返回即可。
复杂度分析：
	时间复杂度O(N)： 其中 N 为字符串 s 的长度，线性遍历字符串。
	空间复杂度O(N)： 新建的 list 中的字符串总长度≤N ，占用 O(N) 大小的额外空间。
```

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip() # 删除首尾空格
        i = j = len(s) - 1
        res = []
        while i >= 0:
            while i >= 0 and s[i] != ' ': i -= 1 # 搜索首个空格
            res.append(s[i + 1: j + 1]) # 添加单词
            while s[i] == ' ': i -= 1 # 跳过单词间空格
            j = i # j 指向下个单词的尾字符
        return ' '.join(res) # 拼接并返回
```

