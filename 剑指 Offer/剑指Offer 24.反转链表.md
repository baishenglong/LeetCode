## 题目

```None
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。
------------------------------------------------------------------
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
------------------------------------------------------------------
限制：0 <= 节点个数 <= 5000
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：双指针

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        cur, pre = None, head
        while pre:
            tmp = pre
            pre = pre.next
            tmp.next = cur 
            cur = tmp
        return cur
```

```

```

复杂度分析：

```
时间复杂度O(): 
空间复杂度O(): 
```

方法2：递归

```python

```

复杂度分析：

```
时间复杂度O(): 
空间复杂度O(): 
```

