
#  Linked list

A linked list is a linear and dynamic data structure that **==stores data sequentially at random memory locations. Instead of storing all the data items in a contiguous block of memory like arrays, a linked list stores them at random locations in memory.==** Whenever a new item is to be added, a new memory block is dynamically created to store this new value, which is then added to the chain of already existing items, effectively extending the **linked list**.

## Linked lists vs arrays

A linked list guarantees the insertion and deletion of items from the **start** and **end** of the list in **O(1)** space and **O(1)** time. It also guarantees the insertion and deletion of any data item **without** using any extra space.

![[Pasted image 20250926111359.png]]


## Advantages

- **Dynamic size:** The size of a linked list is not fixed. Adding or removing items can increase or decrease at will during runtime.
- **Efficient performance:** Insertion and deletion of the first node is an **O(1)** operation.

## Limitations

- **Extra space:** A little extra memory is required to store an item in a linked list compared to an array. The extra space is used to store the information of the next item in the sequence.
- **Traversal:** Traversal in a linked list is more time-consuming than an array since random access using an index is not possible. To access an item at position **n**, one must traverse all the items before it.

# Node 

**==A node is the fundamental building block of a linked list. It holds the actual data item and information of the next node. Multiple nodes, when chained together, make up a single linked list.==** All the operations on a linked list are performed by manipulating individual nodes and their links. Inserting, deleting, or updating data items in a list are all performed using the list's nodes.

## Structure of a node

A singly linked list node has two sections.

> - **val:** The actual data item a node holds. This could be of any type.
> - **next:** This is a reference to the next node in the list

![[Pasted image 20250926111919.png]]

## Implementing a node

```java
  
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
};
```

# Structure of a singly linked list

A linked list is just a chain of nodes.

![[Pasted image 20250926112037.png]]

When represented logically in a diagram, these nodes might look sequential (left to right, one after the other), but in reality, they are scattered all around in memory at random locations, and the only way to access a node is by using its address in memory.

![[Pasted image 20250926112226.png]]

## Head Node

The first node of a linked list is also called the **head** node. a node in the linked list can only be accessed using its memory reference. This reference, however, is stored in the node before it in the logical representation, and **==this is true for every node except the first node, as it does not have any previous node. This is why, to access a linked list, we should always have the reference to the head node stored somewhere.==**

![[Pasted image 20250926112345.png]]

## Tail Node

The last node of a linked list is called a **tail** node. Just like the first node does not have any node before it, the last node does not have any node after it. What is stored in the `next` pointer of the tail node. **==The `next` pointer of the tail node stores a reference to `null`, which means nothing==**

![[Pasted image 20250926112447.png]]

# Supported Operations

Every data structure is essentially used to store, retrieve, and manipulate data efficiently. On a high level, there are three basic types of operations on any data structure. 

- Traversal
- Insertion
- Deletion

![[Pasted image 20250926112918.png]]


## Boundary node

Given the **head** of a singly linked list and a reference to a **random** node, write a function to check if it is a boundary node.

You need to do this without traversing the list. It is guaranteed that the list will not contain duplicates.

A boundary node is a linked list's first or last node.

- If the given node is the first node, return `first`
- If it is the last node, return `last`
- If it is both the first and last node, return `both`
- For all other cases, return `none`

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public String boundaryNode(ListNode head, ListNode node) {

        // If either head or node is null, return "none"
        if (head == null || node == null) {
            return "none";
        }

        // If head and node are the same, and node has no next node, return "both"

        else if (node == head && node.next == null) {
            return "both";
        }

        // If head and node are the same, but node has a next node, return "first"

        else if (node == head) {
            return "first";
        }


        // If node is the last node (i.e., it has no next node), return "last"

        else if (node.next == null) {
            return "last";
        }

        // If none of the above conditions are met, return "none"
        return "none";
    }
}
```

# Traversal

 Traversal in linked lists is quite similar to arrays as they are both linear data structures, but it is also different as the data items in linked lists are not stored in contiguous memory blocks.

Data in a singly linked list is not stored in continuous memory, so we do not have indexes for random access like arrays. All the nodes are present at different memory locations

Instead of an integer loop control variable representing an item's index in an array, we use a variable referencing a node in the linked list as the loop control variable. Every time we want to move forward, we assign the node's reference in the linked list to this variable. We can get the node's reference by looking at the value stored in the `next` pointer of the current node.

**==Since linked lists are dynamic, we don’t know their length in advance, and therefore, we have to keep traversing until we reach a node with a `null` value stored in its `next` pointer. That is how we know we have reached the end of a linked list.==**

![[Pasted image 20250926115937.png]]

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

// For loop to iterate over the linked list

for (ListNode current = head; current != null; current = current.next) {

    // Perform operations on current

    // Example: current.val = current.val + 1;

}

// While loop to iterate over the linked list

ListNode current = head;

while (current != null) {

    // Perform operations on current

    // Example: System.out.println(current.val);

    current = current.next;

}
```

## Example Node expedition

Given the **head** of a singly linked list, write a function to print a comma (`,`) separated list of all the values from the start to the end.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public void nodeExpedition(ListNode head) {

        ListNode current = head;

        while(current != null) {

            System.out.print(current.val);

            if(current.next != null)

                System.out.print(", ");

            current = current.next;

        }
    }
}
```

## Example Length of the list

Given the **head** of a singly linked list, write a function that returns the length of the list.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public int lengthOfTheList(ListNode head) {

        ListNode current = head;

        int counter = 0;

  
        while(current != null) {

            counter++;

            current = current.next;

        }

        return counter;
    }
}
```

## Example Node search

Given the **head** of a singly linked list and a **data** value, write a function to return the first node containing the given data. If no such node is found, return `null`.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode nodeSearch(ListNode head, int data) {

        ListNode current = head;

        while(current != null) {

            if(current.val == data)

                return current;

            current = current.next;

        }

        return null;
    }
}
```

## Example Node search 2

Given the **head** of a linked list and a data value, write a function to return **all** the nodes containing the given data.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public List<ListNode> nodeSearchII(ListNode head, int data) {

        List<ListNode> result = new ArrayList<>();

        ListNode current = head;

        while(current != null) {

            if(data == current.val)

                result.add (current);

            current = current.next;

        }
        return result;
    }
}
```

## Example Intersection point

Given the **head** of two singly linked lists, `headA` and `headB`, write a function to find if these two linked lists intersect at any point, and if they do, return the reference to the node where they intersect. Your function should return `null` if the given lists don't intersect.

The input uses the following format

- **``intersectVal``** - The value of the node where the intersection occurs. This is 0 if there is no intersection.
- **``headA``** - The first linked list.
- **``headB``** - The second linked list.
- **``skipA``** - The number of nodes to skip ahead in ``listA`` (starting from the head) to get to the intersected node.
- **``skipB``** - The number of nodes to skip ahead in ``listB`` (starting from the head) to get to the intersected node.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }

 * };

 */

 import java.util.*;

class Solution {

    public ListNode intersectionPoint(ListNode headA, ListNode headB) {

        if (headA == null || headB == null) return null;

        ListNode pointerA = headA;

        ListNode pointerB = headB;

        // When one pointer reaches the end, redirect it to the other list's head

        // This ensures both pointers travel the same distance

        while (pointerA != pointerB) {

            pointerA = (pointerA == null) ? headB : pointerA.next;

            pointerB = (pointerB == null) ? headA : pointerB.next;

        }

        return pointerA; // Either the intersection node or null

    }
    

	public ListNode intersectionPoint(ListNode headA, ListNode headB) {
	    Set<ListNode> visitedNodes = new HashSet<>();
	    ListNode currentA = headA;
	    
	    // Add all nodes from list A to the set
	    while(currentA != null) {
	        visitedNodes.add(currentA);
	        currentA = currentA.next;
	    }
	    
	    ListNode currentB = headB;
	    // Check each node in list B
	    while(currentB != null) {
	        if(visitedNodes.contains(currentB)) {
	            return currentB;
	        }
	        currentB = currentB.next;
	    }
	    return null;
	}

}
```

# Insertion

## Inserting at the beginning

Inserting at the beginning of a linked list is a fundamental and commonly used operation. When designing an algorithm for any data structure, it's important not to make assumptions about its underlying characteristics and to design the logic for a general case. 

there are two cases to consider when inserting at the beginning of a singly linked list.

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** would be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` pointer of this newly created **head** node is `null`, as this new node will also be the last node of the list.

