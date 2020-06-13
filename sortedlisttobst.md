给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

思路一：因为二叉搜索树满足所有左子树的节点值小于根节点值，右子树的节点值大于根节点值，且具有递归子结构，所以题目可以理解为不断找出有序链表的中间节点并以此截断，其左右孩子分别为左右两个子链表的中间节点值。
用两个指针slow、fast遍历链表确定每一次的中间节点，空间复杂度为二叉树的规模O(log(N))，时间复杂度考虑每个节点遍历的次数，越靠近叶子节点的节点遍历次数越多，
遍历次数为它所在的二叉树的层数，所以以最后一层节点所遍历的次数来代表最坏的时间复杂度，遍历次数为log(N)，最后一层节点数为N/2，时间复杂度为O(Nlog(N)),N为链表元素个数。
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if not head:
            return None
        pre = None
        slow = head
        fast = head
        while fast and fast.next:
            pre = slow
            fast = fast.next.next
            slow = slow.next
        if pre == None:
            return TreeNode(head.val)
        pre.next = None
        mid = slow
        node = TreeNode(mid.val)
        if mid == head:
            return node
        node.left = self.sortedListToBST(head)
        node.right = self.sortedListToBST(mid.next)
        return node
```
思路二：将有序链表转换成数组，从数组中获取中间元素由于可以按索引随机访问所以这一部分的时间复杂度降到了O(1)每个元素都遍历了一次，所以时间复杂度为O(N),N为有序链表的元素个数。
空间复杂度为O(N)，维护了一个数组和树。
```python
class Solution(object):
    def sortedlisttolist(self,head):
        cur = head
        list = []
        while cur:      
            list.append(cur.val)
            cur = cur.next
        return list
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        list = self.sortedlisttolist(head)
        def listtobst(l,r):
            if l > r:
                return None
            mid = (l+r+1)//2
            print(mid)
            node = TreeNode(list[mid])
            if l == r:
                return node
            node.left = listtobst(l, mid-1)
            node.right = listtobst(mid+1,r)
            return node
        return listtobst(0,len(list)-1)
```
