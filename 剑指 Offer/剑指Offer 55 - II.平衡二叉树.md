## 题目

```None
输入一棵二叉树的根节点，判断该树是不是平衡二叉树。
如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。
```

示例 1:给定二叉树 [3,9,20,null,null,15,7]

```
    3
   / \
  9  20
    /  \
   15   7
返回 true 。
```

示例 2:给定二叉树 [1,2,2,3,3,null,null,4,4]

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：求出二叉树深度 + 递归

```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        if root is None : return True
        def depth(root: TreeNode) -> int:
            if root is None: return 0
            return max(depth(root.left), depth(root.right)) + 1
        if abs(depth(root.left) - depth(root.right)) > 1 : return False
        return self.isBalanced(root.left) and self.isBalanced(root.right)
```

方法2：