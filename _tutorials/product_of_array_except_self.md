---
layout: post
title:  "Product of Array Except Self"
categories: website
---

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

### Proposed Brute Force Solution

For this problem the brute force solution is quite straight forward, namely a nested loop. Our logic is to have our output array `out` of the same length as `nums` consisting of `1`'s only. This allows us to update the product for each iteration `i`.  

Within our first loop, We iterate through our array `nums`, and for each element `nums[i]`, we iterate through our elements again in another loop and update our `out[i]` by multiplying all `out[j]` with `out[i]` where `i != j`. Once finished, we return our output array.

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
				out = [1]*len(nums)
				for i in range(len(nums)):
					for j in range(len(nums)):
							if i != j:
								out[i] *= nums[j]
				return out
```

### Working Toward a Better Solution

We can see that the problem requires a solution of `O(n)` time, whereas our solution above is of `O(n^2)`. So, it must be that we can do our desired operations without a nested loop.

As we need to be able to access elements before and after `nums[i]` to get our desired product, we maybe think toward having two arrays that have the product of all elements in our array before `nums[i]`, as well as for those after `nums[i]`. 

Now we think to how would we construct such arrays? 

We will first construct our `left` array, and using the same logic we can construct our `right` array.

It is intuitive to think that our `i`th element in our `left` array is the product of every element before our `i`th element in `nums` so that in the end we can multiply `left[i]*right[i]` to get the product of every element except the `i`th one. 

As `nums[0]` has no elements preceding it, there is no product to compute, so we let it equal `left[0] = 1`. As we iterate through from `1 --> len(nums)` we compute our `left[i]` by taking the product between `left[i-1]` and `nums[i-1]` , where the results are quite self-explanatory by construction of our solution.

We do the same exact for `right`, except we start from the end of the array, namely that `right[len(nums-1)] = 1` as the last element has no elements to the right of it to form a product with.  We traverse from `len(nums)-2 --> 0`, computing `right[i]` by taking the product between `right[i+1]` and `nums[i+1]`.

Now that we have our `left` and `right` arrays, we can iterate from `0 --> len(nums)-1` and multiply the two arrays to get our desired products and output array:

```python
 class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        left,right,out = [1]*len(nums), [1]*len(nums), [1]*len(nums)
        
        left[0] = 1
        
        for i in range(1,len(nums)):
            left[i] = left[i-1]*nums[i-1]
            
        right[-1] = 1
        
        for i in range(len(nums)-2, -1, -1):
            right[i] = right[i+1]*nums[i+1]
            
        for i in range(len(nums)):
            out[i] = left[i]*right[i]
            
        return out
```
