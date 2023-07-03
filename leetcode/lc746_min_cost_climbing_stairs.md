# LC746. Min Cost Climbing Stairs

- Difficulty: Easy
- Type: Array, DP

## Question

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.

**Example 1:**

Input: cost = [10,15,20]

Output: 15

Explanation: You will start at index 1.

- Pay 15 and climb two steps to reach the top.

The total cost is 15.

**Example 2:**

Input: cost = [1,100,1,1,1,100,1,1,100,1]

Output: 6

Explanation: You will start at index 0.

- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.

The total cost is 6.

**Constraints:**

- 2 <= cost.length <= 1000
- 0 <= cost[i] <= 999

## Solution

- Time complexity: `O(cost.length)`
- Space complexity: `O(cost.length)`

### Train of Thought

The minimum cost of reaching `ith` step is the minimum cost of reaching `i-1th` step plus cost of `i-1th` step and minimum cost of reaching `i-2th` step plus cost of `i-2th` step. We can use tabulation (bottom up) to solve.

#### Alternative method

We can use recursion and memoization (top down) to solve. However, memory is allocated on the stack which contains local variables, which cause space complexity to be `O(cost.length^2)` ($\sum_{n=1}^{cost.length} n = \frac{cost.length}{2}(2+cost.length-1)$).

### Python

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        min_costs = [-1] * (len(cost) + 1)
        min_costs[0] = min_costs[1] = 0

        for i in range(2, len(cost)+1):
            min_costs[i] = min(min_costs[i-1] + cost[i-1], min_costs[i-2] + cost[i-2])

        return min_costs[-1]
```

#### Alternative method

```python
class Solution:
    def minCostClimbingStairsHelper(self, cost: List[int]) -> int:
        if len(cost) < 2:
            return 0
            
        if len(cost) not in self.min_cost_memo:
            min_cost1 = self.minCostClimbingStairsHelper(cost[:len(cost)-1]) + cost[-1]
            min_cost2 = self.minCostClimbingStairsHelper(cost[:len(cost)-2]) + cost[-2]
            self.min_cost_memo[len(cost)] = min(min_cost1, min_cost2)

        return self.min_cost_memo[len(cost)]

    def minCostClimbingStairs(self, cost: List[int]) -> int:
        self.min_cost_memo = {}
        
        return self.minCostClimbingStairsHelper(cost)
```
