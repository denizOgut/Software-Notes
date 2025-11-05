
# Binary Tree

A tree is a **nonlinear** data structure that stores elements **hierarchically**. Every element in a tree is called a **node**, and except the topmost node, each node has a **parent** node and zero or more children nodes. The individual nodes in a tree are connected by edges, which may be unidirectional or bidirectional. **==A tree can only have edges between a parent and a child node, and therefore, a tree cannot have cycles.==**

![[Pasted image 20251024163245.png]]

**==A binary tree is one where every node can have at most two children.==**

![[Pasted image 20251024163538.png]]

## Key Tree Terminologies

Trees may exhibit unique properties depending on their shape, size, and structure. 

### Root

**==The root is the only node in the tree without a parent==**. It is the topmost node from which we can reach any node in the tree.

![[Pasted image 20251024163651.png]]

### Leaf

The nodes in the tree **==which do not have any children are called the leaf nodes.==**

![[Pasted image 20251024163806.png]]

### Internal node

**==Every non-leaf node==** in a binary tree is called an internal node.

![[Pasted image 20251024163824.png]]

### Degree

The degree of a node is **==the number of other nodes it is connected to.==**

![[Pasted image 20251024164144.png]]

### Sibling

**==The nodes that are children of the same parent==** in a tree are called siblings.

![[Pasted image 20251024164217.png]]

### Path

The sequence of nodes and edges from one node to another in a tree is called the **path** between those two nodes. **==The length of a path is the total number of nodes in that path.==**


![[Pasted image 20251024164454.png]]

### Subtree

A subtree of a node `a` in a tree is a tree consisting of one of the child nodes of `a` and all its descendants. Every child node of a node makes up a subtree of that node, so every node can have subtrees equal to the number of its children.

![[Pasted image 20251024164524.png]]

### Level

Each step from top to bottom in a tree is called a level. **==The root is at level `0`.==**

![[Pasted image 20251024164548.png]]

### Depth

The node's depth is **==the number of edges between any given node and the root node.==**

![[Pasted image 20251024164754.png]]

### Height

The height of any node is ==the total number of edges in the **longest** path from that node to a leaf node.== The height of all leaves is 0, and the root node's height is also the tree's height.

![[Pasted image 20251024164823.png]]

## Types and properties of binary trees

### Full binary tree

A full Binary tree is a binary tree in which **==every node has two or no children==**. It is also known as a **proper binary tree**.

![[Pasted image 20251024165845.png]]

Some interesting properties of full binary trees are:

- Number of leaf nodes = number of internal nodes + 1
- Number of nodes is = 2 * (number of internal nodes) + 1
- Number of internal nodes = (total number of nodes – 1) / 2
- Number of leaves = (total number of nodes + 1) / 2
- Total number of nodes is = 2 * (number of leaf nodes) – 1
- Number of internal nodes = number of leaf nodes – 1.
- maximum number of leaves = (2 ^ height) - 1.
### Complete binary tree

A complete binary tree has all the levels filled except possibly the lowest one, **filled from the left**.

> A complete binary tree has all levels fully filled except possibly the last level, which must be filled from left to right without gaps. Think of it like filling seats in a theater row by row, always starting from the left side.

![[Pasted image 20251024170215.png]]

### Perfect binary tree

A perfect binary tree is one in which every internal node has **exactly two** child nodes, and **all the leaf nodes are at the same level**.

![[Pasted image 20251024170256.png]]

Some interesting properties of full binary trees are:

- Total number of nodes = (2 ^ (height + 1) – 1)
- Height = log(n + 1)
- Number of leaf nodes = 2 ^ height

### Skew binary tree

A skew binary tree is a binary tree where every internal node has only one child.

![[Pasted image 20251024170340.png]]

# Array Based Binary Trees

a **complete binary tree**. We can see a pattern if we try to **enumerate** the nodes of a complete binary tree, starting from the root and going top to bottom, left to right.

![[Pasted image 20251029145956.png]]

We can see that for any node n:

- The left child = (2 * n) + 1
- The right child = (2 * n) + 2

We can use the enumeration of a complete binary tree to represent a binary tree in an array. The enumeration of a node can be used as an index in an array that stores the value of a given node.

![[Pasted image 20251029150045.png]]

## Defining a Node in Binary Tree

==The array implementation of a binary tree is based on individual nodes making up the entire tree. These individual nodes, however, don't have **left** and **right** sections to hold references like nodes in a linked list.==

### Structure of a node

In the array implementation, the data stored in the node is the node itself. It does not need left and right sections, as moving around in the array implementation of a binary tree is accomplished using simple math

![[Pasted image 20251029150513.png]]

## Structure of a binary tree

Multiple nodes link up together to create the binary tree structure. When implemented as an array, the node's enumeration in its tree representation is used as an index in the array where the data associated with that node is stored.

![[Pasted image 20251029150607.png]]

What looks like a tree on paper looks very different when implemented as an array in the computer memory. The resulting binary tree looks like a regular array of nodes in the memory

![[Pasted image 20251029150634.png]]

### Root node

Unlike when implementing a binary tree using linked lists, we don't need to store the reference to the root node when the binary tree is implemented using an array. **==This is because the first node of the array will always be the root node as the node has the enumeration 0.==**

![[Pasted image 20251029150732.png]]

### Moving down

Unlike a binary tree implemented using a linked list, a binary tree implemented as an array does not have **left** and **right** sections to help move from a parent node to the child node. However, there is a relationship between the enumeration of a node in the tree and the index of the array in which it is stored. Using this enumeration and the special properties of a **complete** binary tree, we can move from a parent node to a child node using simple mathematics.

> For a node at index n:
- Index of left child = (2 * n) + 1
- Index of right child = (2 * n) + 2

![[Pasted image 20251029150842.png]]

### Moving up

There is a special benefit of implementing a binary tree using arrays. **==The linked list implementation of a binary tree uses unidirectional references. This is why we can only move from a parent node to a child node by following these references and not vice versa. In the array representation, however, since arrays provide random access capabilities, we can move up the tree from a child node to a parent node if we know the index of the parent node==**. The index of the parent node can be easily calculated from the index of a child node.

  

> For a node at index n:
> 
> - Index of parent node = (n - 1) / 2

![[Pasted image 20251029151151.png]]

### Leaf nodes

Unlike when implementing a binary tree using linked lists, a binary tree, when implemented using arrays, does not make use of `null` to identify leaf nodes. **==In the array implementation, nodes do not store any information about their children. However, the index of the node in the array is used to identify whether a given node is a leaf node or not.==**

> If the index of the left and right child of a node in the array is out of bounds of the array, it means that the given node does not have a left and a right child and hence is a leaf node.

![[Pasted image 20251029151254.png]]

