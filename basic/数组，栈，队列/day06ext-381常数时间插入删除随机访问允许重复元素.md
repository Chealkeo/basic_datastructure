## 题目
设计一个支持在平均 时间复杂度 O(1) 下， 执行以下操作的数据结构。

注意: 允许出现重复元素。

insert(val)：向集合中插入元素 val。
remove(val)：当 val 存在时，从集合中移除一个 val。
getRandom：从现有集合中随机获取一个元素。每个元素被返回的概率应该与其在集合中的数量呈线性相关。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 思路：
与不允许有重复元素的上一题相比，我们不能再使用dict来根据唯一的key获取索引。现在每一个key可能会对应很多索引，这时候我们要用一种新的数据结构，defaultdict()，括号内可以是list\set\bool\int等类。。
根据题意，我们选择set，set内的元素是唯一且不重复的，符合要求。要添加或删除某个索引时用set的操作add和discard，都是根据元素的值来进行操作的。平均时间复杂度为O(1),空间复杂度为O(N).N为操作数规模。
需要注意的是：
集合中的添加元素用add，添进去之后的顺序是否会改变取决于defaultdict(set/list)的类，集合的话就是无序的，所以pop()的话也不一定是把最后加入的那个元素pop出去，需要指定值来discard。
```python
class RandomizedCollection(object):
    import random
    from collections import defaultdict
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.list = []
        self.idx = defaultdict(set)

    def insert(self, val):
        """
        Inserts a value to the collection. Returns true if the collection did not already contain the specified element.
        :type val: int
        :rtype: bool
        """
        self.list.append(val)
        self.idx[val].add(len(self.list)-1)
        if len(self.idx[val]) == 1:
            return True 
        else:
            return False

    def remove(self, val):
        """
        Removes a value from the collection. Returns true if the collection contained the specified element.
        :type val: int
        :rtype: bool
        """
        if not self.idx[val]:
            return False
        last_ele = self.list[-1]
        tar_index = self.idx[val].pop()
        self.list[tar_index] = last_ele
        
        self.idx[last_ele].add(tar_index)
        self.idx[last_ele].discard(len(self.list)-1)
        self.list.pop()
        return True
        

    def getRandom(self):
        """
        Get a random element from the collection.
        :rtype: int
        """
        return random.choice(self.list)


# Your RandomizedCollection object will be instantiated and called as such:
# obj = RandomizedCollection()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

示例:

// 初始化一个空的集合。
RandomizedCollection collection = new RandomizedCollection();

// 向集合中插入 1 。返回 true 表示集合不包含 1 。
collection.insert(1);

// 向集合中插入另一个 1 。返回 false 表示集合包含 1 。集合现在包含 [1,1] 。
collection.insert(1);

// 向集合中插入 2 ，返回 true 。集合现在包含 [1,1,2] 。
collection.insert(2);

// getRandom 应当有 2/3 的概率返回 1 ，1/3 的概率返回 2 。
collection.getRandom();

// 从集合中删除 1 ，返回 true 。集合现在包含 [1,2] 。
collection.remove(1);

// getRandom 应有相同概率返回 1 和 2 。
collection.getRandom();
