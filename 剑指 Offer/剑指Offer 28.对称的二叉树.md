## 题目

```None
请实现一个函数，用来判断一棵二叉树是不是对称的。
如果一棵二叉树和它的镜像一样，那么它是对称的。
```

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：递归

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def recur(l,r):
            if not l and not r : return True
            if not l or not r or l.val != r.val : return False
            return recur(l.left,r.right) and recur(l.right,r.left)
        if root is None : return True
        return recur(root.left,root.right)
```

复杂度分析：

```
时间复杂度O(N): N为二叉树节点数量，每次执行recur()可以判断一对节点是否对称，因此最多调用N/2次recur()
空间复杂度O(N): 二叉树退化为链表时，系统使用O(N)大小的栈空间
----------------------------------------------------------
  /\
 /  \
/    \
```

方法2：BFS迭代

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        q = [root]
        while q:
            cnt = len(q)
            for i in range(cnt):
                if q[0]: q.extend([q[0].left, q[0].right])
                q.pop(0)
            # after `map` and `reversed` use `list` to transform
            vals = list(map(lambda x: x.val if x else None, q))
            if vals != list(reversed(vals)): return False
        return True
```

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        q = [root]
        while q:
            cnt = len(q)
            for i in range(cnt//2):
                if q[i] is None and q[-i-1] is None : pass
                elif q[i] is None or q[-i-1] is None : return False
                elif q[i].val != q[-i-1].val : return False
            for i in range(cnt): 
                if q[0] : q.extend([q[0].left,q[0].right])
                q.pop(0)
        return True
```

