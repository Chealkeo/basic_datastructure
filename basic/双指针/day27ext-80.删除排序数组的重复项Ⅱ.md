## 题目
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 思路：
题目要求每个元素至多保留两个，那就比较fast指针指向的元素和slow指针指向的元素，不相等则当前slow指针直接后移并赋值为当前fast的值，同时fast指针也后移；
如果相等则比较slow-1的元素值，相等则直接fast指针后移，不相等则slow指针后移并赋值，fast指针也后移；
这里需要注意的是slow-1并不一定存在呀，当slow指向第一个元素时，slow-1的值就超出了数组的index，介于列表的第一个元素肯定可以在，所以两个指针都指向第二个元素开始。
此时又面临一个问题，就是当两个指针指向同一个元素时，我们是不希望进行值的比较的，所以在第二个if语句中要加上fast！=slow的限制条件。
其余条件则fast指针后移即可。

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums)<=2:
            return len(nums)
        fast = 1
        slow = 1
        while fast < len(nums):
            if nums[slow] != nums[fast]:
                slow += 1
                nums[slow] = nums[fast]
            elif slow != fast and  nums[fast]!=nums[slow-1]:
                slow += 1
                nums[slow] = nums[fast]
            fast += 1
        return slow+1
```
