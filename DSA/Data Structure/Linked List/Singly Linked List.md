
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