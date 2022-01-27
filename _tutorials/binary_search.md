# Binary Search

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

### Proposed Solution

We can see that the instructions nudge us in the right direction by mandating an algorithm with an `O(log n)` time complexity. As a result, we need to continually divide our list of elements by two to conform to the constraint.

So, we first discuss the general idea of our algorithm. We will initiate two pointers, namely `left`   and `right` that will keep track of the left and right boundaries of our lists. Then, so long as `left≤right`, we can continually cut our lists until we reach the stopping point of `left>right`.

Now we try to see what determines which half of the list we take between each iteration. What we’ll try to do is look at the midpoint `mid` between our `left` and `right` and determine if `nums[mid]` is our desired element. If so, we’re done and we can return! Our target element being less than our element `nums[mid]` implies that our desired element is to be between `[left, mid)`. If our target element is greater than `nums[mid]`, we know that our desired element is within the indice range of `(mid, right]`. 

If we don’t find such an element at all, we return `-1`.

So now this leads us to our written algorithm with a runtime complexity of `O(log n)`:

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
				left = 0                           # Start at beginning of nums
				right = len(nums) - 1              # Start at the end of nums
                              
				while left <= right: 
            mid  = left + (right-left)//2  # Midpoint of our search window
																					 
            if nums[mid] == target:        # If we find our target, return mid
                return mid 
            elif target < nums[mid]:       # If not, cut size of search in 
                right = mid - 1            # either direction
            else:
                left = mid + 1            
        return -1
```

We could either use `mid = left + (right - left) // 2` or `mid = (right + left) // 2` for computing our midpoint, however I’ve learned that although it is not necessary for Python, it is overall better practice to use the former as the latter can lead to overflow.