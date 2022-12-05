# Dynamic Programming

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
-----------------------
5) https://leetcode.com/problems/house-robber/ </br>
198. House Robber

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        length = len(nums)
        
        if length == 1:
            return nums[0]
        
        maximum_amount_till_now = [0] * length
        maximum_amount_till_now[0] = nums[0]
        maximum_amount_till_now[1] = max(nums[0], nums[1])
        
        for i in range(2, length):
            if maximum_amount_till_now[i-1] == maximum_amount_till_now[i-2]:
                maximum_amount_till_now[i] = maximum_amount_till_now[i-1] + nums[i]
            else:
                maximum_amount_till_now[i] = max(maximum_amount_till_now[i-2] + nums[i], maximum_amount_till_now[i-1])
    
        return maximum_amount_till_now[-1]
```
### Complexity: O(n) , space: O(n)
-----------------------
6) https://leetcode.com/problems/house-robber-ii/ </br>
213. House Robber II

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
             
        length = len(nums)
        
        if length == 1:
            return nums[0]
        elif length == 2:
            return max(nums[0], nums[1])
        
        def linear_rob(nums):
            
            length = len(nums)
            
            maximum_amount_till_now = [0] * length
            maximum_amount_till_now[0] = nums[0]
            maximum_amount_till_now[1] = max(nums[0], nums[1])

            for i in range(2, length):
                if maximum_amount_till_now[i-1] == maximum_amount_till_now[i-2]:
                    maximum_amount_till_now[i] = maximum_amount_till_now[i-1] + nums[i]
                else:
                    maximum_amount_till_now[i] = max(maximum_amount_till_now[i-2] + nums[i], maximum_amount_till_now[i-1])

            return maximum_amount_till_now[-1]
        
        
        return max(linear_rob(nums[1:]), linear_rob(nums[0:-1]))
        
```
### Complexity: O(n) , space: O(n)
-----------------------
7) https://leetcode.com/problems/delete-and-earn/ </br>
740. Delete and Earn

```python
class Solution:
    def deleteAndEarn(self, nums: List[int]) -> int:
        
        maximum_points = 0
        
        # counting the numbers
        num_freq = {}
        for num in nums:
            num_freq[num] = num_freq.get(num, 0) + 1
        
        # add numbers that will be added in any case and delete it from the dict
        for num in nums:
            if (num+1) not in num_freq and (num-1) not in num_freq:
                if num in num_freq:
                    maximum_points += (num*num_freq[num])
                    del num_freq[num]

        sorted_unique_num = sorted(num_freq.keys())
        
        length = len(sorted_unique_num)
        
        if length == 0:
            return maximum_points
        
        maximum_amount_till_now = [0] * length
        maximum_amount_till_now[0] = sorted_unique_num[0] * num_freq[sorted_unique_num[0]]
        maximum_amount_till_now[1] = sorted_unique_num[1] * num_freq[sorted_unique_num[1]]
        maximum_amount_till_now[1] = max(maximum_amount_till_now[0], maximum_amount_till_now[1])
        
        for i in range(2, length):
            if sorted_unique_num[i-1] + 1 == sorted_unique_num[i]:
                maximum_amount_till_now[i] = (sorted_unique_num[i] * num_freq[sorted_unique_num[i]]) + maximum_amount_till_now[i-2]
                maximum_amount_till_now[i] = max(maximum_amount_till_now[i], maximum_amount_till_now[i-1])
            else:
                maximum_amount_till_now[i] = (sorted_unique_num[i] * num_freq[sorted_unique_num[i]]) + maximum_amount_till_now[i-1]
        
        return maximum_amount_till_now[-1] + maximum_points
        
```
### Complexity: O(nlog(n)) , space: O(n)
-----------------------
8) https://leetcode.com/problems/jump-game/ </br>
55. Jump Game

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        
        # Samrter
        length = len(nums)
        max_reach = 0
        
        for ind, num in enumerate(nums):
            if max_reach < ind:
                return False
            elif max_reach >= length-1:
                return True
            max_reach = max(max_reach, ind+num)
        
        
        # First Accepted Sol
        length = len(nums)
        
        if length == 1:
            return True
        
        if nums[0] == 0:
            return False
        
        can_be_reached = [0] * length
        can_be_reached[0] = 1
        
        for ind,num in enumerate(nums[:-1]):
            
            if can_be_reached[ind] == 0:
                return False
            
            for i in range(ind+1, ind+1+num):
                if i < length:
                    can_be_reached[i] = 1
                else:
                    break
            
            if can_be_reached[length - 1] == 1:
                return True
        
        
        return False
        
