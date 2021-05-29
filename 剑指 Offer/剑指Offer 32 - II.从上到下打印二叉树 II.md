## 题目

```None
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。
--------------------------------------------------------------------
给定二叉树: [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：
[
  [3],
  [9,20],
  [15,7]
]
--------------------------------------------------------------------
提示：节点总数 <= 1000
```

## 思路

- BFS遍历


## 补充

```python
# 下面二者等价
if tmp: pass
if tmp != []: pass

# 下面二者等价
if not tmp: pass
if tmp == []: pass
```

## 题解

方法1：BFS遍历

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res, nodes = [], [root]
        while nodes:
            tmp, cnt = [], len(nodes)
            for i in range(cnt):
                node = nodes.pop(0)
                if node:
                    tmp.append(node.val) # 这里是加值，不是结点对象
                    nodes.append(node.left)
                    nodes.append(node.right)
            if tmp: res.append(tmp)
        return res
```

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res, nodes = [], [root]
        while nodes:
            tmp, cnt = [], len(nodes)
            for i in range(cnt):
                node = nodes.pop(0)
                if node: 
                    tmp.append(node.val) 
                    if node.left: nodes.append(node.left)
                    if node.right: nodes.append(node.right)
            if tmp: res.append(tmp)
        return res
```

复杂度分析

```
时间复杂度O(N): N为二叉树节点数量，BFS需循环n次
空间复杂度O(N): 最差情况下，当树为满二叉树时，最多有N/2个树节点同时在列表中，O(N)额外大小空间
```

