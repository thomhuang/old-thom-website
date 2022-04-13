---
layout: post
title:  "Valid Parentheses"
date:   2022-01-25 10:00:00 -0800
categories: website
---

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

### Initial Brainstorming

This time, we are not going to be doing a brute force solution to improve our algorithm. Rather, we will work through why and how our algorithm works, and the thought process behind it.

The data structure of choice for this problem is a `Stack`, a data structure where the first element in is the last element out. 

Let’s work on some practice string, let's say `()[]`. The instructions suggest that once we encounter an open parentheses, we should immediately expect a closed parenthese to be a valid string. 
This idea of keeping track of our open parentheses in search for their complements can be done with our `stack`, where every open parentheses gets added to our stack. Otherwise, we have hit a closed parenthese (or an invalid character) and *expect* our stack to contain its open counterpart. If it is not our expected compliment or an invalid character, we know to return `False`, and if not we continue this process. In the end if our stack is empty, we know that we have dealt with all potential pairs and have no invalid characters and we can return `True`.

We now work toward translating our mental algorithm to code.

### Solution

We will initialize a dictionary `paren_dict` associating closed parentheses characters with their open counterparts (implementing our mental "mapping" of open/closed parentheses) so we know what matches with what, as well as an empty stack to keep track as explained.

As we iterate through `s`, we know that once we run into an open parenthese `s[i]`, we add it to our stack expecting the next character `s[i+1]` to be its counterpart.

If our character `s[i+1]` is a key in our dictionary (essentially that we have run into a closed parenthetical) we have three options:
1. Our stack contains the desired open parenthese
2. Our stack contains some incorrect character
3. Our stack is empty, meaning we have run into a closed parenthetical without its complement.


So in cases (1) and (2), we want to pop our element out of the stack and assign it to some variable `curr` that we use as a check. In case (3) we know our stack is empty so there is nothing to pop, thus we can set our `curr` to some dummy value (in our case`'X'`). What this allows us to do is to check if our `curr` is not our desired open parenthese by checking if `paren_dict[s[i]] != curr`, and if so we return `False`

We continue this process until we have parsed through the entirety of `s`, and if our stack is empty, we know we have a valid string as all open parentheses have found their complements and have been popped from the stack accordingly, so we return `True` in that case.

This leads us to the below solution:

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # Dictionary associating closed parentheses with their open counterpart
        paren_dict = {")" : "(", "}" : "{", "]" : "["} 
        stack = [] #Initialize an empty stack
        for i in range(len(s)): # Iterate through our string s
            if s[i] in paren_dict: # Check if s[i] is a key in paren_dict
                if stack:              # If our stack is not empty,
                    curr = stack.pop() # we set curr to be the top element
                else:                  # Otherwise we set it to a dummy value
                    curr = "X"         # as that means 
                if paren_dict[s[i]] != curr: # If we have no corresponding
                        return False
            else:
                stack.append(s[i])
        return not stack
```