```
### Complexity: O(n) , space: O(1)
-----------------------
9) https://leetcode.com/problems/jump-game-ii/ </br>
45. Jump Game II

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        
        # First Accepted Sol
        length = len(nums)
        
        # The test cases are generated such that you can reach nums[n - 1]
        # if nums[0] == 0:
        #     return False
        
        min_jumps_can_be_reached = [float('inf')] * length
        min_jumps_can_be_reached[0] = 0
        
        for ind,num in enumerate(nums[:-1]):
            
            for i in range(ind+1, ind+1+num):
                if i < length:
                    min_jumps_can_be_reached[i] = min(min_jumps_can_be_reached[i], min_jumps_can_be_reached[ind] + 1)
            
            if min_jumps_can_be_reached[length-1] < float('inf'):
                return min_jumps_can_be_reached[length-1]
            
        return min_jumps_can_be_reached[length-1]
```
### Complexity: O(n) , space: O(n)
-----------------------
10) https://leetcode.com/problems/maximum-subarray/ </br>
53. Maximum Subarray

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        if not nums:
            return 0
        
        length = len(nums)
        
        dp = [0] * length
        dp[0] = nums[0]
        
        
        for i in range(1, length):
            dp[i] = max(nums[i], dp[i-1] + nums[i])
            
            
        return max(dp)
        
```
### Complexity: O(n) , space: O(n)
-----------------------
11) https://leetcode.com/problems/maximum-sum-circular-subarray/ </br>
918. Maximum Sum Circular Subarray

```python
class Solution(object):
    def maxSubarraySumCircular(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
    
        def maxSubArray(nums):

            if not nums:
                return 0

            length = len(nums)

            dp = [0] * length
            dp[0] = nums[0]

            for i in range(1, length):
                dp[i] = max(nums[i], dp[i-1] + nums[i])

            return max(dp)
        
        # SOL 2
        length = len(nums)
        
        nums_sum = sum(nums)
        
        count_negative_nums = sum([1 if num < 0 else 0 for num in nums])
        if count_negative_nums == length:
            return max(nums)
        
        nums_inverted = [num*-1 for num in nums]
        dp = [0] * length
        dp[0] = nums_inverted[0]
        
        for i in range(1, length):
            dp[i] = max(nums_inverted[i], dp[i-1] + nums_inverted[i])
        
        return max(nums_sum - (-max(dp)), maxSubArray(nums))
    
        # SOL 1 but TLE
        length = len(nums)
        
        result = float('-inf')
        
        for i in range(length):
            result = max(result, maxSubArray(nums[i:length] + nums[:i]))
            
        return result
```
### Complexity: O(n) , space: O(n)
-----------------------
12) https://leetcode.com/problems/maximum-length-of-subarray-with-positive-product/ </br>
1567. Maximum Length of Subarray With Positive Product

```python
class Solution(object):
    def getMaxLen(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        nums_splitted = [[]]
        
        for ind, num in enumerate(nums):
            if num == 0:
                if nums_splitted[-1]:
                    nums_splitted.append([])
            else:
                nums_splitted[-1].append(num)
        
        # case when last element is 0
        if not nums_splitted[-1]:
            nums_splitted = nums_splitted[:-1]
        
        if not nums_splitted:
            return 0
        
        nonzeros_subarray_max_product_len = []
        
        for num_array in nums_splitted:
            
            negatives_indcies = [ind for ind,num in enumerate(num_array) if num < 0]
            
            negatives_count = len(negatives_indcies)
            
            if negatives_count % 2 == 0:
                nonzeros_subarray_max_product_len.append(len(num_array))
            else:
                
                if negatives_indcies[0] < len(num_array) - 1 - negatives_indcies[-1]:
                    ind_to_exclude = negatives_indcies[0]
                    nonzeros_subarray_max_product_len.append(len(num_array[ind_to_exclude+1:]))
                else:
                    ind_to_exclude = negatives_indcies[-1]
                    nonzeros_subarray_max_product_len.append(len(num_array[0: ind_to_exclude]))
                
        return max(nonzeros_subarray_max_product_len)
        
```
### Complexity: O(n) , space: O(n)
-----------------------
13) https://leetcode.com/problems/maximum-product-subarray/ </br>
152. Maximum Product Subarray   

```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        '''
        Why do we need to maintain the minimum product while we are asked for a maximum? The fact is that elements in nums can be negative, so it isi possible that for some negative elements the previous min possible product can turn the current product into a greater value.
        '''
        
        curr_min = 1
        curr_max = 1
        
        res = nums[0]
        
        for n in nums:
            
            vals = (n , curr_min*n, curr_max*n)
            
            curr_min = min(vals)
            curr_max = max(vals)
            
            res = max(res, curr_max)
            
        return res
        
```
### Complexity: O(n) , space: O(n)
-----------------------