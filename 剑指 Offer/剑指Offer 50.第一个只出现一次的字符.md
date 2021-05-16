## 题目

```None
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。
s 只包含小写字母。
```

示例：

```None
s = "abaccdeff"
返回 "b"

s = "" 
返回 " 
```

## 思路

（可选）

## 补充

```
reversed()函数：返回一个[元组、列表、字符串、range]反转的迭代器
```

list和string互相转换

```
list -> string:	''.join(some_list)
string -> list:	list(some_string)
```

## 题解

方法1：反转字符串比较索引之和

```python
class Solution:
    def firstUniqChar(self, s: str) -> str:
        rev = list(reversed(s))
        length = len(s) - 1
        for c in s:
            if s.index(c) + rev.index(c) == length:
                return c
        return " "
```

方法2：字典统计每个字符出现次数

```
1.初始化：初始化字典dic
2.统  计：遍历字符串s中每个字符c
	若dic不含key c，则添加键值对(c,True)，表示c的数量为1
	若dic中含key c，则修改c的键值对为(c,False), 表示数量大于1
3.查  找：遍历字符串s中每个字符c，若dic中对应值为True，则返回c
```
```
时间复杂度O(N)：N为字符串s长度，遍历s两轮，HashMap查找复杂度为O(1)
空间复杂度O(1)：最多26个字符，HashMap占用O(26)=O(1)额外空间
```

```python
class Solution:
    def firstUniqChar(self, s: str) -> str:
        dic = dict()
        for c in s: # 统计各字符数量是否>1
            dic[c] = not c in dic
        for c in s: # 找到首个数量为1的字符
            if dic[c]: return c
        return " " # 默认返回空格
```

方法3：有序哈希表（Python 3.6之后默认字典有序），复杂度与方法2相同

```
哈希表是去重的，有序哈希表中的键值对是按照插入顺序排序的
```

```python
class Solution:
    def firstUniqChar(self, s: str) -> str:
        dic = dict() # dic = collections.OrderedDict()
        for c in s:
            dic[c] = not c in dic
        for k, v in dic.items():
            if v: return k
        return ' '
```

