给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

题目链接：https://leetcode-cn.com/problems/sort-colors

```python
#时间复杂度为o(N)，遍历了一次数组，所以复杂度为O(N)，空间复杂度为O(1), 没有额外空间消耗。
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        #three pointer
        i= cur = 0
        j = len(nums)-1
        while cur<=j:
            if nums[cur]==0:
                nums[i],nums[cur] = nums[cur],nums[i]
                cur += 1#这里的cur要+1是因为之前的i已经是比较过了的，i总是小于等于cur嘛
                i += 1
            elif nums[cur]==2:
                nums[cur],nums[j] = nums[j],nums[cur]
                j -= 1#这里cur没后移，是因为刚交换过来的数据是需要进行判断比较的
            else:
                cur += 1
        #下面只是为了回顾一下基本排序算法哈哈哈
        #bubblesort
        n = len(nums)
        for i in range(n-1):
            for j in range (0, n-1-i):
                if nums[j] > nums[j+1]:
                    nums[j],nums[j+1] = nums[j+1],nums[j]
        """
        #insertsort
        n = len(nums)
        for i in range(1,n):
            j = i -1
            while j >= 0:
                if nums[i] < nums[j]:
                    nums[i],nums[j]=nums[j],nums[i]
                    i = j
                    j -= 1
                else:
                    break    
        #selectsort
        n = len(nums)
        for i in range (n-1):
            min = nums[0]
            k = i
            for j in range(i+1,n):
                if nums[j]<min://循环内总是和最值比较
                    min = nums[j]
                    k = j
            nums[i],nums[k] = nums[k],nums[j]
```
