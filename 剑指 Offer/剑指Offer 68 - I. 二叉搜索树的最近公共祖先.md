## 题目

```None
给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

「百度百科」中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]
                                
                                  3
                                /   \
                               5     1
                              / \   / \
                             6   2 0   8
                                / \   
                               7   4
-----------------------------------------------------------------------
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
-----------------------------------------------------------------------
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
-----------------------------------------------------------------------
说明: 所有节点的值都是唯一的。p、q 为不同节点且均存在于给定的二叉搜索树中。
```

## 思路

- 迭代、递归


## 补充

```
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。
如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。
```

```python
>>>a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 打包为元组的列表
[(1, 4), (2, 5), (3, 6)]
>>> zip(a,c)              # 元素个数与最短的列表一致
[(1, 4), (2, 5), (3, 6)]
>>> zip(*zipped)          # 与 zip 相反，*zipped 可理解为解压，返回二维矩阵式
[(1, 2, 3), (4, 5, 6)]
```

## 题解

方法1：两次遍历找到root到p和q的结点路径

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode': 
        def search(n):
            nodes, tmp = [root], root
            while True:
                if tmp.val < n.val: tmp = tmp.right 
                elif tmp.val > n.val: tmp = tmp.left
                else: break
                nodes.append(tmp)
            return nodes
        pNodes, qNodes = search(p), search(q)
        # -------------------------------------
        # 后续解法 1
        i, maxIndex = 0, min(len(pNodes), len(qNodes)) - 1
        while True:
            if i > maxIndex: return pNodes[i-1]
            if pNodes[i].val == qNodes[i].val: i += 1
            else: return pNodes[i-1]
        # -------------------------------------
        # 后续解法 2
       	ancestor = None
        for pNode, qNode in zip(pNodes,qNodes):
            if pNode.val == qNode.val: ancestor = pNode
            else: break
        return ancestor
```

复杂度分析：

```
时间复杂度O(N): N为节点个数，最坏情况树退化成链表，p和q为唯一叶子结点及其父节点
空间复杂度O(N): 要存储root到p和q的路径。最坏情况路径长度为O(N)
```

方法2：一次遍历，从root往下找到p和q出现分歧的位置即为最近公共祖先

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode': 
        res, i, j = root, min(p.val, q.val), max(p.val, q.val) 
        while True:
            if res.val < i: res = res.right 
            elif res.val > j: res = res.left
            else: return res
```

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if p.val > q.val: p, q = q, p # 保证 p.val < q.val
        while root:
            if root.val < p.val:
                root = root.right 
            elif root.val > q.val: 
                root = root.left 
            else: break
        return root
```

复杂度分析：

```
时间复杂度O(N): N为节点个数，每循环一轮排除一层
二叉搜索树最小层数为logN(满二叉树)，最大层数为N(退化为链表)
--------------------------------------------------------
空间复杂度O(1): 仅需要/不需要常数大小额外空间
```

方法3：递归

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode': 
        if root.val < p.val and root.val < q.val: return self.lowestCommonAncestor(root.right,p,q)
        if root.val > p.val and root.val > q.val: return self.lowestCommonAncestor(root.left,p,q)
        return root
```

```
时间复杂度O(N): N为节点个数，每循环一轮排除一层
二叉搜索树最小层数为logN(满二叉树)，最大层数为N(退化为链表)
--------------------------------------------------------
空间复杂度O(N): 最差情况树退化为链表，递归深度达到树的层数N
```

