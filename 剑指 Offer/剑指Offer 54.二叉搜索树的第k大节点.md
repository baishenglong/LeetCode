## 题目

```None
给定一棵二叉搜索树，请找出其中第k大的节点。

示例1:------------------------------
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
示例 2:------------------------------
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
限制：------------------------------
1 ≤ k ≤ 二叉搜索树元素个数
```

## 思路

- 二叉搜索树中序遍历为递增序列，中序遍历倒序为递减序列


## 补充

（可选）


## 题解

方法1：中序遍历 + 提前返回；两次判断的目的是避免不必要的递归

```python
class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        nodes = []

        def tree(node):
            if node:
                tree(node.right)
                if self.cnt == k: return # 第一次判断是否终止
                nodes.append(node.val)
                self.cnt += 1 
                if self.cnt == k: return # 第二次判断是否终止
                tree(node.left)

        self.cnt = 0 # 临时变量用类变量，否则报错
        tree(root)

        return nodes[-1] # 返回列表最后一个元素
```

```python
class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:

        def tree(node):
            if node:
                tree(node.right)
                if self.k == 0: return 
                self.k -= 1 
                if self.k == 0: 
                    self.res = node.val
                    return
                tree(node.left)

        self.k, self.res = k, -1 # 维护类变量k用来计数，维护类变量res用来保存结果
        tree(root)

        return self.res
```

复杂度分析：

```
时间复杂度：O(N) 树退化为链表时(全部右子结点)，无论k，递归深度都为N
空间复杂度：O(N) 树退化为链表时(全部右子结点)，系统使用O(N)大小栈空间
```

