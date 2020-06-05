请你设计一个支持下述操作的栈。

实现自定义栈类 CustomStack ：

CustomStack(int maxSize)：用 maxSize 初始化对象，maxSize 是栈中最多能容纳的元素数量，栈在增长到 maxSize 之后则不支持 push 操作。
void push(int x)：如果栈还未增长到 maxSize ，就将 x 添加到栈顶。
int pop()：弹出栈顶元素，并返回栈顶的值，或栈为空时返回 -1 。
void inc(int k, int val)：栈底的 k 个元素的值都增加 val 。如果栈中元素总数小于 k ，则栈中的所有元素都增加 val 。

提示：
1 <= maxSize <= 1000
1 <= x <= 1000
1 <= k <= 1000
0 <= val <= 100
每种方法 increment，push 以及 pop 分别最多调用 1000 次

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/design-a-stack-with-increment-operation
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


#我的基本解法，时间复杂度为O（n），n为进行增量操作的元素规模。空间复杂度为O(1),未借用辅助空间
```python
class CustomStack(object):

    def __init__(self, maxSize):
        """
        :type maxSize: int
        """
        self.stack = [0]*maxSize
        self.top = -1


    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        if self.top != len(self.stack) - 1:
            self.top += 1
            self.stack[self.top] = x
        else:
            print("stack is full!")



    def pop(self):
        """
        :rtype: int
        """
        if self.top == -1:
            return -1
        else:
            self.top -= 1
            return self.stack[self.top+1]


    def increment(self, k, val):
        """
        :type k: int
        :type val: int
        :rtype: None
        """
        n = min(k,self.top+1)
        for i in range (n):
            self.stack[i] += val



# Your CustomStack object will be instantiated and called as such:
# obj = CustomStack(maxSize)
# obj.push(x)
# param_2 = obj.pop()
# obj.increment(k,val)
```


#lucifer的优化解法，时间复杂度为O(1)，空间复杂度为O(n)，所有元素都只进行了常数次操作，n是栈在操作中的最大长度。
```python
class CustomStack(object):

    def __init__(self, maxSize):
        """
        :type maxSize: int
        """
        self.stack = []
        self.cnt = 0
        self.incstk = []
        self.maxSize = maxSize


    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        if self.cnt < self.maxSize:
            self.cnt += 1
            self.stack.append (x)
            self.incstk.append(0)
        else:
            print("stack is full!")



    def pop(self):
        """
        :rtype: int
        """
        if self.cnt <= 0:
            return -1
        self.cnt -= 1
        if self.cnt >= 1:
            
            self.incstk[-2] += self.incstk[-1]//选择元素对元素进行操作
        return self.stack.pop() + self.incstk.pop()//删除元素


    def increment(self, k, val):
        """
        :type k: int
        :type val: int
        :rtype: None
        """
        n = min(k,self.cnt)
        if self.incstk:
            self.incstk[n-1] += val
```      