![[Pasted image 20250926140616.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Return the new node, as this node is also the **head** node.

### 2. The list is not empty

already have some data in the linked list, so the **head** is not `null`. Therefore, to insert a new node at the beginning of the list, we need to update the `next` pointer of the newly created node to store the reference of the existing **head** node.

![[Pasted image 20250926141001.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.

```java
/**
 * Definition for singly-linked list.
   
 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  

class Solution {

    public ListNode insertAtBeginning(ListNode head, int data) {

        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If the list is empty (head is null)

        if (head == null) {

            // Set the next pointer to null since it's the only node

            newNode.next = null;

            // Return the newNode as this is the new head
            return newNode;
        }

        // Set the next pointer of the new node to the current head,

        // making the new node the new head
        newNode.next = head;

        // Return the newNode as this is the new head
        return newNode;
    }

}
```

## Insertion at End

Unlike insertion at the beginning, this operation adds a new node at the end of the list. To add a new node at the end of a singly linked list, we first need to locate the tail node of the linked list. Then, we can create a new node and update the `next` pointer of the tail node to point to the newly created node. Since we need to traverse the entire list to insert the new node, this operation is not as efficient as insertion at the beginning. When inserting at the end of a singly linked list, there are two cases to consider.

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** will be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` pointer of this newly created **head** node is `null`, as this newly created node will also be the last node of the list.

![[Pasted image 20250926141744.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Return the new node, as this node is also the head node.

### 2. The list is not empty

In this scenario, once the new node is created, we must move through the list from the beginning until we reach the last node. Also, we need to ensure that the `next` pointer of the newly created node is set to `null`. Finally, we update the `next` pointer of the last node to point to the newly created node.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Traverse the list, keeping track of the `current` node until reaching the last node.
- **Step 3:** Set the new node's `next` pointer to `null` since it will be the new last node.
- **Step 4:** Set the last node's `next` pointer to hold the reference of the new node.
- **Step 5:** Return the original head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertAtEnd(ListNode head, int data) {

        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If the list is empty

        if (head == null) {
            // Set the next pointer of the new node to null
            newNode.next = null;

            // Return the new node as the new head of the list
            return newNode;
        }

  
        // Traverse the list to find the last node
        ListNode current = head;
        while (current != null && current.next != null) {
            current = current.next;
        }

        // Set the next pointer of the new node to null
        newNode.next = null;

        // Link the last node to the new node
        current.next = newNode;

  
        // Return the original head of the list
        return head;
    }
}
```

## Insertion After The Given Node

Unlike arrays, we can insert data at any point in a linked list without recreating the entire list. When inserting after a node in a linked list, there are two cases to consider.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, the method would return without making any changes.

### 2. The list is not empty

Since the new node will be inserted between two existing nodes, we must ensure that we properly set up the `next` pointers of these nodes. Inserting after a given node is a three-step process.

**Algorithm**

- ==**Step 1:** Create a new node with the given data.==
- ==**Step 2:** Set the `next` pointer of the new node to hold the node's reference stored in the `next` pointer of the `given` node.==
- ==**Step 3:** Set the `next` pointer of the `given` node to hold the reference of the new node.==

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */  

class Solution {

    public void insertAfterTheGivenNode(ListNode node, int data) {

        // Check if the given node is null

        if (node == null) {
            // If the given node is null, there is nothing to do
            return;
        }

        // Create a new node with the provided data
        ListNode newNode = new ListNode(data);

        // Set the next pointer of the new node to the next pointer of
        // the given node
        newNode.next = node.next;


        // Set the next pointer of the given node to the new node
        node.next = newNode;

    }

}
```

## Insertion Before The Given Node

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, we can return the **head** node that was provided as it is.

### 2. The given node is the first node

This is similar to **inserting at the beginning**, which we learned earlier. To determine if the given node is the first node, we can compare it to the **head** node. If both nodes are the same, then the given node is the **head** node.

![[Pasted image 20250926143332.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.


### 3. The given node is not the first node

The problem we face is that we don't have the reference of the previous node of the given node. This is needed to restore the link after the new node has been inserted.

**How do we get the reference of the previous node?**

**==To achieve this, we can create a new variable called `previous` which will initially be set to `null`. As we traverse through the nodes, we update both the `current` and `previous` variables at each step. When we find the node before which we want to insert the new node, the `current` variable will hold the reference of that node, and the `previous` variable will hold the node's reference just before it.==**

After gaining access to the previous node, this problem boils down to **inserting after a given node**, where the given node is the previous node. Following the four steps below, a new node will be inserted, and the links will be restored.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Search for the node before which we need to insert the new node, while keeping track of the `current` and `previous` nodes.
- **Step 3:** Set the new node's `next` pointer to hold the reference of the `given` node.
- **Step 4:** Set the `next` pointer of the `previous` node to hold the reference of the new node.
- **Step 5:** Return the original head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertBeforeTheGivenNode(

        ListNode head,

        ListNode node,

        int data

    ) {

        // Check if the head or node is null
        if (head == null || node == null) {
            return head;
        }

        // Create a new node with the given data
        ListNode newNode = new ListNode(data);

        // If the given node is the head, insert the new node before it
        if (node == head) {
            newNode.next = head;

            // Return the newNode as this is the new head
            return newNode;

        }

        // Traverse the linked list until the current node matches the
        // given node
        ListNode current = head;
        ListNode previous = null;

  
        while (current != null && current != node) {
            previous = current;
            current = current.next;
        }

  

        // If the current node is null, the given node was not found in
        // the linked list
        if (current == null) {
            return head;
        }

  

        // Insert the new node before the given node
        newNode.next = current;
        previous.next = newNode;


        // Return the head of the modified linked list
        return head;
    }
}
```


**Does the order of updating the previous and next variables matter?**

It is crucial to update the `previous` and `current` variables in the correct order while traversing the list. If we were to change the order and do something like this:
`current = current.next;`
`previous = current;`
We would end up with incorrect results. This is because if we update the `current` variable to hold the reference of the next node in the list and then update the `previous` variable, the `previous` variable will no longer point to the previous node of the current node but to the current node itself. Understanding reference manipulation in a linked list might seem challenging, but once the concepts are clear, it all makes sense.

## Insertion at a Given Distance

 insertion at a given distance `X` can be achieved by piggybacking on the length finding algorithm. Both search and finding length rely on the traversal algorithm.

### 1. If the list is empty and X > 0

Attempting to insert a node at a position greater than 0 in an empty list is an invalid operation. In an empty list, no nodes are present, so the only valid position for insertion would be at position 0, making the new node the head of the list. However, when X is greater than 0, no corresponding position is available for insertion because the list lacks any elements. Therefore, we will return the existing **head**.

### 2. X = 0

This means simply inserting a node at the beginning of a list

![[Pasted image 20250926145649.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.

### 3. X <= size of the list

If the list is not empty, we need to traverse it while keeping a counter variable with the initial value of 0. Moving through the linked list, we increment this counter by 1 to keep track of the current index. We continue traversing the list until the counter has a value of `X-1`, which lands us at the node just **after** where we want to insert the new node. Now, the problem essentially comes down to **inserting after the given node**

> **Algorithm**
> 
> - **Step 1:** Create a new node with the given data.
> - **Step 2:** Traverse a distance of X - 1 while keeping track of the `current` node.
> - **Step 3:** Set the new node's `next` pointer to hold the node's reference stored in the `next` pointer of the `current` node.
> - **Step 4:** Set the current node's `next` pointer to hold the reference of the new node.
> - **Step 5:** Return the original head node.

### 4. X > size of the list

If the value of `X` is greater than the list's size, it indicates an invalid case. For example, it is not possible to insert a node at position 5 in a list with only two items, we will return the existing **head**.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertAtGivenDistance(

        ListNode head,

        int X,

        int data

    ) {

        // If the list is empty and X is greater than 0, insertion is not
        // possible, return null

        if (head == null && X > 0) {
            return null;
        }


        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If X is 0, insert the new node at the beginning of the list

        if (X == 0) {

            // Set the next pointer of the new node to the current head,
            // making the new node the new head.
            newNode.next = head;
            // Return the newNode as this is the new head
            return newNode;
        }

        // Pointer to traverse the list
        ListNode current = head;

        // Counter to track the number of nodes traversed
        int counter = 0;

  
        // Traverse the list until reaching the desired distance or the
        // end of the list
        while (current != null && counter < X - 1) {
            // Move to the next node
            current = current.next;
            // Increment the counter
            counter++;
        }

  
        // If the list is shorter than X-1, it's not possible to insert
        // the new node, so return head.
        if (current == null) {
            return head;
        }

  
        // Set the next pointer of the new node to the current node
        newNode.next = current.next;

        // Update the next pointer of the current node to point to the
        // new node
        current.next = newNode;

        // Return the updated head of the list
        return head;

    }
}
```


# Deletion

## Delete On First Node

Deleting the first node of a singly linked list is similar to **inserting a node at the beginning**. We need to consider two cases.
### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.

## 2. The list is not empty

In this scenario, we update the **head** to hold the reference of the next node in the list, the second node, and then delete the current **head** node. However, before updating the **head**, we need to use a temporary variable to store the reference of the current **head** node so that we can delete it later.

![[Pasted image 20250926192617.png]]

> **Algorithm**
> 
> - **Step 1:** Create a temporary pointer to store the current head node.
> - **Step 2:** Move the head pointer to the next node.
> - **Step 3:** Delete the original head node to free up memory.
> - **Step 4:** Return the new head node.

**What happens if there is only one node in the list and we want to delete it? Do we need some special logic for it?** 

The algorithm we have for Case 2 will take care of this situation. If only a single node is in the list, its `next` pointer will be `null`. So, once we update the **head** to hold the reference of the second node, it will just hold `null`, as expected from an empty list. Then, we can delete the old head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public ListNode deleteFirstNode(ListNode head) {

        // Check if the list is empty

        if (head == null) {
            // Return null since there are no nodes to delete
            return null;

        }

        // Create a temporary pointer to store the current head node
        ListNode nodeToBeDeleted = head;


        // Move the head pointer to the next node
        head = head.next;

  
        // Delete the original head node to free memory
        nodeToBeDeleted = null;

        // Return the new head node
        return head;

    }

}
```


## Delete On Last Node

access the second last node to delete the last node from a linked list. Then, we can update the `next` pointer of this second last node to `null` and delete the last node. This process involves traversing the linked list and keeping track of the previous node (similar to inserting a node at the end). Let's go through the specific cases we need to consider.

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The list has only one node

Deleting the last node is the same as deleting the first node when only one node is in the list. We follow the same steps in both cases, such as deleting the first/last node. This involves storing the reference to the current **head** in a temporary variable, updating the **head** to the next node in the list (which would be `null` in this case), and then deleting the old **head** node.

![[Pasted image 20250926193530.png]]

**Algorithm**

- **Step 1:** Delete the head node to free up memory.
- **Step 2:** Return `null` as the list is now empty.

### 3. The list has more than one node

need to update the `next` pointer of the second last node in the list to hold `null` and then delete the last node. We need access to the list's last and second last nodes to accomplish this. We will traverse the list from the beginning while keeping track of the **current** and **previous** nodes. This way, when we reach the last node, we will have access to the second last node. Thereafter, we can update the `next` pointer of the second last node to `null`, or more intuitively, to the next of the last node, which should already be `null`, and then delete the last node.

**Algorithm**

- **Step 1:** Traverse the list while keeping track of the `current` and `previous` nodes until reaching the last node.
- **Step 2:** Set the `next` pointer of the `previous` node to `null`.
- **Step 3:** Delete the last node to free up memory.
- **Step 4:** Return the original head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public ListNode deleteLastNode(ListNode head) {

        // If the list is empty, there's nothing to delete
        if (head == null) {
            return null;
        }

  

        // If there's only one node in the list, delete it and return
        // nullptr
        if (head.next == null) {
            head = null;
            return null;
        }

  

        // current node being iterated
        ListNode current = head;
        // previous node
        ListNode previous = null;

        // Traverse the list until the last node is reached
        while (current != null && current.next != null) {
            // Move the previous pointer to the current node

            previous = current;
            
            // Move the current pointer to the next node
            current = current.next;
        }

  

        // At this point, current is pointing to the last node and
        // previous is pointing to the second-to-last node Update the
        // next pointer of the second-to-last node to skip the last node
        previous.next = current.next;

        // Delete the last node
        current = null;

        // Return the updated head of the list
        return head;

    }

}
```

## Deletion By Given Data

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.

### 2. The first node is deleted

If the data matches the first node, this case becomes the same as **deleting the first node**. We update the **head** to store the reference to the second node and delete the old head.

![[Pasted image 20250927160359.png]]

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Delete the original head node to free up memory.
- **Step 4:** Return the new head node.


### 3. The node to be deleted is not the first node

To delete a node that is not the first node of the linked list, we need access to the node 1 step before the one to be deleted. We will traverse the list from the beginning while keeping track of the **current** and **previous** nodes. This way, when we reach the node with the given data, we will have access to its previous node, which we need to update. Deleting the given node involves a three-step process.

**Algorithm**

- **Step 1:** Traverse the list, keeping track of `current` and `previous` nodes until reaching the `given` node.
- **Step 2:** Set the `previous` node's `next` pointer to hold the node's reference stored in the `next` pointer of the `current` node.
- **Step 3:** Delete the `current` node to free up memory.
- **Step 4:** Return the original head node.


### 4. The node to be deleted could not be found 

If the data provided does not match the data of any node in the linked list, then such a node does not exist in the list, so we return the existing **head**.


```java
/**
 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };
 */

  
class Solution {
    public ListNode deleteNodeWithGivenData(ListNode head, int data) {

        // If the list is empty, return null

        if (head == null) return null;

        // If the head node contains the given data

        if (head.val == data) {

            // Create a temporary pointer to the head node
            ListNode nodeToBeDeleted = head;

            // Update the head pointer to the next node
            head = head.next;

            // Delete the previous head node
            nodeToBeDeleted = null;

            // Return the updated head pointer
            return head;
        }

        // Pointer to the current node, starting from the head
        ListNode current = head;

  
        // Pointer to the previous node, initially null
        ListNode previous = null;

        // If the target data is not in the first node, search for it in
        // the rest of the list
        while (current != null && current.val != data) {

            // Move the previous pointer to the current node
            previous = current;

            // Move the current pointer to the next node
            current = current.next;

        }

  

        // If the given data is not found, return the original head
        // pointer
        if (current == null) {
            return head;
        }

        // Update the next pointer of the previous node to skip the
        // current node
        previous.next = current.next;

        // Delete the node with the given data
        current = null;

        // Return the head of the list, with the target data node removed
        return head;
    }
}
```

## Deletion After a Given Node

When deleting a node, we require access to the node one step before the node to be deleted to manipulate its `next` pointer. If we already have the previous node, the deletion process becomes straightforward. This is what makes this deletion operation the simplest of all delete operations.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Deleting the node after the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.

### 2. The given node is the last node

When the given node is the last node in the list, attempting to delete a node after it becomes an invalid operation. This is because, by definition, the last node has no successor, i.e., no node following it in the sequence. We can return the **head** because no other operation needs to be done.

### 3. The given node is not the last node

To delete a node after a given node, we can update the `next` pointer of the given node to skip over the node that needs to be deleted. Then, we can remove the node that we want to delete.

![[Pasted image 20250927163612.png]]

**Algorithm:**

- **Step 1:** Create a temporary pointer to store the reference of the node after the `given` node.
- **Step 2:** Set the `next` pointer of the `given` node to hold the node's reference stored in the `next` pointer of the node after the `given` node.
- **Step 3:** Delete the node after the given node to free up memory.
- **Step 4:** Return the original head node.

```java
/**
 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };
 */

class Solution {

    public ListNode deleteNodeAfterTheGivenNode(
        ListNode head,
        ListNode node
    ) {
        // If the list is empty, there's nothing to delete, so return null.
        if (head == null) {
            return null;
        }

  
        // If the given node is null or it is the last node in the list,
        // there's no node to delete, so return the original head.

        if (node == null || node.next == null) {
            return head;
        }

  
        // Store the next node in a temporary variable.
        ListNode nodeToBeDeleted = node.next;

  
        // Link the current node (node) to the node after the one being
        // deleted.
        node.next = nodeToBeDeleted.next;

  
        // Delete the node that was after the given node.
        nodeToBeDeleted = null;

  
        // Return the original head.
        return head;

    }
}
```

## Deletion Before a Given Node

Deleting the node before the given node is similar to **inserting before the given node**. We need access to the node before the one that has to be deleted.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Deleting the node after the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The given node is the first node

When the given node is the first node in the list, attempting to delete a node before it becomes an invalid operation. This is because, by definition, the first node has no predecessor, i.e., no node preceding it in the sequence. We can return the **head** because no other operation needs to be done.

### 3. The given node is the second node

This is a unique situation because removing the node before the second node essentially means deleting the linked list's head node. As learned earlier, this scenario is identical to **deleting the first node**. We need to update the head to store the reference to the second node and then delete the old head.

![[Pasted image 20250927165006.png]]

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Delete the original head node to free up memory.
- **Step 4:** Return the new head node.

### 4. The given node is any other node

To delete the node before a given node, we need to access the node two steps before the given node. We traverse the linked list while keeping track of the **current**, **previous** and **``previousToPrevious``** nodes. As soon as we reach the given node, we update the `next` pointer of the **``previousToPrevious``** node to hold the reference to the current node and then delete the **previous** node.


**Algorithm**

- **Step 1:** Traverse the list, keeping track of `current`, `previous` and `previousToPrevious` nodes until reaching the given node.
- **Step 2:** Set the `previousToPrevious` node's `next` pointer to hold the reference of the `current` node.
- **Step 3:** Delete the `previous` node to free up memory.
- **Step 4:** Return the original head node.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

  

class Solution {
    public ListNode deleteNodeBeforeTheGivenNode(
        ListNode head,
        ListNode node
    ) {

        // If the head or the given node is null, there is nothing to
        // delete Return the existing head
        if (head == null || node == null) {
            return head;
        }

  

        // If the given node is the head node, we cannot delete the node before it

        if (node == head) {
            return head;
        }

  

        // If the node to delete is the immediate next node of the head
        // Update the head to point to the next node, delete the original
        // head, and return the updated head
        if (head.next != null && head.next == node) {
        
            ListNode nodeToBeDeleted = head;
            
            head = head.next;


            // Dereference for garbage collection
            nodeToBeDeleted = null;
            
            return head;
        }

  
        // Initialize variables for traversal

        // current node being examined
        ListNode current = head.next;
        
        // Node preceding the current node
        ListNode previous = head;

  

        // Node preceding the previous node

        ListNode previousToprevious = null;

  

        // Traverse the linked list until we find the node or reach the end.

        while (current != null && current != node) {

            previousToprevious = previous;

            previous = current;

            current = current.next;
        }

  

        // If the node to delete was not found, return the head as is.
        if (current == null) {
            return head;
        }

  

        // Connect the previous node to the current node, bypassing the
        // node to delete.
        previousToprevious.next = current;

        // Dereference for garbage collection
        previous = null;
        return head;
    }
}
```


## Deletion Of The Given Node

Deleting the given node is identical to **deleting the node with the given data**. The only difference is that instead of seeking the node with the specified data value, we will search for the node that matches the given node.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Therefore, deleting the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.

### 2. The first node is deleted

If the given node matches the first node, this case becomes the same as **deleting the first node**. We update the **head** to store the reference to the second node and delete the old head.

![[Pasted image 20250927175912.png]]

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Delete the original head node to free up memory.
- **Step 4:** Return the new head node.

### 3. The node to be deleted is not the first node

To delete a node that is not the first node of the linked list, we need access to the node 1 step before the one to be deleted. We will traverse the list from the beginning while keeping track of the **current** and **previous** nodes. This way, when we reach the given node, we will have access to its previous node, which we need to update. Deleting the given node involves a three step process.

**Algorithm**

- **Step 1:** Traverse the list, keeping track of `current` and `previous` nodes until reaching the given node.
- **Step 2:** Set the `previous` node's `next` pointer to hold the node's reference stored in the `next` pointer of the `current` node.
- **Step 3:** Delete the `current` node to free up memory.
- **Step 4:** Return the original head node.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };

 */

class Solution {
    public ListNode deleteTheGivenNode(ListNode head, ListNode node) {

        // Check if either the head or the given node is null

        if (head == null || node == null) {
            return head;
        }

  

        // The given node is the head node
        if (node == head) {

            // Update the head to the next node
            head = head.next;
            

            // Delete the given node
            node = null;

            // Return the updated head
            return head;

        }

        // Pointer to traverse the list
        ListNode current = head;

  
        // Pointer to track the previous node
        ListNode previous = null;

  

        // Traverse the list until the current node matches the given node
        while (current != null && current != node) {

            // Update the previous node
            previous = current;
            
            // Move to the next node
            current = current.next;

        }

  

        // If the current node becomes null, the given node was not found in the list
        if (current == null) {
            // Return the original head
            return head;
        }

  

        // Update the previous node's next pointer to skip the current node
        previous.next = current.next;

        // Delete the current node
        current = null;

        // Return the head of the modified list
        return head;
    }
}
```

## Deletion at a Given Distance

Deleting a node at a distance `X` is similar to **inserting a node at a given distance**. Just like inserting at a distance `X` We can solve this problem without keeping track of the previous node while traversing.

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.

### 2. X = 0

When X equals 0, we need to **delete the first node**. We have previously covered this concept. We should update the head to store the reference to the second node and then delete the old head.

![[Pasted image 20250927182241.png]]

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Delete the original head node to free up memory.
- **Step 4:** Return the new head node.

### 3. X < size of the list

When we need to delete a specific node from a list, we should traverse the list until we reach the node just before the one we want to delete. Keep track of the current node and traverse `X-1` steps instead of `X`. At the end of the loop, we will reach the node one step before the node that needs to be deleted. Then, the problem becomes **deleting a node after a given node**, where the given node is the node one step before the node that has to be deleted. Update the reference in the given node's `next` pointer to point to the node after the one that has to be deleted. Once the connections have been updated, safely delete the next node.

**Algorithm**

- **Step 1:** Traverse the distance X - 1 while keeping track of the `current` node.
- **Step 2:** Set the `next` pointer of the `current` node to hold the node's reference stored in the `next` pointer of the node to be deleted.
- **Step 3:** Delete the node after the `current` node to free up memory.
- **Step 4:** Return the original head node.

### 4. X >= the size of the list

This indicates an invalid query. For example, we cannot delete the 10th node in a list of size 3. We will return the existing **head** node.

**What about the case when X == size of the linked list?**

This is also an invalid case. To clarify, let's consider a list of size 5. In this scenario, the potential values of `X` could range from 0 to 4, meaning `[0, 4]`. Therefore, an input 5 would be invalid. It's important to note that X represents the distance from the head node, not the node's position.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {
    public ListNode deleteNodeAtGivenDistance(ListNode head, int X) {

        // If the head is null (empty list), return null

        if (head == null) {
            return null;
        }

        // If X is 0, delete the head node

        if (X == 0) {
            ListNode nodeToBeDeleted = head;

            // Update the head to the next node
            head = head.next;

            // Delete the original head node
            nodeToBeDeleted = null;

            // Return the updated head
            return head;
        }

  

        int counter = 0;

        ListNode current = head;

        // Traverse to the node at position X - 1
        while (current != null && counter < X - 1) {

            // Move to the next node
            current = current.next;

            // Increment the counter
            counter++;
        }

  
        // If the node at position X - 1 is null or the next node is null, return the head
        if (current == null || current.next == null) {
            return head;
        }

        // Store the node to be deleted
        ListNode nodeToBeDeleted = current.next;

  
        // Update the next pointer of current node
        current.next = nodeToBeDeleted.next;

        // Delete the node at position X
        nodeToBeDeleted = null;

  
        // Return the head
        return head;

    }

}
```

# Floyd's Cycle Finding Algorithm

Sometimes, a linked list may not terminate at a `null` reference but instead, hold the reference to some other node in the next section of its last node. Such a list is said to have a cycle, as now, if we traverse the list from the start, we will loop indefinitely and never reach a `null` reference.

![[Pasted image 20250928181045.png]]

### Algorithm

Floyd's cycle finding algorithm uses the fast and slow pointer technique to move two pointers through the list until they meet each other. We use two references, `slow` and `fast` initialized with the head node, traverse the list using `fast`. In each iteration, we move `fast` two steps ahead while `slow` only moves 1 step. If they both reach the same node at any point in the traversal, it means there is a cycle; otherwise, `fast` will eventually hit `null` at the end of the list, meaning the list does not have a cycle.

The `fast` and `slow` pointers can meet at any node in the cycle and not necessarily the node where the cycle starts.

![[Pasted image 20250928181419.png]]

Once we confirm that a linked list has a cycle, the next step is to find where the cycle starts. After the `fast` and `slow` pointer meet at some node, we move `fast` back to the head of the list and traverse the list again using both `fast` and `slow`. However, this time, both `fast` and `slow` move at the same speed of one step in each iteration until they meet. The node at which they meet this time is where the cycle starts.

- **Step 1:** Initialize references `slow` and `fast` with the head of the list.
- **Step 2:** Loop while `fast` and `fast.next` are not `null` and do the following:
    - **Step 2.1:** Move ahead `slow` by one step and fast by two steps
    - **Step 2.2:** Check if `slow` == `fast`. If yes, break out of the loop as the list has a cycle.
- **Step 3:** If `slow` != `fast` it means the list doesn't have a cycle, so terminate. Otherwise, continue to the following steps.
- **Step 4:** Set `fast` to the head of the list
- **Step 5:** Loop while `fast` and `slow` are not equal and move both one step in each iteration
- **Step 6:** Return `slow` as the node where the cycle starts.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public ListNode findCycle(ListNode head) {

        ListNode slow = head;

        ListNode fast = head;

        boolean hasLoop = false;

  
        // Check if there is a loop in the linked list
        while (fast != null && fast.next != null) {

            // Move slow pointer by one step
            slow = slow.next;

            // Move fast pointer by two steps
            fast = fast.next.next;

  

            // If slow and fast pointers meet, there is a loop
            if (slow == fast) {
                hasLoop = true;
                break;
            }
        }

        // If no loop is found, return null

        if (!hasLoop) {
            return null;
        }

  
        // Reset fast pointer to the head and move both pointers at the same pace
        fast = head;
        while (slow != fast) {
        
            slow = slow.next;

            fast = fast.next;
        }

        // Return the node where the loop starts
        return slow;

    }
}
```

## Proof of correctness

Floyd's cycle-finding algorithm can detect cycles and find where the cycle starts in any automata (sequence of connected nodes) and not necessarily only a singly linked list.

![[Pasted image 20250928182302.png]]

It can be proved that if we move the `slow` and `fast` pointers at different speeds, they meet at some node in the cycle. This is because, after `m` iterations when `slow` pointer reaches the node `b`, the `fast` pointer will have traversed a distance `2*m` and so will be at some node `c` such that the distance between the node `b` and `c` is `k = m % n`.

![[Pasted image 20250928182334.png]]

From here on, the `slow` and `fast` pointers go around in the cycle but at different speeds. In each iteration, the gap `k` between `slow` and `fast` increases by one, but since it is a cycle, the gap between `fast` and `slow` i.e. `n-k` decreases by one, and so after `n-k` iterations `fast` and `slow` both point to the same node `d` that is at a distance `x` from the node `b` such that `x = n - k`

![[Pasted image 20250928182408.png]]

To find where the cycle starts (node `b`), we move the `fast` pointer back to the head and move both `fast` and `slow` pointer 1 step at a time (at the same speed). It is guaranteed that they will eventually meet at node `b`. This is because after `m` iterations, `fast` will reach node `b`, and `slow` will be at a distance `(x + m) % n` from node `b`. Expanding equations as given below, it can be proved that `(x + m) % n` **equals 0**,

![[Pasted image 20250928182435.png]]

Based on the above, after `m` iterations the `fast` pointer will be at a distance `(x + m) % n` from node `b` but since `(x + m) % n = 0` it means it will be at the node `b` where it will meet the `slow` pointer.

![[Pasted image 20250928182502.png]]

## Example Remove Loop

Given the **head** of a singly linked list that may contain a loop, write a function to remove the loop **in place** if it is present.

> A loop here means that the last node of the list is connected to the node at position X.

```java
class Solution {
    public void removeLoop(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        ListNode slow = head;
        ListNode fast = head;
        boolean hasLoop = false;

        // Döngü tespiti
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            if (slow == fast) {
                hasLoop = true;
                break;
            }
        }

        if (!hasLoop) {
            return;
        }

        // Döngüyü kaldırma işlemi başlıyor
        fast = head;

        // ÖZEL DURUM: Döngü head'de başlıyorsa
        if (slow == fast) {
            while (slow.next != fast) {
                slow = slow.next;
            }
        }
        // NORMAL DURUM: Döngü head'de başlamıyorsa  
        else {
            while (slow.next != fast.next) {
                slow = slow.next;
                fast = fast.next;
            }
        }

        // Döngüyü kır
        slow.next = null;
    }
}
```

# Pattern Reversal

Many linked list problems require us to reverse the entire list or a part of it. For some problems, we may have to perform a reversal many times along with other more complex operations. While we can reverse a linked list using loops in multiple passes, it is not the best way to do it, as the code is complicated and error-prone. The most concise and efficient way to reverse a linked list is to use a single-pass in-place reversal algorithm,

![[Pasted image 20250929110918.png]]

## Reversing the entire list

Reversing the entire linked list is a special case of the generic reversal algorithm to reverse a segment between `start` and `end`. Consider we are given a linked list denoted by `head` and need to reverse it completely.

![[Pasted image 20250929111002.png]]

We initialize two references `previous` and `current` with `nullptr` and the `head` of the list respectively and traverse the list from the head node using `current`. We save the reference of the node after `current` in a reference variable `next`, set the next section of each node to `previous` and update `previous` and `current` for the next iteration.

**Algorithm**

- **Step 1:** Create two references, `previous` and `current`, and initialize them with `nullptr`, and `head` respectively.
- **Step 2:** Loop while `current` is not equal to `nullptr`, do the following:
    - **Step 2.1:** Initialize a reference `next` to store the reference of the node after the `current` node.
    - **Step 2.2:** Update the next section of the `current` node to hold the node held by `previous`.
    - **Step 2.3:** Update `previous` to hold the reference of the `current` node.
    - **Step 2.4:** Update the `current` to hold the node held by `next`
- **Step 3:** Return `previous` as the head of the reversed list.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

public ListNode reverse(ListNode head) {
    // Initialize references

    ListNode current = head;

    ListNode previous = null;

    // Set the next reference of each node to its previous node
    while (current != null) {
    
        ListNode next = current.next;
        
        current.next = previous;

        previous = current;

        current = next;

    }
    return previous;
}
```

