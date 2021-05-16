## 题目

```None
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。
如果有多对数字的和等于s，则输出任意一对即可。
```

示例1：

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

示例 2：

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

## 思路

（可选）

## 补充

```
Python 中 set,dict 都是基于哈希表的数据结构
```

## 题解

方法1：对于大规模数据超出时间限制

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for num in nums:
            if nums.count(target-num):
                return [num,target-num]
```

方法2：哈希

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        s = set()
        for num in nums:
            if target - num in s: return [num,target-num]
            s.add(num)
```

方法3：二分

```
1）从左边开始遍历获取一个较小值
2）然后通过二分法在右边找看合适的值
```

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        j = len(nums) - 1
        for i in range(j):
            left, right = i, j
            wanted = target - nums[left]
            # 下面不能用break，否则直接退出整个for循环
            if wanted < nums[left] or wanted > nums[right]: continue  
            while left <= right:  # 二分查找过程
                mid = (right + left) // 2
                if nums[mid] == wanted: return [nums[i], wanted]
                elif nums[mid] < wanted:
                    left = mid + 1
                elif nums[mid] > wanted:
                    right = mid - 1
        return []
```

方法4：双指针

```
因为是有序数组，所以可以使用双指针法，假设初始指针i,j指向最小,最大元素
如果 nums[i]+nums[j]<target 则nums[i]+nums[i+1..j]<target 故结果中不可能有nums[i]
因此 i+1 不会漏掉可能的正确的结果，nums[i]+nums[j]>target同理分析
```

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        i, j = 0, len(nums)-1
        while i < j:
            # 先计算并保存和，避免后面重复计算，同时使用elif避免不必要的判断
            s = nums[i] + nums[j] 
            if s == target: return [nums[i],nums[j]]
            elif s < target: i += 1
            elif s > target: j -= 1
```

复杂度分析

```
时间复杂度O(N)：N为数组nums的长度；双指针共同线性遍历整个数组
空间复杂度O(1)：变量 i, j 使用常数大小的额外空间
```

