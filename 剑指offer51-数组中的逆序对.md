## 题目
主定理分析：
数据列均分为两部分，分别排序，之后以 O(N)O(N) 的复杂度进行合并。根据主定理（递归函数的时间复杂度分析工具）
$T\left(N\right) = 2T\left(N/2\RIGHT)+O\left(N\right)$
## 思路
利用归并排序分到最后一步，然后合并最后一层的单元素数组。在第二个子区间元素归并回去的时候计算逆序数的个数。此时左边的子空间当前指针到区间末尾之间的元素个数就是针对刚刚合并回去的
那个元素的逆序数。
## 
时间复杂度：O(nlogn)
空间复杂度：O(N)

```python
class Solution:
    def reversePairs(self, nums: List[int]) -> int:   
        self.cnt = 0
        if len(nums)<=1:
            return 0
        def mergeSort(nums):
            l = 0
            r = len(nums)-1
            if r==0:
                return nums
            mid = (l+r)//2
            left = nums[:mid+1]
            right = nums[mid+1:]
            #不断递归，直到有可以返回的最小单位(单个元素的数组肯定有序)的merge值代入到上一层的mergesort中，逐步往上传
            return merge(mergeSort(left),mergeSort(right))

        def merge(left,right):
            res = []
            i,j = 0,0
            while i<len(left) and j<len(right):
                if left[i]<=right[j]:
                    res.append(left[i])
                    i += 1
                else:
                    res.append(right[j])
                    self.cnt += len(left)-i
                    j += 1
            while i<len(left):
                res.append(left[i])
                i += 1
            while j<len(right):
                res.append(right[j])
                j += 1
            return res
        mergeSort(nums)
        return self.cnt
```
