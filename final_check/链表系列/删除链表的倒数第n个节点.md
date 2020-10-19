## 题目
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
## 思路——双指针
前后指针的应用，求倒数第n个节点，那么先让先手指针走n步，然后让先手后手指针同时后移，当先手指针next是空节点时，后手指针走到了要删除节点的前一个节点。
有两个情况要考虑到，一个是要求删除链表的第一个元素，另一个是链表中只有一个元素。所以要设置辅助头节点指向head，便于返回。同时取cnt<n
## 复杂度
时间复杂度O(N),N是链表长度
空间复杂度O(1)
## 代码（python）
删除链表的倒数第K个节点，找到链表尾节点和要修改后继的节点，之间相差的个数，往往就是n，所以让先行节点向前走n步，range (n)。  
因为有可能会删除头节点，所以我们使用辅助节点指向头节点。然后后行指针也从dummy出发，只要先行指针和next不为空节点，则两节点同时向后。  
跳出循环后，后行节点的后继等于后继的后继，返回辅助节点的next即可。
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        if not head:
            return None
        dummy = ListNode(0)
        dummy.next = head
        former,latter = dummy,dummy
        cnt = 0
        while cnt<n:
            former = former.next
            cnt += 1
        while former.next:
            former = former.next
            latter = latter.next
        
        latter.next = latter.next.next
        return dummy.next
```

```python
#返回链表中倒数第k个结点
class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        former,latter = head,head
        for i in range(k):
            former = former.next
        while former:
            former, latter = former.next,latter.next
        return latter
```


