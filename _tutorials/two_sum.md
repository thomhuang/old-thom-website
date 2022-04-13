---
layout: page
title: Two Sum
date:   2022-01-14 15:00:00 -0800
description: Array
---

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

### Proposed Brute Force Solution

The most obvious approach for a brute force solution in my eyes was to first iterate through our `nums`, and for each iteration `i` , iterate and search for some `nums[j]` such that `nums[i] + nums[j] == target` and return the indices if found (as there is exactly one solution). We’ll return the empty list otherwise.

So, below is the accepted proposed solution with a time complexity of O(N<sup>2</sup>):

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
		for i in range(len(nums)):
        for j in range(len(nums)):
            if i != j and nums[i] + nums[j] == target:
                return [i,j]
    return []
```

You can see that in our if-statement we check if `i != j` as you may not use the same element twice.

### Working toward a better solution

We can see that at the very least we need to traverse through our elements, so there is not much we can do about the first loop. However, there may be a better way in which we can search for our desired value. 

As we pass through our elements with each iteration `i`, instead of looking at elements (not `nums[i]`) that could add up to `target`, why don’t we search for the specific element we want by searching for some`to_find = target - nums[i]`! If we cannot find such value, we move on to the next iteration of `i` and repeat the process:

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
		for i in range(len(nums)):
		    to_find = target - nums[i]
		    if to_find in nums:
			      idx = nums.index(to_find)
		        if i != idx:
		            return [i, nums.index(to_find)]
		return []
```

### My Most Optimal Solution

After studying and looking to the problem a bit more, another way to go about this is to use a Hash Map by associating each element to their position in `nums` to keep track of our elements; the general approach is to search for our addends as we populate our Hash Map. 

So, we first traverse our array and compute  `to_find` for our `nums[i]`. If our Hash Map contains such a value, we return it. Otherwise, we add add `nums[i]` and its position to our hashmap and repeat our process. 

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
		hashmap = {}
		for i in range(len(nums)):
		    to_find = target - nums[i]
		    if to_find in hashmap and hashmap[to_find] != i:
						return [i, hashmap[to_find]]
				hashmap[nums[i]] = i
		return []
```