## Reversing a segment

![[Pasted image 20250929111346.png]]

To connect the first node of the segment back to the list after reversal, we need to know the node after `end`. We create a reference variable `rightBound` and initialize it with the node after `end`.

![[Pasted image 20250929111405.png]]

Next, we initialize two references `previous` and `current` with the `rightBound` and `start` respectively and traverse the list from `start` to `end` using `current`.

In each iteration, we save the reference to the node after `current` in a reference `next` to use it later. We then set the next section of `current` node to `previous`.  We then set `previous` to `current` and `current` to `next` for the next iteration. At the end of all iterations, the node held in `previous` becomes the new head of the reversed segment.

The last step is to connect the reversed head back to the list.

**Algorithm**

- **Step 1:** Create three references, `previous`, `current`, and `rightBound` and initialize them with `end.next`, `start`, and `end.next` respectively.
- **Step 2:** Loop while `current` is not equal to `rightBound`, do the following:
    - **Step 2.1:** Initialize a reference `next` to store the reference of the node after the `current` node.
    - **Step 2.2:** Update the next section of the `current` node to hold the node held by `previous`.
    - **Step 2.3:** Update `previous` to hold the reference of the `current` node.
    - **Step 2.4:** Update the `current` to hold the node held by `next`
- **Step 3:** Return `previous` as the new head of the list and connect the node before `start` to this new head in the caller of this reverse function.


