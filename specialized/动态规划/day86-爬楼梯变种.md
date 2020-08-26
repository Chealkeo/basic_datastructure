
746.使用最小花费爬楼梯
https://leetcode-cn.com/problems/min-cost-climbing-stairs/
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
		#爬到楼顶有两种方案，一种是从n-2爬上去，一种是从n-1爬上去，所以最后返回的是最后两个花费的最小值（`可以不踏上最后一层，只要走到楼顶也就是走过最后一层即可，所以可以是走到最后一层也可以是走到倒数第二层`）。
        n = len(cost)
        dp = [float('inf')]*(n)
        dp[0] = cost[0]
        dp[1] = cost[1]
        for i in range(2,n):
            dp[i] = min(dp[i-1],dp[i-2])+cost[i]
        return min(dp[-1],dp[-2])
```
746变种.使用最小花费爬楼梯:
已知有一个 n 级的台阶，我们的目标是走到第 n 级，但是踩到不同的台阶需要耗费不同的你能量，我们用 enegy 数组 来表示。  
其中 enegy[i] 表示爬到 第 i 级台阶需要掉的能量。我们可以一次走一级或者一次走两级。 求走到第 n 级需要的最少能量(`意味着最后一层必须走，所以最后返回最后一个元素即可`)。

输入：
[1,2,3,4]

输出:
6

解释：
我们先一次走两级，走到 i = 1 的位置，此时需要耗费 2 的能量，接着我们再走两级，此时需要 4。 2 + 4 = 6
```python
class Solution:
    def minCostClimbingStairs(self, energy: List[int]) -> int:
				n = len(energy)
				#需要考虑n不大于2的情况
				if n<=2:
						return energy[-1]
				dp = [float('inf')]*n
				dp[0] = energy[0]
				dp[1] = energy[1]
				for i in range(2,n):
						dp[i] = min(dp[i-1],dp[i-2])+energy[i]
				return dp[-1]
```
