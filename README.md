# basic_datastructure

## 输入输出
自己实现输入输出时，要看清楚题目给的输入的字符串形式，读入字符串后，可以通过split('分割字符')将字符串改成包含字符串元素的列表；（strip()操作是去掉两端的空白符）

如果是数字操作，记得int()作类型转换；
可以使用map函数，如：
输入: [2,1,5,6,2,3]
输出: 10
```python
if __name__ == '__main__':
    k = input()
    k = k[1:len(k)-1]
    s = list(map(int,k.strip().split(',')))
    print(s)
    sl = Solution()
    ans = sl.largestRectangleArea(s)
    print(ans)
```
## 包含类方法调用的输入输出python实现
输入：
["Trie","insert","search","search","startsWith","insert","search"]
[[],["apple"],["apple"],["app"],["app"],["app"],["app"]]
输出：
[null,null,true,false,true,null,true]
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
