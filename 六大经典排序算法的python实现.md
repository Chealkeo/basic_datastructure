# 衡量指标
## 时间复杂度
对待排序数组进行的操作规模。
## 空间复杂度
空间复杂度是指该算法所耗费的存储空间，即对一个算法在运行过程中临时占用存储空间大小的度量。
## 稳定性
排序算法中还有一个度量指标是稳定性。如果算法执行前后相同数量值的元素的相对位置不发生改变，则算法是稳定的；若可能发生改变，则是不稳定的。
# 排序算法
## 直接选择排序
### 思想
从n个未排序元素中找最小/大的，遍历n-1次，交换最值和第一个元素；在剩下的n-1个未排序元素中再找最小/大的，遍历n-2次，交换最值和第二个元素；  
...直到最后，在剩下的两个元素中找出大小，并交换位置。比较n(n-1)/2次，时间复杂度为O（n^2），空间复杂度为O(1)。  
但由于此算法涉及元素之间的互换位置，可能会改变相同数值元素的相对位置，故为不稳定。
### 复杂度分析
直接选择排序的时间复杂度不随数据序列中关键字分布的变化而变化，故其平均、最好、最坏时间复杂度均为$O\left(n^{2}\right)$  
排序是原地完成，不需要辅助空间，故空间复杂度为$O\left(1\right)$
### python实现
```python
def selectsort(nums):
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
## 直接插入排序
### 思想
将首元素看作已排序序列，对其后的未排序序列中的每个元素依次扫描，将扫描到的每个元素插入有序序列的适当位置（由后向前）  
（若待插入的元素与有序序列中的某个元素相等，则插入到相等元素的后面，保证了其稳定性）。时间复杂度和空间复杂度同上，具有稳定性。
### 复杂度分析
最坏时间复杂度为$O\left(n^{2}\right)$, 平均时间复杂度为$O\left(n^{2}\right)$，最好时间复杂度为$O\left(n\right)$(基本有序)  
也是原地进行的排序，没有占用额外内存，$O\left(1\right)$
### python实现
```python
def insertsort(nums):
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
```
## 冒泡排序
### 思想
依次比较相邻的元素，[0]和[1],[1]和[2]等等，第一次比较n-1次，最大元素filter到最后；  
第二次依次比较前n-1个，比较n-2次；...直到最后i=n-2，比较一次前两个数即完成排序。不涉及跨元素交换，是稳定的。  
### 复杂度分析
最坏时间复杂度为$O\left(n^{2}\right)$, 平均时间复杂度为$O\left(n^{2}\right)$，最好时间复杂度为$O\left(n\right)$(基本有序)  
也是原地进行的排序，没有占用额外内存，$O\left(1\right)$
### python实现
```python
def sortColors(nums):
        n = len(nums)
        for i in range(n-1):
            for j in range (0, n-1-i):
                if nums[j] > nums[j+1]://每次都是不同的元素相互比较
                    nums[j],nums[j+1] = nums[j+1],nums[j]
```
## 归并排序
### 思想
采用分治法，将已有序的子序列合并，得到完全有序的序列；当分得的子序列中只有一个元素时自然有序，此时开始进行有序序列自下而上，由少至多的合并  
### 复杂度分析
归并排序的时间复杂度不随数据序列中关键字分布的变化而变化，其平均、最好、最坏时间复杂度均为$O\left(nlogn\right)$,每一趟归并的时间复杂度为$O\left(n\right)$, 总共需要归并$logn$趟  
归并排序中需要一个与表等长的存储单元数组空间，故空间复杂度为$O\left(n\right)$
### python实现
```python
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
            #这里归并时可以用三指针
            while left and right:
                if left[0]<=right[0]:
                    res.append(left.pop(0))
                else:
                    res.append(right.pop(0))
            while left:
                res.append(left.pop(0))
            while right:
                res.append(right.pop(0))
            return res
        mergeSort(nums)
```
## 快速排序
快速排序的排序函数给定原始待排序列表即可，（如果是求K大或K小则需要传个参数K）。分块函数需要的参数则是待排序数组，左索引和右索引。
### 思想
首先选定一个基准元素left，一个指向基准元素的下标j，从基准元素的下一个元素开始遍历到right边界为止，遇到比基准元素小的元素，则下标j向后移一位，  
并交换此刻遍历的元素和j下标指向的元素，遍历结束之后，交换left和j指向的元素，实现把比基准元素小的元素均保留在了基准元素的左侧，比基准元素大的元素均保留在了基准元素的右侧。  
基准元素通常随机获取。  
### 复杂度分析
快速排序的平均时间复杂度为$O\left(nlogn\right)$,当序列有序或基本有序时，快排的时间复杂度退化为$O\left(n^{2}\right)$，（每次找到的都是边界上的元素的位置）
快速排序故空间复杂度为$O\left(logn\right)$，递归栈的深度。
### python实现
```python
class Solution:
    import random 
    def quicksort(self,nums):
    #def findKthLargest(self, nums: List[int], k: int) -> int:       
        left = 0
        right = len(nums)-1
        while True:
            index = self.partion(left,right,nums)
            '''一下是找第k大的数字
            if index==len(nums)-k:
                return nums[index]
            elif index>len(nums)-k:
                right = index-1
            else:
                left = index+1
            '''
            self.quicksort(nums[left:index])
            self.quicksort(nums[index+1:right])
        return nums

    def partion(self,left, right, nums):
        ranindex = random.randint(left,right)
        nums[left],nums[ranindex] = nums[ranindex],nums[left]
        pivot = nums[left]
        j = left
        for i in range(left+1,right+1):
            if nums[i] < pivot:
                j += 1
                nums[i],nums[j] = nums[j],nums[i]
        nums[left],nums[j] = nums[j],nums[left]
        return j
```
## 堆排序
### 思想
根据升序、降序需求分别构建大小顶堆，从非叶子节点开始调整构建，使其满足大小顶堆的性质，每得到一个堆顶元素将其与数组末端元素进行交换，不断选择剩下的元素里最大的元素。
建堆的时候从最后一个非叶子节点开始到第一个叶子节点；调整堆的时候从上往下。
### 复杂度分析
时间复杂度不随数据序列中关键字分布的变化而变化，其平均、最好、最坏时间复杂度均为$O\left(nlogn\right)$
空间复杂度为O(1)
### python实现
```python
    def heapmax(self, nums):
        for i in range(len(nums)//2-1,-1,-1): 
            self.modifyheap(nums,i)


    def modifyheap(self,nums,i):  
        l = 2*i+1
        r = 2*i+2
        largest = i
        if l<len(nums) and nums[largest]<nums[l]:
            largest = l
        if r<len(nums) and nums[largest] < nums[r]:
            largest = r
        if largest!=i:
            nums[i],nums[largest] = nums[largest],nums[i]
            self.modifyheap(nums,largest)
```
# 算法之间的比较
## 不稳定
简单选择排序、快速排序、堆排序和希尔排序是不稳定的算法。
## 不变化
简单选择排序、归并排序和堆排序是时间复杂度不随数据序列中关键字分布的变化而变化的算法。
## 原地排序
简单选择排序、直接插入排序、冒泡排序、堆排序、希尔排序都是原地排序算法，不占用额外内存。