```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

public ListNode reverse(ListNode start, ListNode end) {

    // Initialize references

    ListNode current = start;

    ListNode rightBound = end.next;

    ListNode previous = rightBound;

  

    // Set the next reference of each node to its previous node
    while (current != rightBound) {

        ListNode next = current.next;

        current.next = previous;

        previous = current;

        current = next;

    }

    return previous;

}
```

## Example Reverse first K nodes

Given the **head** of a singly linked list and a positive integer **k**, write a function to reverse the first k nodes of the list and return the head of the reversed list.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public ListNode reverseFirstKNodes(ListNode head, int k) {

        // if K is less than or equal to 0, return the original head

        if (k <= 0) {
            return head;
        }

        // Initialize pointers current and previous
        ListNode current = head;

        ListNode previous = null;

        int count = 0;

  
        while (current != null && count < k) {
            // Save the address of next node
            ListNode next = current.next;

            // Update the next of current node
            current.next = previous;

            // Move previous to hold current node
            previous = current;

            // Move current ahead
            current = next;

            // Increment count
            count++;

        }

        // Connect the reversed sublist with the remaining part
        if (head != null) {
            head.next = current;
        }
        
        return previous;
    }
}
```

## Example Reverse the given segment

Given the **head** of a singly linked list and two integers **left** and **right** where **left <= right**. Write a function to reverse the list nodes from the position left to the right and return the head of the reversed list.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  

class Solution {

    public ListNode getNodeAtPosition(ListNode head, int position) {

        ListNode current = head;
        for (int i = 1; i < position; ++i) {
            current = current.next;

        }
        return current;

    }

  

    public ListNode reverse(ListNode start, ListNode end) {

        ListNode current = start;

        ListNode rightBound = end.next;

        ListNode previous = rightBound;

  
        while (current != rightBound) {

            ListNode next = current.next;

            current.next = previous;

            previous = current;

            current = next;

        }

        return previous;
    }

  

    public ListNode reverseTheGivenSegment(

        ListNode head,

        int left,

        int right

    ) {


        // Handle cases where reversal is not needed

        if (head == null || head.next == null || left == right) {
            return head;
        }

  

        // Get the end node of the segment
        ListNode end = getNodeAtPosition(head, right);

  
        // If the left position is 1, reverse from the head
        if (left == 1) {
            return reverse(head, end);
        }

  

        // Get the node before the 'left' position to connect after reversal
        ListNode leftBound = getNodeAtPosition(head, left - 1);

  
        // Node at the start of the segment to reverse
        ListNode start = leftBound.next;

  
        // Reverse the segment and connect to the leftBound node
        leftBound.next = reverse(start, end);

        // Return the modified list
        return head;
    }
}
```