## Understanding a Generic Binary Tree

how we can **extend** the same idea to any generic binary tree. Generic binary trees cannot be implemented using an array as easily as complete binary trees. This is because the implementation relies on some structural properties of a complete binary tree

### Understanding the problem

The problem here is pretty clear. To implement a binary tree using an array and be able to move around easily, the tree should follow some structural characteristic properties. The properties are given below.

> When the nodes of the tree are enumerated:
> 
> - For any node **n**, the **left** child should be enumerated as **(2 * n ) + 1**
> - For any node **n**, the **right** child should be enumerated as **(2 * n ) + 2**

However, only **complete binary trees** have this property. This means it is not possible to implement non-complete binary trees using arrays.

![[Pasted image 20251029151901.png]]

### Exploring a possible solution

The fix to this problem, however, is straightforward. **==We can first convert any given tree into a complete binary tree by filling in the empty spaces with dummy nodes. These dummy nodes hold a garbage value that helps us identify them as dummy nodes. This way, a non-complete binary tree is first converted to a complete binary tree,==** which is then enumerated and implemented as an array.

![[Pasted image 20251029151949.png]]

**Do we have to modify the original tree by adding dummy nodes?**

We do **not** have to modify the original tree. You can think of it as implementing the original tree in the **skeleton** of the closest complete binary tree. In that skeleton, we mark the dummy nodes to clarify that they are not in the original tree. We also modify all our algorithms that traverse or operate on the tree to ignore the dummy nodes completely. We use these dummy nodes to ensure our mathematical equations to hop around the tree still work as before.

### Limitations

The limitations of implementing a non-complete binary tree using arrays should be pretty clear now. Dummy nodes do not store any data but still use the same amount of memory as any other node in the array implementation. Depending on the structure of the tree we are trying to implement, this extra wasted space maybe even more than the size of the actual tree.

![[Pasted image 20251029152037.png]]

# Linked List Based Binary Trees

a binary tree as a two-dimensional linked list. Instead of just having just one `next` section, what if the linked list had two `next` sections.

![[Pasted image 20251029154823.png]]

This is exactly what a linked list implementation of a binary tree is. To implement a binary tree, we extend the general idea of a linked list node to two dimensions.

## Defining a Node in Binary Tree

Every data structure comprises some fundamental elementary units that connect to make up that data structure. A node is the fundamental building block of a binary tree. Since a binary tree can have only two children, they can be conveniently named **left** and **right** depending on which side of the parent node they fall into when drawn on a 2D surface. 

### Structure of a node

A binary tree node has three sections. It holds references to its two children in its `left` and `right` sections and the data items in the `data` section.

> - **data** - The actual data item a node holds. This could be of any type.
> - **left** - The is a reference to the **left** child of this node.
> - **right** - The is a reference to the **right** child of this node.

![[Pasted image 20251029154926.png]]

```java
// Definition for a binary tree node.
class TreeNode {

     int val;

     TreeNode left;

     TreeNode right;

     TreeNode() {}

     TreeNode(int val) { this.val = val; }
}
```

## Structure of a Binary Tree

 Multiple nodes link up by referencing child nodes to create the binary tree structure.
 
![[Pasted image 20251029155141.png]]

What looks like a tree on paper looks very different in computer memory. This is because a binary tree comprises nodes created at runtime and can be located anywhere in the memory. The tree structure we imagine or draw on paper **logically** represents this linked data structure in memory. Let us look at a binary tree in the computer memory.

![[Pasted image 20251029155206.png]]

### Root node

The tree's **root** node is the most important as it is this node from where it starts. Nodes of a binary tree are scattered all around the memory, so a node can only be accessed using its reference in the memory. This reference, however, is stored in the **left** or **right** section of the parent of a node. This is true for every node except the **root** node, as it does not have a parent. We can reach any node in the tree from the root node by following the appropriate path. This is why, **==to access a tree, we should always have the reference to its root node stored somewhere.==**

![[Pasted image 20251029155317.png]]

### Leaf nodes

A node in the tree that does not have any children is called the **leaf** node. Because they do not have children, a leaf node's **left** and **right** sections are **null**, just like the last node of a singly linked list. Just like a singly linked list, these `null` references help us know when to stop when traversing the tree.

![[Pasted image 20251029155346.png]]

# Recursive traversals

A binary tree is a non-linear data structure spread out in two dimensions, so we need to move in both dimensions. 

Because we have two dimensions to worry about in trees, there can be many different ways to traverse a tree.

Any sequence of moving forward, backward, up, and down that eventually visits each node in the tree can be counted as a traversal algorithm.

## Preorder Traversal

**==In this method, each node is processed in a specific sequence: first, the root node is visited, followed by the left subtree, and then the right subtree.==**

 A simple recursive equation can summarize the traversal process.

![[Pasted image 20251030152534.png]]

- **Step 1:** Visit the node.
- **Step 2:** Recursively traverse the node's `left` subtree.
- **Step 3:** Recursively traverse the node's `right` subtree.

```java
import java.util.*;

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
    public void preorder(TreeNode root, List<Integer> result) {
        // Base case: If the current node is null (empty), return.
        if (root == null) {
            return;
        }

        // Step 1: Visit the current node and store its value in the
        // 'result' list
        result.add(root.val);

        // Step 2: Recursively traverse the left subtree
        preorder(root.left, result);

        // Step 3: Recursively traverse the right subtree
        preorder(root.right, result);
    }

    public List<Integer> recursivePreorderTraversal(TreeNode root) {
        // Create an empty list to store the preorder traversal result.
        List<Integer> result = new ArrayList<>();

        // Start the recursive preorder traversal from the 'root' node.
        preorder(root, result);

        // Return the final result containing the preorder traversal of
        // the binary tree.
        return result;
    }
}
```

## Inorder Traversal

 **==In this method, each node is processed in the given sequence: first, the left subtree is visited, then the root node, and finally, the right subtree.==**

**In what scenarios is inorder traversal useful?**

Inorder traversal is particularly valuable when dealing with binary search trees (BSTs). It accesses the nodes in ascending order, making it an essential method for sorting and validating the BST property.

![[Pasted image 20251030153125.png]]

- **Step 1:** Recursively traverse the node's `left` subtree.
- **Step 2:** Visit the node.
- **Step 3:** Recursively traverse the node's `right` subtree.

