---
layout: page
title: Maximum Subarray
description: Array
---

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

A **subarray** is a **contiguous** part of an array.

### Proposed Brute Force Solution

My initial idea for a brute force solution was to first iterate through our `nums`, and for each iteration `i`, we initialize our sub-array’s sum, `curr_sum` , for the sub-array from `i --> len(nums)-1`. 

We iterate again, but through all the elements from `nums[i]` onward and compute each sub-array’s sum while keeping track of the maximum sum `max_sum` from some subarray. Return `max_sum`. 

Below is the solution in Python (Time Limit Exceeded) with a time complexity of O(N<sup>2</sup>):

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_sum = -10E10
        for i in range(len(nums)):
            curr_sum = 0
            for j in range(i, len(nums)):
                curr_sum += nums[j]
                max_sum = max(max_sum, curr_sum)
        return max_sum
							
```

### Working Toward a Better Solution

Let’s first inspect our brute force solution and see where we can improve on it. So, let’s first explain what each section of our code does after initializing our `max_sum`:

1. `for i in range(len(nums)):` Here we traverse through all of our elements in the order it was placed in `nums` and initialize the running sum of the sub-arrays from `i --> len(nums)-1`
2. `for j in range(i, len(nums)):` Here we traverse through all the elements from the i<sup>th</sup> element onward, and keep track of the running sum with `curr_sum`. If our current subarray’s sum is greater than the curent `max_sum`, we change the value

We can see that we really only have one option to improve our algorithm, namely the second loop, as we must pass through our array at the very least to compute the sums.

After some deliberating, notice that the second loop is not exactly necessary! 

For each iteration in the loop, we check if `nums[i] > curr_sum`  (if the current element is greater than the previous subarray’s sum), and if so, we start our subarray from a new position, namely the element we are at. 

If this new `curr_sum` is greater than the last `max_sum` we update the value.

This gives us our updated algorithm, with time complexity O(N).

```python
class Solution(object):
    def maxSubArray(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
        curr_sum = nums[0]
        max_sum = nums[0]
        for i in range(1, len(nums)):
                curr_sum = max(curr_sum + nums[i], nums[i])
                max_sum = max(max_sum, curr_sum)
        return max_sum
```

[](https://www.notion.so/1861de3b264a4fa5953b3038ae33d162)
