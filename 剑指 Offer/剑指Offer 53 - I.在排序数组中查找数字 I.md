## 题目

```None
统计一个数字在排序数组中出现的次数。
---------------------------------------
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
---------------------------------------
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
---------------------------------------
限制：0 <= 数组长度 <= 50000
```

## 思路

（可选）

## 补充

（可选）

## 题解

方法1：二分法定位到target，然后左右指针向两侧移动计数直到不是target

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right, cnt = 0, len(nums)-1, 0
        while left <= right: 
            middle = left + (right-left) // 2  # 这样写能防止类型越界
            if nums[middle] > target: right = middle - 1
            elif nums[middle] < target: left = middle + 1
            else: # nums[middle] == target
                left, right, cnt = middle-1, middle+1, 1
                while left >= 0 and nums[left] == target:
                    cnt += 1
                    left -= 1
                while right <= len(nums)-1 and nums[right] == target:
                    cnt += 1
                    right += 1 
                return cnt
        return cnt
```

复杂度分析：

```
时间复杂度O(N): 虽然二分查找是O(logN)
但是最差情况所有元素都相同，找到target后仍然遍历整个数组，所以是O(N)
-----------------------------------------------------------------
空间复杂度O(1): 使用常数大小额外空间
```

方法2：二分法定位到target的左右边界

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l <= r: # 先找右边界
            m = l + (r - l) // 2
            if nums[m] <= target: l = m + 1
            else: r = m - 1
        rightbound = l # 此时指向target的右边一位

        # l, r = 0, rightbound - 1 # 优化1:不用搜索整个区间
        l = 0 # 优化3: r不用赋值，因为循环完毕后正好是rightbound - 1
        if r >= 0 and nums[r] != target: return 0 # 优化2:先判断有没有target元素

        while l <= r: # 再找左边界
            m = l + (r - l) // 2
            if nums[m] >= target: r = m - 1
            else: l = m + 1
        leftbound = r # 此时指向target的左边一位

        return rightbound - leftbound - 1 # 所以这里要-1
```

复杂度分析：

```
时间复杂度O(N): 两次二分查找复杂度都是O(logN)
空间复杂度O(1): 使用常数大小额外空间
```

方法3：二分查找target和target-1的右边界，将两结果相减并返回即可，复杂度同上

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        def findRightBound(target):
            l, r = 0, len(nums) - 1
            while l <= r:
                m = l + (r - l) // 2
                if nums[m] <= target: l = m + 1
                else: r = m - 1
            return l # 此时指向target的右边一位
        
        return findRightBound(target) - findRightBound(target-1)
```

