---
layout: post
title:  "Add Two Numbers"
date:   2022-02-03 15:00:00 -0800
categories: website
---

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Initial Brainstorm

First, we begin by illustrating an example that will help us understand the various cases we will run into, as well as the general procedure we want moving forward.

So, let our first list`l1 = 2 --> 4 --> 3` and our second list `l2 = 5 --> 6 --> 4`, representing the numbers `342` and `465` respectively. As the numbers we are given are reversed from their true values, adding from left to right (with respect to our lists) reflects naturally adding two numbers, starting from the ones place, then the tens, and so on. 

Therefore, adding our first values in `l1` and `l2`, we get that the ones place in our sum is `7` clearly. 

Moving on to `l1.next` and `l2.next` and taking the sum of their values, we get `10`. When adding usually, we leave the quantity `(l1.val + l2.val) % 10` in its respective place, and store a `1` to reflect the carry to our next “column” of significant digits. 

Adding the next set of values we get `7`, and remembering we have a carry value `carry = 1`, we get the final digit to be `8`. If we construct our linked list properly, we should have our output `out = 7 --> 0 --> 8`, reflecting the sum of `342 + 465 = 807`, reversed.

Now we look torward actually implementing the above process!

### Initial Solution

We will need some other list `root` where we store our added values for each “column” of addition done between values in `l1` and `l2`. Furthermore, we need to have some temporary node that allows us to append on `root` and create new nodes, as well as traverse alongside our additions, which we will call `curr`, reflecting the “current” node we are currently working to compute and append.

We will have a `carry` value defaulted to `0` that will be updated pending the sum of values we get from `l1` and `l2`, where:

1. `l1.val + l2.val < 10 --> carry = 0` 
2. and `l1.val + l2.val >= 10 --> carry = 1`

Where the `carry` value will maintain up until our next iteration in the loop and we compute our new `curr_sum`.

We now traverse through `l1` and `l2` as long as one of them are not `None` as it could be that `l1` is a digit with more significant digits than `l2`, or vice versa. This leads us to think that we should traverse `while l1 or l2`, or in other words, loop while `l1` OR `l2` are valid (i.e. not `None`).

We also have to think of the edge case that the if `l1` and `l2` are of the same length and their final addition greater than `10` necessitating a carry to a new tier of significant digits, so we think to having `while l1 or l2 or carry`, which allows our loops to continue if `carry = 1`.

Next, we actually compute the sum for each place of values represented in `l1` and `l2`! To add values in `l1` and `l2`, we must access their values. However, just as we precautioned earlier, `l1` could be of greater length than `l2` for example, thus trying to assign or view `l2.val` after making an `n = # of nodes in l2` amount of steps would leave us with `None` when in reality we want a leading `0` in front of our `l2`. This leads us to set our values `l2_val = l2.val if l2 else 0`, and vice versa. Succinctly, the line sets `l2_val` to `l2.val` if it actually exists and is valid, otherwise we set it to `0`.

Now we compute the sum `curr_sum` as described previously, keeping in mind the possible two cases that our sum could have with respect to needing a carry or not. 

From here, we append/update onto our `root` a new value reflecting the sum we have computed. When first working through it, I thought to have it such that we change `curr`'s value as we iterate through, and set `curr.next` to some dummy node that will be changed in the next iteration of our loop, and update `curr` to be our new dummy node just as in the below snippet:

```python
# ... code above ...#

curr.val = curr_sum
curr.next = ListNode(0)
curr = curr.next
```

We can see that once we are finished, our `root` will have a dummy node at the end of our linked list with value `0`, which is not what we want in the context of the problem although our logic is correct. So we maybe think to have our dummy node be at the front of our linked list, and update the next node during each iteration so that we can return `root.next` to get our linked list excluding our dummy node. 

Now that we have taken care of our sum, we move onto the next nodes in `l1` and `l2` if they exist, otherwise we assign `l1` or `l2` to `None`. Combining all of this, we have our solution:

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        root = ListNode(0)
        curr = root
        
        carry = 0
        
        while l1 or l2 or carry:
            l1_val = l1.val if l1 else 0
            l2_val = l2.val if l2 else 0
            
            curr_sum = l1_val + l2_val + carry
            if curr_sum >= 10:
                carry = 1
                curr_sum %= 10
            else:
                carry = 0
            curr.next = ListNode(curr_sum)
            curr = curr.next
            
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            
        return root.next
```
