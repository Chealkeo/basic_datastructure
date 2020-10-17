## 题目描述
https://leetcode-cn.com/problems/merge-k-sorted-lists/

## 思路
类似归并排序的方法，分而治之，作为列表组成的单个链表之间两两合并，合并的时候借助辅助结点变换链表中结点的后继关系，再逐步向上合并。

## 复杂度
时间复杂度：O(nk*logk)，k是列表的长度，n是单个链表的长度。
空间复杂度：O(logk)，递归栈的复杂度。
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists: return None
        def mergesort(nums):
            l,r = 0,len(nums)-1
            if r==0:
                return nums[l]
            mid = (l+r)//2
            left = nums[:mid+1]
            right = nums[mid+1:]
            return merge(mergesort(left),mergesort(right))
        
        def merge(left,right):
            prehead = ListNode(-1)
            cur = prehead
            #每个子列表的元素是链表的头结点
            while left and right:
                if left.val<=right.val:
                    cur.next = left
                    left = left.next
                else:
                    cur.next = right
                    right = right.next
                cur = cur.next
            cur.next = left if left else right
            return prehead.next

        return mergesort(lists)
```
