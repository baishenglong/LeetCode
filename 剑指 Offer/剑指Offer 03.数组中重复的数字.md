## 题目

```None
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。
数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。
请找出数组中任意一个重复的数字。

示例 1：----------------
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
------------------------
限制：2 <= n <= 100000
```

## 思路

- 哈希表、原地置换


## 补充

```
python中 a,b = c,d操作的原理是先暂存元组(c,d),然后按左右顺序赋值给a和b
--< 本题中如果写成 nums[i], nums[nums[i]] = nums[nums[i]], nums[i]
--> nums[i]先被赋值，之后nums[nums[i]]指向的元素则会出错(nums[i]变化)
--------------------------------------------------------------------
记nums[i]=a，nums[nums[i]]=nums[a]=b,那么交换后
nums[i]=b, nums[nums[i]]=nums[a]=a，这时候下标 a 对应的元素也是a
```

## 题解

方法1：使用哈希表，利用set中元素不能重复的特性

```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        s = set()
        for num in nums:
            if num in s: return num
            s.add(num)
        return -1
```

复杂度分析：

```
时间复杂度：O(N) 遍历数组使用O(N)，HashSet添加和查找元素皆为O(1)
空间复杂度：O(N) HashSet占用O(N)大小的额外空间
```

方法2：因为数组长度为n，元素均在[0,n-1]，说明数组元素的索引和值是一对多的关系。因此可以遍历数组并交换，使元素的索引和值一一对应(即nums[i]=i)。因而通过索引映射对应的值，起到与字典等价的作用。遍历中，第一次遇到数字x时，将其交换至索引x处；而当第二次遇到数字x时，一定有nums[x] = x ，此时即可得到一组重复数字。

```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        i = 0
        while i < len(nums): # 每个位置一直交换直到nums[i] == i, 然后转到下一个位置
            if nums[i] == i:
                i += 1
                continue
            if nums[i] == nums[nums[i]]: return nums[i] # 重复值
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
            # nums[i], nums[nums[i]] = nums[nums[i]], nums[i] # 错误写法, 见补充
```

时间复杂度

```
时间复杂度O(N)： 遍历数组使用O(N)，每轮遍历的判断和交换操作使用O(1)
空间复杂度O(1)： 使用常数复杂度的额外空间
```