# Pattern Reversal Subproblem

Asking yourself the following questions will help you determine whether a problem is a reversal subproblem pattern problem or not.

**Ask yourself questions:**

Q1. Can the problem or solution be broken down into smaller subproblems?

Q2. Can any subproblem be solved by reversing a part of the linked list?

## Example

> **Problem statement:** Given a linked list, reverse the list in groups of K in-place. If the last group in the list does not have K nodes, don't reverse it.

![[Pasted image 20250929122015.png]]

**Template:**

Q1. Can the problem or solution be broken down into smaller subproblems?

A1. Yes, we can break down the solution as a combination `length / k` reversal operations, where `length` is the length of the linked list.

Q2. Can any subproblem be solved by reversing a part of the linked list?

A2. Yes, all subproblems except finding the length can be solved by reversing a part of the linked list.

The critical observation here is that reversing a group of size `k` is the same as reversing a part of the linked list between start and end. We traverse the linked list `k` nodes at a time and reverse each group as we go. We initialize a variable `groups` with the number of k-groups (`length / k`) to reverse, truncating the fractional part as the number of k groups will always be a whole number. We use `groups` to iterate, reversing a k-group in each iteration.

![[Pasted image 20250929122344.png]]

We use two reference variables `start` and `end` to denote the boundary of a k-group that we need to reverse and a variable `leftBound` to hold the node before `start` that is used to correctly connect the head of the reversed segment to the list.

