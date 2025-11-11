
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

# Recursive searching

- All nodes in a node's `left` subtree are `less in value` than the node's value.
- All nodes in a node's `right` subtree are `greater in value` than the node's value.

## Algorithm

 The search operation in a binary search tree can be implemented as a simple recursive algorithm that discards either the left or right subtree at every point until it finds the value to be searched or reaches the end of the tree.

![[Pasted image 20251110114022.png]]

> **Algorithm**
> 
> - **Step 1:** If the `current` node is `null`, return it (base case).
> - **Step 2:** If the `current` node's value equals the `target`, return it.
> - **Step 3:** Else, if the `current` node's value exceeds the `target`, recursively call the search operation on the `left` subtree.
> - **Step 4:** Else, if the `current` node's value is less than the `target`, recursively call the search operation on the `right` subtree.


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
    public TreeNode recursiveSearch(TreeNode root, int target) {
        // If the root is null, the tree is empty, and we can't find the target
        if (root == null) {
            return null;
        }

        // If the root's value matches the target we are looking for, we found the node
        if (root.val == target) {
            return root;
        }
        // If the target is less than the current root's value, search in the left subtree
        else if (target < root.val) {
            return recursiveSearch(root.left, target);
        }
        // If the target is greater than the current root's value, search in the right subtree
        else {
            return recursiveSearch(root.right, target);
        }
    }
}
```

## Recursive Minimum Search

- **Step 1:** If the `current` node is `null`, return it (base case).
- **Step 2:** If the `current` node does not have a `left` subtree return the node.
- **Step 3:** Else, if the `current` node has a `left` subtree, recursively call the search operation on the `left` subtree.

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
    public TreeNode recursivelyFindMinimum(TreeNode root) {
        // Base case: If the root is null (empty tree or leaf node) return null
        if (root == null) {
            return null;
        }

        // If the left child of the current node is null, then this node
        // is the minimum value node. Return the current node
        if (root.left == null) {
            return root;
        }
        // If the left child is not null, recursively traverse to the left subtree
        // as the minimum value node will be in the left subtree
        else {
            return recursivelyFindMinimum(root.left);
        }
    }
}
```

## Recursive Maximum Search

- **Step 1:** If the `current` node is `null`, return it (base case).
- **Step 2:** If the `current` node does not have a `right` subtree return the node.
- **Step 3:** Else, if the `current` node has a `right` subtree, recursively call the search operation on the `right` subtree.

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
    public TreeNode recursivelyFindMaximum(TreeNode root) {
        // Base case: If the root is null (empty tree or leaf node) return null
        if (root == null) {
            return null;
        }

        // If the right child of the current node is null, then this node
        // is the maximum value node. Return the current node
        if (root.right == null) {
            return root;
        }
        // If the right child is not null, recursively traverse to the right subtree
        // as the maximum value node will be in the right subtree
        else {
            return recursivelyFindMaximum(root.right);
        }
    }
}
```

## Recursive Lower Bound Search

 It is very similar to searching for a value, so we can exploit the special property of a binary search tree to devise an exponentially faster algorithm. Let us look at the cases we need to consider

### Algorithm

We follow the same path as the search by slightly modifying the search algorithm to find the first element greater than or equal to the given value. To search for the lower bound, we keep track of the most recent value we have seen so far that is **greater than or equal to** the given value. We will have our answer in that variable when hitting a leaf node.

#### 1. The value is present in the tree

In this case, the given value is the lower bound, and we will reach it during the search.

#### 2. The value is not present in the tree

When we try to search for the value, we will hit a leaf node. On hitting the leaf node, the lower bound in the variable storing the most recently seen value will be greater than the given value. Let us look at a few examples to understand this case better.

##### 2.1 The lower bound is a leaf node

In this case, the leaf node will have the smallest value greater than the given value, which will be the lower bound of the given value.

##### 2.2 The lower bound is an internal node

In this case, the leaf node's value will be smaller than the given value, so its parent will be the lower bound of the given value.

**==The idea can be summarized as a recursive algorithm having a simple recursive equation. We create a global variable called `loweBoundNode` to maintain state throughout recursion. It will store the most recent node seen so far whose value is greater than or equal to the given value. All different function calls will have access to the same copy of `loweBoundNode` which they can update. We follow the same path as search down the tree and update the `lowerBoundNode` variable when needed.==**

![[Pasted image 20251110115751.png]]

- **Step 1:** If the `current` node is `null`, return (base case).
- **Step 2:** If the `current` node's value exceeds the `target`, update the `lowerBoundNode` and recursively call the search operation on the `left` subtree.
- **Step 3:** Else, if the `current` node's value equals the `target`, update the `lowerBoundNode` and return.
- **Step 4:** Else, if the `current` node's value is less than the `target`, recursively call the search operation on the `right` subtree.

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
    // Global variable to store the lower bound node found during the traversal
    TreeNode lowerBoundNode = null;

    void helper(TreeNode root, int target) {
        // Base case: If the current node is null, return
        if (root == null) {
            return;
        }

        // If the target is less than the value in the current node,
        // update the lower bound node to the current node and
        // continue searching in the left subtree
        if (target < root.val) {
            lowerBoundNode = root;
            helper(root.left, target);
        }
        // If the target is equal to the value in the current node,
        // update the lower bound node to the current node and return
        else if (root.val == target) {
            lowerBoundNode = root;
            return;
        }
        // If the target is greater than the value in the current node,
        // continue searching in the right subtree
        else {
            helper(root.right, target);
        }
    }

    TreeNode recursivelyFindLowerBound(TreeNode root, int target) {
        // Initialize the lower bound node to null
        lowerBoundNode = null;
        // Find the lower bound node in the binary search tree
        helper(root, target);
        // Return the lower bound node found during the search
        return lowerBoundNode;
    }
}
```