```JAVA
import java.util.*;

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
    public void inorder(TreeNode root, List<Integer> result) {
        // Base case: If the current node is null, return.
        if (root == null) {
            return;
        }

        // Step 1: Recursively traverse the left subtree.
        inorder(root.left, result);

        // Step 2: Visit the current node and store its value in
        // 'result'.
        result.add(root.val);

        // Step 3: Recursively traverse the right subtree.
        inorder(root.right, result);
    }

    public List<Integer> recursiveInorderTraversal(TreeNode root) {
        // Create an empty list to store the inorder traversal result.
        List<Integer> result = new ArrayList<>();

        // Start the recursive inorder traversal from the 'root' node.
        inorder(root, result);

        // Return the final result containing the inorder traversal of
        // the binary tree.
        return result;
    }
}
```

## Postorder Traversal

 **==This method recursively visits the left subtree, the right subtree, and finally, the root node.==**

![[Pasted image 20251030153540.png]]

- **Step 1:** Recursively traverse the node's `left` subtree.
- **Step 2:** Recursively traverse the node's `right` subtree.
- **Step 3:** Visit the node.

```java
import java.util.*;

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
    public void postorder(TreeNode root, List<Integer> result) {
        // Base case: If the current node is null (empty), return.
        if (root == null) {
            return;
        }

        // Step 1: Recursively traverse the left subtree.
        postorder(root.left, result);

        // Step 2: Recursively traverse the right subtree.
        postorder(root.right, result);

        // Step 3: Visit the current node and store its value in
        // 'result'.
        result.add(root.val);
    }

    public List<Integer> recursivePostorderTraversal(TreeNode root) {
        // Create an empty list to store the postorder traversal result.
        List<Integer> result = new ArrayList<>();

        // Start the recursive postorder traversal from the 'root' node.
        postorder(root, result);

        // Return the final result containing the postorder traversal of
        // the binary tree.
        return result;
    }
}
```

# Iterative Traversals

The recursive tree traversal algorithms they all have a major limitation: ==They rely on recursive function calls, which rely on **stack memory**.==

Recursive function calls repeatedly call the same function until a base case is reached. Consequently, the call stack **grows** linearly with the number of function calls before reaching the base case. The call stack, however, is **limited** in space, so it can only accommodate a certain number of stack frames, after which there is a stack overflow and the program crashes

Iterative tree traversal algorithms overcome this limitation by not relying on recursive function calls. The iterative preorder, ``inorder``, and ``postorder`` traversal versions don't rely on the call stack and use an explicit stack to simulate the same **LIFO** behavior.

## Iterative Preorder Traversal

- **Step 1:** Visit the node.
- **Step 2:** Recursively traverse the node's `left` subtree.
- **Step 3:** Recursively traverse the node's `right` subtree.

### Iterative Steps

This traversal is recursive as the second and third steps of preorder traversal use preorder traversal again.

- **Step 1:** Visit the node and traverse its `left` subtree.
- **Step 2:** Traverse the node's `right` subtree.

### 1. Visit the node and traverse its left subtree.

The first step of preorder traversal is to visit the current node. The next step is to traverse the left subtree. Following the definition, for a tree rooted at node **R,** we visit the node **R** and then go to its left subtree. We then visit the root node of the left subtree and then go further to its left subtree. This process goes on and on and on until we finally hit a `null`. We stop at `null` because there is nowhere to go beyond that. Let's say this `null` was the **left** child of node **N**

In the recursive implementation of preorder traversal, hitting a `null` is the base case of recursion, and if we hit it, we backtrack to the parent with the help of the function call stack. However, we can't leverage the function call stack in the iterative implementation, so we use our own stack to replicate this behavior.

To visit the node and traverse its left subtree, we initialize a `current` variable and set it to hold the node **R**. Once we are done visiting the node, we push `current` to the stack and set `current` to hold to its left child. We repeat this process until we hit a `null`

- **Step 1:** While `current` is not equal to `null`, do the following:
    - **Step 1.1:** Visit the `current` node.
    - **Step 1.2:** Push the `current` node to the stack.
    - **Step 1.3:** Set the `current` pointer to hold the reference of the `current` node's `left` child.


### 2. Traverse the node's right subtree

Once we hit a `null` it means that we are done traversing a node's left subtree. The next step is to identify that node and preorder traverse its right subtree

We look at the top of the stack to get the node for which the left subtree has been completely traversed and set `current` to this node to effectively **jump** back to this node. Once we have made the jump, we remove the top of the stack by doing a pop operation.

Next, we move to the right subtree by setting `current` to the popped node's right child. Then, we repeat the entire process from **Step 1: Visit the node and traverse its left subtree** for the subtree rooted at the node held by `current`.

- **Step 1:** If the stack is not empty, do the following:
    - **Step 1.1:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 1.2:** Pop the top of the stack.
    - **Step 1.3:** Set the `current` pointer to hold the reference of the `current` node's `right` child.


### Algorithm

- **Step 1:** Set the `current` pointer to hold the reference of the `root` node.
- **Step 2:** While `current` is not equal to `null` or the stack is not empty, do the following:
    - **Step 2.1:** While `current` is not equal to `null`, do the following:
        - **Step 2.1.1:** Visit the `current` node.
        - **Step 2.1.2:** Push the `current` node to the stack.
        - **Step 2.1.3:** Set the `current` pointer to hold the reference of the `current` node's `left` child.
    - **Step 2.2:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 2.3:** Pop the top of the stack.
    - **Step 2.4:** Set the `current` pointer to hold the reference of the `current` node's `right` child.

```java
import java.util.*;

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
    public List<Integer> iterativePreorderTraversal(TreeNode root) {
        // Create a list to store the result of preorder traversal
        List<Integer> result = new ArrayList<>();
        // Create a stack to help traverse the binary tree iteratively
        Stack<TreeNode> stack = new Stack<>();
        // Start from the root node
        TreeNode current = root;

        // Continue traversal until we reach the end of the tree (current is null) and the stack is empty
        while (current != null || !stack.isEmpty()) {
            // Traverse to the leftmost node and store the node values in the result list
            while (current != null) {
                result.add(current.val);
                stack.push(current);
                current = current.left;
            }

            // If the current node is null, we reached the leftmost leaf or subtree
            // We backtrack to the parent node by popping from the stack and move to its right subtree
            current = stack.pop();
            current = current.right;
        }

        // Return the result list containing the preorder traversal of the binary tree
        return result;
    }
}

```


## Iterative Inorder Traversal

> - **Step 1:** Recursively traverse the node's `left` subtree.
> - **Step 2:** Visit the node.
> - **Step 3:** Recursively traverse the node's `right` subtree.

### Iterative Steps

> - **Step 1:** Traverse the node's `left` subtree.
> - **Step 2:** Visit the node.
> - **Step 3:** Traverse the node's `right` subtree.

### 1. Traverse the node's left subtree

The first step of inorder traversal is to visit the left subtree using inorder traversal. Following this definition, for a tree rooted at node **R**, we start from the node **R** and then keep going left until we reach a `null`. We stop at `null` because there is nowhere to go beyond that. Let's say this `null` was the left child of node **N**

