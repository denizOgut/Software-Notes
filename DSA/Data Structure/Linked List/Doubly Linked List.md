
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