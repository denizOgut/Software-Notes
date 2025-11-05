
# Binary Search Tree

A binary search tree is a data structure that utilizes the two-dimensional structure of binary trees by exploiting the fact that we can impose some conditions on who gets to be the left and right child of a node. The nodes in a binary search tree follow a particular order

![[Pasted image 20251105110144.png]]

## Structure of a Binary Search Tree

A binary search tree is a special type of binary tree that follows the binary search property.

> For every node **N** in the binary search tree :
> 
> ==- All the values stored in the **left subtree** of `N` are **less than** the value stored in **N**==
> ==- All the values stored in the **right subtree** of **N** are **greater than** the value stored in **N**==

![[Pasted image 20251105110226.png]]

## Characteristics of a Binary Search Tree

### Minimum

in a binary search tree, for any given node, all the values in its left subtree are less than the value at the given node. This logic makes it easy to see where the **minimum** value in a binary search tree would reside.

The first node in inorder traversal of a binary search tree has the minimum value in the tree

![[Pasted image 20251105110440.png]]

### Maximum

Just like the left subtree, we know that in a binary search tree, for any given node, all the values in its right subtree are greater than the value at the given node. This logic makes it easy to see where the **maximum** value in a binary search tree would reside. 

The first node in the reverse inorder traversal of a binary search tree has the minimum value in the tree

![[Pasted image 20251105110501.png]]

### Inorder traversal

The inorder traversal of a binary search tree will always be a list of sorted values. This is because, in a binary search tree, the nodes are structured so that for every node, ``the left subtree < node < right subtree``. If we follow the inorder traversal that is left, center, and right, we are guaranteed to get a list of sorted values.

![[Pasted image 20251105110716.png]]

### Reverse inorder traversal

Just like the inorder traversal of a binary search always results in a sorted list, if we follow the reverse inorder traversal, which is right, center, and left, we can get a list in reverse sorted order (descending order).

![[Pasted image 20251105110739.png]]

## Implementation of Binary Search Trees

Since a binary search tree is just one that follows some special properties, its structure is the same as any other binary tree. We know that a binary tree can be represented using arrays and linked structures, so a binary search tree can also be represented using any of those.

**Why are binary search trees stored and represented as linked structures?**

Binary search trees are typically represented and stored as linked structures because we rarely need to go upwards in a binary search tree during any operation. Representing and storing binary search trees as a linked data structure allows us to dynamically increase or decrease the size.

Every node stores a value and the addresses of the left and right children. When linked together, multiple nodes form the binary search tree, just like generic binary trees.

![[Pasted image 20251105111755.png]]

## Height & Balance in Binary Search Trees

The height of a binary search tree is a **critical** property. So far, **==all the operations we have seen depend critically on the tree's height.==** There can be many tree representations for any given tree with N nodes. Not all tree representations are the same, however

![[Pasted image 20251105111903.png]]

### Most performant binary trees

The trees with the least height will perform best.

![[Pasted image 20251105112009.png]]
### Least performant binary trees

The trees with the greatest height will perform the worst. These trees are all skew trees, where every node increases the tree's height by one.

![[Pasted image 20251105112022.png]]

### Limitation in using height for perforamnce

The worst-case runtime complexity for most binary search tree operations is **O(h)**, where h is the tree's height. Following this statement, all trees with the same height should perform the same. But this is not always true. The big O notation only tells us the bounds of performance and not the actual performance. When we have a large number of nodes, the constant factor that we usually ignore while calculating the big O notation starts to make a difference, so not all trees with the same height perform the same.

![[Pasted image 20251105112114.png]]

the average number of hops needed to search for a node in two trees of the same height might not be equal, so height alone is not the correct metric for judging the performance of binary search trees.

## The Impact of Balance on Performance

 not all binary search trees are equal in performance, we can dive deeper and try to understand the metric that can measure how good a binary search tree is performance-wise. This metric is called the balance factor.

Balance factor

> ==**The balance factor for a node is the difference between the height of its left and right subtree.==**


![[Pasted image 20251105112509.png]]

![[Pasted image 20251105112531.png]]

> The absolute value of the balance factor is called the absolute balance factor.

![[Pasted image 20251105112554.png]]

### Characteristics of optimal binary search trees

The best-performing binary search trees are the ones that have the **minimum** possible height and the **minimum** possible absolute balance factor. A tree is guaranteed to have the minimum possible height if all the nodes in the tree have the minimum possible absolute balance factor.