In the recursive implementation of inorder traversal, hitting a `null` is the base case of recursion, and if we hit it, we backtrack to the parent with the help of the function call stack. However, we can't leverage the function call stack in the iterative implementation, so we use our own stack to replicate this behavior.

To traverse the left subtree, we initialize a `current` variable and set it to hold the node **R**. We push `current` to the stack and set `current` to hold its left child. We repeat this process until we hit a `null`

> - **Step 1:** While `current` is not equal to `null`, do the following:
>     - **Step 1.1:** Push the `current` node to the stack.
>     - **Step 1.2:** Set the `current` pointer to hold the reference of the `current` node's `left` child.

### 2. Visit the node

Once we hit a `null` it means that we are done traversing a node's left subtree. The next step is to identify that node and visit it.

We look at the top of the stack to get the node for which the left subtree has been completely traversed and set `current` to this node to effectively **jump** back to this node. Once we have made the jump, we remove the top of the stack.

We then go ahead and visit the node held in `current`.

- **Step 1:** If the stack is not empty, do the following:
    - **Step 1.1:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 1.2:** Pop the top of the stack.
    - **Step 1.3:** Visit the `current` node.

## 3. Traverse the node's right subtree

Once the traversing of the left subtree and the node itself is complete, the next step is to traverse its right subtree. We move to the right subtree by setting `current` to hold its right child. Then, we repeat the entire process from **Step 1: Traverse the node's left subtree** for the subtree rooted at the node held by `current`.

**Algorithm**

- **Step 1:** Set the `current` pointer to hold the reference of the `current` node's `right` child.
- **Step 2:** Go the initial step of traversing the node's `left` subtree

### Algorithm

- **Step 1:** Set the `current` pointer to hold the reference of the `root` node.
- **Step 2:** While `current` is not equal to `null` or the stack is not empty, do the following:
    - **Step 2.1:** While `current` is not equal to `null`, do the following:
        - **Step 2.1.1:** Push the `current` node to the stack.
        - **Step 2.1.2:** Set the `current` pointer to hold the reference of the `current` node's `left` child.
    - **Step 2.2:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 2.3:** Pop the top of the stack.
    - **Step 2.4:** Visit the `current` node.
    - **Step 2.5:** Set the `current` pointer to hold the reference of the `current` node's `right` child.


```java
import java.util.*;

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *      int val;
 *      TreeNode left;
 *      TreeNode right;
 *      TreeNode() {}
 *      TreeNode(int val) { this.val = val; }
 * }
 */

class Solution {
    public List<Integer> iterativeInorderTraversal(TreeNode root) {
        // Create a list to store the result of inorder traversal
        List<Integer> result = new ArrayList<>();
        // Create a stack to help traverse the binary tree iteratively
        Stack<TreeNode> stack = new Stack<>();
        // Start from the root node
        TreeNode current = root;

        // Continue traversal until we reach the end of the tree (current is null) and the stack is empty
        while (current != null || !stack.empty()) {
            // Traverse to the leftmost node and store the node values in the result list
            while (current != null) {
                stack.push(current);
                current = current.left;
            }

            // If the current node is null, we have reached the leftmost leaf or subtree
            // We backtrack to the parent node by popping from the stack, process the current node
            // and move to its right subtree.
            current = stack.pop();
            result.add(current.val);
            current = current.right;
        }

        // Return the result list containing the inorder traversal of the binary tree
        return result;
    }
}

```

## Iterative Postorder Traversal

> - **Step 1:** Recursively traverse the node's `left` subtree.
> - **Step 2:** Recursively traverse the node's `right` subtree.
> - **Step 3:** Visit the node.

### Iterative Steps

> - **Step 1:** Traverse the node's `left` subtree.
> - **Step 2:** Traverse the node's `right` subtree.
> - **Step 3:** Visit the node.

To create an iterative algorithm, we will first follow these steps sequentially. The complete algorithm will make sense when we combine all these steps and consider the big picture.

### 1. Traverse the node's left subtree

The first step of postorder traversal is to traverse the left subtree using postorder traversal. Following this definition, for a tree rooted at node **R**, we start from the node **R** and then keep going left until we reach a `null`. We stop at `null` because there is nowhere to go beyond that. Let's say this `null` was the left child of node **N.**

In the recursive implementation of postorder traversal, hitting a `null` is the base case of recursion, and we backtrack to the parent with the help of the function call stack and move to the node's right subtree.

Two possible cases when we backtrack to the node N are

> 1. If the right subtree of N has not yet been traversed, then we should traverse it (common with preorder and inorder traversals).
> 2. If the right subtree of N has already been traversed, we should stop here and visit the node (specific to postorder traversal).

In the recursive implementation of postorder traversal, we do not need any extra information to decide between the cases as we place the recursive function calls and code to process the node in the proper sequence in the recursive function. However, we can't leverage the function call stack and this execution sequence in the iterative implementation, so we use our own stack to replicate this behavior.

To go left, we initialize a `current` variable and set it to hold the node **R**. We push `current` to the stack **two times** and set `current` to hold its right child. We repeat this process until we hit a `null`

> - **Step 1:** While `current` is not equal to `null`, do the following:
>     - **Step 1.1:** Push the `current` node to the stack.
>     - **Step 1.2:** Push the `current` node again to the stack.
>     - **Step 1.3:** Set the `current` pointer to hold the reference of the `current` node's `left` child.

### 2. Traverse the node's right subtree

We must traverse a node's right subtree(go right) once we traverse its left subtree. Since `null` is the termination of a tree, hitting a `null` as the left child for a node means that we are done traversing the **left** subtree for that node.

There is one other way we can reach this step without hitting `null`  but we will learn that in **Step 3: Visit the node**. The next step is to identify that node(**N**) and traverse its right subtree.

We look at the top of the stack to get the node for which the left subtree has been completely traversed and set `current` to this node to effectively **jump** back to this node and pop the address from the top of the stack.

Then, we move to the right subtree by setting `current` to its right child. Then, we repeat the entire process from **Step 1: Traverse the node's left subtree** for the subtree rooted at the node held in `current`.

- **Step 1:** If the stack is not empty, do the following:
    - **Step 1.1:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 1.2:** Pop the top of the stack.
    - **Step 1.3:** If the stack is not empty, and the top of the stack is the same as the `current` node, do the following:
        - **Step 1.3.1:** Set the `current` pointer to hold the reference of the `current` node's `right` child.
        - **Step 1.3.2:** Go to the initial step of traversing the node's `left` subtree.


### 3. Visit the node