We initialize `start` and `end` with the `head` of the list and iterate `k-1` times using `end` to find the end of the first k-group. We initialize `leftBound` with null for the first k-group, as there is no node before the head of the list.

![[Pasted image 20250929122403.png]]

After reversing the first k-group, we need to update the `head` of the list, as the previous `end` node will be the new head of the list.

![[Pasted image 20250929122427.png]]

Similarly, after reversing the first k-group, the previous `start` and the node after it would be the `leftBound` and `start` for the next k-group respectively.

![[Pasted image 20250929122446.png]]

We repeat the process to find the `end` of the next segment and reverse the list between `start` and `end` and for all the subsequent k-group reversals, we use `leftBound` to connect the reversed head of the segment back to the list. At the end of all iterations, all the k-groups in the list are reversed in place

```java
class Solution {
    public int findLength(ListNode head) {
        int length = 0;
        while (head != null) {
            length++;
            head = head.next;
        }
        return length;
    }

    public ListNode getNodeAtPosition(ListNode head, int position) {
        ListNode current = head;
        for (int i = 1; i < position; ++i) {
            current = current.next;
        }
        return current;
    }

    public ListNode reverse(ListNode start, ListNode end) {
        ListNode current = start;
        ListNode rightBound = end.next;
        ListNode previous = rightBound;

        while (current != rightBound) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }

        return previous;
    }

    public ListNode reverseKSegments(ListNode head, int k) {
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        ListNode start = head;
        ListNode leftBound = null;
        int totalSegments = findLength(head) / k;

        for (int i = 0; i < totalSegments; i++) {
            ListNode end = getNodeAtPosition(start, k);
            ListNode reversedHead = reverse(start, end);

            if (leftBound == null) {
                head = reversedHead;
            } else {
                leftBound.next = reversedHead;
            }

            leftBound = start;
            start = leftBound.next;
        }

        return head;
    }
}
```

## Example Pairwise swap

Given the **head** of a singly linked list, write a function to **swap every two adjacent nodes** of this list and return the head of the reordered list.

The problem needs to be solved without modifying the values in the list's nodes. The nodes should be reordered by updating links.

```java
class Solution {
    public ListNode reverse(ListNode start, ListNode end) {
        ListNode current = start;
        ListNode rightBound = end.next;
        ListNode previous = rightBound;

        while (current != rightBound) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }

        return previous;
    }

    public ListNode pairwiseSwap(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode start = head;
        ListNode leftBound = null;

        while (start != null && start.next != null) {
            ListNode end = start.next;
            ListNode reversedHead = reverse(start, end);

            if (leftBound == null) {
                head = reversedHead;
            } else {
                leftBound.next = reversedHead;
            }

            leftBound = start;
            start = start.next;
        }

        return head;
    }
}
```

## Example Reverse K-segments

Given the **head** of a singly linked list and a positive integer **k**, write a function to reverse the list in groups of k and return the head of the reversed list.

If, at the end, the length of the remaining list is less than k, do not reverse that part of the list.

```java
class Solution {
    public int findLength(ListNode head) {
        int length = 0;
        while (head != null) {
            length++;
            head = head.next;
        }
        return length;
    }

    public ListNode getNodeAtPosition(ListNode head, int position) {
        ListNode current = head;
        for (int i = 1; i < position; ++i) {
            current = current.next;
        }
        return current;
    }

    public ListNode reverse(ListNode start, ListNode end) {
        ListNode current = start;
        ListNode rightBound = end.next;
        ListNode previous = rightBound;

        while (current != rightBound) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }

        return previous;
    }

    public ListNode reverseKSegments(ListNode head, int k) {
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        ListNode start = head;
        ListNode leftBound = null;
        int totalSegments = findLength(head) / k;

        for (int i = 0; i < totalSegments; i++) {
            ListNode end = getNodeAtPosition(start, k);
            ListNode reversedHead = reverse(start, end);

            if (leftBound == null) {
                head = reversedHead;
            } else {
                leftBound.next = reversedHead;
            }

            leftBound = start;
            start = leftBound.next;
        }

        return head;
    }
}
```

# Pattern: Sliding Window Traversal

The traversal of a linked list is generally done using a single reference variable to hold the current node. Some problems, however, require you to perform some operations on two nodes at some distance from each other. Unlike arrays, where we can access item **k** steps ahead of the current item by adding **k** to the current index, we need to iterate **k** times and traverse the list from the current node for a singly linked list, which is inefficient if we need to do this for multiple nodes.

This presents another use case for the sliding window technique, apart from aggregating values in a subarray or sublist. We can use a window of size **k** denoted by two references and move it to access all nodes **k** steps apart in a singly linked list.

![[Pasted image 20250929124011.png]]

Consider we are given a singly linked list and need to perform some operations on all nodes that are at a distance of `k` from each other. We create two references `start` and `end`, and initialize them with the head of the linked list.

We then iterate `k` times and move the `end` reference `k` steps ahead from `start`. This way, `start` and `end` denote a window of size `k+1` such that `end` is exactly `k` steps away from `start`.

It is important to note that two nodes that are at a distance `k` from each other denote a window of size `k+1` as both nodes are included in the window.

![[Pasted image 20250929124333.png]]

We perform the required operations on the nodes held in `start` and `end` and move both of them one step ahead by setting them to their respective next nodes. We repeat this process until `end` hits `null` at the end of the list. At the end of all iterations, we would have applied the given operation on all nodes that are `k` steps away from each other.

## Algorithm

The algorithm given below outlines the sliding window traversal technique for a window of size k.

> - **Step 1:** Initialize two references, `start` and `end` to the head of the list.
> - **Step 2:** Iterate k times using a loop and move `end` reference k steps ahead
> - **Step 3:** Loop while `end` != `null` and do the following
>     - **Step 3.1:** Process nodes held in `start` and `end` as they are k steps apart
>     - **Step 3.2:** Move both `start` and `end` one step ahead by setting them to their next nodes.


```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class SlidingWindowTraversal {

    void slidingWindowTraversal(ListNode head, int k) {

        // Initialize start and end to head

        ListNode start = head;

        ListNode end = head;

        // Move end k steps ahead

        for (int i = 0; i < k; i++) {
            if (end == null) {
                return; // Exit early if the list is shorter than k
            }
            end = end.next;
        }

        // Traverse the list while end is not null
        while (end != null) {

            // Apply operation on start and end
            // these nodes are k steps apart
            // Example: start.val = start.val + end.val;
            // Move ahead both start and end by one step

            start = start.next;

            end = end.next;
        }
    }
}
```

## Example K maximum sum

Given the **head** of a singly linked list and a positive integer **k**, write a function to find and return the maximum sum of any contiguous k nodes. If the list contains fewer than `k` nodes, return `-1`.

```java
class Solution {
    public int kMaximumSum(ListNode head, int k) {
        if (head == null || k <= 0) {
            return -1;
        }

        ListNode start = head;
        ListNode end = head;
        int sum = 0;
        int count = 0;

        while (end != null && count < k) {
            sum += end.val;
            end = end.next;
            count++;
        }

        if (count < k) {
            return -1;
        }

        int maxSum = sum;

        while (end != null) {
            sum = sum - start.val + end.val;

            if (sum > maxSum) {
                maxSum = sum;
            }

            start = start.next;
            end = end.next;
        }

        return maxSum;
    }
}
```

## Example Trim Nth node

Given the **head** of a singly linked list and a non-negative integer **N**, write a function to remove the Nth node from the end of the list and return the head of the updated list.

