## 题目

```None
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。
返回删除后的链表的头节点。
```

示例 1:

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
```

示例 2:

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：单指针

```python
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if head.val == val: return head.next
        pre = head
        while pre.next:
            if pre.next.val == val:
                pre.next = pre.next.next
                return head
            else:
                pre = pre.next
        return head
```

方法2：双指针

```python
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if head.val == val: return head.next
        pre, cur = head, head.next
        while cur:
            if cur.val == val:
                pre.next = cur.next
                return head
            else:
                pre, cur = pre.next, cur.next
        return head
```

方法3：递归

```python
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if head is None:
            return head
        if head.val == val:
            return head.next
        head.next = self.deleteNode(head.next, val)
        return head      
```