We reach this step when we hit a `null` as the **right** child of a node. Hitting a `null` as the right child means that the traversal of the right subtree for some node(say N) has finished. Since we are following postorder traversal, the traversal of both the left and right subtree for the node has finished, and we need to process the node itself now.

We look at the top of the stack to get the node(N) for which both the left and right subtree have been completely traversed and set `current` to this node to effectively **jump** back to this node and pop it from the top of the stack.

Once the node(N) is processed, we will complete the postorder traversal for the entire subtree at node N. This also means we have completely traversed the **left** subtree of the parent of node N, say P. This is logically equivalent to hitting a `null` as the **left** child of P. The next step is to traverse the right subtree of P, so we repeat the steps from **Step 2: Traverse the node's right subtree**.

- **Step 1:** If the stack is not empty, do the following:
    - **Step 1.1:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 1.2:** Pop the top of the stack.
    - **Step 1.3:** If the stack is empty, or the top of the stack is not equal to the `current` node, do the following:
        - **Step 1.3.1:** Visit the `current` node.
        - **Step 1.3.2:** Set the `current` pointer to `null` so that in the next iteration, the algorithm goes to the second step of traversing the node's `right` subtree.


### Algorithm

- **Step 1:** Set the `current` pointer to hold the reference of the `root` node.
- **Step 2:** While `current` is not equal to `null` or the stack is not empty, do the following:
    - **Step 2.1:** While `current` is not equal to `null`, do the following:
        - **Step 2.1.1:** Push the `current` node to the stack.
        - **Step 2.1.2:** Push the `current` node again to the stack.
        - **Step 2.1.3:** Set the `current` pointer to hold the reference of the `current` node's `left` child.
    - **Step 2.2:** Set the `current` pointer to store the reference of the node at the top of the stack.
    - **Step 2.3:** Pop the top of the stack.
    - **Step 2.4:** If the stack is not empty, and the top of the stack is the same as the `current` node, do the following:
        - **Step 2.4.1:** Set the `current` pointer to hold the reference of the `current` node's `right` child.
    - **Step 2.5:** Else, if the stack is empty, or the top of the stack is not equal to the `current` node, do the following:
        - **Step 2.5.1:** Visit the `current` node.
        - **Step 2.5.2:** Set the `current` pointer to `null` so that in the next iteration, the algorithm goes to the second step of traversing the node's `right` subtree.


```java
import java.util.*;

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *      int val;
 *      TreeNode left;
 *      TreeNode right;
 *      TreeNode() {}
 *      TreeNode(int val) { this.val = val; }
 * }
 */

class Solution {
    public List<Integer> iterativePostorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;

        // Iterate until the current node is null and the stack is empty
        while (current != null || !stack.isEmpty()) {

            // Traverse the left subtree and push nodes twice into the stack
            while (current != null) {
                stack.push(current);
                // Push the node twice to indicate it's not yet processed
                stack.push(current);
                current = current.left;
            }

            // Retrieve the top node from the stack
            current = stack.pop();

            // Check if the next node on top of the stack is the same as the current node
            // If yes, it means the right subtree of the current node hasn't been processed yet
            if (!stack.isEmpty() && current == stack.peek()) {
                // Move to the right subtree
                current = current.right;
            } else {
                // Add the value of the current node to the result
                result.add(current.val);
                // Set current to null to avoid revisiting the node
                current = null;
            }
        }
        return result;
    }
}
```

## Level Order Traversal

Level order traversal is a way of traversing a tree, where we traverse one level at a time. **==The nodes in the tree are traversed from top to bottom, from left to right.==**


Level order traversal follows the following order:

![[Pasted image 20251031123839.png]]


1. Process level 0
2. Process level 1
3. ...
4. ...

### Algorithm

Level order traversal is implemented quite differently than all the other traversals we have seen. It has a non-recursive implementation that uses a `queue` data structure. The traversal is the same as a **Breadth First Search** in a graph that follows exactly the same order.

- **Step 1:** Create a queue and a list of lists called `levels` to store all the levels of the tree.
- **Step 2:** Add the `root` node to the queue.
- **Step 3:** While the queue is not empty, do the following:
    - **Step 3.1:** Store the queue size (also the size of the current level) in a variable `levelSize`.
    - **Step 3.2:** Iterate over this level using the `levelSize` and do the following:
        - **Step 3.2.1:** Pop the first node from the queue and process it.
        - **Step 3.2.2:** If the `left` child of the popped node is not `null`, add it to the queue.
        - **Step 3.2.3:** If the `right` child of the popped node is not `null`, add it to the queue.
        - **Step 3.2.4:** Decrement the `size` by `1`.
    - **Step 3.3:** Add the processed level to the `levels` list.


```java
import java.util.*;

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *      int val;
 *      TreeNode left;
 *      TreeNode right;
 *      TreeNode() {}
 *      TreeNode(int val) { this.val = val; }
 * }
 */

class Solution {
    public List<List<Integer>> levelOrderTraversal(TreeNode root) {
        // Create a queue to perform level-order traversal
        Queue<TreeNode> queue = new LinkedList<>();
        // Create a list to store the final result
        List<List<Integer>> levels = new ArrayList<>();

        // If the tree is empty, return an empty result
        if (root == null) {
            return levels;
        }

        // Start the traversal by adding the root node into the queue
        queue.add(root);

        // Perform level-order traversal using the queue
        while (!queue.isEmpty()) {
            // Get the number of nodes in the current level
            int levelSize = queue.size();
            // Create a list to store the nodes in the current level
            List<Integer> level = new ArrayList<>();

            // Process all nodes in the current level
            for (int i = 0; i < levelSize; i++) {
                // Get the front node from the queue
                TreeNode node = queue.poll();
                // Add the value of the current node to the level list
                level.add(node.val);

                // Add the left child of the current node to the queue if it exists
                if (node.left != null) {
                    queue.add(node.left);
                }

                // Add the right child of the current node to the queue if it exists
                if (node.right != null) {
                    queue.add(node.right);
                }
            }

            // Add the current level list to the levels list
            levels.add(level);
        }

        // Return the final result after completing the traversal
        return levels;
    }
}
```

# Constructing a Binary Tree

## Challenges in Construction From Preorder Traversal

### Serialization

To serialize the tree, we write down its preorder traversal sequence.

### Deserialization

When deserializing, we need to only look at the preorder traversal sequence and reconstruct the same tree we serialized earlier.

Reconstructing a tree by looking only at the preorder traversal sequence consists of the following steps.

> 1. The first element in the preorder traversal array is the root node.
> 2. The next element in the preorder traversal array can be either:
>     - The left node of the root if the root has a left subtree.
>     - The right node of the root if the root does not have a left subtree.


![[Pasted image 20251102110909.png]]