## Recursive Upper Bound Search

 It is very similar to searching for the value, so we can exploit the special property of a binary search tree to devise an exponentially faster algorithm. Let us look at the cases we need to consider

### Algorithm

To find the smallest element greater than the given value, we follow an algorithm similar to search. We create a variable that stores the smallest value greater than the given value seen so far. Starting from the root, we check if the value at the node is less than or equal to the given value, and we go to the right child. If the value at the node is greater than the given value, we compare it with the value stored in our variable and update it if needed.

The above idea can be summarized as a recursive algorithm with a simple recursive equation. **==We create a global variable called to maintain state across recursion. It will store the node's reference with the smallest value greater than the given value. All different function calls will have access to the same copy of `upperBoundNode` which they can update. We follow a similar path as searching down the tree and updating the `upperBoundNode` variable where needed.==**

![[Pasted image 20251110120308.png]]

- **Step 1:** If the `current` node is `null`, return (base case).
- **Step 2:** If the `current` node's value exceeds the `target`, update the `upperBoundNode` and recursively call the search operation on the `left` subtree.
- **Step 3:** Else, if the `current` node's value is less than the `target`, recursively call the search operation on the `right` subtree.

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
    // Global variable to store the upper bound node found during the traversal
    TreeNode upperBoundNode = null;

    void helper(TreeNode root, int target) {
        // Base case: If the current node is null, return
        if (root == null) {
            return;
        }

        // If the target is less than the value in the current node,
        // update the upper bound node to the current node and
        // continue searching in the left subtree
        if (target < root.val) {
            upperBoundNode = root;
            helper(root.left, target);
        }
        // If the target is greater than or equal to the value in the
        // current node, continue searching in the right subtree
        else {
            helper(root.right, target);
        }
    }

    TreeNode recursivelyFindUpperBound(TreeNode root, int target) {
        // Initialize the upper bound node to null
        upperBoundNode = null;
        // Find the upper bound in the binary search tree
        helper(root, target);
        // Return the upper bound node found during the search
        return upperBoundNode;
    }
}
```

# Iterative Search

The iterative search operation in a binary search tree can be implemented as a very simple three-line algorithm that discards either the left or right subtree at every point until it finds the value to be searched or reaches the end of the tree.

> **Algorithm**
> 
> - **Step 1:** While `root` is not `null`, do the following:
>     - **Step 1.1:** If the `root` node's value equals the `target`, return it.
>     - **Step 1.2:** Else, if the `root` node's value exceeds the `target`, update the root node to hold the reference of its `left` child.
>     - **Step 1.3:** Else, if the `root` node's value is less than the `target`, update the root node to hold the reference of its `right` child.

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
    public TreeNode iterativeSearch(TreeNode root, int target) {
        // Loop until we reach the end of the tree (or find the desired node)
        while (root != null) {
            // Check if the current node's value matches the target data
            if (root.val == target) {
                // Return the node since we found it
                return root;
            }
            // If the target data is smaller, move to the left subtree
            else if (target < root.val) {
                root = root.left;
            }
            // If the target data is larger, move to the right subtree
            else {
                root = root.right;
            }
        }

        // If the while loop ends without finding the node, return null
        return null;
    }
}
```

