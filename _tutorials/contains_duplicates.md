---
layout: page
title: Contains Duplicates
description: Array
---

# Contains Duplicates

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct. 

### Proposed Brute Force Solution

My initial idea for a brute force solution was to first iterate through our `nums` , and for each iteration `i` , iterate through all elements placed after `nums[i]` and if there is a match, return `True`, indicating we’ve found a duplicate. If not continue this process and return `False` when you have iterated through `nums` in its entirety.

Below is the solution in Python (Time Limit Exceeded) with a time complexity of O(N<sup>2</sup>):

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        for i in range(len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i] == nums[j]:
	                  return True
        return False
```

In the first loop, you can see that we traverse from `0 --> len(nums)-2` instead of the full length of the array. This is because we check all values after the i<sup>th</sup> element, and we don’t want to go out of bounds of the array.

# Working toward a better solution

Let’s first inspect our brute force solution and see where we can improve on it. So, let’s first explain what each section of our code does:

1. `for i in range(len(nums-1)):` Here we traverse through all of our elements minus the last element in the order it was placed in `nums`. 
2. `for j in range(i+1, len(nums)):` Here we traverse through all the elements placed after the i<sup>th</sup> element
3. `if nums[i] == nums[j]:` Here we if the  j<sup>th</sup> element is identical to the i<sup>th</sup>.

My approach is to first think about this as simply as I can while trying to improve our algorithm. We can see our first loop accesses our elements, so let us not change that. 

Looking at our second loop, this is where we search for the desired values, i.e. the duplicated values. Thinking about the problem a bit, we can see that we can easily know if we have duplicates of integers if we sort the array initially. It allows us to iterate through as in our first loop, and check if the i<sup>th</sup> and i<sup>th</sup> element matches such as:

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        nums.sort()
        for i in range(len(nums)-1):
        if nums[i] == nums[i+1]:
              return True
        return False
```

Where the sorting takes O(logN), meaning our algorithm has sped up a bit with a time complexity of O(logN).

### My Most Optimal Solution

Thinking about this problem a bit mathematically was helpful for me. After a bit of staring, I realized that if our `List` contained duplicates, the length of the `Set` of our elements will be less than that of the list, so we can solve the problem as such:

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) == len(set(nums)):
                return False
        return True
```

I’m not too sure of the time complexity of converting our `List` to a `Set`, but I would not expect anything more than `O(N)`

There is also a less trivial solution that we have, namely working with hashmaps. Our idea is to traverse through our array `nums`, and add our element `nums[i]` to our hashmap corresponding to some dummy value, let's say `1`. Before we add each element to our hashmap, we can check if our element is *already* in the hashmap, and if so we know we have run into a duplicate value, thus we return `True`. If we iterate through the entirety of `nums` without running into such case, we return `False`. 

This gives the below solution:

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        
        hashmap = {}
        for i in range(len(nums)):
            if nums[i] in hashmap:
                return True
            hashmap[nums[i]] = 1
        return False
```