Because deciding whether the next element in the preorder traversal sequence is the left node or the right node is ambiguous, the sequence can generate multiple tree representations depending on the decision between left and right made at each step. This means that preorder traversal cannot be used to deserialize a tree uniquely.

## Challenges in Construction From Inorder Traversal

Constructing a tree just by looking at its inorder traversal sequence is impossible. This is because, **==unlike preorder and postorder traversal sequences, we cannot look at the inorder traversal sequence and find the root node. The root node can be anywhere in the sequence.==**

![[Pasted image 20251102111120.png]]

Because deciding the root node in the in-order traversal sequence is ambiguous, it can generate multiple different tree representations depending on what node we select as the root node at every step. This means that inorder traversal cannot be used to deserialize a tree uniquely.

## Challenges in Construction From Postorder Traversal

The reconstruction process of a tree by looking only at the postorder traversal sequence looks something like the steps below.

> 1. The last element in the postorder traversal sequence is the root node.
> 2. The second last element in the postorder traversal sequence can be either:
>     - The right node of the root if the root has a right subtree.
>     - The left node of the root if the root does not have a right subtree.

![[Pasted image 20251102111508.png]]

Because of the ambiguity in deciding if the next element in the postorder traversal sequence is the left node or the right node, the postorder traversal sequence can generate multiple tree representations depending on the decision between left and right made at each step. This means that postorder traversal alone cannot be used to deserialize a tree uniquely.

## Understanding Construction Using Preorder and Inorder Traversal

If given both the preorder and inorder traversal sequence of a binary tree, we can construct the tree. We use both sequences in tandem to construct the tree and resolve any ambiguity incrementally.

![[Pasted image 20251102111723.png]]

- **Step 1:** We know the first element in the preorder traversal sequence is the root node, so we use it to construct the `root` node.
- **Step 2:** Find the location of the `root` node in the inorder traversal sequence.
- **Step 3:** If the `root` node in the inorder traversal sequence has elements to its left, it indicates the presence of a `left` subtree. In this case, the next element in the preorder sequence is the `left` child, which is a clear and straightforward condition.
- **Step 4:** If the `root` node in the inorder traversal sequence does not have elements to its left but elements to its right, the root node does not have a left subtree, so the next element in the preorder sequence is the `right` child.
- **Step 5:** If the `root` node in the inorder traversal sequence does not have elements to its left and right, we are done creating the tree.

![[Pasted image 20251102111741.png]]

### Algorithm

To implement the idea, we move the preorder traversal array from start to end and construct a binary tree in **a preorder fashion**. Constructing a tree in a preorder fashion means we first construct the current node, followed by the left and right subtree of the current node recursively. We use the given inorder traversal array to resolve ambiguity at every step and decide if the next node is the left and right subtree or if we are done constructing the entire subtree from the current node and must return the node.

- **Step 1:** Set the global variable `preInd` = `0`
- **Step 2:** Recursively start constructing the tree for the range `[0, inorder.length - 1]`.
    - **Step 2.1:** Return `null` if the `inStart > inEnd` means it is a `null` node.
    - **Step 2.2:** Create a node with the value `preorder[preInd]`.
    - **Step 2.3:** Find the `index` of value `preorder[preInd]` in the inorder array from `inStart` to `inEnd`. The current node's left and right subtree in the inorder array are in the range `[inStart, index - 1]` and `[index + 1, inEnd]`, respectively.
    - **Step 2.4:** Increment `preInd` by `1`.
    - **Step 2.5:** Recursively construct the left subtree using the range `[inStart, index - 1]`
    - **Step 2.6:** Recursively construct the right subtree using the range `[index + 1, inEnd]`
    - **Step 2.7:** Return the node created in `Step 2.2`.


```java
import java.util.*;

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
    // Global variable to keep track of the current index in the preorder traversal
    int preInd = 0;

    // Helper function to find the index of a given value in the inorder traversal
    int findIndex(int[] inorder, int start, int end, int val) {
        for (int i = start; i <= end; i++) {
            if (inorder[i] == val) return i;
        }
        // If the value is not found in the inorder array, return the start index
        return start;
    }

    TreeNode buildTree(int[] inorder, int inStart, int inEnd, int[] preorder) {
        // Base case: if the inorder range is empty, return null to indicate an empty subtree
        if (inStart > inEnd) return null;

        // Create a new node using the current value from the preorder traversal
        TreeNode currentNode = new TreeNode(preorder[preInd]);

        // Find the index of the current value in the inorder traversal
        int index = findIndex(inorder, inStart, inEnd, preorder[preInd]);

        // Move to the next value in the preorder traversal
        preInd++;

        // Recursively construct the left and right subtrees using the appropriate ranges
        currentNode.left = buildTree(inorder, inStart, index - 1, preorder);
        currentNode.right = buildTree(inorder, index + 1, inEnd, preorder);

        // Return the current node, which is the root of the constructed subtree
        return currentNode;
    }

    public TreeNode preorderAndInorderReconstruction(int[] preorder, int[] inorder) {
        // Call the recursive buildTree function with the entire ranges
        return buildTree(inorder, 0, inorder.length - 1, preorder);
    }
}
```

## Understanding Construction Using Postorder and Inorder Traversal

Just like with preorder and inorder construction, we can construct a binary tree if both its postorder and inorder traversal sequence are given. We use both sequences in tandem to construct the tree and resolve any ambiguity incrementally.

![[Pasted image 20251102111953.png]]


- **Step 1:** In constructing a binary tree, we identify the last element in the postorder traversal sequence, the `root `node.
- **Step 2:** Find the location of the `root` node in the inorder traversal sequence.
- **Step 3:** If the `root` node in the inorder traversal sequence has elements to its right, the root node has a `right` subtree, so the second last element in the postorder sequence is the `right` child.
- **Step 4:** If the `root` node in the inorder traversal sequence does not have elements to its right but elements to its left, the root node does not have a `right` subtree, so the second last element in the postorder sequence is the `left` child.
- **Step 5:** If the `root` node in the inorder traversal sequence does not have elements to its right and left, we are done creating the tree.

![[Pasted image 20251102112048.png]]

### Algorithm

- **Step 1:** Set the global variable `postInd` = `postOrder.length - 1`
- **Step 2:** Recursively start constructing the tree for the range `[0, inorder.length - 1]`.
    - **Step 2.1:** Return `null` if the `inStart > inEnd` means it is a `null` node.
    - **Step 2.2:** Create a node with the value `postorder[postInd]`.
    - **Step 2.3:** Find the `index` of value `postorder[postInd]` in the inorder array from `inStart` to `inEnd`. The current node's right and left subtree in the inorder array are in the range `[index + 1, inEnd]` and `[inStart, index - 1]`, respectively.
    - **Step 2.4:** Decrement `postInd` by `1`.
    - **Step 2.5:** Recursively construct the right subtree using the range `[index + 1, inEnd]`
    - **Step 2.6:** Recursively construct the left subtree using the range `[inStart, index - 1]`
    - **Step 2.7:** Return the node created in `Step 2.2`.

