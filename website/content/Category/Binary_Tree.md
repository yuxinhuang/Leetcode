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

DFS Preorder Top->Bottom Left->Right
```
     1
    / \
   2   5
  / \
 3   4

```
- **stack先放进root,所以先确保root is not None**，while（stack）

- while 内部 **三个if， 先右后左**

- if （root is not None） pop root， 加进res

    - if （root.right is not None） stack append

    - if （root.left is not None） stack append

* [144. Binary Tree Preorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0100~0199/0144.Binary-Tree-Preorder-Traversal.md)

## In-order Traversal
左中右

### 思路

DFS Inorder Left->Node->Right
```
     4
    / \
   2   5
  / \
 1   3

```
**因为我们一直从stack里面append，不需要if， 只用一个while curr来检测None**

- curr指针到root

- **空白stack**，空白result

- while （curr or stack）

    - while curr 指针从root开始先挪到树的最左下角，过程中stack append

    - curr = stack pop（）

    - append curr to res

    - curr = curr.right

* [94. Binary Tree Inorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0001~0099/0094.Binary-Tree-Inorder-Traversal.md)


# Post-order Travresal
左右中
### 思路
DFS Postorder Bottom->Top Left->Right
```
     5
    / \
   3   4
  / \
 1   2
```

按照顺序中左右，然后倒序

- **stack先放进root,所以先确保root is not None**，while（stack）

- while 内部 **三个if， 先左后右**

- if （root is not None） pop root， 加进res

    - if （root.left is not None） stack append

    - if （root.right is not None） stack append

- return res[::-1]

* [145. Binary Tree Postorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0100~0199/0145.Binary-Tree-Postorder-Traversal.md)

## Level-order Traversal
### 思路
BFS Left->Right Top->Bottom

```
     1
    / \
   2   3
  / \
 4   5
```
Let's keep nodes of each tree level in the queue structure, which typically orders elements in a **FIFO (first-in-first-out)** manner. In Java one could use LinkedList implementation of the Queue interface. In Python using Queue structure would be an overkill since it's designed for a safe exchange between multiple threads and hence requires locking which leads to a performance loose. In Python the queue implementation with a fast atomic ``append()`` and ``popleft()`` is ``deque``.

The zero level contains only one node root. The algorithm is simple :

- Initiate queue with a root and start from the level number 0 : level = 0.

- While queue is not empty :

    - Start the current level by adding an empty list into output structure levels.

    - Compute how many elements should be on the current level : **it's a queue length**.

        - Pop out all these elements from the queue and add them into the current level.

        - Push their child nodes into the queue for the next level.

    - Go to the next level level++.

* [102. Binary Tree Levelorder Traversal](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0100~0199/0102.Binary-Tree-Level-Order-Traversal.md/)

## Exercise

* [104. Maximum Depth of Binary Tree](https://github.com/yuxinhuang/Leetcode/blob/main/website/content/ChapterFour/0100~0199/0104.Maximum-Depth-of-Binary-Tree.md/)