```java
class Solution {
    public ListNode trimNthNode(ListNode head, int N) {
        if (head == null) {
            return null;
        }

        ListNode current = head;

        for (int i = 1; i < N; i++) {
            if (current == null) {
                return head;
            }
            current = current.next;
        }

        if (current.next == null) {
            return head.next;
        }

        ListNode nthNodeFromEnd = head;
        ListNode prevToNthNodeFromEnd = null;

        while (current != null && current.next != null) {
            prevToNthNodeFromEnd = nthNodeFromEnd;
            nthNodeFromEnd = nthNodeFromEnd.next;
            current = current.next;
        }

        prevToNthNodeFromEnd.next = nthNodeFromEnd.next;

        return head;
    }
}
```

# Pattern Fast and Slow Pointers

 unlike arrays, singly linked lists don't have a fixed size, and we cannot randomly access items using indices. **==Finding the middle node in the list requires two passes, first to find the length of the list and second to find the node at half the length from the start==**.

The problem can be further extended to find a node between two given nodes at a proportional distance from both. The fast and slow pointer technique can find that node in a single pass.

![[Pasted image 20250929162733.png]]

Consider we are given a singly linked list and two nodes `start` and `end`, and we need to find a node that is at a distance `x` from `start` and `n*x` from `end`. It is guaranteed that a solution node node exists.

It should be noted that a solution node will only exist if the length **L** between start and end is a multiple of **n** i.e, **L % n == 0**

The idea is to initialize two references `flast` and `slow` with `start` and move them forward at different speeds until `fast` reaches `end`.The `slow` reference moves **1** step in each iteration, while the `fast` reference moves **(n+1)** steps. This way, at the end of every iteration, the `slow` reference is at a proportional distance from the `start` and `fast` reference. When the `fast` reference reaches `end`, the `slow` reference points to the solution node.

## Algorithm

- **Step 1:** Initialize two references, `slow` and `fast` with the head of the list.
- **Step 2:** Loop while `fast.next` != `null` and `fast` != `end` and do the following
    - **Step 2.1:** Move slow 1 step ahead by setting `slow` = `slow.next`
    - **Step 2.2:** Move `fast` `n+1` times setting `fast` = `fast.next` `n+1` times.