## Iterative Minimum Search

- **Step 1:** While `root` is not `null`, do the following:
    - **Step 1.1:** If the `root` node does not have a `left` child, return it.
    - **Step 1.2:** Else, if the `root` node has a `left` child, update the `root` node to hold the reference of its `left` child.

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
    TreeNode iterativelyFindMinimum(TreeNode root) {
        // Start from the given root node and iterate until we reach the leftmost node
        while (root != null) {
            // If the left child of the current node is null, it means
            // we have reached the leftmost node, which contains the
            // minimum value in the binary search tree
            if (root.left == null) {
                return root;
            }
            // If the left child is not null, move to the left child
            // to continue the search for the minimum value
            else {
                root = root.left;
            }
        }

        // If the tree is empty (root is null), or for some reason,
        // the while loop exits without finding the minimum node, we return the current root
        return root;
    }
}
```

## Iterative Maximum Search

- **Step 1:** While `root` is not `null`, do the following:
    - **Step 1.1:** If the `root` node does not have a `right` chil,d return it.
    - **Step 1.2:** Else, if the `root` node has a `right` child, update the `root` node to hold the reference of its `right` child.


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
    TreeNode iterativelyFindMaximum(TreeNode root) {
        // Start from the given root node and iterate until we reach the rightmost node
        while (root != null) {
            // If the right child of the current node is null, it means
            // we have reached the rightmost node, which contains the
            // maximum value in the binary search tree
            if (root.right == null) {
                return root;
            }
            // If the right child is not null, move to the right child
            // to continue the search for the maximum value
            else {
                root = root.right;
            }
        }

        // If the tree is empty (root is null), or for some reason,
        // the while loop exits without finding the maximum node, we return the current root
        return root;
    }
}
```

## Iterative Lower Bound Search

The iterative algorithm for finding the lower bound is similar to the recursive algorithm. We can piggyback on the iterative search algorithm we learned earlier and keep track of the most recent value seen so far that is **greater than or equal** to the given value as we go down the tree along the search path. The cases we may encounter are the same as those for the recursive algorithm.

### 1. The value is present in the tree

In this case, the given value is the lower bound, and we will reach it during the search.

### 2. The value is not present in the tree

When we try to search for the value, we will hit a leaf node. On hitting the leaf node, the lower bound in the variable storing the most recently seen value will be greater than the given value.

**Algorithm**

