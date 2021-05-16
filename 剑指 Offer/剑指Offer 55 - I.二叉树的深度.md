## 题目

```None
输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。
```

示例：

```
给定二叉树 [3,9,20,null,null,15,7],返回它的最大深度 3
    3
   / \
  9  20
    /  \
   15   7
```

## 思路

- 采用递归方式：

  如果知道 左子树 和 右子树 的最大深度 l 和 r，该二叉树的最大深度即为`max(l,r)+1`

- 采用迭代方式：

  使用BFS，一次遍历一层所有节点并扩展，然后层数+1

## 补充

（可选）

## 题解

方法1：递归 / 后序遍历DFS

```python
class Solution: 
    def maxDepth(self, root: TreeNode) -> int:
        if root is None: return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```

复杂度分析

- 时间复杂度O(n)：n为树的节点数量，计算树的深度需要遍历所有节点
- 空间复杂度O(height)： 最差情况下（当树退化为链表时），递归深度可达到N

方法2：层序遍历BFS

```python
class Solution: 
    def maxDepth(self, root: TreeNode) -> int:
        q ,res = [root] ,0
        while q:
            cnt = len(q)
            for i in range(cnt):
                if q[0]:
                    q.extend([q[0].left,q[0].right])
                q.pop(0)
            res += 1
        return res - 1
```

```python
class Solution: # 大神解法
    def maxDepth(self, root: TreeNode) -> int:
        if not root: return 0
        queue, res = [root], 0
        while queue:
            tmp = []
            for node in queue:
                if node.left: tmp.append(node.left)
                if node.right: tmp.append(node.right)
            queue = tmp
            res += 1
        return res
```

复杂度分析

- 时间复杂度O(n)：n为树的节点数量，计算树的深度需要遍历所有节点
- 空间复杂度O(n)：最差情况下（当树平衡时），队列同时存储N/2个节点（最后一层）