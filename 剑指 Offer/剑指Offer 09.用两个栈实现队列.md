## 题目

```None
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，
分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
--------------------------------------------------------------------------------------------
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
--------------------------------------------------------------------------------------------
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
--------------------------------------------------------------------------------------------
提示：
· 1 <= values <= 10000
· 最多会对 appendTail、deleteHead 进行 10000 次调用
```

## 思路

- 两个栈，一个入栈，一个出栈，在出栈没有元素的时候入栈[全部]元素移动到出栈中
- 后进入入栈的元素放在出栈的栈底，先进入入栈的元素放在出栈的栈顶

## 补充

```
Python数据结构：
· https://docs.python.org/3/tutorial/datastructures.html
```

## 题解

方法1：双栈

```python
class CQueue:

    def __init__(self):
        self.inStack, self.outStack = [], []

    def appendTail(self, value: int) -> None:
        self.inStack.append(value)

    def deleteHead(self) -> int:
        if self.outStack: return self.outStack.pop()
        if not self.inStack: return -1
        # 当outStack没有元素且instack有元素时
        while self.inStack:
            self.outStack.append(self.inStack.pop())
        return self.outStack.pop() # 这一句不要忘了


# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()
```

复杂度分析：

```
时间复杂度: 
· appendTail()函数为O(1)
· deleteHead()函数在N次队首元素删除操作中总共需完成N个元素的倒序
-------------------------------------------------------------
空间复杂度O(N): 最差情况下inStack和outStack共保存N个元素 
```