- **Step 1:** While `root` is not `null`, do the following:
    - **Step 1.1:** If the `root` node's value exceeds the `target`, update the `lowerBoundNode` and set the `root` node to hold the reference of its `left` child.
    - **Step 1.2:** Else, if the `root` node's value equals the `target`, update the `lowerBoundNode` and return.
    - **Step 1.3:** Else, if the `root` node's value is less than the `target`, set the `root` node to hold the reference of its `right` child.


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
    TreeNode iterativelyFindLowerBound(TreeNode root, int target) {
        // Initialize a pointer to the lower bound node as null
        TreeNode lowerBoundNode = null;

        // Traverse the binary search tree iteratively until root becomes null
        while (root != null) {
            // If the target is less than the current node's value, move to the left subtree
            if (target < root.val) {
                // Update the lower bound node to the current node as it is the potential lower bound
                lowerBoundNode = root;
                // Move to the left subtree to find a closer lower bound
                root = root.left;
            }
            // If the target is equal to the current node's value, we found an exact match
            else if (root.val == target) {
                // Update the lower bound node to the current node (exact match is also a lower bound)
                lowerBoundNode = root;
                // Return the node as we have found an exact match for the given target
                return lowerBoundNode;
            }
            // If the target is greater than the current node's value, move to the right subtree
            else {
                // We are not updating the lower bound node in this case as the current node
                // is not a lower bound. Continue searching in the right subtree
                root = root.right;
            }
        }

        // Return the lower bound node
        return lowerBoundNode;
    }
}
```

## Iterative Upper Bound Search

The iterative algorithm for finding the upper bound is similar to the recursive algorithm. We can piggyback on the iterative search algorithm we learned earlier and keep track of the most recent value **greater** than the given value as we go down the tree to get the upper bound.

The iterative search for the upper bound of a given value in a binary search tree can be summarised as the following algorithm.

> **Algorithm**
> 
> - **Step 1:** While `root` is not `null`, do the following:
> - **Step 2:** If the `root` node's value exceeds the `target,` update the `upperBoundNode` set root node to hold the reference of its `left` child.
> - **Step 3:** Else, if the `root` node's value is less than the target, set the `root` node to hold the value of its `right` child.

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
    TreeNode iterativelyFindUpperBound(TreeNode root, int target) {
        // Initialize a pointer to the upper bound node as null
        TreeNode upperBoundNode = null;

        // Traverse the binary search tree iteratively until root becomes null
        while (root != null) {
            // If the target is less than the current node's value, move to the left subtree
            if (target < root.val) {
                // Update the upper bound node to the current node as it is the potential upper bound
                upperBoundNode = root;
                // Move to the left subtree to find a closer upper bound
                root = root.left;
            }
            // If the target is greater than or equal to the current node's value, move to the right subtree
            else {
                // We are not updating the upper bound node in this case as the current node
                // is not an upper bound. Continue searching in the right subtree
                root = root.right;
            }
        }

        // Return the upper bound node
        return upperBoundNode;
    }
}
```

## Example  Closest value

Given the **root** of a binary search tree and **target** value, write a function to find and return the value in the BST that is closest to the target. You are guaranteed to have only one unique value in the BST closest to the target.

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
    public int closestValue(TreeNode root, double target) {
        // Start with the root as the closest value
        int closest = root.val;

        while (root != null) {
            // Update closest if the current node is closer to the target
            if (Math.abs(root.val - target) < Math.abs(closest - target)) {
                closest = root.val;
            }

            // Traverse to the left subtree if the target is smaller
            if (target < root.val) {
                root = root.left;
            }
            // Traverse to the right subtree if the target is larger
            else {
                root = root.right;
            }
        }

        return closest;
    }
}
```

# Insertion in Binary Search Trees

## Recursive Insertion

- **Step 1:** Search for the position of insertion
- **Step 2:** Insert the node at the insertion position


**How do you find the position of insertion?**

To find the insertion position of a given value in the binary search tree, we will **assume** that the tree already has the given value and try to search for it. When we follow our search algorithm, we will arrive at a node with no way ahead. This is precisely where we have to perform the insertion to ensure that the tree remains a binary search tree after insertion.

The insert operation in a binary search tree can be implemented as a straightforward recursive algorithm that first searches for the insertion position by going either to the left or right subtree at every point until it reaches the final position. A new node is created with the value inserted and connected to the tree.

![[Pasted image 20251111113804.png]]

- **Step 1:** If the `current` node is `null`, create a new node and return it (base case).
- **Step 2:** If the `current` node's value exceeds the new value, recursively call the insert operation on the `left` subtree and store its result in the `left` child.
- **Step 3:** Else, if the `current` node's value is less than the new value, recursively call the insert operation on the `right` subtree and store its result in the `right` child.
- **Step 4:** Return the `current` node when the recursion exits.

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
    public TreeNode recursiveInsertion(TreeNode root, int data) {
        // If the root is null, it means the tree is empty,
        // so create a new node and return it as the new root
        if (root == null) {
            return new TreeNode(data);
        }

        // If the data is less than the value of the current root node,
        // it should be inserted in the left subtree of the current root
        if (data < root.val) {
            root.left = recursiveInsertion(root.left, data);
        }
        // If the data is greater than or equal to the value of the current root node,
        // it should be inserted in the right subtree of the current root
        else {
            root.right = recursiveInsertion(root.right, data);
        }

        // Return the root of the tree after insertion
        return root;
    }
}
```

