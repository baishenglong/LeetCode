## 题目

```None
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，
第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。
-----------------------------------------------------------------------
给定二叉树: [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：
[
  [3],
  [20,9],
  [15,7]
]
-----------------------------------------------------------------------
提示：节点总数 <= 1000
```

## 思路

（可选）

## 补充

```
- python官方时间复杂度说明
- https://wiki.python.org/moin/TimeComplexity
```

## 题解

方法1：BFS遍历 + reversed() / 切片

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res, nodes, flag = [], collections.deque([root]), True
        while nodes:
            cnt, tmp = len(nodes), []
            for _ in range(cnt):
                node = nodes.popleft()
                if node:
                    tmp.append(node.val)
                    nodes.append(node.left)
                    nodes.append(node.right)
            if tmp:
                res.append(tmp) if flag else res.append(tmp[::-1])
            flag = not flag
        return res
```

复杂度分析：

```
时间复杂度O(N): N为二叉树节点数量，循环N次，双端队列添加删除队首队尾元素O(1)
               切片操作O(K)，共完成少于N个节点的倒序操作，占用O(N)
空间复杂度O(N): 最差情况下，满二叉树时，最多有N/2个节点同时在deque中，占用O(N)大小额外空间
```

方法2：BFS遍历 + 双端队列，判断语句位置和条件与上一种写法略有不同

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res, nodes, flag = [], collections.deque([root]), True
        if not root: return [] # 判断root是不是None
        while nodes: 
            tmp = collections.deque()
            for _ in range(len(nodes)):
                node = nodes.popleft()
                tmp.append(node.val) if flag else tmp.appendleft(node.val) # 关键
                if node.left: nodes.append(node.left)
                if node.right: nodes.append(node.right)
            res.append(list(tmp)) # 将deque转为list
            flag = not flag
        return res
```

复杂度分析：

```
时间复杂度O(N): N为二叉树节点数量，循环N次，双端队列添加删除队首队尾元素O(1)
空间复杂度O(N): 最差情况下，满二叉树时，最多有N/2个节点同时在deque中，占用O(N)大小额外空间
```

方法3：BFS遍历 +  奇偶层逻辑分离

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        res, nodes = [], collections.deque()
        nodes.append(root)
        while nodes:
            tmp = []
            # 打印奇数层
            for _ in range(len(nodes)):
                # 从左向右打印
                node = nodes.popleft()
                tmp.append(node.val)
                # 先左后右加入下层节点
                if node.left: nodes.append(node.left)
                if node.right: nodes.append(node.right)
            res.append(tmp)
            if not nodes: break # 若为空则提前跳出
            # 打印偶数层
            tmp = []
            for _ in range(len(nodes)):
                # 从右向左打印
                node = nodes.pop()
                tmp.append(node.val)
                # 先右后左加入下层节点
                if node.right: nodes.appendleft(node.right)
                if node.left: nodes.appendleft(node.left)
            res.append(tmp)
        return res
```

复杂度分析

```
时间复杂度O(N)：同方法2
空间复杂度O(N)：同方法2
```

