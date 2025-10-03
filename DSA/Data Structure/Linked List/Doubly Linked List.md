
# Doubly Linked List

Consider a scenario where Neha leaves the class and transfers to another school. Even if we have the node storing Neha's information, deleting it is still not easy. To delete a node in a singly linked list, we need access to the node **1 step before** the node that has to be deleted. It is this node whose `next` pointer has to be updated to remove the given node. This operation, however, has a worst-case time complexity of **O(N)**, as we might have to traverse the entire list to get access to the node **1 step before** the given node. This is not efficient when we have very large lists.

Now, consider a case where we have a new student, Anmol, join the class, and we want to insert a node storing her information before Hari. Just like deletion, even if we have access to the node storing Hari's information, we still need to traverse the entire list to access the node **1 step before** the given node, as this node's `next` pointer has to be updated. Again, this operation has a worst-case time complexity of **O(N)** as we might have to traverse the entire list, which is inefficient.

## Limitations of singly linked lists

 singly linked lists have some serious limitations. Some basic operations are inefficient, as we might need to traverse the entire list to implement them.

![[Pasted image 20251001105921.png]]

The following operations have poor performance in singly linked lists:

- Insert at end
- Insert before a given node
- Delete the last node
- Delete the given node
- Delete node before a given node

## Doubly linked list

A doubly linked list is a bidirectional linear and dynamic data structure that stores data sequentially at random memory locations. **==Instead of storing just information about the next node in the list, a doubly linked list node also stores information about the previous node==**

![[Pasted image 20251001110216.png]]

## Advantages

If the address of the node is given, a doubly linked list guarantees the insertion and deletion of items in `O(1)` space and `O(1)` time. Since it is also bidirectional, it can be traversed in both directions from the **head** node to the **tail** node and similarly from the **tail** node to the **head** node.

![[Pasted image 20251001110243.png]]

a doubly linked list has a few advantages over a singly linked list, which are listed below.

> - **Traversal:** A doubly linked list is bidirectional and can be traversed in both directions.
> - **Efficient Insertion:** Insertion of a node next to a given node is much more efficient than a singly linked list.
> - **Efficient Deletion:** Deletion of a node next to a given node is much more efficient than deleting a single node in a singly linked list.


## Limitations

Doubly linked lists are very efficient for certain use cases but also have some limitations.

> - **Extra memory:** Compared to a singly linked list, a doubly linked list uses extra memory to store the information of the previous node in the sequence.
> - **More complicated:** Because a doubly linked list stores extra information in every node, the programmer must ensure it is always correct and up to date.


## Defining a node

Like singly linked lists, a **node** in a doubly linked list is its fundamental building block. Multiple nodes, when chained together, make up a doubly linked list. All operations performed on the list nodes, be they inserting, deleting, or updating data items, are performed on the list nodes.

## Structure of a node

The node of a doubly linked list is a simple yet highly effective extension of the node of a singly linked list. **==It just has an extra pointer called  `previous` in every node that stores the reference to the node before it in the list.==** This way, we can move **forward** and **backward** from any node, and operations involving reference manipulation become much easier. A doubly linked list node has three sections

> - **data:** The actual data item a node holds. This could be of any type.
> - **previous:** The is a reference to the previous node in the list
> - **next:** The is a reference to the next node in the list


![[Pasted image 20251001110827.png]]

```java
class ListNode {

    int val;

    ListNode prev;

    ListNode next;

    ListNode() {}

    ListNode(int val) { this.val = val; }

};
```

## Structure of a doubly linked list

Like a singly linked list, a doubly linked list is a chain of nodes. Below is how these nodes chain together to form a doubly linked list.

![[Pasted image 20251001111410.png]]

### Head node

Similar to a singly linked list, the first node of a doubly linked list is also called its **head**. The only difference between a singly and doubly linked list arises from the fact that a doubly linked node also has a `previous` pointer just like `next`. The `previous` pointer of the **head** node of a doubly-linked list is `null` just like the `next` pointer of the **tail** node in a singly linked list. This informs us that this is the last node traversing the list from **tail** to **head**. A representation of a doubly linked list in memory is given below.

![[Pasted image 20251001111642.png]]

### Tail node

Similar to a singly linked list, the **last** node of a doubly linked list is also called its **tail.** However, unlike a singly linked list, we can traverse a doubly linked list from the last node to the first node. For this to happen, however, we must always reference the **tail** node of a doubly-linked list just like we always have a reference to its **head**.

![[Pasted image 20251001111751.png]]


# Traversal

Traversal is the most fundamental operation on a doubly linked list and is the same as in a singly linked list. The extra information about the previous node that every node in a doubly linked list stores gives a doubly linked list the ability to traverse in two directions.

## Forward Traversal

Forward traversal is moving from the **head** to the **tail** node in the doubly linked list. It is implemented in the same way as in a singly linked list. We use a variable that holds a reference to a node in the linked list as the loop control variable, and every time we want to move forward we assign the reference of the `next` node in the linked list to this variable. We can get the reference of the `next` node by looking at the node pointed by the `next` pointer of the current node.

```java
  
// for loop
for(Node current = head; current != null; current = current.next);

  
// while loop
Node current = head;
while(current != null) {
    current = current.next;
}
```

## Reverse Traversal

Unlike a singly linked list, we can also traverse a doubly linked list in the reverse direction from the **tail** node to the **head** node, thanks to the `previous` pointer in every node that stores the reference to the previous node. Like forward traversal, we use a variable referencing a node as the loop control variable. We initialize it with the address of the **tail** node and follow the reference stored in the `previous` pointer in every iteration until we reach the **head** node, whose `previous` pointer is `null`

```java
//for
for(Node current = tail; current != null; current = current.prev) {
    System.out.print(current.data + " -> ");
}

// while
Node current = tail;
while(current != null) {
    System.out.print(current.data + " -> ");
    current = current.prev;
}
```


## Example: Node expedition

Given the **head** of a doubly linked list, write a function to print a comma (`,`) separated list of all the values from the start to the end.

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  

class Solution {

    public void nodeExpedition(ListNode head) {

        // Start from the head of the linked list

        ListNode current = head;

        // Iterate until the current node is not null

        while (current != null) {

            // Print the value of the current node

            System.out.print(current.val);

  
            // If there is a next node, print a comma after the value
            if (current.next != null) {
                System.out.print(", ");
            }

  
            // Move to the next node
            current = current.next;
        }
    }
}
```


## Example Node expedition II

Given the **tail** of a doubly linked list, write a function to print a comma (`,`) separated list of all the values from the start to the end.

```java
/**
 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public void nodeExpeditionII(ListNode tail) {

        ListNode current = tail;

        while(current != null) {

            System.out.print(current.val);

            if(current.prev != null) {
                System.out.print(", ");
            }

            current = current.prev;
        }
    }
}
```

## Example Node search

Given the **tail** of a doubly linked list and a **data** value, write a function to return the first node containing the given data. If no such node is found, return `null`.

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */


