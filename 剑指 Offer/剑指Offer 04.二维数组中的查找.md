## 题目

```None
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

## 思路

- 从矩阵 右上角|左下角 开始遍历，作为探索根节点


## 补充

（可选）

## 题解

方法1：线性查找

```python
class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if matrix == []: return False
        n, m = len(matrix), len(matrix[0])
        x, y = 0, m-1
        while x <= n-1 and y >=0:
            if matrix[x][y] == target: return True
            elif matrix[x][y] > target : y-=1
            elif matrix[x][y] < target : x+=1
        return False
```

复杂度分析

```
时间复杂度：O(m+n)。访问的下标的行最多增加n次，列最多减少m次，循环体最多执行n+m次
空间复杂度：O(1)。指针使用常数大小额外空间
```

