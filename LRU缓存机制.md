运用你所掌握的数据结构，设计和实现一个 LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:你是否可以在 O(1) 时间复杂度内完成这两种操作？
链接地址：https://leetcode-cn.com/problems/lru-cache

思路：没想到双链表，也没想到字典里value存的是node，趁机膜了一下双链表，节点的添加删除以及给定点的移动都是常数时间复杂度。
本体涉及的三个关于链表的操作是更新update：即把最近访问的节点移动到链表尾部，这里要涉及五个节点共六次前后继指向关系更新；
addup：把节点加到链表尾部，涉及三个节点的4次前后继指向关系更新。这里要注意需要同时更新字典，把新添加的节点键值对加进去；
删除节点：这里只涉及两个节点的2次前后继指向关系更新，这里也要同步更新字典。
时间复杂度O(1)
空间复杂度O(Capacity),Capacity是题目给定的容量。
```python
class DbLinked:
    def __init__(self, key=0, val=0):
        self.key = key
        self.val = val
        self.next = None
        self.prev = None



class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.dic = dict()
        self.head = DbLinked()
        self.tail = DbLinked()
        self.head.next = self.tail
        self.tail.prev = self.head
    def update(self,node):
        node.prev.next = node.next
        node.next.prev = node.prev
        self.tail.prev.next = node
        node.prev = self.tail.prev
        node.next = self.tail
        self.tail.prev = node
    def addup(self,key,val):
        node = DbLinked()
        node.key = key
        node.val = val
        node.prev = self.tail.prev
        self.tail.prev.next = node
        node.next = self.tail
        self.tail.prev = node
        self.dic[key] = node

    def get(self, key: int) -> int:
        if key not in self.dic:
            return -1
        node = self.dic[key]
        self.update(node)
        return node.val


    def put(self, key: int, value: int) -> None:
        if key in self.dic:
            node = self.dic[key]
            node.val = value
            self.update(node)
        elif len(self.dic)==self.capacity:
            node = self.head.next
            self.head.next = node.next
            node.next.prev = self.head
            self.dic.pop(node.key)
            self.addup(key,value)
        else:
            self.addup(key,value)

           
# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
