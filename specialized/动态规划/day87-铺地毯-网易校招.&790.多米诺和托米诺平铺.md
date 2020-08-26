## 题目描述
牛牛有一块 2 * n 的空白瓷砖，并且有 1 * 2 和 2 * 3 两种类型的地毯（地毯可以旋转）。现在他想满足以下条件：

瓷砖需要被铺满
地毯之间没有重叠
地毯不能铺出瓷砖外
求一共有多少种铺地毯的方案，由于结果可能很大，因此你需要返回结果取模 10007。

## 思路
长度为n的瓷砖的铺法取决于n-1, n-2, n-3三种之前的情况  
去除三种情况里的重复方案，可以得到状态转移方程其实就是三种之前长度方案的和。  
`补的部分一定要不可从某列中间断开，否则会重复！比如两个竖着放的多米诺这种补法一定会和上面的一个竖着的方案重复`

## 复杂度分析
时间复杂度：O(N)  
空间复杂度：O(1)
```python
def floordes(n):
    a = 1
    b = 2
    c = 4
    if n==1: return a
    if n==2: return b
    if n==3: return c
    for i in range(4,n+1):
        tmp = a+b+c
        a = b
        b = c
        c = tmp
    return tmp%10007
```

790.多米诺和托米诺平铺
https://leetcode-cn.com/problems/domino-and-tromino-tiling/
## 思路
主要在于状态转移方程的建立，这里与一般题目不太一样的是，托米诺牌的特殊性，由于托米诺牌的存在，dp[i]可以由任意一个dp[i-x](x=3,4,5,...,i)唯二地得到,  
即此时的状态转移方程应该是dp[i] = dp[i-1]+dp[i-2]+(dp[i-3]+dp[i-4]+...+dp[0])*2  
dp[i-1] = dp[i-2]+dp[i-3]+(dp[i-4]+...+dp[0])*2  
dp[i] = dp[i-1]+dp[i-2]+dp[i-3]-dp[i-2]+dp[i-1] = 2*dp[i-1]+dp[i-3]  
## 复杂度分析
时间复杂度O(N)
空间复杂度O(1)
## 代码
```python
class Solution:
    def numTilings(self, N: int) -> int:
        if N ==1: return 1
        if N ==2: return 2
        if N ==3: return 5
        a,b,c = 1,2,5
        for i in range(4,N+1):
            a,b,c = b,c,a+2*c
        return c%(10**9+7)
```
## 一定要从问题本身出发，不要被惯性思维框住，要准确分析到达每一个状态可以采取的之前的所有状态。