class Solution {

    public ListNode nodeSearch(ListNode tail, int data) {

        ListNode current = tail;

  
        while(current != null && current.val != data) {
            current = current.prev;
        }

        return current;
    }
}
```


# Insertion

## Insertion at Beginning

Inserting a node at the beginning of a doubly linked list is similar to inserting a node at the beginning of a singly linked list. The main difference is that a doubly linked list has two references stored in a node, and we need to keep track of both references

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** will be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` and `previous` pointers of this newly created **head** node are `null`, as this node is also the **tail** node of the list.

![[Pasted image 20251001125109.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set this new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Set this new node's `previous` pointer to `null` since it's the only node.
- **Step 4:** Return the new node, as this node is also the head node.

### 2. The list is not empty

In this scenario, the linked list already contains some data, so the **head** is not `null`, rather, it is the first node of the linked list. To insert a new node at the beginning of the list, create a new node and update its `next` pointer to hold the reference to the old **head**. Additionally, update the `previous` pointer of the original **head** node to point to the newly created node to maintain the bidirectional property. Finally, ensure that the `previous` pointer of the newly created node is `null`, as it is the end of the linked list in the reverse direction.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the `next` pointer of the new node to the current head, as the new node the will be the new head.
- **Step 3:** Set the `previous` pointer of current head to the new node to restore the bidirectional link.
- **Step 4:** Set the new node's `previous` pointer to `null` since it's the new head node.
- **Step 5:** Return the new node, as this is the new head.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  

class Solution {

    public ListNode insertAtBeginning(ListNode head, int data) {

        // Create a new node with the given data
        ListNode newNode = new ListNode(data);

  
        // Check if the list is empty
        if (head == null) {

            // Set the next pointer to null since it's the only node
            newNode.next = null;
            newNode.prev = null;

            // Return the newNode as this is the new head
            return newNode;
        }

  
        // Set the next pointer of the new node to the current head
        newNode.next = head;

  
        // Set the prev pointer of the new node to null since it will be
        // the new head
        newNode.prev = null;

  
        // Set the prev pointer of the current head to the new node
        head.prev = newNode;

        // Return the new node as the new head of the list
        return newNode;

    }
}
```


## Insertion at End

When inserting at the end of a doubly linked list, we must access the linked list's tail node. Fortunately, we have direct access to the list's tail node in a doubly linked list. This makes insertion at the end quite similar to insertion at the beginning.

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** will be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` and `previous` pointers of this newly created **head** node are `null`, as this node is also the **tail** node of the list.

![[Pasted image 20251001125746.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set this new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Set this new node's `previous` pointer to `null` since it's the only node.
- **Step 4:** Return the new node, as this node is also the tail node.

### 2. The list is not empty

In this scenario, the linked list already contains some data, so the **tail** is not `null`, rather, it is the last node of the linked list. To insert a new node at the end of the list, create a new node and update its `prev` pointer to hold the reference to the old **tail**. Also, ensure that the `next` pointer of the newly created node is `null`, as it is now the last node of the linked list. Finally, update the `next` pointer of the original **tail** node to point to the newly created node to maintain the bidirectional property.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the current tail's `next` pointer to hold the reference of the new node.
- **Step 3:** Set the new node's `previous` pointer to hold the reference of the current tail.
- **Step 4:** Set the new node's `next` pointer to `null`.
- **Step 5:** Return the new node, as this is the new tail.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {
    public ListNode insertAtEnd(ListNode tail, int data) {

        // Create a new node with the given data
        ListNode newNode = new ListNode(data);

  
        // Check if the list is empty
        if (tail == null) {
            // Set the next and prev pointer of the new node to null
            newNode.next = null;
            newNode.prev = null;

            // Return the newNode as this is the new tail
            return newNode;
        }

        // Set the next pointer of the tail to the new node
        tail.next = newNode;

        // Set the previous pointer of the new node to the current tail
        newNode.prev = tail;

        // Set the next pointer of the new node to null since it will be the new tail
        newNode.next = null;

        // Return the new node as the new tail of the list
        return newNode;

    }
}
```


## Insertion After the Given Node

Inserting a node after the given node is a simple operation. It is similar to inserting after the given node in a singly linked list. For a doubly linked list, we need to update the `previous` pointer of the newly created node to maintain the bidirectional structure.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, the method would return without making any changes.  

### 2. The list is not empty

Since the new node will be inserted between two existing nodes, we must ensure that we properly set up the `next` and `previous` pointers of these nodes. Inserting after a given node is a 5-step process.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the node's reference stored in the `next` pointer of the `given` node.
- **Step 3:** Set the new node's `previous` pointer to hold the reference of the `given` node.
- **Step 4:** Set the `given` node's `next` pointer to hold the reference of the new node.
- **Step 5:** Set the `previous` pointer of the node after the `given` node to hold the the reference of the `given` node.

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {
    public void insertAfterTheGivenNode(ListNode node, int data) {

        // Check if the given node is valid (not null)
        if (node == null) {
            // If the node is null, we cannot insert after it, so return.
            return;
        }

        // Create a new node with the given data
        ListNode newNode = new ListNode(data);
  

        // Link the new node to the next node in the list
        newNode.next = node.next;

  
        // Link the new node to the current node as its previous node
        newNode.prev = node;

        // Link the current node to the new node, effectively inserting the new node after it
        node.next = newNode;

  

        // If the new node has a valid next node, update its previous
        // node to point back to the new node
        if (newNode.next != null) {
            newNode.next.prev = newNode;
        }
    }
}
```


## Insertion Before the Given Node

In linked lists, it is important to access the node before the one being inserted or deleted. In a singly linked list, finding the node before the given one requires traversing the entire list. However, in a doubly linked list, the node before the given one can be accessed directly using the `previous` pointer stored in each node, simplifying the operation

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, we can return the **head** node that was provided as it is.

### 2. The given node is the first node

This is similar to **inserting at the beginning**, which we learned earlier. To determine if the given node is the first node, we can compare it to the **head** node. If both nodes are the same, then the given node is the **head** node.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the `next` pointer of the new node to the current head, as the new node the will be the new head.
- **Step 3:** Set the new node's `previous` pointer to `null` since it's the new head node.
- **Step 4:** Set the `previous` pointer of current head to the new node to restore the bidirectional link.
- **Step 5:** Return the new node, as this is the new head.

### 3. The given node is not the first node

In this scenario, we employ a reference manipulation similar to the one used for **inserting after a given node**. However, this time we use the `previous` pointer instead of the `next` one. The process of inserting before a given node involves five steps.

**Algorithm**

- **Step 1:** Create a new node with the `given` data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the `given` node.
- **Step 3:** Set the new node's `previous` pointer to hold the reference of the node before the `given` node.
- **Step 4:** Set the `next` pointer of the node before the given node to hold the the reference of the new node.
- **Step 5:** Set the `given` node's `previous` pointer to hold the reference of the new node.
- **Step 6:** Return the original head node.

### Implementation

```java
/**
 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

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
        // Check if the head or the node to insert before is null
        if (head == null || node == null) {
            return head;
        }

  

        // Create a new node with the provided data
        ListNode newNode = new ListNode(data);

        // Check if the node to insert before is the head of the list.
        if (node == head) {
            // Set the next pointer of the new node to the current head
            newNode.next = head;

            // Set the prev pointer of the new node to null since it will be the new head
            newNode.prev = null;

            // Set the prev pointer of the current head to the new node
            head.prev = newNode;

            // Return the newNode as this is the new head
            return newNode;
        }

  

        // Update the pointers of the new node to connect it with the
        // list. The next node of the new node is the node given
        newNode.next = node;

        // The previous node of the new node is the prev node of the given node
        newNode.prev = node.prev;

        // Update the next pointer of the previous node of the node to point to the new node.
        if (newNode.prev != null) {
   
            newNode.prev.next = newNode;
        }

        // Update the prev pointer of the node to point back to the new  node
        node.prev = newNode;

  
        // Return the updated head of the list
        return head;
    }
}
```

## Insertion at a Given Distance

a doubly linked list does not offer any specific advantage in this case because we don’t know the exact address of the node where we want to insert the new node, so we will have to traverse the list anyway. On the downside, it adds some extra complexity as now we also need to update the `previous` pointer of some nodes. Let’s look at all the cases we need to consider.

### 1. If the list is empty and X > 0

Attempting to insert a node at a position greater than 0 in an empty list is an invalid operation. In an empty list, no nodes are present, so the only valid position for insertion would be at position 0, making the new node the head of the list. However, when X is greater than 0, no corresponding position is available for insertion because the list lacks any elements. Therefore, we will return the existing **head**.  

### 2. X = 0

This means simply inserting a node at the beginning of a list, as we covered previously.

![[Pasted image 20251001133907.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the `next` pointer of the new node to the current head, as the new node the will be the new head.
- **Step 3:** Set the new node's `previous` pointer to `null` since it's the new head node.
- **Step 4:** Set the `previous` pointer of current head to the new node to restore the bidirectional link.
- **Step 5:** Return the new node, as this is the new head.

### 3. X <= size of the list

If the list is not empty, we need to traverse it while keeping a counter variable with the initial value of 0. Moving through the linked list, we increment this counter by 1 to keep track of the current index. We continue traversing the list until the counter has a value of `X-1`, which lands us at the node just **after** where we want to insert the new node. Now, the problem essentially comes down to **inserting after the given node**, which we have learned earlier.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Traverse the distance X - 1 while keeping track of the `current` node.
- **Step 3:** Set the new node's `next` pointer to hold the node's reference stored in the `next` pointer of the `current` node.
- **Step 4:** Set the new node's `previous` pointer to hold the reference of the `current` node.
- **Step 5:** Set the `current` node's `next` pointer to hold the reference of the new node.
- **Step 6:** Set the `previous` pointer of the node after the `current` node to hold the reference of the new node.
- **Step 7:** Return the original head node.

### 4. X > size of the list

If the value of `X` It is greater than the list's size, indicating an invalid case. For example, if we want to insert a node at position 5 in a list with only two items, we will return the existing **head**.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

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

        // If the list is empty, head is null, and X is greater than 0,
        // it's not possible to insert the new node, so return null.

        if (head == null && X > 0) {
            return null;
        }

        // Create a new node with the given data.
        ListNode newNode = new ListNode(data);

        // If X is 0, insert the new node at the beginning of the list.
        if (X == 0) {
        
            // Set the next pointer of the new node to the current head
            newNode.next = head;

  
            // Set the prev pointer of the new node to null since it will be the new head
            newNode.prev = null;
            if (head != null) {
                // Set the prev pointer of the current head to the new node
                head.prev = newNode;
            }

            // Return the new node as the new head of the list
            return newNode;
        }

        // Traverse the list to find the node at position X-1.
        ListNode current = head;

        // Counter to track the number of nodes traversed
        int counter = 0;

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

  
        // Insert the new node after the node at position X-1.

        newNode.next = current.next;

        newNode.prev = current;

        current.next = newNode;

        if (newNode.next != null) {
            newNode.next.prev = newNode;
        }

        // Return the updated head of the list
        return head;
    }
}
```

# Deletion

## Deletion of First Node

 Deleting the first node is similar to **inserting at the beginning** and is also one of the simplest deletion operations. We need to consider two cases.

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.

### 2. The list has only one node

Deleting the first node involves storing the reference to the current **head** in a temporary variable, updating the **head** to the next node in the list (which would be `null` in this case), and then deleting the old **head** node.

![[Pasted image 20251002105551.png]]

> **Algorithm**
> 
> - **Step 1:** Delete the head node to free up memory.
> - **Step 2:** Return `null` as the list is now empty.

### 3. The list has more than one node

When removing the first node, we update the **head** to hold the reference of the second node in the list. We also set the `previous` pointer of the second node to `null` and then delete the first node. However, before updating the **head**, it's important to use a temporary variable to store the reference of the current head node so that we can delete it later.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Set the `previous` pointer of the new head node to `null`.
- **Step 4:** Delete the original head node to free up memory.
- **Step 5:** Return the new head node.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */


class Solution {
    public ListNode deleteFirstNode(ListNode head) {

        // Check if the list is empty (no nodes)
        if (head == null) {

            // If the list is empty, there is nothing to delete, so return null
            return null;
        }

        // Check if there is only one node in the list
        if (head.next == null) {

            // Delete the single node
            head = null;

            // After deletion, the list becomes empty, so return null
            return null;
        }

        // If there are multiple nodes in the list Store the first node in a temporary pointer
        ListNode nodeToBeDeleted = head;

        // Update the head to point to the second node
        head = head.next;

        // Update the previous pointer of the new head to null
        head.prev = null;

        // Delete the first node
        nodeToBeDeleted = null;

        // Return the updated head of the list
        return head;
    }
}
```

## Deletion of Last Node

Deleting the last node in a doubly linked list is similar to **deleting the first node**. This is because we can access both the tail node and the previous pointer in each node.

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **tail**, as the list is empty, and no node needs to be deleted.  

### 2. The list has only one node

Deleting the last node in a linked list is the same as deleting the first node if there's only one node. The process involves storing the reference to the current **tail** in a temporary variable, updating the **tail** to the previous node in the list (which would be `null` in this case), and then deleting the old **tail** node.

![[Pasted image 20251002110643.png]]

**Algorithm**

- **Step 1:** Delete the tail node to free up memory.
- **Step 2:** Return `null` as the list is now empty.

### 3. The list has more than one node

When removing the last node, we update the **tail** to hold the reference of the second last node in the list. We also set the `next` pointer of the second last node to `null` and then delete the last node. However, before updating the **tail**, it's important to use a temporary variable to store the reference of the current tail node so that we can delete it later.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current tail node.
- **Step 2:** Move the tail pointer to the previous node.
- **Step 3:** Set the `next` pointer of the new tail node to `null`.
- **Step 4:** Delete the original head node to free up memory.
- **Step 5:** Return the new tail node.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {
    public ListNode deleteLastNode(ListNode tail) {

        // If the list is empty, there is nothing to delete, so return null
        if (tail == null) {
            return null;
        }

        // Check if there is only one node in the list
        if (tail.prev == null) {

            // Delete the single node
            tail = null;

            // After deletion, the list becomes empty, so return null
            return null;
        }
        
        // If there are multiple nodes in the list

        // Store the last node (tail) in a temporary pointer
        ListNode nodeToBeDeleted = tail;

        // Update the tail to point to the second-to-last node
        tail = tail.prev;

        // Update the next pointer of the new tail to null
        tail.next = null;

        // Delete the last node
        nodeToBeDeleted = null;

        // Return the updated tail of the list
        return tail;
    }
}
```

## Deletion by Given Data

deleting a node with a given data in a doubly linked list can be done by using the search operation. Instead of returning the data after finding it, we delete it during this operation

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The first node is deleted

If the data matches the first node, this case becomes the same as **deleting the first node**. We update the **head** to store the reference to the second node and delete the old head.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Set the `previous` pointer of the new head node to `null`.
- **Step 4:** Delete the original head node to free up memory.
- **Step 5:** Return the new head node.

### 3. The node to be deleted is not the first node

We need access to the node one step before it to delete a node that is not the first node of the linked list. This information can be obtained from the node's `previous` pointer. Deleting a node from within the list involves a four-step process.

> **Algorithm**
> 
> - **Step 1:** Traverse the list, keeping track of `current` node until reaching the given node.
> - **Step 2:** Set the `next` pointer of the node before the `current` node to hold the reference of the node after the `current` node.
> - **Step 3:** Set the `previous` pointer of the node after the `current` node to hold the reference of the node before the `current` node.
> - **Step 4:** Delete the `current` node to free up memory.
> - **Step 5:** Return the original head node.

### 4. The node to be deleted could not be found 

If the data provided does not match the data of any node in the linked list, then such a node does not exist in the list, so we return the existing **head**.

### Implementation

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode deleteNodeWithGivenData(ListNode head, int data) {

        // If the list is empty, there is nothing to delete, so return null

        if (head == null) {
            return null;
        }
        
        // If the first node's value matches the target data, delete the  first node
        if (head.val == data) {

  
            // Store the current head in a separate variable to be deleted later
            ListNode nodeToBeDeleted = head;

            // Move the head to the next node in the list
            head = head.next;


            // If the new head exists, update its previous pointer to be
            // null, as it is now the first node

            if (head != null) {
                head.prev = null;
            }

            // Delete the node with the target data by dereferencing it
            nodeToBeDeleted = null;

            // Return the new head of the list
            return head;
        }

        // Pointer to the current node, starting from the second node
        ListNode current = head.next;


        // If the target data is not in the first node, search for it in  the rest of the list
        while (current != null && current.val != data) {

            // Continue traversing the list until the target data is found or the end of the list is reached
            current = current.next;
        }

        // If the target data is not found in the list, return the head
        if (current == null) {
            return head;
        }

        // If the target data is found, remove the node from the list
        current.prev.next = current.next;

  

        // If the next node exists, update its previous pointer to skip the deleted node
        if (current.next != null) {
            current.next.prev = current.prev;
        }

  
        // Delete the node with the target data by dereferencing it
        current = null;

        // Return the head of the list, with the target data node removed
        return head;
    }
}
```


## Deletion After the Given Node

as an extra step, we also need to update the `previous` pointer after the deletion operation, but we have already done it for other operations, so you must be familiar with it by now. Let's examine all the cases we need to consider.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Deleting the node after the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The given node is the last node

When the given node is the last node in the list, attempting to delete a node after it becomes an invalid operation. This is because, by definition, the last node has no successor, i.e., no node following it in the sequence. We can return the **head** because no other operation needs to be done.  

### 3. The given node is not the last node

To delete a node after a given node, we can update the `next` pointer of the given node to skip over the node that needs to be deleted. Then, we can remove the node that we want to delete. However, since it is a doubly linked list, we must also update the `previous` pointers of the nodes involved.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the node's reference after the `given` node.
- **Step 2:** Set the `given` node's `next` pointer to hold the reference of the node stored in the `next` pointer of the node after the `given` node.
- **Step 3:** Set the `previous` pointer of the node after the `given` node to hold the reference of the `given` node.
- **Step 4:** Delete the node after the given node to free up memory.
- **Step 5:** Return the original head node.

### Implementation

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public ListNode deleteNodeAfterTheGivenNode(ListNode head, ListNode node) {
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

        // Link the current node (node) to the node after the one being deleted.
        node.next = nodeToBeDeleted.next;

        // Check if the node to be deleted is not the last node in the list
        if (nodeToBeDeleted.next != null) {
            // Point the previous node of the node to be deleted to the given node
            nodeToBeDeleted.next.prev = node;
        }

        // Dereference nodeToBeDeleted to allow garbage collection
        nodeToBeDeleted = null;

        // Return the original head.
        return head;
    }
}
```

## Deletion Before a Given Node

Deleting a node before the given node is an operation that gives a doubly linked list a significant advantage over a singly linked list. In a singly linked list, the implementation of this operation is complicated as it requires keeping a `previousToPrevious` reference variable to delete the node before a given node.

However, in a doubly linked list, we can access the nodes in the reverse direction using the `previous` pointer stored in every node, making the entire operation much simpler

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Deleting the node after the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The given node is the first node

When the given node is the first node in the list, attempting to delete a node before it becomes an invalid operation. This is because, by definition, the first node has no predecessor, i.e., no node preceding it in the sequence. We can return the **head** because no other operation needs to be done.  

### 3. The given node is the second node

This is a unique situation because removing the node before the second node essentially means deleting the linked list's head node. As learned earlier, this scenario is identical to **deleting the first node**. We need to update the head to store the reference to the second node and then delete the old head.

> **Algorithm**
> 
> - **Step 1:** Create a temporary pointer to store the current head node.
> - **Step 2:** Move the head pointer to the next node.
> - **Step 3:** Set the `previous` pointer of the new head node to `null`.
> - **Step 4:** Delete the original head node to free up memory.
> - **Step 5:** Return the new head node.

### 4. The given node is any other node

Deleting a node before a given node is similar to **deleting the given node**. The only difference is that the node to be deleted is the one before the given node. This process involves four steps.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the reference of the node before the `given` node.
- **Step 2:** Set the given node's `previous` pointer to hold the reference of the node before the node to be deleted.
- **Step 3:** Set `next` pointer of the node before the to-be-deleted node to hold the reference of the `given` node.
- **Step 4:** Delete the node before the `given` node to free up memory.
- **Step 5:** Return the original head node.

### Implementation

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public ListNode deleteNodeBeforeTheGivenNode(ListNode head, ListNode node) {
        // If the head or the given node is null, there is nothing to delete
        // Return the existing head
        if (head == null || node == null) {
            return head;
        }

        // If the given node is the head node, we cannot delete the node before it
        if (node == head) {
            return head;
        }

        // If the node to delete is the immediate next node of the head
        // Update the head to point to the next node, delete the original head,
        // and return the updated head
        if (head.next != null && head.next == node) {
            ListNode nodeToBeDeleted = head;
            head = head.next;

            // Update the new head's previous pointer to null
            head.prev = null;

            // Dereference for garbage collection
            nodeToBeDeleted = null;
            return head;
        }

        // If the node before the given node is not the head,
        // update the pointers of the neighboring nodes and delete the
        // node before the given node

        // Get the node before the given node
        ListNode nodeToBeDeleted = node.prev;

        // Update the previous pointer of the given node
        node.prev = nodeToBeDeleted.prev;
        if (nodeToBeDeleted.prev != null) {
            // Update the next pointer of the node before the given node
            nodeToBeDeleted.prev.next = node;
        }

        // Dereference for garbage collection
        nodeToBeDeleted = null;

        // Return the head of the updated linked list
        return head;
    }
}
```

## Deletion of the Given Node

The presence of a `previous` pointer in each node eliminates the need to traverse the list to locate the node immediately preceding the one that needs to be deleted.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Therefore, deleting the given node is not possible because there is no reference point within the list to perform the deletion. In this case, we can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. The first node is deleted

If the given node matches the first node, this case becomes the same as **deleting the first node**. We update the head to store the reference to the second node and delete the old head.

**Algorithm**

- **Step 1:** Create a temporary pointer to store the current head node.
- **Step 2:** Move the head pointer to the next node.
- **Step 3:** Set the `previous` pointer of the new head node to `null`.
- **Step 4:** Delete the original head node to free up memory.
- **Step 5:** Return the new head node.

### 3. The node to be deleted is not the first node

This case is super easy as it is very similar to **deleting the node with given data** but even easier as we do not need to traverse the linked list to find the node to be deleted. We already have the node to be deleted and need to update some references in the linked list to delete it. Deletion of a given node from between the list is a 3-step process.

**Algorithm**

- **Step 1:** Set the `next` pointer of the node before the `given` node to hold the reference of the node after the `given` node.
- **Step 2:** Set the `previous` pointer of the node after the `given` node to hold the reference of the node before the `given` node.
- **Step 3:** Delete the `given` node to free up memory.
- **Step 4:** Return the original head node.


### Implementation

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public ListNode deleteTheGivenNode(ListNode head, ListNode node) {
        // If the list is empty or the given node is null, there's nothing to do
        if (head == null || node == null) {
            return head;
        }

        // If the node to be deleted is the head node
        if (node == head) {
            head = head.next;

            // If there is a new head, update its previous pointer to null
            if (head != null) {
                head.prev = null;
            }

            // Dereference the node for garbage collection
            node = null;
            return head;
        }

        // If the node to be deleted is not the head node
        // Update the previous node's next pointer to skip the given node
        node.prev.next = node.next;

        // If the node to be deleted is not the last node in the list
        // Update the next node's previous pointer to skip the given node
        if (node.next != null) {
            node.next.prev = node.prev;
        }

        // Dereference the node for garbage collection
        node = null;

        // Return the original head of the list
        return head;
    }
}
```

## Deletion at a Given Distance

The aim is to create a logical and comprehensive approach encompassing various scenarios. Although the process is similar to a singly linked list, keeping track of the previous node in each case requires additional effort

### 1. The list is empty

When the list is empty, meaning it contains no elements, any attempt to delete a node is unnecessary because there are no nodes in the list. Since there is nothing to remove, the list remains unchanged. We can return the existing **head**, as the list is empty, and no node needs to be deleted.  

### 2. X = 0

In this scenario, we must delete the head node, i.e., **deleting the first node** in the linked list. We should update the **head** to point to the second node in the linked list and set the `previous` pointer of the second node to `null`. After completing these steps, we can then delete the original head node.

> **Algorithm**
> 
> - **Step 1:** Create a temporary pointer to store the current head node.
> - **Step 2:** Move the head pointer to the next node.
> - **Step 3:** Set the `previous` pointer of the new head node to `null`.
> - **Step 4:** Delete the original head node to free up memory.
> - **Step 5:** Return the new head node.

### 3. The node to be deleted is not the first node

In a doubly linked list, each node has a `previous` pointer, so we can move `X` steps using the current reference variable to reach the node that needs to be deleted. After that, the process is the same as **deleting the given node**. We need to adjust the pointers of the nodes that come before and after the current node and then delete the current node.

> **Algorithm**
> 
> - **Step 1:** Traverse the distance X while keeping track of the `current` node.
> - **Step 2:** Set the `next` pointer of the node before the `current` node to hold the reference of the node after the `current` node.
> - **Step 3:** Set the `previous` pointer of the node after the `current` node to hold the reference of the node before the `current` node.
> - **Step 4:** Delete the `current` node to free up memory.
> - **Step 5:** Return the original head node.

### 4. X >= the size of the linked list

This indicates an invalid query. For example, we cannot delete the 10th node in a list of size 3. We will return the existing **head** node.

**What about the case when X == size of the linked list?**

This is also an invalid case. To clarify, let's consider a list of size 5. In this scenario, the potential values of `X` could range from 0 to 4, meaning `[0, 4]`. Therefore, an input 5 would be invalid. It's important to note that X represents the distance from the head node, not the node's position.

### Implementation

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public ListNode deleteNodeAtGivenDistance(ListNode head, int X) {
        // Check if the list is empty. If so, there's nothing to delete,
        // so return null.
        if (head == null) {
            return null;
        }

        // If X is 0, we need to delete the first node
        if (X == 0) {
            // Store the node to be deleted in a temporary pointer
            ListNode nodeToBeDeleted = head;

            // Move the head to the next node, removing the first node
            head = head.next;

            // Update the new head's prev pointer
            if (head != null) {
                head.prev = null;
            }

            // Delete the node that was previously the head
            nodeToBeDeleted = null;

            // Return the new head
            return head;
        }

        // Initialize a current pointer to traverse the list
        ListNode current = head;

        // Initialize a counter to keep track of the distance from the head
        int counter = 0;

        // Traverse the list until either the end is reached or the
        // desired distance X is reached
        while (current != null && counter < X) {
            current = current.next;
            counter++;
        }

        // If the end of the list is reached before reaching the desired
        // distance X, there is no node to delete, so we return the original head.
        if (current == null) {
            return head;
        }

        // If the desired node is found at the given distance X,
        // update the previous node's next pointer to skip the current node
        if (current.prev != null) {
            current.prev.next = current.next;
        }

        // Update the next node's previous pointer to skip the current node
        if (current.next != null) {
            current.next.prev = current.prev;
        }

        // Delete the current node as it is no longer part of the list
        current = null;

        // Return the original head of the list
        return head;
    }
}
```

# Reversal

While we can reverse the list using loops in multiple passes, it is not the best way to do it, as the code is complicated and error-prone. Just like the singly linked list, the most concise and efficient way to reverse a doubly linked list is to use a single-pass in-place reversal algorithm,

![[Pasted image 20251003125906.png]]

## Reversing the entire list

Reversing the entire linked list is a special case of the generic reversal algorithm to reverse a segment between `start` and `end`.  We initialize a reference two references `newHead` and `current` and with `null` and the `head` of the list respectively and traverse the list from head to tail using `current`. In each iteration, we swap the `next` and `prev` section of the `current` node and move it forward by one step. We save the reference of the tail node in `newHead` when we reach it as it will be the head of the reversed list. At the end of all iterations, the entire list will be reversed and `newHead` will be the head of the reversed list.

**Algorithm**

- **Step 1:** Initialize `newHead` with `null` and `current` with `head`.
- **Step 2:** Iterate until `current` hits `null` and in each iteration do the following
    - **Step 2.1:** Swap `current.next` and `current.prev`
    - **Step 2.2:** Set `newHead` to `current` if `current.next` is `null`
    - **Step 2.3:** Set `current` to `current.prev` to move to next node
- **Step 3:** Return `newHead`

```java
/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

public class Reverse {
    public ListNode reverse(ListNode head) {

        // If the head is null or if it's the only node in the list, return the head as it is
        if (head == null || (head.next == null)) {
            return head;
        }

        // Reference to track the current node
        ListNode current = head;

        // Reference to hold the reversed head
        ListNode newHead = null;

        while (current != null) {
            // Swap the previous and next pointers
            ListNode temp = current.prev;
            
            current.prev = current.next;
            current.next = temp;

            // If the previous node is now null, the current node is the new head
            if (current.prev == null) {
                newHead = current;
            }

            // Move the current reference to the next node, which is now the previous node
            current = current.prev;
        }

        // Return the new head, which was the last node in the original list
        return newHead;
    }
}
```

## Reversing a segment

Reversing a segment between two nodes is the generic case of the reversal algorithm. Consider we are given a doubly linked list and references of two nodes `start` and `end` and we need to reverse the segment (including `start` and `end`).

For this example, the two references can never be `null` and will always point to some node in the list such that `start` comes before `end` when traversing the list in the forward direction from `head`.

![[Pasted image 20251003130357.png]]

create two references `leftBound` and `rightBound` and initialize them with the node before `start` and after `end` respectively. As we will see later, these references will be used to correctly connect the ends of the reversed segment back to the parent list.

![[Pasted image 20251003130421.png]]

The reversal algorithm can be broken down into two steps as given below.
### 1. Swap next and prev sections of nodes

We initialize a `current` reference with `start` and traverse the list until we hit `rightBound`. In each iteration, we swap the `next` and `prev` section of the `current` node.

### 2. Connect the reversed segment to the parent list

At the end of all iterations, the segment between `start` and `end` will be reversed, but its connection with the parent list will be incorrect.  The resulting list after all iterations is given below. We will have to connect `leftBound` with `end` (the start of the reversed list and `rightBound` with `start` (the end of the reversed list).

![[Pasted image 20251003130544.png]]

We then set the `next` section of `start` to  `rightBOund` and the `prev` section of the `rightBound` node to `start` to connect the tail of the reversed segment correctly with the parent list.

Similarly, we set the `next` section of the `leftBound` node to `end` and the `prev` section of `end` to  `leftBound` to connect the head of the reversed segment correctly with the parent list.

**Algorithm**

- **Step 1:** Check if the segment has less than two nodes. In that case, the reversed segment is the same as the original.
- **Step 2:** Initialize `leftBound` and `rightBound` with the node before `start` and after `end` respectively after doing null checks.
- **Step 3:** Initialize `current` with `start` and iterate until `current` hits `rightBound` and in each iteration do the following
    - **Step 3.1:** Swap `current.next` and `current.prev`
    - **Step 3.2:** Set `current` to `current.prev` to move to next node
- **Step 4:** Connect the tail of the reversed segment to `rigthBound` but setting `start.next` to `rightBound` and `rightBound.prev` to `start` after doing null checks.
- **Step 5:** Connect the head of the reversed segment to `leftBound` but setting `leftBound.next` to `end` and `end.prev` to `leftBound` after doing null checks.

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class ReverseALinkedList {
    public void reverse(ListNode start, ListNode end) {
        // If the start and end nodes are the same, no reversal needed
        if (start == end) {
            return;
        }

        // Initialize leftBound and rightBound
        ListNode leftBound = start.prev; // start can never be null
        ListNode rightBound = end.next; // end can never be null

        // Initialize current pointer to the start node
        ListNode current = start;

        // 1. Swap next and prev pointers of nodes within the segment
        while (current != rightBound) {
            // Swap the previous and next pointers
            ListNode temp = current.prev;
            current.prev = current.next;
            current.next = temp;

            // Move to what was previously the previous node (now stored in prev)
            current = current.prev;
        }

        // 2. Update boundary nodes

        // Correctly connect the new tail of the reversed segment to the rightBound
        start.next = rightBound;
        if (rightBound != null) {
            rightBound.prev = start;
        }

        // Correctly connect the new head of the reversed segment to the leftBound
        end.prev = leftBound;
        if (leftBound != null) {
            leftBound.next = end;
        }
    }
}
```

## Example Reverse first K nodes

Given the **head** of a doubly linked list and a positive integer **k**, write a function to reverse the first k nodes of the list and return the head of the reversed list.

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
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

            // Swap the previous and next nodes pointers of the current node
            ListNode temp = current.prev;
            current.prev = current.next;
            current.next = temp;

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

        // Update prev of the next node to point back to new tail
        if (current != null) {
            current.prev = head;
        }

        // Mark the previous pointer of the new head to nullptr
        if (previous != null) {
            previous.prev = null;
        }

        return previous;
    }
}
```

## Example Reverse last K nodes

Given the **head** of a doubly linked list and a positive integer **k**, write a function to reverse the last k nodes of the list and return the head of the reversed list.

You need to reverse the list in place.

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public int lengthOfList(ListNode head) {
        int length = 0;

        // Traverse the list and increment the length until the end
        while (head != null) {
            length++;
            head = head.next;
        }

        // Return the length
        return length;
    }

    public ListNode reverseAList(ListNode head) {
        // If the head is null or if it's the only node in the list,
        // return the head as it is
        if (head == null || (head.prev == null && head.next == null)) {
            return head;
        }

        // Pointer to track the current node
        ListNode current = head;

        // Pointer to track the previous node
        ListNode previous = null;

        while (current != null) {
            // Save the address of next node
            ListNode next = current.next;

            // Swap the previous and next nodes pointers of the current node
            ListNode temp = current.prev;
            current.prev = current.next;
            current.next = temp;

            // Store the previous node in the previous pointer
            previous = current;

            // Move the current pointer to the next node
            current = next;
        }

        // Return the new head, which is stored in the previous pointer
        return previous;
    }

    public ListNode reverseLastKNodes(ListNode head, int k) {
        // if K is less than or equal to 0, return the original head
        if (k <= 0) {
            return head;
        }

        // Find the length of the list
        int length = lengthOfList(head);

        // If k is greater than or equal to length, reverse the entire list
        if (k >= length) {
            return reverseAList(head);
        }

        // Find the (length - k)th node after which the reversal should occur
        ListNode current = head;
        for (int i = 1; i < length - k; i++) {
            current = current.next;
        }

        // Disconnect the last k nodes from the main list
        if (current.next != null) {
            current.next.prev = null;
        }

        // Reverse the last k nodes
        ListNode lastKReverseHead = reverseAList(current.next);

        // Connect the (length - k)th node to the new head
        current.next = lastKReverseHead;

        // Connect the new head of the reversed list to the (length - k)th node
        if (lastKReverseHead != null) {
            lastKReverseHead.prev = current;
        }

        return head;
    }
}
```

# Pattern Reversal Subproblem

Asking yourself the following questions will help you determine whether a problem is a reversal subproblem pattern problem or not.

**Ask yourself questions:**

Q1. Can the problem or solution be broken down into smaller subproblems?

Q2. Can any subproblem be solved by reversing a part of the linked list?

> **Problem statement:** Given a doubly linked list, reverse the list in groups of K in-place. If the last group in the list does not have K nodes, don't reverse it.


Consider the following example with `k = 3` for a linked list of size 7.

![[Pasted image 20251003132455.png]]

## Linked list reversal solution

Let's ask ourselves the questions we listed above to identify if we can reduce this problem to the two-pointer pattern problem.

**Template:**

Q1. Can the problem or solution be broken down into smaller subproblems?

A1. Yes, we can break down the solution as a combination `length / k` reversal operations, where `length` is the length of the linked list.

Q2. Can any subproblem be solved by reversing a part of the linked list?
A2. Yes, all subproblems except finding the length can be solved by reversing a part of the linked list.

The critical observation here is that reversing a group of size `k` is the same as reversing a part of the linked list between start and end. We traverse the linked list `k` nodes at a time and reverse each group as we go. We initialize a variable `groups` with the number of k-groups (`length / k`) to reverse. The number of k groups will always be a whole number, so we truncate the fractional part on division. We use the variable groups to iterate, and in each iteration, we reverse a k-group.

![[Pasted image 20251003132524.png]]

We initialize `start` and `end` with the `head` node and iterate `k-1` times using `end` to find the corresponding end for the first k-group. We then reverse the list between `start` and `end` using the reversal algorithm we learned earlier.

![[Pasted image 20251003132737.png]]

The reversed head of the first group will be the new head of the linked list, and so after the first reversal, we initialize a reference `newHead` with `end` as the new head of the doubly linked list.

![[Pasted image 20251003132836.png]]

Once the segment is reversed, the `start` for the next iteration will be the node after `start` , and so we update `start` to `start.next` and repeat the process.

![[Pasted image 20251003132850.png]]

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

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
        for (int i = 1; i < position; i++) {
            current = current.next;
        }
        return current;
    }

    public void reverse(ListNode start, ListNode end) {
        if (start == null || start == end) {
            return;
        }

        ListNode leftBound = start.prev;
        ListNode rightBound = end.next;
        ListNode current = start;
        ListNode previous = leftBound;

        while (current != rightBound) {
            ListNode next = current.next;

            ListNode temp = current.prev;
            current.prev = current.next;
            current.next = temp;

            previous = current;
            current = next;
        }

        start.next = rightBound;
        if (rightBound != null) {
            rightBound.prev = start;
        }

        end.prev = leftBound;
        if (leftBound != null) {
            leftBound.next = end;
        }
    }

    public ListNode reverseKSegments(ListNode head, int k) {
        // If the list is empty, has only one node, or k is 1, no need to
        // reverse segments
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        // Start of the current segment to be reversed
        ListNode start = head;

        // Find the total number of segments in the linked list
        int totalSegments = findLength(head) / k;

        // Loop through the list to reverse every k-length segment
        for (int i = 0; i < totalSegments; i++) {
            // Get the end node of the current segment
            ListNode end = getNodeAtPosition(start, k);

            // Reverse the segment
            reverse(start, end);

            // Check if the existing head needs to be updated.
            if (end.prev == null) {
                // If previous pointer of the end node (which becomes
                // start after the swap) is null, it means we're at the
                // first segment. So, we need to update the head to the
                // new head node
                head = end;
            }

            // Move start to the next segment
            start = start.next;
        }

        // Return the head of the modified list
        return head;
    }
}
```

## Example Pairwise swap

Given the **head** of a doubly linked list, write a function to **swap every two adjacent nodes** of this list and return the head of the reordered list.

The problem needs to be solved without modifying the values in the list's nodes. The nodes should be reordered by updating links

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public void reverse(ListNode start, ListNode end) {
        if (start == null || start == end) {
            return;
        }

        ListNode leftBound = start.prev;
        ListNode rightBound = end.next;
        ListNode current = start;
        ListNode previous = leftBound;

        while (current != rightBound) {
            ListNode next = current.next;

            ListNode temp = current.prev;
            current.prev = current.next;
            current.next = temp;

            previous = current;
            current = next;
        }

        start.next = rightBound;
        if (rightBound != null) {
            rightBound.prev = start;
        }

        end.prev = leftBound;
        if (leftBound != null) {
            leftBound.next = end;
        }
    }

    public ListNode pairwiseSwap(ListNode head) {
        // If the list is empty or has only one element, no reversal needed.
        if (head == null || head.next == null) {
            return head;
        }

        // Start of the current pair to be reversed
        ListNode start = head;

        // Loop while there are pairs to be swapped
        while (start != null && start.next != null) {
            // Get the end node of the current pair
            ListNode end = start.next;

            // Reverse the pair
            reverse(start, end);

            // Check if the existing head needs to be updated.
            if (end.prev == null) {
                // If previous pointer of the end node (which become
                // start after the swap) is null, it means we're at the
                // first pair. So, we need to update the head to the new
                // head node
                head = end;
            }

            // Move the start to the next pair.
            start = start.next;
        }

        // Return the head of the modified list
        return head;
    }
}
```

# Pattern Two Pointers

To perform any operation on the data items in a singly linked list, we must traverse it from head to tail and find those items. A doubly linked list, however, can be traversed in two directions, i.e., either from head to tail or tail to head, and depending on the problem, we may choose one direction over the other.

However, some problems require us to traverse the linked list in both directions simultaneously. While this is impossible with singly linked lists, we can simultaneously traverse in both directions in a doubly linked list using the two-pointer technique.

![[Pasted image 20251003133653.png]]

## Two pointer technique

The two-pointer technique uses two references, `left` and `right` initialized with the `head` and `tail` of the doubly linked list, respectively. We traverse in both directions by following the `next` and `prev` sections of nodes while iterating using `left` and `right`, respectively, until they meet in the middle or `left` goes beyond `right`. As we traverse the linked list, we perform the operations on the node held in `left` and `right` to solve the problem. At the end of each iteration, we hop as many nodes as dictated by the problem to close the gap `left` and `right`.

**Algorithm**

- **Step 1:** Initialize two references, `left` and `right,` to the `head `and `tail` of the doubly linked list.
- **Step 2:** Loop while `left` != `right` and `left.prev` != `right` do the following
    - **Step 2.1:** Do some operations on nodes held in `left` and `right` as dictated by the problem
    - **Step 2.2:** Decide if `left` should move forward and set `left` to `left.next` as many times as needed
    - **Step 2.3:** Decide if `right` should move forward and set `right` to `right.prev` as many times as needed


```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class ReverseALinkedList {
    public void twoPointer(ListNode head, ListNode tail) {
        // If the head and tail are the same or adjacent, nothing needs to be done
        if (head == null || tail == null || head == tail || head.next == tail) {
            return;
        }

        // Initialize left and right references
        ListNode left = head;
        ListNode right = tail;

        // Loop until the left and right pointers meet or cross each other
        while (left != right && left.prev != right) {
            /*
            Perform the operation on left and right
            Example: swapping values, comparing nodes, etc.
            */

            // Adjust pointers based on conditions
            if (shouldMoveLeft) {
                left = left.next;
            }

            if (shouldMoveRight) {
                right = right.prev;
            }
        }
    }
}
```

## Example Palindrome number

Given the **head** and **tail** of a sorted doubly linked list, write a function that returns `true` if the list represents a palindrome number or `false` otherwise.

```java
import java.util.*;

/**

 * Definition for doubly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode prev;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    boolean palindromeNumber(ListNode head, ListNode tail) {

        if (head == null || tail == null) {

            return true;
        }

        ListNode left = head;

        ListNode right = tail;

        while(left != right && left.prev != right) {

            if(left.val != right.val)
                return false;

            left = left.next;
            right = right.prev;
        }
        return true;
    }
}
```

## Example Two sum

Given the **head** and **tail** of a sorted doubly linked list along with an integer **target**, write a function to return all the pairs that sum up to the given target. You must do this without using any extra space.

```java
import java.util.*;

/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Solution {
    public List<List<Integer>> twoSum(ListNode head, ListNode tail, int target) {
        // Check if the list is empty or has only one element
        if (head == null || head.next == null) {
            // Return an empty list since there are no pairs to be found
            return new ArrayList<>();
        }

        // Store the pairs of values that sum up to the target
        List<List<Integer>> result = new ArrayList<>();
        ListNode left = head;
        ListNode right = tail;

        // Iterate until either left or right becomes null or left's
        // value becomes greater than right's value
        while (left != null && right != null && left.val < right.val) {
            if (left.val + right.val == target) {
                // If the sum of left and right values is equal to the target
                // Add the pair to the result list
                List<Integer> pair = new ArrayList<>();
                pair.add(left.val);
                pair.add(right.val);
                result.add(pair);

                // Move left to the next node
                left = left.next;

                // Move right to the previous node
                right = right.prev;
            }
            // If the sum of left and right values is less than the target
            // Move left to the next node
            else if (left.val + right.val < target) {
                left = left.next;
            }
            // If the sum of left and right values is greater than the target
            // Move right to the previous node
            else {
                right = right.prev;
            }
        }

        // Return the list containing pairs of values that sum up to the target
        return result;
    }
}
```

# Pattern Reorder

Some linked list problems require us to reorder the nodes of the given list in place based on some conditions. In most cases, this requires first splitting the list based on the outcome of some function `f1` and then merging back the split list together either by using another function `f2` or simply concatenating them.

![[Pasted image 20251003152103.png]]

## Reordering technique

Consider that we are given a doubly linked list whose nodes must be reordered. The problem almost always has a split function `f1`, that we use to split the list into multiple lists using the split technique. The split technique for a doubly linked list is exactly the same as for a singly linked list, with only one extra step to connect the `prev` section of nodes as we move them.

In most cases, concatenating these split lists to merge them is sufficient, but sometimes, we may also have a function `f2` that must be used to merge the lists. We use the merge technique to merge them to solve the problem. The merge technique for a doubly linked list is exactly the same as for a singly linked list, with only one extra step to connect the `prev` section of nodes as we move them.

**Algorithm**

- **Step 1:** Use the split technique to split the list in **two** using the function `f1`
- **Step 2:** Use the merge technique to merge the **two** lists using the function `f2`.
- **Step 3:** Return the head of the merged list.

```java
/**
 * Definition for doubly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode prev;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

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
                current.prev = tailA;
                tailA = tailA.next; // Move tailA forward
            } else {
                // `current` node goes to the second split list
                tailB.next = current;
                current.prev = tailB;
                tailB = tailB.next; // Move tailB forward
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

        // Set prev pointer of head of both list to null
        if (currentA != null) currentA.prev = null;
        if (currentB != null) currentB.prev = null;

        // Create dummy node and tail reference for the merged list
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (currentA != null && currentB != null) {
            // Use the function `f2` to determine which node to merge
            boolean mergeA = f2(currentA, currentB);

            if (mergeA) {
                tail.next = currentA;     // Merge node from currentA
                currentA.prev = tail;     // Connect the prev section to tail
                currentA = currentA.next; // Move currentA forward
            } else {
                tail.next = currentB;     // Merge node from currentB
                currentB.prev = tail;     // Connect the prev section to tail
                currentB = currentB.next; // Move currentB forward
            }

            // Move tail forward to the merged node
            tail = tail.next;
        }

        // If currentA is not completely traversed, attach remaining nodes
        if (currentA != null) {
            tail.next = currentA;
            currentA.prev = tail;
        }

        // If currentB is not completely traversed, attach remaining nodes
        if (currentB != null) {
            tail.next = currentB;
            currentB.prev = tail;
        }

        // Capture the merged list's head
        ListNode newHead = dummy.next;
        if (newHead != null) newHead.prev = null;

        return newHead;
    }
}
```