- **Step 3:** Node held in `slow` is the solution node

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
public ListNode findTheSolutionNode(ListNode start, ListNode end, int n) {
    // Create two references slow and fast and point them to the start
    ListNode slow = start;

    ListNode fast = start;

    // Null checks to take care of edge cases
    while(fast.next != null && fast != end) {
        // Move slow 1 step
        slow = slow.next;

  
        // Move fast n+1 step
        for(int i=0; i<n+1; i++) {
            if(fast && fast.next)
                fast = fast.next;
        }
    }
  
    // Node pointed by slow is the solution
    return slow;
}
```

## Example Middle node search

Given the **head** of a singly linked list, write a function to find and return the reference of the middle node of this list.

If there are two middle nodes, return the reference of the second one.

```java
class Solution {
    public ListNode middleNodeSearch(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```

## Example Split list in half

Given the **head** of a singly linked list, write a function to split the input linked list into two halves and return the heads of the two split halves. 

If there is only one middle node, that node should be part of the first half.

```java
import java.util.*;

class Solution {
    public List<ListNode> splitListInHalf(ListNode head) {
        // If the list is empty or has only one element, return the original head and null
        if (head == null || head.next == null) {
            return Arrays.asList(head, null);
        }

        ListNode slow = head;
        ListNode fast = head;
        ListNode prevToSlow = null;

        // Find the midpoint of the list using the slow and fast pointer technique
        while (fast != null && fast.next != null) {
            // Keep track of the node before the midpoint
            prevToSlow = slow;
            // Move the slow pointer by one step
            slow = slow.next;
            // Move the fast pointer by two steps
            fast = fast.next.next;
        }

        ListNode secondHalf;

        // If the fast pointer reached the end of the list, it has an even number of nodes
        if (fast == null) {
            // The second half starts from the next node of the previous slow pointer
            secondHalf = prevToSlow.next;
            // Disconnect the two halves by setting the next of the previous slow pointer to null
            prevToSlow.next = null;
        } else {
            // The list has an odd number of nodes
            // The second half starts from the node after the slow pointer
            secondHalf = slow.next;
            // Disconnect the two halves by setting the next of the slow pointer to null
            slow.next = null;
        }

        // Return a list containing the head of the first half and the head of the second half
        return Arrays.asList(head, secondHalf);
    }
}
```


# Pattern Split

Many linked list problems require splitting a given linked list into two or more lists based on the outcome of some function. One solution to this problem is traversing the list for every new list that has to be created and copying items from the original list into the new nodes created for the new lists. However, this requires multiple passes over the list and is inefficient. Also, in many cases, we need to split the original list into separate lists instead of creating copies of nodes. The linked list split technique can be applied to such problems to solve them efficiently in a single pass.

![[Pasted image 20250929163700.png]]

Consider we are given a singly linked list that we need to split into `k` lists using a function `f` that maps every node in the original list to the list it should go to after splitting. the function`f`simply round robins amongst all the`k`lists. The split technique uses dummy nodes to simplify splitting the original lists. We create two arrays of node references `dummy` and `tails` of size `k` each. Both the arrays initialized it with references of newly created dummy nodes where the item at the index `i` is the dummy node for the list `i`.

We initialize a `current` reference with the head of the list and traverse the original list from start to end. In each iteration, we use the function `f` to identify which list the current node should go to. We get the tail node for that list from the `tail` array, update its next section to hold the current node, and update the tail reference. Then, we move `current` one step ahead for the next iteration and finally set the next section of the new tail node to `null`. This process is repeated until we reach the end of the list when the original list is split into `k` lists.

At the end of all iterations, we iterate in `dummy` and move the references one step ahead to hold the real head of the corresponding list and delete the dummy node.

## Algorithm

- **Step 1:** Create two arrays of node references `dummy` and `tails` of size `k` and initialize each item in both arrays with the reference of a newly created dummy node.
- **Step 2:** Create a reference `current` and initialize it with the head of the list.
- **Step 3:** Loop while `current` != `null` and do the following:
    - **Step 3.1:** Apply the function `f` to the `current` node and retrieve `idx`, which is the index of the list where this node should be placed.
    - **Step 3.2:** Add the `current` node to the end of the list stored at `idx` using `tails` array.
    - **Step 3.3:** Update `tails[idx]` to now store the reference of the new tail node.
    - **Step 3.4:** Update the `current` pointer to hold the reference of the node after the `current` node.
    - **Step 3.5:** Set the next section of `tails[idx]` to `null`
- **Step 4:** Move all the dummy nodes one step ahead to obtain the heads of the split lists and delete the old dummy nodes.

```java
class SplitLists {
    ListNode[] splitLists(ListNode head, int k) {
        // Create an array of references for dummy and tail nodes
        ListNode[] dummy = new ListNode[k];
        ListNode[] tails = new ListNode[k];

        // Initialize the dummy and tail nodes
        for (int i = 0; i < k; i++) {
            dummy[i] = new ListNode();
            tails[i] = dummy[i];
        }

        // Iterate in the list using current
        ListNode current = head;
        while (current != null) {
            // Use the function `f` to decide which list this node should go to
            int idx = f(current);

            // Add node to the list and update tail
            tails[idx].next = current;
            tails[idx] = current;

            // Move current ahead
            current = current.next;

            // Set the next of the current tail node to null
            tails[idx].next = null;
        }

        // Remove the dummy nodes and assign actual heads to the dummy array
        for (int i = 0; i < k; i++) {
            ListNode dummyNode = dummy[i];
            dummy[i] = dummy[i].next;
            dummyNode = null;
        }

        // Return the array of split lists' heads
        return dummy;
    }
}
```

## Example  K-way list split

```java
class KWayListSplit {
    
    // Function to find the length of a linked list
    int lengthOfLinkedList(ListNode head) {
        int length = 0;
        while (head != null) {
            ++length;
            head = head.next;
        }
        return length;
    }

    List<ListNode> kWayListSplit(ListNode head, int k) {
        // Count the number of nodes in the linked list
        int length = lengthOfLinkedList(head);
        // Calculate the size of each part
        int partSize = length / k;
        // Calculate the number of lists with partSize + 1 nodes
        int bigLists = length % k;

        // Create an array of references for dummy and tail nodes
        List<ListNode> dummy = new ArrayList<>(Collections.nCopies(k, null));
        List<ListNode> tails = new ArrayList<>(Collections.nCopies(k, null));

        for (int i = 0; i < k; i++) {
            dummy.set(i, new ListNode(0));
            tails.set(i, dummy.get(i));
        }

        // Iterate in the list using current
        ListNode current = head;

        // Initialize counter to count number of nodes added to current split list
        int count = 0;

        // Initialize variable to denote current split list
        int idx = 0;

        while (current != null) {
            // Add node to the current split list and update tail
            tails.get(idx).next = current;
            tails.set(idx, current);

            // Move current ahead
            current = current.next;

            // Set the next section of tail node to null
            tails.get(idx).next = null;

            // Increment count after adding the node
            count++;

            if (bigLists > 0 && count == partSize + 1) {
                count = 0;
                idx++;
                bigLists--;
            } else if (bigLists == 0 && count == partSize) {
                count = 0;
                idx++;
            }
        }

        // Delete the dummy nodes
        for (int i = 0; i < k; i++) {
            dummy.set(i, dummy.get(i).next);
        }

        // Return the list of split lists' heads
        return dummy;
    }
}
```

## Example Even odd split

Given the **head** of a singly linked list, write a function to split the list into two separate lists such that the first list contains the nodes with even values and the second list contains the nodes with odd values. Your function should return the heads of both these lists.

```java
import java.util.*;

class Solution {
    public List<ListNode> evenOddSplit(ListNode head) {
        // Initialize head and tail references for the two split lists
        ListNode evenDummy = new ListNode(0);
        ListNode evenTail = evenDummy;

        ListNode oddDummy = new ListNode(0);
        ListNode oddTail = oddDummy;

        // Create current reference to iterate through the list
        ListNode current = head;

        // Iterate through the list and split nodes into two lists
        while (current != null) {
            // If the current node's value is even then the node goes to the even list
            if (current.val % 2 == 0) {
                // `current` node goes to the even split list
                evenTail.next = current;
                // Move evenTail forward
                evenTail = evenTail.next;
            } else {
                // `current` node goes to the odd split list
                oddTail.next = current;
                // Move oddTail forward
                oddTail = oddTail.next;
            }

            // Move to the next node in the original list
            current = current.next;
        }

        // Terminate the even list
        evenTail.next = null;

        // Terminate the odd list
        oddTail.next = null;

        return Arrays.asList(evenDummy.next, oddDummy.next);
    }
}
```

# Pattern Merge

Like splitting a linked list into multiple lists, many linked list problems require merging multiple linked lists into one based on the outcome of some function. Also, in most cases, we must merge the lists by moving around the original nodes instead of creating copies.

![[Pasted image 20250930104102.png]]

Consider that we are given two singly linked lists denoted by `headA` and `headB`, and we have to merge them into a single list based on the output of some function `f`. Given any two nodes, one from each list, the function `f` decides which node goes before the other node in the merged list.

The merge technique uses a dummy node to simplify the merging algorithm. We create a `dummy` node and a reference variable `tail` which we initialize with it. We create two references `currentA` and `currentB` and initialize them with `headA` and `headB` which we use to traverse the respective lists. We then simultaneously traverse both lists using these references and, in each iteration, apply the function `f` on nodes held in `currentA` and `currentB` to decide which node should be added to the merged list. We use the `tail` reference to easily add the node at the end of the merged list, update `tail`, and move ahead either `currentA` or `currentB` accordingly.

If either `currentA` or `currentB` hits `null`, it means we have traversed one of the lists completely, and we terminate the iterations. At this point, we identify the list that is not completely traversed and add the remaining nodes at the end of the merged lists to completely merge both lists. Consider the example below where the function `f` is a simple function that alternates (round robin) between both lists to select the node that goes to the merged list.

## Algorithm

The algorithm given below summarizes the linked list merge technique for two lists. It can be easily extended for `k` lists.

 
> - **Step 1:** Create a `dummy` node and initialize a `tail` reference with it.
> - **Step 2:** Create two references `currentA` and `currentB` and initialize them with `headA` and `headB` respectively.
> - **Step 3:** Loop while `currentA` != `null` and `currentB` != `null` and do the following:
>     - **Step 3.1:** Apply the function `f` to the node held in `currentA` and `currentB` to decide which node to add to the merged list.
>     - **Step 3.2:** If `currentA` has to be added, add it to the end of the merged list by updating `tail` and moving `currentA` ahead.
>     - **Step 3.3:** If `currentB` has to be added, add it to the end of the merged list by updating `tail` and moving `currentB` ahead.
>     - **Step 4:** If `currentA` != `null` attach the remaining list to the merged list using `tail`
>     - **Step 5:** If `currentB` != `null` attach the remaining list to the merged list using `tail`
>     - **Step 6:** Delete the `dummy` node and return the next node as real head of merged list.


```java
class MergeLists {
    // Function to merge two linked lists
    ListNode mergeLists(ListNode headA, ListNode headB) {
        // Create a dummy node and a tail reference for the merged list
        ListNode dummy = new ListNode();
        ListNode tail = dummy;

        // Create current references
        ListNode currentA = headA;
        ListNode currentB = headB;

        while (currentA != null && currentB != null) {
            // Use the function `f` to determine which node to merge
            boolean mergeA = f(currentA, currentB);

            if (mergeA) {
                tail.next = currentA;
                currentA = currentA.next;
                tail = tail.next;
            } else {
                tail.next = currentB;
                currentB = currentB.next;
                tail = tail.next;
            }
        }

        // If the first list is not completely traversed, attach remaining nodes to merged list
        if (currentA != null) {
            tail.next = currentA;
        } else if (currentB != null) {
            tail.next = currentB;
        }

        // Return the real head of the merged list
        return dummy.next;
    }

    // Example function `f` that determines which node to merge (for demonstration)
    boolean f(ListNode nodeA, ListNode nodeB) {
        // Custom comparison logic: e.g., merge nodeA if its value is smaller
        return nodeA.val <= nodeB.val;
    }
}
```


# Pattern Reorder

Some linked list problems require us to reorder the nodes of the given list in place based on some conditions. In most cases, this requires first splitting the list based on the outcome of some function `f1` and then merging back the split list together either by using another function `f2` or simply concatenating them.

![[Pasted image 20250930104857.png]]

Consider that we are given a singly linked list whose nodes must be reordered. The problem almost always has a split function `f1` that we use to split the list into multiple lists using the split technique.

In most cases, concatenating these split lists to merge them is sufficient, but sometimes, we may also have a function `f2` that must be used to merge the lists. We use the merge technique to merge them back together to solve the problem.

Consider the example execution below, where we use the function `f2` that merges alternate nodes to merge back the split lists starting with the second list, effectively reordering the nodes.

## Algorithm

The algorithm given below summarizes the reorder technique for **two** lists. It can be easily extended for `k` lists.

> - **Step 1:** Use the split technique to split the list in **two** using the function `f1`
> - **Step 2:** Use the merge technique to merge the **two** lists using the function `f2`.
> - **Step 3:** Return the head of the merged list.


```java
class ReorderNodes {
    // Function to reorder nodes based on conditions defined by f1 and f2
    public ListNode reorderNodes(ListNode head) {
        // Create dummy nodes and tail references for the two split lists
        ListNode dummyA = new ListNode(0);
        ListNode tailA = dummyA;

        ListNode dummyB = new ListNode(0);
        ListNode tailB = dummyB;

        // Create current reference to iterate through the list
        ListNode current = head;

        while (current != null) {
            // Use the function `f1` to decide which list this node should go to
            boolean splitFirst = f1(current);

            if (splitFirst) {
                // `current` node goes to the first split list
                tailA.next = current;
                tailA = tailA.next;
            } else {
                // `current` node goes to the second split list
                tailB.next = current;
                tailB = tailB.next;
            }

            // Move to the next node in the original list
            current = current.next;
        }

        // Ensure the two split lists end properly
        tailA.next = null;
        tailB.next = null;

        // Move ahead dummy nodes of split lists to hold the real head
        ListNode currentA = dummyA.next;
        ListNode currentB = dummyB.next;

        // Create dummy node and tail reference for the merged list
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (currentA != null && currentB != null) {
            // Use the function `f2` to determine which node to merge
            boolean mergeA = f2(currentA, currentB);

            if (mergeA) {
                tail.next = currentA;
                currentA = currentA.next;
            } else {
                tail.next = currentB;
                currentB = currentB.next;
            }

            // Move tail forward to the merged node
            tail = tail.next;
        }

        // If currentA is not completely traversed, attach remaining nodes
        if (currentA != null) {
            tail.next = currentA;
        }

        // If currentB is not completely traversed, attach remaining nodes
        if (currentB != null) {
            tail.next = currentB;
        }

        // Capture the merged list's head
        ListNode newHead = dummy.next;

        return newHead;
    }

    // Placeholder for the function `f1`, which decides how to split the nodes
    private boolean f1(ListNode node) {
        return node.val % 2 == 0;
    }

    // Placeholder for the function `f2`, which decides how to merge nodes
    private boolean f2(ListNode a, ListNode b) {
        return a.val <= b.val;
    }
}
```