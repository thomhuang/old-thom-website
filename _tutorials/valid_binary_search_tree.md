---
layout: post
title:  "Valid Binary Search Tree"
categories: website
---

A binary search tree is a binary tree with the property that any of its node's value is greater than or equal to *any* node in its left subtree and less than or equal to *any* node's value in its right subtree.

Given a binary tree, determine whether it is a binary search tree.

### Initial Ideas

While going through this problem, I know from my own experience that the most tempting first step was performing a DFS, and checking if their left and right children are less than and greater than the current node respectively, such as the below code snippet:

```python
class Node: # Node definition
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def valid_bst(root):
    if not root:
        return True
    if root.left:
        if root.left.val > root.val:
            return False
    if root.right:
        if root.right.val < root.val:
            return False
            
    return valid_bst(root.left) and valid_bst(root.right)
```

At first glance this may seem like the correct procedure, however we’ll show that this is not the case through an example.

After running our above algorithm on the above binary tree, notice that the way we have it structured, it would return true, although the tree is invalid as the `7` should have traversed down the right of the root node as we only check their children, but not the value conditions of the previous sub-trees!

Let me illustrate this with an example. Let us call some node `A`, and let it have left child `B` and right child `C`. We know that `B` must be less than `A`, or in other words, `A` serves as an upper bound for the value of `B`, and its lower limit is the same as `A`'s. The same logic applies to the right child `C`.

### Working Solution

To implement what was described in the previous section, we can transfer the bounds information from parent to child through the parameters of our dfs function as such:

```python
class Node: # Node definition
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def valid_bst(root):
		def bst(root, lower_limit, upper_limit):
            if not root:
                return True
            if root.val < lower_limit or root.val > upper_limit:
                return False
        return bst(root.left, lower_limit, root.val) and bst(root.right, root.val, upper_limit)

    return bst(root, float('-inf'), float('inf'))
```

Which is our final solution!
