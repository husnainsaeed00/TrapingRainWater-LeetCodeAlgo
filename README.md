# TrapingRainWater-LeetCodeAlgo

Given an elevation map represented by an array of non-negative integers height, where the width of each bar is 1, we need to compute how much water it can trap after raining.

Example
Input: height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]


Explanation: The above elevation map (black section) is represented by the array [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]. In this case, 6 units of rainwater (blue section) are being trapped.

Solution Approach
We can use a two-pass approach to compute the trapped water. In the first pass, we calculate the maximum height from the left at each index and store it in an array left_max. Similarly, in the second pass, we calculate the maximum height from the right at each index and store it in an array right_max.

Next, we iterate through the height array and for each index i, the amount of water trapped at that index is given by min(left_max[i], right_max[i]) - height[i]. We sum up the trapped water at each index to get the total trapped water.

## Implementation

class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0
        
        n = len(height)
        left_max = [0] * n
        right_max = [0] * n
        trapped_water = 0
        
        left_max[0] = height[0]
        for i in range(1, n):
            left_max[i] = max(left_max[i-1], height[i])
        
        right_max[n-1] = height[n-1]
        for i in range(n-2, -1, -1):
            right_max[i] = max(right_max[i+1], height[i])
        
        for i in range(n):
            trapped_water += min(left_max[i], right_max[i]) - height[i]
        
        return trapped_water
## Complexity Analysis
Time Complexity: O(N) - We perform two passes over the height array to calculate the maximum heights from the left and right side at each index.
Space Complexity: O(N) - We use additional space to store the left_max and right_max arrays.
This solution efficiently calculates the trapped water for the given elevation map and satisfies the linear runtime complexity and constant extra space requirements.
