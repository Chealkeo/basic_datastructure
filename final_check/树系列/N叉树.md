## 589-N叉树的前序遍历
## 代码
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        
        if not root: return []
        res = []
        def dfs(node):
            if not node: return
            res.append(node.val)
            for child in node.children:
                dfs(child)
        dfs(root)
        return res
```

## 590-N叉树的后序遍历
## 代码
```python
class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        res = []
        def dfs(node):
            if not node: return
            for child in node.children:
                dfs(child)
            res.append(node.val)
        dfs(root)
        return res
```

## 559-N叉树的最大深度
## 代码
```python
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0
        res = 0
        for child in root.children:
            res = max(res,self.maxDepth(child))
        return res+1
```

## 429-N叉树的层次遍历
## 代码
```python
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root: return []
        cur = [root]
        res = []
        while cur:
            lay, layer = [],[]
            for node in cur:
                layer.append(node.val)
                for _ in node.children:
                    lay.append(_)
            res.append(layer)
            cur = lay
        return res
```
