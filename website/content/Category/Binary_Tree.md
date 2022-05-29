# [Binary Tree](https://leetcode.com/explore/learn/card/data-structure-tree/134/traverse-a-tree/)

```python
class TreeNode(object):
    """ Definition of a binary tree node."""
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```
**所有recursion问题，设计一个trav function with param root，result[]。在trav里首先if root == None return。**

## Pre-order Traversal
中左右

### 思路

DFS Top->Bottom Left->Right

     1
    / \
   2   5
  / \
 3   4

- **stack先放进root,所以先确保root is not None**，while（stack）

- while 内部 **三个if， 先右后左**

- if （root is not None） pop root， 加进res

- if （root.right is not None） stack append

- if （root.left is not None） stack append

* [144. Binary Tree Preorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0100~0199/0144.Binary-Tree-Preorder-Traversal.md)

## In-oreder Traversal
左中右

### 思路
**因为我们一直从stack里面append，不需要if， 只用一个while curr来检测None**

- curr指针到root

- **空白stack**，空白result

- while （curr or stack）

    - while curr 指针从root开始先挪到树的最左下角，过程中stack append

    - curr = stack pop（）

    - append curr to res

    - curr = curr.right

* [94. Binary Tree Inorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0001~0099/0094.Binary-Tree-Inorder-Traversal.md)