he restriction for every node to have the minimum possible absolute balance factor forces us to fill all the nodes for a level before inserting a node in the next level. This, in turn, generates a **complete binary tree**, which is the **most optimal** tree structure for N nodes as it is a tree with the minimum possible height and minimum possible absolute balance factor for all nodes.

```java
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 * }
 */

class Solution {
    public int findHeight(TreeNode root) {
        // Empty tree has height 0
        if (root == null) {
            return 0;
        }

        // Recursively calculate the height of the left and right subtrees
        int leftHeight = findHeight(root.left);
        int rightHeight = findHeight(root.right);

        // Return the maximum height among the left and right subtrees plus 1
        return Math.max(leftHeight, rightHeight) + 1;
    }

    public int balanceFactor(TreeNode root) {
        if (root == null) {
            return 0;
        }

        // Calculate the height of the left subtree
        int leftHeight = findHeight(root.left);
        // Calculate the height of the right subtree
        int rightHeight = findHeight(root.right);
        // Calculate the balance factor
        int balanceFactor = leftHeight - rightHeight;

        return balanceFactor;
    }
}
```

## Challenges in Implementing Complete Binary Search Trees

### Modifications

If we do not have to modify the tree, it will always remain complete and perform best. However, when we try to insert or delete data from the tree, the tree may no longer remain complete, and its performance will degrade.

![[Pasted image 20251105113740.png]]

To solve this problem, after each modification, we can apply the two steps below to check its completeness and rebalance it if needed.
#### Step 1: Verify the completeness

The verify operation verifies whether the given tree is a complete binary search tree.

![[Pasted image 20251105113811.png]]

#### Step 2: Rebalance the tree

The rebalance operation takes a binary search tree that became unbalanced(non-complete) after an operation and reorganizes it to make it balanced(complete) again.

![[Pasted image 20251105113835.png]]

## Height Balanced Binary Trees

Our implementation of a balanced binary tree should have a **weaker** balancing condition for it to be practically useful. We need the tree to always perform well and be **easy** to create, validate, and rebalance. Keeping this in mind, we define a balanced binary tree as the following.

Height Balanced Binary Tree

> A height-balanced binary tree is a tree where, for every node in the tree, the absolute difference between the height of the left and right subtree is at most 1

This definition is less restrictive than the definition of the most optimal binary search tree possible with N nodes (complete tree). It allows the tree to have a height or absolute balance factor that is not the minimum possible for every node.

![[Pasted image 20251105113938.png]]

### Modifications

Like the complete binary search tree, it may become unbalanced when we insert or delete nodes from a balanced binary tree. 

![[Pasted image 20251105114103.png]]

To address this issue, following each modification, we can follow the two steps below to check whether the tree is height balanced and rebalance it if it is not.

#### Step 1: Verify the balance

The verify operation verifies whether the given tree is a balanced binary search tree. This operation is much simpler than checking whether a binary search tree is complete and can be recursively implemented in **O(logN)** time.

![[Pasted image 20251105114124.png]]

#### Step 2: Rebalance the tree

The rebalance operation takes a binary search tree that became unbalanced after an operation and reorganizes it to make it balanced again. This operation is much simpler to implement than a complete binary search tree. Depending on the type of balanced binary search tree, there may be different rebalancing techniques; the most common one is via **rotation**. The rebalance operation on a binary search tree is out of the scope of this course, but for a balanced binary search tree, it can be proved that all rebalance operations will have a worst-case time complexity of **O(logN)**.

![[Pasted image 20251105114143.png]]

```java
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 * }
 */

class Solution {
    public int findHeight(TreeNode root) {
        // Empty tree has height 0
        if (root == null) {
            return 0;
        }

        // Recursively calculate the height of the left and right subtrees
        int leftHeight = findHeight(root.left);
        int rightHeight = findHeight(root.right);

        // Return the maximum height among the left and right subtrees plus 1
        return Math.max(leftHeight, rightHeight) + 1;
    }

    public boolean heightBalancedTree(TreeNode root) {
        // Base case: empty tree
        if (root == null) {
            return true;
        }

        int leftHeight = findHeight(root.left);
        int rightHeight = findHeight(root.right);

        if (Math.abs(leftHeight - rightHeight) <= 1) {
            // Check if both left and right subtrees are height-balanced
            return heightBalancedTree(root.left) && heightBalancedTree(root.right);
        }

        return false;
    }
}
```