## Iterative Insertion

The idea is simple. We know that insertion is a two-step process. In the first step, we search for the insertion position and then insert the node in the second step. We need to convert the first step to its iterative form to get an iterative algorithm. Once we find the insertion position, we create a new node and return its reference to the caller.

**Algorithm**

- **Step 1:** Store the reference of the root node in a new variable called `current`.
- **Step 2:** While `current` is not `null`, do the following:
    - **Step 2.1:** If the `current` node's value exceeds the new value, do the following:
        - **Step 2.1.1**: If the `current` node's `left` child is `null`, insert data as the `left` child. Otherwise, move to the `left` child and continue searching.
    - **Step 2.2:** Else, if the `current` node's value is less than or equal to the new value, do the following:
        - **Step 2.2.1:** If the `current` node's `right` child is `null`, insert data as the right child. Otherwise, move to the `right` child and continue searching.
- **Step 3:** Return the tree's `root` after the successful insertion.

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
    TreeNode iterativeInsertion(TreeNode root, int data) {
        // If the root is null, create a new node with data and make it the root
        if (root == null) {
            return new TreeNode(data);
        }

        // Initialize a pointer current to traverse the tree starting from the root
        TreeNode current = root;

        // Traverse the tree until we find the appropriate position to insert the data
        while (current != null) {
            // If the data is less than the current node's value, move to the left subtree
            if (data < current.val) {
                // If the left child of the current node is null, insert data as the left child
                if (current.left == null) {
                    current.left = new TreeNode(data);
                    return root;
                }
                // Move to the left child
                else {
                    current = current.left;
                }
            }
            // If data is greater than or equal to the current node's value,
            // insert in the right subtree
            else {
                // If the right child of the current node is null, insert data as the right child
                if (current.right == null) {
                    current.right = new TreeNode(data);
                    return root;
                }
                // Move to the right child
                else {
                    current = current.right;
                }
            }
        }

        // Return the root of the tree after all insertions
        return root;
    }
}
```

# Deletion in Binary Search Trees

## Recursive Deletion

Deleting a node from a binary search tree is a two-step process.

> - **Step 1:** Search the node to be deleted
> - **Step 2:** Delete the node

We search for the node to be deleted using the search algorithm we learned earlier. However, deleting the node once we find it is not straightforward, as there are three different cases we need to consider. Let us look at these cases.

### 1. Node to be deleted is a leaf node

This is the most straightforward case of deletion. If the node to be deleted is the leaf node, we can search for the node using the search algorithm we learned earlier and delete the node.

### 2. Node to be deleted has one child

If the node to be deleted only has one child node, we cannot delete it simply as the leaf node. This is because if we delete the node, its descendent subtree will become an orphan (without a parent), and the tree will split into two trees. We do the following to delete a node **N** with only one child, **C**.

> - **Step 1:** Find the node `N` to be deleted.
> - **Step 2:** Delete node `N` and reconnect `C` to the parent on `N`

### 3. Node to be deleted has two children

If the node to be deleted has **two children**, it makes deleting it a bit more complicated. We cannot just delete the node like a leaf node, nor can we delete the node and connect the child as we have two children. After deleting the node, we must also ensure the tree remains a binary search tree. To delete a node, in this case, we must first find its **inorder successor.**

We do the following to delete the value **V** at node **N**, which has two children.

> - **Step 1:** Find the node `N` to be deleted.
> - **Step 2:** Find the inorder successor `S` of node `N`.
> - **Step 3:** Swap of the value `V` at node `N` and the value stored in node `S`.
> - **Step 4:** Delete value `V` from the `right` subtree of node `N` recursively.

**Algorithm**

- **Step 1:** If the `current` node is `null`, return `null` (base case).
- **Step 2:** If the `key` exceeds the `current` node's value, recursively search it in the `right` subtree.
- **Step 3:** Else, if the `key` is smaller than the `current` node's value, recursively search it in the `left` subtree.
- **Step 4:** Else, if the `key` matches the `current` node's value, do the following:
    - **Step 4.1:** If the `current` node has no `left` child, do the following:
        - **Step 4.1.1:** Save the `right` child of the `current` node in a temporary variable.
        - **Step 4.1.2:** Delete the `current` node.
        - **Step 4.1.3:** Return the `right` child to reconnect it with the parent.
    - **Step 4.2:** Else, if the `current` node has no `right` child, do the following:
        - **Step 4.2.1:** Save the `current` node's `left` child in a temporary variable.
        - **Step 4.2.2:** Delete the `current` node.
        - **Step 4.2.3:** Return the `left` child to reconnect it with the parent.
    - **Step 4.3:** Else, if the `current` node has both the `left` and `right` children, do the following:
        - **Step 4.3.1:** Find the in-order successor of the `current` node (the smallest node in the right subtree).
        - **Step 4.3.2:** Copy the value of the inorder successor to the `current` node.
        - **Step 4.3.3**: Recursively delete the original inorder successor from the `right` subtree.
- **Step 5**: Return the binary search tree's updated `root` node at the end of recursion.

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
    public TreeNode inorderSuccessor(TreeNode root, TreeNode node) {
        TreeNode successor = null;

        while (root != null) {
            if (root.val > node.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        return successor;
    }

    public TreeNode recursiveDeletion(TreeNode root, int key) {
        // Base case: if the root is null, return null
        if (root == null) {
            return null;
        }

        // If the key is greater than the current node's value, search in the right subtree
        if (root.val < key) {
            root.right = recursiveDeletion(root.right, key);
        }
        // If the key is smaller than the current node's value, search in the left subtree
        else if (root.val > key) {
            root.left = recursiveDeletion(root.left, key);
        }
        // If the key matches the current node's value, found the node to delete
        else {
            // Case 1: Node has no left child
            if (root.left == null) {
                // Save the right child of the current node
                TreeNode temp = root.right;
                // Delete the current node
                root = null;
                // Return the right child to reconnect it with the parent
                return temp;
            }
            // Case 2: Node has no right child
            else if (root.right == null) {
                // Save the left child of the current node
                TreeNode temp = root.left;
                // Delete the current node
                root = null;
                // Return the left child to reconnect it with the parent
                return temp;
            }
            // Case 3: Node has both left and right children
            else {
                // Find inorder successor of the node
                TreeNode successor = inorderSuccessor(root.right, root);
                // Copy successor's value to current node
                root.val = successor.val;
                // Delete successor
                root.right = recursiveDeletion(root.right, successor.val);
            }
        }

        // Return the updated root node of the binary search tree
        return root;
    }
}
```