```java
import java.util.*;

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
    // Global variable to keep track of the index in the postorder traversal
    public int postInd;

    // Helper function to find the index of a given value in the inorder traversal
    public int findIndex(int[] inorder, int start, int end, int val) {
        for (int i = start; i <= end; i++) {
            if (inorder[i] == val) return i;
        }
        // If the value is not found in the inorder array, return the start index
        return start;
    }

    public TreeNode buildTree(int[] inorder, int inStart, int inEnd, int[] postorder) {
        // Base case: If the current inorder range is empty, return null
        if (inStart > inEnd) return null;

        // Create a new node with the current postorder element
        TreeNode currentNode = new TreeNode(postorder[postInd]);

        // Find the index of this element in inorder
        int index = findIndex(inorder, inStart, inEnd, postorder[postInd]);

        // Move to the next postorder element
        postInd--;

        // Recursively build the right subtree with elements after the current index
        currentNode.right = buildTree(inorder, index + 1, inEnd, postorder);

        // Recursively build the left subtree with elements before the current index
        currentNode.left = buildTree(inorder, inStart, index - 1, postorder);

        // Return the current node with its left and right subtrees constructed
        return currentNode;
    }

    public TreeNode postorderAndInorderReconstruction(int[] postorder, int[] inorder) {
        // Initialize the postInd to the last index of the postorder traversal
        postInd = postorder.length - 1;

        // Call the helper function with the full range of inorder traversal
        return buildTree(inorder, 0, inorder.length - 1, postorder);
    }
}
```

# Insertion in Binary Trees

## Insertion at Root

The operation is simple as it does not involve any tree traversal and adds links to the existing tree. There are two cases to consider.

### 1. The tree is empty

If the given tree is empty, we can create a new node with the given value, which becomes the tree itself.

![[Pasted image 20251103111831.png]]

> - **Step 1**: Create a new node with the given data.
> - **Step 2**: Return the new node, as this is the new `root`.

### 2. The tree is not empty

If the tree is not empty, we create a new node and link the existing tree as its left or right subtree. Deciding whether the old tree should be the left or right child of the newly created node is subjective.

![[Pasted image 20251103112140.png]]

- **Step 1**: Create a new node with the given data.
- **Step 2**: Set the new node's `left`(or `right`) pointer to hold the reference of the existing `root`.
- **Step 3**: Return the new node, as this is the new `root`.

```java
/**
 * Definition for a binary tree node.

 * class TreeNode {

 *      int val;

 *      TreeNode left;

 *      TreeNode right;

 *      TreeNode() {}

 *      TreeNode(int val) { this.val = val; }

 * }

 */
 
class Solution {
    public TreeNode insertRoot(TreeNode root, int data) {
        // Create a new node with the given data value
        TreeNode newRoot = new TreeNode(data);

        // Set the current root as the left child of the new node
        newRoot.left = root;

        // Return the new root
        return newRoot;
    }
}
```

## Insertion of a Leaf

A new node can be easily inserted in the binary tree as a leaf node by recursively going down the tree from top to bottom. The insert process can be summarized in three simple steps, which are given below.

> - **Step 1:** Traverse the tree and find the first node that does **not** have a `left` or `right` subtree.
> - **Step 2:** Create a new node with the given data and link it to the node found in step 1.

### Algorithm

To insert a new node as a leaf node, we first need to decide which node in the given tree would be the parent of the newly inserted node. To do this, we have to traverse the tree and identify the first node that does not have either a left child, a right child, or both. This node can act as the parent of our newly inserted node. We can use any traversal algorithms we have learned so far to find this node.

- **Step 1:** Look for a free spot from the `root` node.
- **Step 2:** If the `root` node is `null`, create a new node with the given data and return it.
- **Step 3:** Else, if the `root` node does not have a `left` subtree, create and insert the new node as the `left` child of the `root` and return the `root`.
- **Step 4:** Else, if the `root` node does not have a `right` subtree, create and insert the new node as the `right` child of the `root` and return the `root`.
- **Step 5:** Else, recursively call **Step 1** with the `left/right` subtree.

