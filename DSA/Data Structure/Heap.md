# Heap

## Understanding the problem

When writing a program, we often need a data store that is smart enough to remember the smallest or largest data items stored in it at all times. Inserting new data items and retrieving the new minimum or maximum should be very efficient.

One way to implement such a data store would be to use a linked list in which each node stores the patient's name and priority.

This is an easy way to store data, but what if a new patient comes in? In this case, we can add the new patient to the head of the linked list, which is a constant-time operation.

 What if a doctor becomes available, and we must extract the patient with the highest priority? We can perform a linear scan to find the highest-priority patient and delete that node from the linked list.
 
This will solve the problem at hand. However, the most frequent operation (finding the max and extracting it) involves doing a linear scan of the entire list, which is inefficient if there are many patients.

### Limitations of a linked list

Even though we can solve the problem at hand using a linked list, it is inefficient if we have to find or extract maximum priority items frequently. The solution above performs poorly.

> 1. **Extra space:** Implementing the data store as a linked list uses extra space for the next and previous pointers of the node
> 2. **Performance:** The algorithm to find and extract the min/max performs poorly as it involves a linear scan of all items.


## Exploring a possible solution

A priority queue is a data structure designed to keep track of the maximum or minimum of a continuously changing dataset.

### What is a priority queue?

A priority queue is a specialized data structure that stores data items with associated priorities. Like a regular queue, data can only be added at the end and extracted from the front.

Unlike a regular queue, which serves data in the FIFO (first in, first out) order, a priority queue always serves the highest priority data first. If two data items have the same priority, it serves them in a FIFO order.

![[Pasted image 20251119111532.png]]

 It is an abstract data type and can be implemented in many ways, including sorted arrays, self-balancing search trees, etc. Every implementation has its advantages and disadvantages.

## Understanding a heap

One of the most common priority queue implementations uses a special type of tree called a heap. It is just a tree that follows a special **heap property**. It can be implemented using a binary of N-ary tree

A heap implemented using a binary tree is also called a **binary heap,** and its heap property is as follows. 

> - The tree is a complete binary tree.
> - It follows the heap ordering property

### Complete binary tree

A complete binary tree is one in which all the levels are filled except possibly the last level, with all the nodes as left as possible.

![[Pasted image 20251119112104.png]]

### Heap ordering property

The heap ordering property makes the insertion and extraction of the highest-priority data items from a regular binary tree so efficient. It is a condition enforced on all nodes of the binary tree for it to qualify as a heap. Every node in the tree should follow the condition given below.

> A node has higher priority than both its children

![[Pasted image 20251119112253.png]]

## Types of Heaps

Priority is a subjective term but can be generally classified as numeric values. In some cases, having a lower value means having a higher priority (like ranks), while in others, having a higher value may mean having a higher priority (like scores). Depending on what classifies as a high priority, a heap can be categorized into two types.

> - Max heap
> - Min heap

### Max heap

A max heap follows the max heap ordering property, which states that the value of any given node should be **greater** than the value of all its children. **==The root node of the tree has the maximum value.==**

![[Pasted image 20251119112547.png]]

#### Min Heap

A min heap is a tree that follows the min heap ordering property, which states that the value of any given node should be **less** than the value of all its children. **==The root node of the tree has the minimum value.==**

![[Pasted image 20251119112630.png]]

## Supported Operations

**==Every data structure has its special powers, and for a heap, it is ultra-fast insertion and extraction of the highest-priority data item.==**

### Insert

The insert operation is one of the primary operations on a heap and is used to insert a data item and its associated priority. A new node with the given priority is created and added to the tree. If the new data item has the highest priority in the dataset, it makes its way to the root of the tree at the end of the operation.

![[Pasted image 20251119113116.png]]

### Delete

The delete operation is another primary operation on a heap and is used to delete an item from the heap. The node with the given data is searched and deleted from the tree. The tree is then recalibrated, and nodes are rearranged to ensure that the tree still follows the heap property. If the highest priority data item (root) is deleted, the data item with the next highest priority makes its way to the root (top) of the tree.

![[Pasted image 20251119113143.png]]

### Peek

The peek operation only looks at the highest-priority data item from the heap and returns its value. Unlike extract, it does not remove it from the heap, so it is a read-only operation that leaves the heap unmodified.

![[Pasted image 20251119113559.png]]

### Extract

The extract operation extracts the highest-priority data item from the heap. This operation removes the root node of the tree and returns its value. The data item with the next highest priority moves to the root(top) of the tree and the end of this operation.

![[Pasted image 20251119113623.png]]

### Construct

In most cases, a heap starts empty and grows as more data items are added. In some cases, however, we might need to create a heap from an existing dataset. Constructing a heap from a given dataset is a slightly more efficient way than inserting data only into an empty heap.