## Iterative Deletion

The idea is simple. We know that deletion is a two-step process: in the first step, we search for the node to be deleted, and then in the second step, we delete it. We need to convert the first step to its iterative form to get an iterative algorithm. Once we find the node to be deleted, we remove the links to it from its parent. 

To delete a node, we need access to its parent. Unlike in the recursive algorithm, we cannot rely on the recursive call stack to hold the parent's information, so we must keep track of it while traversing iteratively. 

### 1. Node to be deleted is a leaf node

This is the most straightforward case of deletion. If the node to be deleted is the leaf node, we can search for it using the iterative search algorithm we learned earlier and delete it.

### 2. Node to be deleted has one child

If the node to be deleted only has one child node, we cannot delete it simply as the leaf node. This is because if we delete the node, its descendent subtree will become an orphan (without a parent), and the tree will split into two trees. We do the following to delete node **N** with only one child, **C**, and parent, **P**.

> - **Step 1:** Find the node `N` to be deleted.
> - **Step 2:** Delete node `N` and reconnect `C` to the parent `P` of `N` as the correct (`left` or `right`) child.

![[Pasted image 20251111115308.png]]
### 3. Node to be deleted has two children

If the node to be deleted has two children, it makes deleting the node a bit more difficult. We cannot simply delete the node like a leaf node, nor can we delete the node and connect the child, as we now have two children. We must also ensure the tree remains a binary search tree after deletion. Like the recursive implementation, we find the node's **inorder successor** first.

