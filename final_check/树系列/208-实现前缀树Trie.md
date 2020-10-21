## 题目
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

示例:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true

## 思路
构建前缀树节点，属性有孩子结点和每个节点是否是结束字母的标志。创建前缀树类，init根节点为前缀树节点，应用于后面的函数定义。

## 代码
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isEnd = False


class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.root
        for w in word:
            #查询串里的每个字符查的时候需要依附的结点是不同的，所以需要一个node中间变量来代表不断更新的结点
            if w not in node.children:
                node.children[w] = TrieNode()
            node = node.children[w]
        node.isEnd = True


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.root
        for w in word:
            if w not in node.children:
                return False
            node = node.children[w]
        return node.isEnd


    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self.root
        for w in prefix:
            if w not in node.children:
                return False
            node = node.children[w]
        return True
```