![[Pasted image 20251119113646.png]]

##  Tree Heap Validator

Given the **root** of a binary tree, write a function that returns `true` if the tree represents a valid min heap and returns `false` otherwise.

```java
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
    private boolean isValidHeap(TreeNode root, int parentVal) {

        // Base case: if the current root is null, it's a valid
        // heap root
        if (root == null) {
            return true;
        }

        // Check if the current root violates the min-heap property
        if (root.val < parentVal) {
            return false;
        }

        // Recursively check the left and right subtrees
        boolean isLeftSubtreeValid = isValidHeap(root.left, root.val);
        boolean isRightSubtreeValid = isValidHeap(root.right, root.val);

        // Return true only if both subtrees are valid heaps
        return isLeftSubtreeValid && isRightSubtreeValid;
    }

    public boolean treeHeapValidator(TreeNode root) {

        // Check if the root is null (empty tree), which is considered
        // a valid min-heap
        if (root == null) {
            return true;
        }

        // Start the depth-first search (DFS) from the root with an
        // initial parent value of negative infinity
        return isValidHeap(root, Integer.MIN_VALUE);
    }
}
```

# Array Implementation of Heaps

## Structure of array based heap

For any given node at the given `index` :

- **Parent** = (`index` - `1`) / `2`
- **Left child** = (`2` * `index`) + `1`
- **Right child** = (`2` * `index`) + `2`

We can use the enumeration of a complete binary tree to implement the tree in an array. The enumeration of a node can be used as an index in an array that stores the value of the respective node.

### Structure of a node

Since the heap is just a complete binary tree, the node only stores the data in the array implementation and has no left or right pointers. Simple multiplication and division can be used to move from a parent node to a child and vice versa.

## Inserting an Item in the Heap

The implementation is encapsulated in the insert function, which inserts a new node in the binary tree and ensures the resulting tree still follows the max-heap property

### Algorithm

The algorithm for inserting a new value in a heap is quite simple. Since the heap is a complete binary tree, we insert a new node at the first available free spot. When implemented in an array, this free spot is the index after the last element of the heap in the array.

The newly inserted node might violate the heap property in the resulting tree, so we recalibrate the tree to enforce the heap property. To do this, we traverse **upwards** from the newly inserted node and compare the current node with its parent at each iteration. If the value at the child node is larger than the parent, we swap the nodes. The traversal stops when we reach the root node, or the current node is no longer larger than its parent.

This way, at the end of the insert operation, the resulting binary tree still follows the heap property and remains a heap.

**Algorithm**

- **Step 1:** Insert the new element at the end of the array
- **Step 2:** Traverse upwards in the tree from the node, moving the larger value up to enforce max heap property.

### Up Heapify

The insertion algorithm inserts a new node at the end of the heap and re-enforces the heap property going **upwards** from that node. This process is also sometimes called **up-heapify**. It is generally applied when a new node is inserted, or the value of a node changes, and the subtree rooted at the new/updated node still follows the heap property. There may be a possibility that nodes above it may now violate the heap property, and so this information has to be propagated upwards.

![[Pasted image 20251119134044.png]]

```java
import java.util.*;

class MaxHeap {
    List<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Helper function to restore heap property upwards (used in insert)
    private void upHeapify(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap.get(parent) < heap.get(index)) {
            swap(index, parent);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    public void insert(int val) {
        // Insert the new value at the end of the heap
        heap.add(val);

        // Get the index of the new value
        int index = heap.size() - 1;

        // Restore the max heap property by comparing with parent nodes
        upHeapify(index);
    }
}
```

## Deleting an item from the heap

The delete operation is another primary operation on a heap and is used to delete a given node (by address) from the tree. The implementation is encapsulated in the delete function, which deletes the given node in the binary tree and ensures the resulting tree still follows the max-heap property.

### Algorithm

The algorithm for deleting a new value in a heap is quite similar to insert. However, we cannot delete a non-leaf node, which would break the tree. To overcome this, we swap the value at the given node with the last node in the binary tree. Since the last node is a leaf node, we can easily delete it.

Swapping the value from the last node to the given node might violate the heap property in the resulting tree, so we need to recalibrate it to enforce the heap property. To do this, we traverse **downwards** from the given node (that now has the swapped value) and, at each iteration, compare the current node with its children. If the value of any child node is larger than the parent, we swap the nodes and continue traversal in that direction. The traversal stops when we reach a leaf node, or the current node is larger than its children.

This way, at the end of the delete operation, the resulting binary tree still follows the heap property and remains a heap.

> **Algorithm**
> 
> - **Step 1:** Swap the value at the given node with the last node in the tree.
> - **Step 2:** Delete the last node.
> - **Step 3:** Traverse downwards in the tree from the given node, moving the smaller value down to enforce the max heap property.