**Note :** We can choose any direction, `left` or `right`, but it should be consistent throughout the traversal

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
    public TreeNode recursivelyInsertALeaf(TreeNode root, int value) {
        // If the tree is empty, create a new node and return it as the root
        if (root == null) {
            return new TreeNode(value);
        }

        // Recursively insert into the left subtree
        if (root.left == null) {
            root.left = new TreeNode(value);
        }
        // Recursively insert into the right subtree
        else if (root.right == null) {
            root.right = new TreeNode(value);
        }
        // If both left and right subtrees are not null,
        // recursively try inserting into the left subtree
        else {
            recursivelyInsertALeaf(root.left, value);
        }

        return root;
    }
}
```

**Why only go in one direction when a node has both left and right subtrees?**

Let's assume we are at a node X with both left and right subtrees. In that case, we will hit the final `else` statement and go down in one direction (left in this case). We are guaranteed to find either a leaf node or a node without a left or right node. This is the reason we do not traverse in the other direction when we recurse back to node X.

##  Iterative Insertion of a Leaf

The algorithm is still the same. We move in the tree using the **level order traversal** algorithm. This way, we only move to the next level once we have checked all the nodes for the current level.

- **Step 1:** Add the `root` node to the traversal queue.
- **Step 2:** While the queue is not empty, do the following:
    - **Step 2.1:** Pop the first node from the queue.
    - **Step 2.2:** If the `left` child of the popped node is `null`, insert the new node as its left child and return the `root` node.
    - **Step 2.3:** Else, if the `left` child of the popped node is not `null`, add it to the queue.
    - **Step 2.4:** If the `right` child of the popped node is `null`, insert the new node as its right child and return the `root` node.
    - **Step 2.5:** Else, if the `right` child of the popped node is not `null`, add it to the queue.
- **Step 3:** Return the `root` node.

```java
import java.util.*;

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
    public TreeNode iterativelyInsertALeaf(TreeNode root, int data) {
        // If the tree is empty, create a new node and return it
        if (root == null) {
            return new TreeNode(data);
        }

        // Use a queue to perform level-order traversal
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();

            // Check if the left child is null, if so, insert the new node here
            if (node.left == null) {
                node.left = new TreeNode(data);
                return root;
            } else {
                queue.add(node.left);
            }

            // Check if the right child is null, if so, insert the new node here
            if (node.right == null) {
                node.right = new TreeNode(data);
                return root;
            } else {
                queue.add(node.right);
            }
        }

        return root;
    }
}
```


## Insertion of a Child

Inserting a child is an operation in which we insert a new node with the given data as the child of a node with the given value in a binary tree. The operation is not as straightforward as inserting at the root and involves two major steps.

> - **Step 1**: Search for the node with the given value.
> - **Step 2**: Create and insert the new node.

### Step 1: Search for the node with the given value

The first step in inserting a new node as the child of a node with the given value in a binary tree is to find the node, after which the newly created node will be inserted.

> - **Step 1:** Check if the `current` node is the node with the given value.
> - **Step 2:** Search the `left` subtree of the `current` node by recursively performing a preorder traversal.
> - **Step 3:** Search the `right` subtree of the `current` node by recursively performing a preorder traversal.

### Step 2: Create and insert the new node

Once we find the node with the given value, the next step is to create a new node and insert it in the tree as the child node of the node we just found. We create a new node with the given data and add it as the left or right child of the node we found, ensuring that we relink the old child of the node. Deciding if the newly created node should be the left or right child is subjective.

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the `left` pointer of the new node to hold the node's reference stored in the `left` pointer of the node with the given value.
- **Step 3:** Set the `left` pointer of the node with the given value to hold the reference of the new node.

### Algorithm

- **Step 1:** If the `current` node is the node with the given value, do the following:
    - **Step 1.1:** Create a new node with the given data.
    - **Step 1.2:** Set the `left` pointer of the new node to hold the node's reference stored in the `left` pointer of the node with the given value.
    - **Step 1.3:** Set the `left` pointer of the node with the given value to hold the reference of the new node.
    - **Step 1.4:** Return the `current` node.
- **Step 2:** Go to `Step 1` with the `left` subtree.
- **Step 3:** Go to `Step 1` with the `right` subtree.
- **Step 4:** Return the `current` node after both the left and right subtrees are traversed.

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
    public TreeNode insertChild(TreeNode root, int parent, int data) {
        // If the root is null, there's nothing to do, return null
        if (root == null) {
            return root;
        }

        // Search for the parent node in the tree
        if (root.val == parent) {
            // If the parent is found, insert the new node as the left child
            TreeNode newNode = new TreeNode(data);
            // Attach the existing left child to the new node
            newNode.left = root.left;
            // Set the new node as the left child of the parent
            root.left = newNode;
            // Return the root (no change to the root itself)
            return root;
        }

        // Recurse for the left and right subtrees
        root.left = insertChild(root.left, parent, data);
        root.right = insertChild(root.right, parent, data);

        // Return the root of the tree
        return root;
    }
}
```

## Insertion of a Parent

Inserting a parent is an operation where we have to insert a new node with the given data as the parent of a node with the given value in a binary tree. Inserting a node as a parent is more complex than inserting it as a child. This is because, unlike when inserting the node as a child, in this case, we have first to search for the parent of the node with the given value to get the insertion position. This is not straightforward, and we will have to consider two cases.

### 1. Insert a parent of the root node

In this case, since we have to insert a node as the parent of the root node, we are essentially changing the tree's root node. Also, since the root node has no parent, we cannot use our generic algorithm to search for the parent of a node with the given value, so we will have to deal with this edge case separately.

![[Pasted image 20251103114510.png]]

- **Step 1**: Create a new node with the given data.
- **Step 2**: Set the new node's `left`(or `right`) pointer to hold the reference of the existing `root`.
- **Step 3**: Return the new node, as this is the new `root`.

### 2. Insert a parent of a non root node

This is the generic case of inserting a parent. Inserting a node as a parent of a node with the given value in a binary tree involves two major steps.

> **Algorithm**
> 
> - **Step 1**: Search the parent of the node with the given value.
> - **Step 2**: Create and insert the new node.

#### Step 1: Search the parent of the node with the given value

The first step is to find the node, **after** which the newly created node will be inserted. This node would be the **node's parent,** whose value is given. So, instead of searching for the node with the given value, **we search for a node whose left or right child has the given value**.

![[Pasted image 20251103114541.png]]

> - **Step 1:** Check if the `current` node's `left` or `right` child is the node with the given value.
> - **Step 2:** Search the `left` subtree of the `current` node by recursively performing a preorder traversal.
> - **Step 3:** Search the `right` subtree of the `current` node by recursively performing a preorder traversal.

#### Step 2: Create and insert the new node

Once we find the node **after** which we have to do the insertion (let's say X), the next step is to create a new node and insert it in the tree as the child node of X. However, we need to make sure that we add it as the correct (left or right) child of X to ensure that the newly inserted node is also the parent of the node whose value we were originally given. If the original node is the left child of its parent, we insert the newly created node as the left child. Otherwise, it is the right child. Also, we need to reconnect any broken links to ensure the tree is not split in two.

![[Pasted image 20251103114626.png]]

- **Step 1:** If the `left` node of the `current` node is the node with the given value, do the following:
    - **Step 1.1:** Create a new node with the given data.
    - **Step 1.2:** Set the `left` pointer of the new node to hold the node's reference stored in the `left` pointer of the node with the given value.
    - **Step 1.3:** Set the `left` pointer of the node with the given value to hold the reference of the new node.
- **Step 2:** Else, if the `right` node of the `current` node is the node with the given value, do the following:
    - **Step 2.1:** Create a new node with the given data.
    - **Step 2.2:** Set the `right` pointer of the new node to hold the node's reference stored in the `right` pointer of the node with the given value. This will establish the correct reference for the new node.
    - **Step 2.3:** Set the `right` pointer of the node with the given value to hold the reference of the new node.


```JAVA
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
    public TreeNode insertParent(TreeNode root, int child, int data) {
        // If root is null, return null (base case)
        if (root == null) {
            return null;
        }

        // If root itself is the child, new node becomes the root
        if (root.val == child) {
            TreeNode newNode = new TreeNode(data);
            newNode.left = root;
            return newNode;
        }

        // Check if the left child matches the child
        if (root.left != null && root.left.val == child) {
            TreeNode newNode = new TreeNode(data);
            // Set existing left child as new node's left child
            newNode.left = root.left;
            // Update parent's left child to new node
            root.left = newNode;
            return root;
        }

        // Check if the right child matches the child
        if (root.right != null && root.right.val == child) {
            TreeNode newNode = new TreeNode(data);
            // Set existing right child as new node's right child
            newNode.right = root.right;
            // Update parent's right child to new node
            root.right = newNode;
            return root;
        }

        // Recurse for the left and right subtrees
        root.left = insertParent(root.left, child, data);
        root.right = insertParent(root.right, child, data);

        // Return the root of the tree
        return root;
    }
}
```