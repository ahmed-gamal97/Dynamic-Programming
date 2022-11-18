# May LeetCoding Challenge

1) https://leetcode.com/problems/fibonacci-number/ </br>
509. Fibonacci Number


```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N == 0:
            return 0
        
        fib_array = [0] * (N+1)
        
        fib_array[1] = 1
        
        for i in range(2, N+1):
            fib_array[i] = fib_array[i-1] + fib_array[i-2] 
        
        return fib_array[N]
    
```

### Complexity: O(n) , space: O(n)
----------------------
2) https://leetcode.com/problems/n-th-tribonacci-number </br>
1137. N-th Tribonacci Number

```python
class Solution:
    def tribonacci(self, n: int) -> int:
        
        tiponacci_dict = {0:0, 1:1, 2:1}
        
        for i in range(3, n+1):
            tiponacci_dict[i] = tiponacci_dict[i-1] + tiponacci_dict[i-2] + tiponacci_dict[i-3]
            
        return tiponacci_dict[n]

```
### Complexity: O(n) , space: O(n)
-----------------------
3) https://leetcode.com/problems/climbing-stairs/ </br>
70. Climbing Stairs
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        
        result = [0] * (n+1)
        result[0] = 1
        result[1] = 1
        
        for i in range(2, n+1):
            result[i] = result[i-1] + result[i-2]
            
        return result[n]
```
### Complexity: O(nlog(n)) , space: O(1)
-----------------------
4) https://leetcode.com/problems/min-cost-climbing-stairs </br>
746. Min Cost Climbing Stairs

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        
        length = len(cost)
        
        min_current_cost = [0] * length
        min_current_cost[0] = cost[0]
        min_current_cost[1] = cost[1]

        for i in range(2, length):
            min_current_cost[i] = min(min_current_cost[i-1], min_current_cost[i-2])
            min_current_cost[i] += cost[i]
            
        return min(min_current_cost[length-2], min_current_cost[length-1])
```
### Complexity: O(n) , space: O(n)