### Down Heapify

The deletion algorithm updates the value of the root node of the heap and re-enforces the heap property going **downwards** from the root. This process is also sometimes called **down-heapify** and is generally applied in cases when the value of a node changes, which may cause the subtree rooted at that node to violate the heap property. Unlike up-heapify, down-heapify is applied when the nodes above the updated node still follow the heap property. Still, there may be a possibility that the nodes below it now violate the heap property, and so new information has to be propagated downwards.

![[Pasted image 20251119134250.png]]

```java
import java.util.*;

class MaxHeap {
    List<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Helper function to restore heap property upwards (used in insert)
    private void upHeapify(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap.get(parent) < heap.get(index)) {
            swap(index, parent);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to maintain the max heap property downwards
    private void downHeapify(int index) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Find the largest among the node and its left child
        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        // Find the largest among the node and its right child
        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        // If the largest is not the current node, swap and continue
        // heapify
        if (largest != index) {
            swap(index, largest);
            downHeapify(largest);
        }
    }

    public void insert(int val) {
        // Insert the new value at the end of the heap
        heap.add(val);

        // Get the index of the new value
        int index = heap.size() - 1;

        // Restore the max heap property by comparing with parent nodes
        upHeapify(index);
    }

    public void remove(int index) {
        // Replace the value with the largest possible value and heapify
        heap.set(index, heap.get(heap.size() - 1));

        // Remove the last node
        heap.remove(heap.size() - 1);

        // Restore the max heap property
        downHeapify(index);
    }
}
```

## Peeking the top item in the heap

The peek operation gets the maximum value from a max heap. The implementation is encapsulated in the peek function that copies the root node's value in the binary tree to the passed reference

### Algorithm

The algorithm for getting the maximum value in a max-heap is very simple. We return the value stored at the root node of the tree. Since we do not modify the tree, the resulting binary tree still follows the heap property and remains a heap.

**Algorithm**

- **Step 1:** Return the value stored in the root node of the tree.

```java
import java.util.*;

class MaxHeap {
    List<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Helper function to restore heap property upwards (used in insert)
    private void upHeapify(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap.get(parent) < heap.get(index)) {
            swap(index, parent);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to maintain the max heap property downwards
    private void downHeapify(int index) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Find the largest among the node and its left child
        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        // Find the largest among the node and its right child
        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        // If the largest is not the current node, swap and continue
        // heapify
        if (largest != index) {
            swap(index, largest);
            downHeapify(largest);
        }
    }

    public void insert(int val) {
        // Insert the new value at the end of the heap
        heap.add(val);

        // Get the index of the new value
        int index = heap.size() - 1;

        // Restore the max heap property by comparing with parent nodes
        upHeapify(index);
    }

    public void remove(int index) {
        // Replace the value with the largest possible value and heapify
        heap.set(index, heap.get(heap.size() - 1));

        // Remove the last node
        heap.remove(heap.size() - 1);

        // Restore the max heap property
        downHeapify(index);
    }

    public int getMax() {
        if (heap.isEmpty()) {
            return -1;
        }
        // Return the root node
        return heap.get(0);
    }
}
```

## Extracting the top item from the heap

The extract operation extracts the maximum value from a max heap. Unlike the peek operation, it also deletes the node with the maximum value from the heap. The implementation is encapsulated in the extract function that deletes the root node in the binary tree and returns its value while ensuring that the resulting binary tree is still a heap

### Algorithm

The algorithm for extracting the maximum value in a max-heap is very simple. It combines peek and delete operations. We copy the value at the tree's root node to return it later and then delete the root node using the delete operation. The delete operation ensures that the resulting binary tree still follows the heap property and remains a heap.

**Algorithm**

- **Step 1:** Copy the value of the root node in the given reference
- **Step 2:** Delete the root node

```java
import java.util.*;

class MaxHeap {
    List<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Helper function to restore heap property upwards (used in insert)
    private void upHeapify(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap.get(parent) < heap.get(index)) {
            swap(index, parent);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to maintain the max heap property downwards
    private void downHeapify(int index) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Find the largest among the node and its left child
        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        // Find the largest among the node and its right child
        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        // If the largest is not the current node, swap and continue
        // heapify
        if (largest != index) {
            swap(index, largest);
            downHeapify(largest);
        }
    }

    public void insert(int val) {
        // Insert the new value at the end of the heap
        heap.add(val);

        // Get the index of the new value
        int index = heap.size() - 1;

        // Restore the max heap property by comparing with parent nodes
        upHeapify(index);
    }

    public void remove(int index) {
        // Replace the value with the largest possible value and heapify
        heap.set(index, heap.get(heap.size() - 1));

        // Remove the last node
        heap.remove(heap.size() - 1);

        // Restore the max heap property
        downHeapify(index);
    }

    public int getMax() {
        if (heap.isEmpty()) {
            return -1;
        }
        // Return the root node
        return heap.get(0);
    }

    public int extractMax() {
        if (heap.isEmpty()) {
            return -1;
        }
        // Extract the root node
        int root = heap.get(0);

        // Delete the root node
        remove(0);

        // Return the extracted root node
        return root;
    }
}
```

