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

### Proposed Solution

This time, we are not going to be doing a brute force solution to improve our algorithm. Rather, we will work through why and how our algorithm works, and the thought process behind it.

The data structure of choice for this problem is a `Stack`, a data structure where the first element in, is the last element out. We want to do this as we traverse through our array, as we want to keep track of multiple parentheses while searching for their complements.

So, if suppose our algorithm works, and let’s work on some practice string ...

**TO BE CONTINUED**

We will initialize a dictionary associating closed parentheses characters with their open counterparts so we know what matches with what, as well as an empty stack to keep track of our parentheses.

Now iterating through `s`, if our current character `s[i]` is a key in our dictionary we have two options:

**TO BE CONTINUED**

So, here is our solution:

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
            if s[i] in paren_dict: # Check if s[i] is a key in paren_d
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
