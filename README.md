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
