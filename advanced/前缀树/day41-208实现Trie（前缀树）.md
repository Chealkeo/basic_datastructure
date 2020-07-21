## 问题
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。
示例:
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple"); // 返回 true
trie.search("app"); // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");
trie.search("app"); // 返回 true
说明:

你可以假设所有的输入都是由小写字母 a-z 构成的。
保证所有输入均为非空字符串。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/implement-trie-prefix-tree

## 思路：
构建前缀树节点，属性有孩子结点和每个节点是否是结束字母的标志。创建前缀树类，init根节点为前缀树节点，应用于后面的函数定义。
## 复杂度分析：
插入、搜索和前缀查询的时间复杂度都是O(n), n是要操作的单词的长度。
查询和搜索的空间复杂度均为O(1)，插入操作的空间复杂度为O(mn)，m是字符集中的字符个数，n是要操作的单词的长度。要操作的单词的每个字母节点都会产生m个子节点。

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isEnd = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for s in word:
            if s not in node.children:
                node.children[s] = TrieNode()
            node = node.children[s]
        node.isEnd = True

    def search(self,word):
        node = self.root
        for s in word:
            if s not in node.children:
                return False
            node = node.children[s]
        return node.isEnd

    def startsWith(self, prefix):
        node = self.root
        for s in prefix:
            if s not in node.children:
                return False
            node = node.children[s]
        return True
```
## leetcode输入输出的python实现
```python
if __name__ == '__main__':
    op1 = input().replace('\"','')
    op1 = op1[1:len(op1)-1].split(',')
    op2 = input().replace('\"','').replace('[','').replace(']','')
    op2 = op2[:len(op2)-1].split(',')
    
    if op1[0]=="Trie":
        trie = Trie()
        output=[None]
        for i in range(1,len(op1)):    
            #反射
            #opt = getattr(trie,op1[i])(op2[i]) 
            #字典
            dic = {'insert':trie.insert,'search':trie.search,'startsWith':trie.startsWith}
            opt = dic.get(op1[i])(op2[i])
            output.append(opt)
        print(output)
```
