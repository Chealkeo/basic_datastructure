## 题目：
给定一个较长字符串big和一个包含较短字符串的数组smalls，设计一个方法，根据smalls中的每一个较短字符串，对big进行搜索。输出smalls中的字符串在big里出现的所有位置positions，其中positions[i]为smalls[i]出现的所有位置。

示例：
输入：
big = "mississippi"
smalls = ["is","ppi","hi","sis","i","ssippi"]
输出： [[1,4],[8],[],[3],[1,4,7,10],[5]]
提示：
0 <= len(big) <= 1000
0 <= len(smalls[i]) <= 1000
smalls的总字符数不会超过 100000。
你可以认为smalls中没有重复字符串。
所有出现的字符均为英文小写字母。
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/multi-search-lcci

场景描述from unclegem：
该题这个情景我们挺常见的，我们打游戏的时候有时候生气骂人发出去的却是被和谐掉了，这就是因为我们发送的文本中包含敏感词，于是把敏感词替换成了***，而Trie的其中一种作用就是检测敏感词
## 思路：
到处通过题解修正过来的，首先是通过前缀树把要查询的子串存进去，然后对big字符串可能包含的所有子串进行搜索判断是否在树中。有几点需要注意：
1、前缀树节点中要添加索引属性，即当当前节点构成一个字符串的结尾时，要把它出现在small数组里的索引保存起来。这样才能在后面方便地返回所有small字符串里的位置索引。
一开始想把每个字符串的位置索引直接保存在节点属性上，到后来发现无法很好地将这些列表元素整合到返回列表里去，所以节点上的字符串索引是必要的。
2、对big的可能子串搜索时，如果某个字符不在根节点的孩子节点中，那么说明不存在以该字符开头的子串，进入下一个字符的循环。确定了起始字符的有效性后，分别遍历该字符后面的字符和该节点的孩子节点进行比较，如果不相等则跳出该起始字符的循环；否则判断命中的孩子节点的set属性是否为-1，是的话, j和node继续后移比较；不是的话则对该节点对应的返回列表进行位置索引的扩充，然后再后移比较。
以及涉及索引的时候就尽量用下标表示元素。
## 复杂度分析
时间复杂度：建树的时间复杂度是O(an), a 是small中所有元素的平均长度，n是small中的元素个数；搜索的时间复杂度是所有命中子串的长度和。
空间复杂度：建立前缀树的复杂度，即O(m^n), m是字符集中字符的个数，n是small中的元素个数

```python
class TrieNode:
    def __init__(self):
        self.set = -1
        self.children = {}

class Solution:
    def __init__(self):
        self.root = TrieNode()
    def multiSearch(self,big,smalls):   
        res = []     
        for id,w in enumerate(smalls):
            node = self.root
            for s in w:
                if s not in node.children:
                    node.children[s] = TrieNode()
                node = node.children[s]
            node.set = id
            res.append([])
      
        for i in range(len(big)):
            node = self.root
            if big[i] not in node.children:
                continue
            for j in range(i,len(big)):
                if big[j] not in node.children:
                    break
                node = node.children[big[j]]
                if node.set != -1:
                    res[node.set].append(i)
        return res
```