There are two important observations to make here.

> - The inorder successor of a node with two children will always be in its `right` subtree. This is because the inorder traversal follows `left`, `center`, `right` order.
> - The inorder successor node will not have any `left` child.

We do the following to delete the value **V** at node **N**, which has two children.

> - **Step 1:** Find the node `N` to be deleted.
> - **Step 2:** Find the inorder successor `S` of node `N` iteratively.
> - **Step 3:** Swap the value `V` at node `N` and the value stored in node `S`.
> - **Step 4:** Delete value `V` from the `right` subtree of node `N` iteratively.

Step 4 of the above algorithm is a bit tricky to implement. The inorder successor is guaranteed to be in the right subtree. However, it can be either the root node of the right subtree or any other node in the right subtree.

The recursive algorithm stored the parent node in the call stack, implicitly taking care of both cases. However, for the iterative implementation, we need to consider both cases.

![[Pasted image 20251111115336.png]]

**Algorithm**

- **Step 1:** If the `root` node is `null`, return `null`.
- **Step 2:** Create variables to store the `current` node and it's `parent`.
- **Step 3:** While `current` is not `null` and the value in current is not equal to the `key`, search for the `key` in `left` and `right` subtrees while keeping track of `current` and `parent` nodes.
- **Step 4:** Return' `null` if the `key` is not found.
- **Step 5:** If the `current` node has zero or one child, do the following:
    - **Step 5.1:** Connect the `parent` node to the `left` or `right` child (which ever is present).
    - **Step 5.2:** Delete the `current` node.
- **Step 6:** Else, if the `current` node has both `left` and `right` children, do the following:
    - **Step 6.1:** Find the in-order successor of the `current` node (the smallest node in the `right` subtree).
    - **Step 6.2:** Copy the value of the inorder successor to the `current` node.
    - **Step 6.3**: Delete the original inorder successor node.
- **Step 7**: Return the binary search tree's updated `root` node.

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
    public TreeNode iterativeDeletion(TreeNode root, int key) {
        // If the root is null, return null (no node to delete)
        if (root == null) {
            return null;
        }

        TreeNode parent = null;
        TreeNode current = root;

        while (current != null && current.val != key) {
            // Keep track of the parent of the current node
            parent = current;
            // Search in the left subtree
            if (key < current.val) {
                current = current.left;
            }
            // Search in the right subtree
            else {
                current = current.right;
            }
        }

        // If the key was not found, return null (no node to delete)
        if (current == null) {
            return null;
        }

        // Case 1: Node has zero or one child
        if (current.left == null || current.right == null) {
            TreeNode newCurrent = null;
            // Choose the right child if it exists
            if (current.left == null) {
                newCurrent = current.right;
            }
            // Choose the left child if it exists
            else {
                newCurrent = current.left;
            }

            // If the current node is the root, return the new current node
            if (parent == null) {
                return newCurrent;
            }

            // Reconnect the left child of the parent to the new current node
            if (current == parent.left) {
                parent.left = newCurrent;
            }
            // Reconnect the right child of the parent to the new current node
            else {
                parent.right = newCurrent;
            }

            // Delete the current node
            current = null;
        }
        // Case 2: Node has both left and right children
        else {
            // Keep track of the parent of the in-order successor
            TreeNode inParent = current;
            // Find the in-order successor (the smallest node in the right subtree)
            TreeNode successor = current.right;

            while (successor != null && successor.left != null) {
                // Traverse to the leftmost node of the right subtree
                inParent = successor;
                successor = successor.left;
            }

            // If the parent of the in-order successor is not the current node
            if (inParent != current) {
                // Reconnect the parent of the in-order successor to its right child
                inParent.left = successor.right;
            }
            // If the in-order successor is the right child of the current node
            else {
                // Reconnect the current node to the right child of the in-order successor
                current.right = successor.right;
            }

            // Copy the value of the in-order successor to the current node
            current.val = successor.val;
            // Delete the in-order successor node
            successor = null;
        }

        // Return the updated root node of the binary search tree
        return root;
    }
}
```