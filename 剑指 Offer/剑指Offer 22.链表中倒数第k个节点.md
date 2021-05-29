## 题目

```None
输入一个链表，输出该链表中倒数第k个节点。
为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。
例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。
这个链表的倒数第 3 个节点是值为 4 的节点。

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

## 思路

- 双指针，两个指针相距k，一个指针走到结尾时，另一个指针距尾部正好是k


## 补充

（可选）

## 题解

方法1：双指针

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        i = j = head
        for _ in range(k): j = j.next  # 注意这里不能用 i 做临时变量，否则覆盖前面已定义变量
        while j:
            i, j = i.next, j.next
        return i
```

复杂度分析

```
时间复杂度：O(N) N为链表长度，前指针走了N步，后指针走了N-K步
空间复杂度：O(1) 双指针使用常数大小额外空间
```

