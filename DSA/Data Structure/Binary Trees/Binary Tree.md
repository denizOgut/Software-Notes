
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

The degree of a node is the number of other nodes it is connected to.

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