## Constructing a heap

The construct operation constructs a max heap from the given list of data items. The implementation is encapsulated in the construct function, which relies on the special properties of a complete binary tree and repeatedly applies the heapify function on the input list to convert it into a heap

### Algorithm

The algorithm for constructing a heap from a given list relies on a special property and a complete binary tree. The array representation of a complete binary tree is just its level-order traversal. Putting this the other way around, we can visualize any sequence of data items as a complete binary tree.

Now the problem boils down to converting the complete binary tree to a heap. Since it is a complete binary tree, it already follows one of the requirements to be called a heap. The other requirement is that the value at any node should be greater than its children. To enforce this second requirement, we can traverse from the last node to the root node and, at each iteration, run a down heapify operation to make sure the current node is greater than both its children.

Since we are traversing from the last (lowest) node to the first (highest) node, we can be sure that when we reach any node, its subtrees are already converted to heaps. So we only need to run down heapify once to ensure the subtree rooted at the current node is also a heap. At the end of the traversal, the tree rooted at the root node (entire tree) is converted to a heap.

An important observation can make this entire algorithm twice as fast. We know that the leaf nodes do not have any children, so they fully comply with the heap property. Running down heapify for leaf nodes is a no-op and can be skipped. The traversal should start from the first non-leaf node in the tree. We can use the special property of a complete binary tree to find the index of the last non-leaf node easily.

**Algorithm**

- **Step 1:** Begin traversing the array in reverse order, starting from the middle and moving towards the beginning.
    - **Step 1.1:** For each index, perform the downheapify operation on the value at that position.


```java
import java.util.*;

class MaxHeap {
    List<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Helper function to maintain the max heap property downwards
    private void downHeapify(int index) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Find the largest among the node and its left child
        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        // Find the largest among the node and its right child
        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        // If the largest is not the current node, swap and continue
        // heapify
        if (largest != index) {
            swap(index, largest);
            downHeapify(largest);
        }
    }

    public void construct(int[] arr) {
        int n = arr.length;

        // Add all elements from array to heap
        for (int i = 0; i < n; i++) {
            heap.add(arr[i]);
        }

        // Start from the last non-leaf node and perform max-heapify
        for (int i = (n / 2) - 1; i >= 0; i--) {
            downHeapify(i);
        }
    }
}
```

## Example Min heap to max heap

```java
class Solution {
    private void maxHeapify(int[] arr, int n, int index) {
        // Initialize the current node as the largest
        int largest = index;

        // Calculate the left child index
        int left = 2 * index + 1;

        // Calculate the right child index
        int right = 2 * index + 2;

        // Compare the current node with its left child
        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        // Compare the current node with its right child
        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        // If the largest is not the current node, swap the values and
        // recursively max-heapify the affected child
        if (largest != index) {
            int temp = arr[index];
            arr[index] = arr[largest];
            arr[largest] = temp;
            maxHeapify(arr, n, largest);
        }
    }

    public void minHeapToMaxHeap(int[] arr) {
        int n = arr.length;

        // Start from the last non-leaf node and perform max-heapify
        for (int i = (n / 2) - 1; i >= 0; i--) {
            maxHeapify(arr, n, i);
        }
    }
}
```

## Example Max heap to min heap

```java
class Solution {
    private void minHeapify(int[] arr, int n, int index) {
        // Initialize the current node as the smallest
        int smallest = index;

        // Calculate the left child index
        int left = 2 * index + 1;

        // Calculate the right child index
        int right = 2 * index + 2;

        // Compare the current node with its left child
        if (left < n && arr[left] < arr[smallest]) {
            smallest = left;
        }

        // Compare the current node with its right child
        if (right < n && arr[right] < arr[smallest]) {
            smallest = right;
        }

        // If the smallest is not the current node, swap the values and
        // recursively min-heapify the affected child
        if (smallest != index) {
            int temp = arr[index];
            arr[index] = arr[smallest];
            arr[smallest] = temp;
            minHeapify(arr, n, smallest);
        }
    }

    public void maxHeapToMinHeap(int[] arr) {
        int n = arr.length;

        // Start from the last non-leaf node and perform min-heapify
        for (int i = (n / 2) - 1; i >= 0; i--) {
            minHeapify(arr, n, i);
        }
    }
}
```