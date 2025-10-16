
# Stack

## Understanding the problem

Many times in a program, we need to have a data store that is **smart** enough and remembers the order in which the data was added. This is especially useful in cases where we want to process data items in a **L**ast **I**n **F**irst **O**ut **(LIFO)** or **F**irst **I**n **L**ast **O**ut (**FILO**) order. This is a fairly common requirement in many use cases

### Web browsers

This is perhaps the most visible use case where the order of data items matters. All modern web browsers have a **back** button that takes you to the previous webpage you were browsing. This functionality is very simple and straightforward, but to implement this, we need to store all the web pages the user visits and present the data in reverse **(LIFO)** order when the user clicks the back button.

### Text editors

Like web browsers, this is another example of a problem that relies on the order of data added to a data store. Almost all text editors have an **undo** feature that lets us revert changes in the order we make them. To implement this functionality, text editors need to store all the user data somewhere and retrieve it in the reverse (**LIFO**) order.

### Nested function calls

This is another problem where the order of data items in a data store matters. A function call in almost all programming languages returns the execution to the calling function, which returns the execution to the function that called it, and this chain goes on. This order of returning control is essentially the reverse order in which the functions were called. The processor in a computer system has a smart data structure that stores the order of these function calls and returns the control in the reverse **(LIFO)** order when requested.

## Exploring a possible solution

**==A stack is a linear container that allows adding and removing items at only one end. This restriction on adding and removing items only from one end ensures that what goes last in the stack comes out first (LIFO).==**

### Stack data structure

![[Pasted image 20251012201707.png]]

Like a real-world stack, we can mimic the LIFO order by restricting the addition and removal of data only at one end. 

## Key properties of a stack

### Capacity

A stack's capacity is the maximum number of data items it can hold. Only **bounded** stacks have a predefined capacity. **Unbounded** stacks ideally have an unlimited capacity restricted only by the amount of memory available on the system where the code executing the stack implementation is running.

![[Pasted image 20251012201807.png]]

### Size

The size of a stack is the number of data items it holds at any given time. This value changes when data items are added to or removed from the stack.

![[Pasted image 20251012202341.png]]

### Top

The data item inserted last into the stack appears to be at the top of the stack in its logical representation; hence, it is called the **top** of the stack. If the stack is empty, there is no data at the top of the stack.

## Supported Operations

### Push

The push operation on a stack is the only way to add data to a stack. This operation adds a data item to the **top** of the stack and increases its size by 1.

![[Pasted image 20251012202558.png]]

![[Pasted image 20251012202611.png]]


### Pop

The pop operation is the only way to remove data from a stack. It removes the data item at the **top** of the stack and decreases its size by 1

![[Pasted image 20251012202645.png]]

![[Pasted image 20251012202656.png]]

### Size

Size is also a property of the stack. The size operation returns the value of this property, which is the current size of the stack.

![[Pasted image 20251012202904.png]]

### Top

Like size, the top is also a property of the stack, and the top operation returns the value of this property, which is the data item at the top of the stack.

![[Pasted image 20251012202926.png]]

# Array Implementation Of Stack

A stack is a linear data structure that only supports push and pop operations to add and remove data items from one end of the stack. This makes the **array** the perfect candidate to implement stacks. Most use cases can be solved using a **bounded** stack with a fixed capacity and cannot grow beyond that.

![[Pasted image 20251012203027.png]]

## State information

To implement a stack using an array, we also need to hold and keep up-to-date certain information about the stack alongside the array that holds all the data items. This information is necessary to ensure all stack operations work as desired

### Top Index

The index of the data item in the array that holds the top of the stack is the `topIndex`. The value of the `topIndex` changes when data items are pushed onto and popped from the stack. It is important to make sure that the `topIndex` always stores the index of the top of the stack for the proper functioning of all the operations.

![[Pasted image 20251012203328.png]]

### Size

It is important to keep track of the number of data items currently held in the stack. This value is also modified whenever data is pushed in or popped from the stack. It is important to ensure that this value is always correct and less than the total capacity of the array to prevent attempts to access memory outside the array, which is a frequent cause of program crashes. We don't need to hold the value of the size of the stack in a separate variable, as it can be derived from the value of `topIndex` in the array implementation of a stack.

![[Pasted image 20251012203412.png]]

### Capacity

Since an array has a fixed size when implementing a stack using an array, the size of the stack is **bounded** by the size of the array. It's very important to ensure we never exceed this capacity, so we must hold this information about the array's capacity somewhere. Just like the `topIndex` variable, we use another variable, `capacity` to hold the size of the array used to implement the stack.

![[Pasted image 20251012203434.png]]

## Representation in memory

We know that data items in an array reside in contiguous memory, so if we implement a stack as an array, all the data items in the stack will reside next to each other.

![[Pasted image 20251012203456.png]]


## Implementation

when implementing a stack using an array, we always need to keep track of some state information, which is necessary to perform operations on a stack. The state information, the array, and all the operations performed on a stack can be **encapsulated in a class**.

![[Pasted image 20251012203622.png]]

```java
class Stack {
    // Array to store the stack elements
    public int[] arr;
    // Maximum capacity of the stack
    public int capacity;
    // Index of the top element in the stack
    public int topIndex;

    public Stack(int capacity) {
        this.capacity = capacity;
        // Dynamically allocate memory for the stack array
        arr = new int[capacity];
        // Set initial top index to -1 (indicating an empty stack)
        topIndex = -1;
    }

    public int size() {
        // Size of the stack is the index of the top element plus 1
        return topIndex + 1;
    }

    public boolean empty() {
        // If top index is -1, the stack is empty
        return topIndex == -1;
    }

    public int top() {
        if (empty()) {
            // Return -1 if the stack is empty
            return -1;
        }
        // Return the element at the top index of the stack
        return arr[topIndex];
    }

    public boolean push(int val) {
        if (topIndex == capacity - 1) {
            // Return false if the stack is already full
            return false;
        }
        // Increment top index and add the val to the new top position
        arr[++topIndex] = val;
        // Return true to indicate successful push operation
        return true;
    }

    public int pop() {
        if (empty()) {
            // Return -1 if the stack is empty (nothing to pop)
            return -1;
        }
        // Return the element at the top index and decrement top index
        return arr[topIndex--];
    }
}
```


##  Design two stacks in an array

Given the skeleton of a **TwoStack class** that supports two stacks internally using a single array, complete this class by implementing all the stack operations below. 

> - **TwoStack(int capacity)** - Initializes the TwoStack object with the given capacity, which represents the total capacity of both stacks. Both stacks must share the same capacity. If it is not feasible for both internal stacks to be of equal size, the first stack should have a greater capacity than the second stack.
> - **top1()** - Returns the element at the top of the first stack. If the stack is empty, it returns `-1`.
> - **top2()** - Returns the element at the top of the second stack. If the stack is empty, it returns `-1`.
> - **push1(int val)** - Pushes the given value onto the first stack and returns `true` if the operation is successful. It returns `false` if the stack is full.
> - **push2(int val)** - Pushes the given value onto the second stack and returns `true` if the operation is successful. It returns `false` if the stack is full.
> - **pop1()** - Pops the top element from the first stack and returns its value. If the stack is empty, it returns `-1`.
> - **pop2()** - Pops the top element from the second stack and returns its value. If the stack is empty, it returns `-1`.

You must abide by the following constraints

1. Use a **single array** to implement both stacks. 

> The input should adhere to the following rules:
> 
> 1. The input should contain two arrays of the same size.
> 2. The first array should contain the list of operations, while the second should contain the corresponding operands for those operations.
> 3. The first index in the first array should contain **TwoStack**, and the first index in the second array should contain a single positive integer representing the capacity of the stack. This value is used to initialise the stack.
> 4. For each index in the first array that contains **push1**, or **push2** operations, the corresponding index in the second array should contain the value that needs to be pushed.
> 5. For each index in the first array that contains **pop1**, **top1**, **pop2**, or **top2** operations, the corresponding index in the second array should contain an empty array.

```java
class TwoStack {
    // Array to store elements
    public int[] arr;
    // Capacity of the array
    public int capacity;
    // Top index of the first stack
    public int topIndex1;
    // Top index of the second stack
    public int topIndex2;

    public TwoStack(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        // Initialize top index of the first stack as -1 (empty)
        topIndex1 = -1;
        // Initialize top index of the second stack as capacity (empty)
        topIndex2 = capacity;
    }

    public int top1() {
        if (topIndex1 == -1) {
            // Stack 1 is empty, return -1
            return -1;
        }
        // Return the element at the top of Stack 1
        return arr[topIndex1];
    }

    public int top2() {
        if (topIndex2 == capacity) {
            // Stack 2 is empty, return -1
            return -1;
        }
        // Return the element at the top of Stack 2
        return arr[topIndex2];
    }

    public boolean push1(int val) {
        if (topIndex1 + 1 >= topIndex2) {
            // Stack 1 is full, cannot push more elements
            return false;
        }
        // Increment top index of Stack 1 and assign val to that position
        arr[++topIndex1] = val;
        // Push operation was successful
        return true;
    }

    public boolean push2(int val) {
        if (topIndex2 - 1 <= topIndex1) {
            // Stack 2 is full, cannot push more elements
            return false;
        }
        // Decrement top index of Stack 2 and assign val to that position
        arr[--topIndex2] = val;
        // Push operation was successful
        return true;
    }

    public int pop1() {
        if (topIndex1 == -1) {
            // Stack 1 is empty, cannot pop any element
            return -1;
        }
        // Return the element at the top of Stack 1 and decrement top index
        return arr[topIndex1--];
    }

    public int pop2() {
        if (topIndex2 == capacity) {
            // Stack 2 is empty, cannot pop any element
            return -1;
        }
        // Return the element at the top of Stack 2 and increment top index
        return arr[topIndex2++];
    }
}
```

# Linked List Implementation Of Stack

 a linked list is another data structure that is the perfect candidate for implementing a stack. Unlike arrays, which have a fixed size and are used to implement **bounded** stacks, linked lists can be as big as the computer memory permits, so they can be used to implement an **unbounded** stack.

![[Pasted image 20251013122824.png]]

## State information

Like the array implementation, when implementing a stack using a linked list, we need to hold and keep updated certain **state information** alongside the linked list that holds all the data items to ensure all stack operations work as desired. Let us look at all the state information we need to maintain.

### Top

Unlike in the array implementation, where we had to use the `topIndex` to store the index of the top item in the array, in the linked list implementation, we can use the `head` or `tail` of the list as a reference to the top. If we restrict inserting data items only at the beginning of the list, the `head` of the list is also becomes the top of the stack. On the other hand, if we restrict inserting data items only at the end of the list, the `tail` becomes the top of the stack. In this course, we will use a linked list implementation that only allows insertion at the beginning of the list and hence the `head`  will be at the top of the stack.

![[Pasted image 20251013122852.png]]

### Current Size

Unlike the array implementation of a stack, where we derive the stack size using the value stored in the `topIndex` variable, the linked list implementation has no `topIndex` variable. To always know the current size of the stack, we need to store this information in a `currentSize` variable. Every time data is pushed onto or popped from the stack, the value of `currentSize` variable is incremented or decremented by 1.

![[Pasted image 20251013122915.png]]

### Capacity

The linked list implementation of a stack can be used to implement both **bounded** and **unbounded** stacks. Since unbounded stacks have unlimited capacity, we don't need to store the maximum limit in any variable. However, when implementing a bounded stack using linked lists, we store that maximum limit in a `capacity`variable similar to the array implementation. Whenever we add a data item to the stack, we must ensure that the queue size doesn't exceed the stack's capacity.

## Stack class

The fundamental idea is the same. However, the implementation is different.

![[Pasted image 20251013123425.png]]

## Implementation

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Stack {
    // Reference to the head of the stack
    public ListNode head;
    // Maximum capacity of the stack
    public int capacity;
    // Current number of elements in the stack
    public int currentSize;

    public Stack(int capacity) {
        // Initialize the capacity of the stack
        this.capacity = capacity;
        // Initialize the currentSize to zero
        this.currentSize = 0;
        // Initialize the head reference to null
        this.head = null;
    }

    public int size() {
        // Return the current number of elements in the stack
        return currentSize;
    }

    public boolean empty() {
        // Return true if the stack is empty, false otherwise
        return currentSize == 0;
    }

    public int top() {
        if (empty()) {
            // If the stack is empty, return -1 (an invalid value)
            return -1;
        }
        // Return the value of the element at the top of the stack
        return head.val;
    }

    public boolean push(int val) {
        if (currentSize == capacity) {
            // If the stack is already full, return false
            return false;
        }
        // Create a new node with the given val
        ListNode newNode = new ListNode(val);
        // Set the next reference of the new node to the current head
        newNode.next = head;
        // Update the head reference to the new node
        head = newNode;
        // Increment the count of elements in the stack
        currentSize++;
        // Return true to indicate a successful push operation
        return true;
    }

    public int pop() {
        if (empty()) {
            // If the stack is empty, return -1 (an invalid value)
            return -1;
        }
        // Store the value of the element at the top of the stack
        int value = head.val;
        // Create a temporary reference to the current head
        ListNode temp = head;
        // Update the head reference to the next node
        head = head.next;
        // Delete the old head node to free memory
        temp = null;
        // Decrement the count of elements in the stack
        currentSize--;
        // Return the value of the popped element
        return value;
    }
}
```

# Infix Postfix and Prefix Notations

## Infix Notation

The style of writing mathematical expression we humans are used to is called the **infix notation**. It is characterized by the placement of operation **between** its operands.

![[Pasted image 20251013141740.png]]

The infix notation seems very intuitive and easy to understand for us humans; however, parsing evaluation and expression written in this notation is quite a challenge for computer systems.

### Challenges with the infix notation

Let's consider how a computer evaluates a mathematical expression to understand the problem better. Most CPUs at the root level only do one mathematical operation, such as addition, subtraction, etc., at a time. Since all these are binary operations, they only take two input values at a time.

Consider the example of a mathematical expression where we must add two numbers. A CPU takes these two numbers as its input, performs the addition, and generates the result.

![[Pasted image 20251013141810.png]]

![[Pasted image 20251013141836.png]]

An expression must be evaluated in the correct order of precedence of its operations to get the correct results. Consider the following mathematical expression with different types of operations. To evaluate it correctly, the evaluation order of operation should follow the operator precedence rule, which means, in this case, we must start the evaluation from the middle and not the left.

Such an evaluation is quite easy for humans because we can easily jump back and forth in the expression, solve parts of expressions first, save contextual information in our brain, and iteratively evaluate each operation in the order of precedence until the entire expression is evaluated.

However, formulating this entire process as an algorithm for a CPU that only performs one binary operation at a time is very difficult. We would first need to parse the entire expression, identify all operations and their precedence, solve individual operations in the correct order, save the intermediate results, and repeat this process multiple times. All this becomes even more difficult when we add parentheses to this mix that can create an arbitrary level of nesting.

![[Pasted image 20251013141923.png]]

## Postfix Notation

The idea behind the postfix notation is quite simple: instead of writing operations between the operands, the operation is written **after** the operand. Hence, the name postfix notation is also known as the reverse Polish notation.

![[Pasted image 20251013142246.png]]

### Examples

![[Pasted image 20251013142455.png]]

### How does postfix notation work

In the infix notation, parentheses dictate the order in which operations are performed, and all operators follow specific precedence rules. The postfix notation, on the other hand, can be evaluated by traversing the expression sequentially from start to end.

![[Pasted image 20251013142644.png]]

To evaluate the postfix notation, we start from the leftmost item and keep moving to the right until we encounter an operator. We then use the required number of operands from the most recently seen operands to evaluate the operation, store the result, and keep moving right. This left-to-right evaluation implicitly enforces precedence, i.e., the operator operand pair that comes first is evaluated first. Hence, the postfix notation also eliminates the need for parentheses and operator precedence rules.

![[Pasted image 20251013142733.png]]

## Prefix Notation

 It is an alternative notation to write the mathematical expression where the operator is written **before** the operands. It is also called the Polish notation.

![[Pasted image 20251013143207.png]]

### Examples

![[Pasted image 20251013143232.png]]

### How does prefix notation work

The prefix notation is evaluated very similarly to the postfix notation, the only difference being that we evaluate the expression in reverse from end to start.

![[Pasted image 20251013143338.png]]

 start from the rightmost item and move to the left until we encounter any operator. We then use the required number of operands from the most recently seen operands to evaluate the operation, store the result, and keep moving left. This right-to-left evaluation implicitly enforces precedence, i.e., the operator operand pair that comes first is evaluated first. Hence, the prefix notation eliminates the need for parentheses and operator precedence rules.


![[Pasted image 20251013143419.png]]

# Evaluating Expressions

## Postfix Expression

computers can easily understand these expressions as evaluating them only requires traversal from left to right, no back-and-forth jumping, and complex precedence rules.

Consider we are given the postfix notation of a mathematical expression as a string given below, where every operand is a single-digit number.

![[Pasted image 20251014161145.png]]

To evaluate a postfix notation, we create a stack `stack` to keep track of all the operands. We then traverse the string from start to end and, in each iteration, check if the current character is a digit or an operator. If the character is a digit, we push it to the top of the stack. If not, we pop two items from the top of the stack and use them as operands for the current operation. We then store the result at the top of the stack to be used as an operand for a subsequent iteration and continue the traversal.

This process is repeated in each iteration until the string traversal is complete. At the end of all iterations, the stack only has one item, which is the output of the complete evaluation of the expression.

### Algorithm

- **Step 1:** Create a stack `stack` to keep track of the most recent operands
- **Step 2:** Iterate in the sequence from start to end, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, push it to the `stack`
    - **Step 2.2:** Otherwise, if the current item is an operator, do the following:
        - **Step 2.2.1:** Pop two items(`operand2` and `operand1`) from the `stack` and use them as operands for the current operator
        - **Step 2.2.2:** Push the result to the top of the `stack`
- **Step 3:** Return the item at the top of the `stack`

```java
import java.util.*;

class Solution {
    // Function to perform arithmetic operations
    public float performOperation(
        float operand1,
        float operand2,
        char operation
    ) {
        switch (operation) {
            case '+':
                return operand1 + operand2;
            case '-':
                return operand1 - operand2;
            case '*':
                return operand1 * operand2;
            case '/':
                return operand1 / operand2;
            default:
                return 0;
        }
    }

    public float evaluateAPostfixExpression(String postfix) {
        // Stack to store operands
        Stack<Float> stack = new Stack<>();
        // Iterate through each character in the postfix expression
        for (char ch : postfix.toCharArray()) {
            // If the character is an operand (a digit)
            if (Character.isDigit(ch)) {
                // Convert it to a float and push it onto the stack
                stack.push((float) (ch - '0'));
            }
            // If the character is an operator (an arithmetic symbol)
            // perform the operation on the top two operands in the stack
            // and push the result back onto the stack
            else {
                // Get the top operand from the stack
                float operand2 = stack.pop();
                // Get the second top operand from the stack
                float operand1 = stack.pop();
                // Apply the arithmetic operation and push the result
                // back to the stack
                stack.push(performOperation(operand1, operand2, ch));
            }
        }
        // Return the final result
        return stack.peek();
    }
}
```

## Prefix Expression

Evaluation of the prefix notation of a mathematical expression is very similar to the postfix notation. Since the placement of operators and operands in the notation implicitly enforces precedence, we traverse the sequence and incrementally evaluate results as we see the operands. The only between evaluation postfix and prefix notation is that for evaluating a prefix notation we traverse the sequence in reverse from end to start.

Consider we are given the prefix notation of a mathematical expression as a string given below, where every operand is a single-digit number.

![[Pasted image 20251014162933.png]]

To evaluate a prefix notation, we create a stack `stack` to keep track of all the operands. We then traverse the string from right to left and, in each iteration, check if the current character is a digit or an operator. If the character is a digit, we push it to the top of the stack. If not, we pop two items from the top of the stack and use them as operands for the current operation. We then store the result at the top of the stack to be used as an operand for a subsequent iteration and continue the traversal to the left.

This process is repeated in each iteration until the string traversal is complete. At the end of all iterations, the stack only has one item, which is the output of the complete evaluation of the expression.

>It is important to note that when traversing the string from right to left, the most recent item in the stack is the leftmost item seen so far. And so, the first item popped from the stack is the **first** operand, and the second item popped is the **second** operand. This is because the order of writing the operands is always left to right regardless of infix, prefix, or postfix notation.

### Algorithm

**Algorithm**

- **Step 1:** Create a stack `stack` to keep track of the most recent operands
- **Step 2:** Iterate in the sequence in reverse, from end to start, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, push it to the `stack`
    - **Step 2.2:** Otherwise, if the current item is an operator, do the following:
        - **Step 2.2.1:** Pop two items(`operand1` and `operand2`) from the `stack` and use them as operands for the current operator
        - **Step 2.2.2:** Push the result to the top of the `stack`
- **Step 3:** Return the item at the top of the `stack`

```java
import java.util.*;

class Solution {
    // Function to perform arithmetic operations
    public float performOperation(
        float operand1,
        float operand2,
        char operation
    ) {
        switch (operation) {
            case '+':
                return operand1 + operand2;
            case '-':
                return operand1 - operand2;
            case '*':
                return operand1 * operand2;
            case '/':
                return operand1 / operand2;
            default:
                return 0;
        }
    }

    public float evaluateAPrefixExpression(String prefix) {
        // Initialize an empty stack to store operands
        Stack<Float> stack = new Stack<>();
        // Reverse the prefix expression
        String reversedPrefix = new StringBuilder(prefix)
            .reverse()
            .toString();
        // Iterate through each character in the reversed prefix
        // expression
        for (char ch : reversedPrefix.toCharArray()) {
            // If the character is an operand (a digit)
            if (Character.isDigit(ch)) {
                // Convert it to a float and push it onto the stack
                stack.push((float) (ch - '0'));
            }
            // If the character is an operator (an arithmetic symbol)
            // perform the operation on the top two operands in the stack
            // and push the result back onto the stack
            else {
                // Pop the top element from the stack as the first
                // operand
                float operand1 = stack.pop();
                // Pop the top element from the stack as the second
                // operand
                float operand2 = stack.pop();
                // Apply the arithmetic operation and push the result
                // back to the stack
                stack.push(performOperation(operand1, operand2, ch));
            }
        }
        // Return the final result
        return stack.pop();
    }
}
```

# Converting expressions using stack

## Understanding postfix to prefix conversion

Both the prefix and postfix notation may seem just the opposite of each other but it is important to note that simply reversing the postfix notation does not convert it to the prefix notation. This is because certain operators like division and modulo operators also follow associativity rules, meaning that the relative order of operands affects the results. Moreover, nested expressions, where the evaluated result of a sub-expression is used as an operand for evaluating the remaining expression, rely on the correct order of operators and operands.

![[Pasted image 20251015105525.png]]

reversing the postfix expression in an attempt to generate the prefix expression. This will generate an incorrect prefix notation that does not evaluate the same as the original postfix notation. **==This is because, in the postfix notation, an operator must follow its operands, and simply reversing does not consider this pairing and associativity of the operator.==**

![[Pasted image 20251015105615.png]]

>To correctly convert a postfix notation to a prefix notation, we need to ensure that the operators are placed **before** the operands while maintaining the original evaluation order. It is important to note that since, for nested expression, evaluated results of subexpressions are treated as operands, we also need to keep track of subexpressions and decide when to use them as operands.

We can use a stack to group operands together and create a prefix expression when we see an operator. The LIFO order of stack ensures we group the current operator with the most recent previous operands, which may be subexpressions themselves.


![[Pasted image 20251015105810.png]]

To convert a postfix notation to a prefix notation, we create a stack `stack` to hold string values that we will use to build the prefix expression incrementally. We iterate in the string from start to end and in each iteration, check if the current character is an operator or operand. If it is an operand, we push it to the top of the stack. If not, we extract two operands from the top of the stack and construct a prefix expression by concatenating the operands and the current operator such that the operator is before the operands. We then push this expression to the top of the stack to be used as an operand in later iterations.

**==It is important to note that because the stack follows the LIFO order, the first pop operation on the stack gives us the second operand, while the second pop operation gives us the first operand.==**

### Algorithm

- **Step 1:** Create a stack `stack` to incrementally build the prefix expressions
- **Step 2:** Iterate in the string from start to end, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, push it to the top of the `stack`
    - **Step 2.2:** Otherwise, if it is an operator, do the following
        - **Step 2.2.1:** Pop `operand2` and `operand1` respectively from the top of the `stack` and use the operator to create a prefix expression
        - **Step 2.2.2:** Push the result to the `stack`
- **Step 3:** Return the top of the `stack` as the prefix string.

```java
import java.util.*;

class Solution {
    // Function to check if a character is an operator
    public boolean isOperator(char ch) {
        return (!Character.isLetter(ch) && !Character.isDigit(ch));
    }

    public String convertPostfixToPrefix(String postfix) {
        Stack<String> stack = new Stack<>();
        int length = postfix.length();

        for (int i = 0; i < length; i++) {
            // If the character is an operator, pop the top two
            // elements from the stack
            if (isOperator(postfix.charAt(i))) {
                // Pop the top element from the stack as the second
                // operand
                String operand2 = stack.pop();
                // Pop the top element from the stack as the first
                // operand
                String operand1 = stack.pop();
                // Construct the prefix expression by placing the
                // operator before the operands
                String expr = postfix.charAt(i) + operand1 + operand2;
                stack.push(expr);
            }
            // If the character is not an operator, push it to the
            // stack as a single-character string
            else {
                stack.push(String.valueOf(postfix.charAt(i)));
            }
        }
        // The final element in the stack will be the prefix expression
        return stack.pop();
    }
}
```

## Understanding postfix to infix conversion

 To convert a postfix expression into an infix, we need to traverse through the expression and place the operator between the operands for all operand pairs. As we will see shortly, this process creates small infix expressions from the initial operators and operands that then serve as operands themselves to form bigger infix expressions. At the end of the process, the entire postfix expression is converted into an infix expression.

To convert a postfix expression to an infix expression, we follow the same idea as its evaluation with only a slight difference. **==On finding an operator, instead of evaluating the results using the most recent operands, we create an infix expression from the operator and operands and save it on a stack as the operand in a subsequent iteration.==**

To evaluate a postfix notation, we create a stack `stack` to keep track of all the operands. We then traverse the string from start to end and, in each iteration, check if the current character is a digit or an operator. If the character is a digit, we push it to the top of the stack. If not, we pop two items from the top of the stack and use them as operands for the current operation to create an infix expression, also adding parentheses at both ends. We then store the expression at the top of the stack as an operand to be used in a subsequent iteration and continue the traversal.

This process is repeated in each iteration until the string traversal is complete. At the end of all iterations, the top of the stack has the infix expression.

>It is important to note that when traversing the string from left to right, the most recent item in the stack is the rightmost item seen so far. And so, the first item popped from the stack is the **second** operand, and the second item popped is the **first** operand. This is because the order of writing the operands is always left to right regardless of infix, prefix, or postfix notation.


### Algorithm

```java
import java.util.*;

class Solution {
    // Function to check if a character is an operator
    public boolean isOperator(char ch) {
        return (!Character.isLetter(ch) && !Character.isDigit(ch));
    }

    public String convertPostfixToInfix(String postfix) {
        Stack<String> stack = new Stack<>();
        int length = postfix.length();

        for (int i = 0; i < length; i++) {
            // If the character is an operator, pop the top two elements
            // from the stack and construct the infix expression by
            // placing the operands and operator within parentheses
            if (isOperator(postfix.charAt(i))) {
                // Pop the top element from the stack as the second
                // operand
                String operand2 = stack.pop();
                // Pop the top element from the stack as the first
                // operand
                String operand1 = stack.pop();
                // Construct the infix expression by placing the operands
                // and operator within parentheses
                String expr =
                    "(" + operand1 + postfix.charAt(i) + operand2 + ")";
                stack.push(expr);
            }
            // If the character is not an operator, push it to the
            // stack as a single-character string
            else {
                stack.push(String.valueOf(postfix.charAt(i)));
            }
        }
        // The final element in the stack will be the infix expression
        return stack.pop();
    }
}
```

## Understanding prefix to postfix conversion

reversing the prefix notation does not convert it to the postfix notation. This is because reversing the string does not respect the associativity of operators and their pairing with operands. Moreover, nested expressions, where the evaluated result of a sub-expression is used as an operand for evaluating the remaining expression, rely on the correct order of operators and operands.

![[Pasted image 20251015111439.png]]

consider reversing the prefix expression in an attempt to generate the postfix expression. This will generate an incorrect postfix notation that does not evaluate the same as the original prefix notation. This is because, in the prefix notation, an operator must precede its operands, and simply reversing does not consider this pairing and associativity of the operator.

![[Pasted image 20251015111456.png]]

> To correctly convert a prefix notation to a postfix notation, we need to ensure that the operators are placed **after** the operands while maintaining the original evaluation order. It is important to note that since, for nested expression, evaluated results of subexpressions are treated as operands, we also need to keep track of subexpressions and decide when to use them as operands.

We can use a stack to group operands together and create a postfix expression when we see an operator. The LIFO order of stack ensures we group the current operator with the most recent previous operands, which may be subexpressions themselves. Consider we are given a string `s` denoting the prefix notation of an expression and we need to convert it to postfix notation.

![[Pasted image 20251015111515.png]]

To convert a prefix notation to a prefix notation, we create a stack `stack` to hold string values that we will use to build the postfix expression incrementally. We iterate in the string in reverse, from end to start and in each iteration, check if the current character is an operator or operand. If it is an operand, we push it to the top of the stack. If not, we extract two operands from the top of the stack and construct a postfix expression by concatenating the operands and the current operator such that the operator is after the operands. We then push this expression to the top of the stack to be used as an operand in later iterations.

It is important to note that because the stack follows the LIFO order and because we iterate in reverse, the first pop operation on the stack gives us the first operand, while the second pop operation gives us the second operand.

### Algorithm

- **Step 1:** Create a stack `stack` to incrementally build the postfix expressions
- **Step 2:** Iterate in the string in reverse from end to start, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, push it to the top of the `stack`
    - **Step 2.2:** Otherwise, if it is an operator, do the following
        - **Step 2.2.1:** Pop `operand1` and `operand2` respectively from the top of the `stack` and use the operator to create a postfix expression
        - **Step 2.2.2:** Push the result to the `stack`
- **Step 3:** Return the top of the `stack` as the postfix string.

```java
import java.util.*;

class Solution {
    // Function to check if a character is an operator
    public boolean isOperator(char ch) {
        return !Character.isLetter(ch) && !Character.isDigit(ch);
    }

    public String convertPrefixToPostfix(String prefix) {
        Stack<String> stack = new Stack<>();
        int length = prefix.length();

        for (int i = length - 1; i >= 0; i--) {
            // If the character is an operator, pop the top two
            // elements from the stack
            if (isOperator(prefix.charAt(i))) {
                // Pop the top element from the stack as the first
                // operand
                String operand1 = stack.pop();
                // Pop the top element from the stack as the second
                // operand
                String operand2 = stack.pop();
                // Construct the postfix expression by placing the
                // operands followed by the operator
                String expr = operand1 + operand2 + prefix.charAt(i);
                stack.push(expr);
            }
            // If the character is not an operator, push it to the
            // stack as a single-character string
            else {
                stack.push(String.valueOf(prefix.charAt(i)));
            }
        }
        // The final element in the stack will be the postfix expression
        return stack.pop();
    }
}
```

## Understanding prefix to infix conversion

 To convert a prefix expression into an infix, we need to traverse through the expression and place the operator between the operands for all operand pairs

To convert a prefix expression to an infix expression, we follow the same idea as its evaluation with only a slight difference. On finding an operator, instead of evaluating the results using the most recent operands, we create an infix expression from the operator and operands and save it on a stack as the operand in a subsequent iteration.

To evaluate a prefix notation, we create a stack `stack` to keep track of all the operands. We then traverse the string in reverse from end to start and, in each iteration, check if the current character is a digit or an operator. If the character is a digit, we push it to the top of the stack. If not, we pop two items from the top of the stack and use them as operands for the current operation to create an infix expression, also adding parentheses at both ends. We then store the expression at the top of the stack as an operand to be used in a subsequent iteration and continue the traversal.

This process is repeated in each iteration until the string traversal is complete. At the end of all iterations, the top of the stack has the infix expression.

It is important to note that when traversing the string from right to left, the most recent item in the stack is the leftmost item seen so far. And so, the first item popped from the stack is the **first** operand, and the second item popped is the **second** operand. This is because the order of writing the operands is always left to right regardless of infix, prefix, or postfix notation.

### Algorithm

**Algorithm**

- **Step 1:** Create a stack `stack` to keep track of the most recent operands
- **Step 2:** Iterate in the sequence in reverse from end to start, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, push it to the `stack`
    - **Step 2.2:** Otherwise, if the current item is an operator, do the following:
        - **Step 2.2.1:** Pop two items(`operand1` and `operand2`) from the `stack` and use them as operands for the current operator
        - **Step 2.2.2:** Create an infix expression from the operator and operands and push the result to the top of the `stack`
- **Step 3:** Return the item at the top of the `stack`

```java
import java.util.*;

class Solution {
    // Function to check if a character is an operator
    public boolean isOperator(char ch) {
        return !Character.isLetter(ch) && !Character.isDigit(ch);
    }

    public String convertPrefixToInfix(String prefix) {
        Stack<String> stack = new Stack<>();
        int length = prefix.length();

        for (int i = length - 1; i >= 0; i--) {
            // If the character is an operator, pop the top two
            // elements from the stack and construct the infix expression
            // by placing the operator in between the operands
            if (isOperator(prefix.charAt(i))) {
                // Pop the top element from the stack as the first
                // operand
                String operand1 = stack.pop();
                // Pop the top element from the stack as the second
                // operand
                String operand2 = stack.pop();
                // Construct the infix expression by placing the operator
                // in between the operands
                String expr =
                    "(" + operand1 + prefix.charAt(i) + operand2 + ")";
                stack.push(expr);
            }
            // If the character is not an operator, push it to the
            // stack as a single-character string
            else {
                stack.push(String.valueOf(prefix.charAt(i)));
            }
        }
        // The final element in the stack will be the infix expression
        return stack.pop();
    }
}
```

## Understanding infix to postfix conversion

Any expression written in the postfix notation can be easily parsed and evaluated by a computer as opposed to the infix notation. However, for us humans, writing postfix expressions is very difficult and error-prone as we are not used to it. However, we can convert an expression written in the infix notation to postfix using the infix to postfix conversion algorithm.

We use a stack and operator precedence rules to convert an infix notation to postfix. We will learn more about the proof of correctness of this technique later in this lesson.

  
To convert the expression to postfix, we create a stack `stack` to hold all operators seen so far in the increasing order of precedence. We also create an empty string `postfix` to hold the postfix notation. We then iterate in the infix string from start to end and, in each iteration, check if the current character is an operator or an operand. If it is an operand, we append it to the `postfix` string. Otherwise, we check the precedence value of the current operator.

If it is greater than the precedence of the operator at the top of the `stack` we push it to the top of the stack. Otherwise, we repeatedly pop items from the stack and append them to the `postfix` string until the precedence of the operator at the top of the `stack` becomes less than the current operator or the stack becomes empty and finally push the current operator to the stack.

At the end of the traversal, we repeatedly pop all operators from the `stack` and append them to the `postfix` string until the stack becomes empty. The `postfix` string will then have the postfix notation of the given string.

The only change now is that we also check for opening or closing parentheses as we traverse the infix notation string. If we find an opening parenthesis, we push it to the `stack` and exclude it from subsequent comparison with other operators. However, when we find closing parenthesis, we repeatedly pop all operands from the `stack` and append them to the `postfix` string until we find the corresponding opening parenthesis and finally pop it from the `stack`. We then continue the traversal of the infix string and follow the same steps as before.

### Algorithm



- **Step 1:** Create a stack `stack` to keep track of operators in increasing order of precedence and a string `postfix` to hold the converted string
- **Step 2:** Iterate in the string from start to end, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, append it to the `postfix` string
    - **Step 2.2:** Otherwise, if it is an opening parenthesis, push it to the top of the `stack`
    - **Step 2.3:** Otherwise, if it is a closing parenthesis, do the following:
        - **Step 2.3.1:** Pop all operators from the `stack` until we find an opening parenthesis and append them to the `postfix` string.
        - **Step 2.3.2:** Pop the opening parenthesis from the `stack`
    - **Step 2.4:** Otherwise, if it is an operator, do the following:
        - **Step 2.4.1:** Pop operators from the `stack` and append them to the `postfix` string until the precedence of the operator and the top becomes less than the current operator or `stack` becomes empty.
        - **Step 2.4.2:** Push the current operator to the `stack`.
    - **Step 2.5:** Pop all operators from the `stack` and append them to the `postfix` string until `stack` becomes empty.
- **Step 3:** Return the `postfix` string

```java
import java.util.*;

class Solution {
    // Function to check if the character is an operator
    public boolean isOperator(char ch) {
        return (!Character.isLetter(ch) && !Character.isDigit(ch));
    }

    // Function to get the priority of operators
    public int getPrecedence(char operator) {
        // Assign precedence values to different operators
        if (operator == '^') {
            return 3;
        } else if (operator == '*' || operator == '/') {
            return 2;
        } else if (operator == '+' || operator == '-') {
            return 1;
        }
        // Default value for unknown operators
        return -1;
    }

    public String convertInfixToPostfix(String infix) {
        // Stack to hold operators and parentheses
        Stack<Character> stack = new Stack<>();
        // Final postfix expression
        StringBuilder postfix = new StringBuilder();

        for (char ch : infix.toCharArray()) {
            // If the character is not an operator or parentheses,
            // add it to the postfix string
            if (!isOperator(ch) && ch != '(' && ch != ')') {
                postfix.append(ch);
            }
            // If the character is an opening parentheses, push it
            // onto the stack
            else if (ch == '(') {
                stack.push(ch);
            }
            // If the character is a closing parentheses, pop
            // operators from the stack and add them to the postfix
            // string until an opening parentheses is encountered
            else if (ch == ')') {
                while (!stack.empty() && stack.peek() != '(') {
                    postfix.append(stack.peek());
                    stack.pop();
                }
                // Remove the opening parentheses from the stack
                if (!stack.empty() && stack.peek() == '(') {
                    stack.pop();
                }
            }
            // If the character is an operator, compare its
            // precedence with the top of the stack and add higher or
            // equal precedence operators to the postfix string
            else {
                while (
                    !stack.empty() &&
                    getPrecedence(ch) <= getPrecedence(stack.peek())
                ) {
                    if (stack.peek() != '(') {
                        postfix.append(stack.peek());
                    }
                    stack.pop();
                }
                // Push the current operator onto the stack
                stack.push(ch);
            }
        }
        // Pop any remaining operators from the stack and add them to the
        // postfix string
        while (!stack.empty()) {
            postfix.append(stack.peek());
            stack.pop();
        }

        return postfix.toString();
    }
}
```

## Understanding infix to prefix conversion

Any expression written in the prefix notation can be easily parsed and evaluated by a computer as opposed to the infix notation. However, for us humans, writing prefix expressions is very difficult and error-prone as we are not used to it. However, we can convert an expression written in the infix notation to a prefix using the infix-to-prefix conversion algorithm.

To convert the expression to prefix, we create a stack `stack` to hold all operators seen so far in the increasing order of precedence. We also create an empty string `prefix` to hold the prefix notation. We then iterate in the infix string in reverse, i.e., from end to start, and, in each iteration, check if the current character is an operator or an operand. If it is an operand, we append it to the `prefix` string. Otherwise, we check the precedence value of the current operator.

If it is greater than the precedence of the operator at the top of the `stack` we push it to the top of the stack. Otherwise, we repeatedly pop items from the stack and append them to the `prefix` string until the precedence of the operator at the top of the `stack` becomes less than the current operator or the stack becomes empty and finally push the current operator to the stack. At the end of the traversal, we repeatedly pop all operators from the `stack` and append them to the `prefix` string until the stack becomes empty.

At the end of all iterations the`prefix` string will have the prefix notation in **reverse**, and so will reverse it to get the correct prefix notation.

Note that ideally we should be **prepending** characters to the prefix string instead of **appending** them as we are moving from right to left in the infix string. However, since in most programming languages, appending to the end of a string is a constant time operation while preceding is not, we chose to append, which will create a prefix string in **reverse**.

The only change now is that we also check for opening or closing parentheses as we traverse the infix notation string. If we find a closing parenthesis, we push it to the `stack` and exclude it from subsequent comparison with other operators. However, when we find an opening parenthesis, we repeatedly pop all operands from the `stack` and append them to the `prefix` string until we find the corresponding closing parentheses and finally pop it from the `stack`. We then continue the traversal of the infix string and follow the same steps as before.

### Algorithm

- **Step 1:** Create a stack `stack` to keep track of operators in increasing order of precedence and a string `prefix` to hold the converted string
- **Step 2:** Iterate in the string from end to start, and in each iteration, do the following:
    - **Step 2.1:** If the current item is an operand, append it to the `prefix` string
    - **Step 2.2:** Otherwise, if it is a closing parenthesis, push it to the top of the `stack`
    - **Step 2.3:** Otherwise, if it is an opening parenthesis, do the following:
        - **Step 2.3.1:** Pop all operators from the `stack` until we find a closing parenthesis and append them to the `prefix` string.
        - **Step 2.3.2:** Pop the closing parenthesis from the `stack`
    - **Step 2.4:** Otherwise, if it is an operator, do the following:
        - **Step 2.4.1:** Pop operators from the `stack` and append them to the `prefix` string until the precedence of the operator and the top becomes less than the current operator or `stack` becomes empty.
        - **Step 2.4.2:** Push the current operator to the `stack`.
    - **Step 2.5:** Pop all operators from the `stack` and append them to the `prefix` string until `stack` becomes empty.
- **Step 3:** Reverse the `prefix` string
- **Step 4:** Return the `prefix` string

```java
import java.util.*;

class Solution {
    // Function to check if the character is an operator
    public boolean isOperator(char ch) {
        return (!Character.isLetter(ch) && !Character.isDigit(ch));
    }

    // Function to get the priority of operators
    public int getPrecedence(char operator) {
        // Assign precedence values to different operators
        if (operator == '^') {
            return 3;
        } else if (operator == '*' || operator == '/') {
            return 2;
        } else if (operator == '+' || operator == '-') {
            return 1;
        }
        // Default value for unknown operators
        return -1;
    }

    public String convertInfixToPrefix(String infix) {
        // Stack to hold operators and parentheses
        Stack<Character> stack = new Stack<>();
        // Final prefix expression
        StringBuilder prefix = new StringBuilder();
        String reversedInfix = new StringBuilder(infix)
            .reverse()
            .toString();
        // Reverse the infix string for easier processing

        for (char ch : reversedInfix.toCharArray()) {
            // If the character is not an operator or parentheses,
            // add it to the prefix string
            if (!isOperator(ch) && ch != ')' && ch != '(') {
                prefix.append(ch);
            }
            // If the character is a closing parentheses, push it
            // onto the stack
            else if (ch == ')') {
                stack.push(ch);
            }
            // If the character is an opening parentheses, pop
            // operators from the stack and add them to the prefix
            // string until a closing parentheses is encountered
            else if (ch == '(') {
                while (!stack.empty() && stack.peek() != ')') {
                    prefix.append(stack.peek());
                    stack.pop();
                }
                // Remove the closing parentheses from the stack
                if (!stack.empty() && stack.peek() == ')') {
                    stack.pop();
                }
            }
            // If the character is an operator, compare its
            // precedence with the top of the stack and add higher
            // precedence operators to the prefix string
            else {
                while (
                    !stack.empty() &&
                    getPrecedence(ch) < getPrecedence(stack.peek()) &&
                    stack.peek() != ')'
                ) {
                    prefix.append(stack.peek());
                    stack.pop();
                }
                // Push the current operator onto the stack
                stack.push(ch);
            }
        }
        // Pop any remaining operators from the stack and add them to the
        // prefix string
        while (!stack.empty()) {
            prefix.append(stack.peek());
            stack.pop();
        }
        // Reverse the prefix string to get the final result
        return prefix.reverse().toString();
    }
}
```

# Pattern: Reversal

can access data items anywhere in sequential data structures like arrays and linked lists either via random access or traversal. However, inserting and accessing data in a stack is only restricted to one end in the stack giving it its unique LIFO (Last in first out) property.

The reversal technique leverages the LIFO property of a stack to reverse any sequence of data by inserting all the items into the stack and then retrieving them one at a time from the top. This way, the resulting sequence from the retrieved items will be in reverse order. Almost all sequences that can be reversed using a stack can also be reversed using another technique.

![[Pasted image 20251016112312.png]]

The reversal technique is quite simple and easy to understand. Consider we are given an array of data items `arr` that we need to reverse.

We create a stack `stack` that will hold the data items in `arr`. We then iterate in the array `arr` from start to end and in each iteration, push the current item on top of the stack. At the end of all iterations, all items in the array `arr` will be copied to the stack, with the last item at the top. We then iterate in the array `arr` again from start to end, and in each iteration, pop the item from the top of the stack and overwrite the current item in `arr` with it. At the end of all iterations, the stack `stack` will be empty, and the array `arr` will be reversed.

**Algorithm**

- **Step 1:** Initialize a stack `stack` to store the data items of the array `arr`
- **Step 2:** Iterate in the array `arr` from start to end and push each item to the top of the stack `stack`.
- **Step 3:** Iterate in the array `arr` from start to end, pop the item from the top of the stack `stack` and overwrite the current item in`arr` with it.

```java
class Solution {

    public void reverseUsingStack(List<Integer> arr) {

    // Initialize a stack to hold array items

    Stack<Integer> stack = new Stack<>();

    // Traverse the list and push items onto the stack

    for (int item : arr) {
        stack.push(item);
    }

    // Traverse the list again and overwrite the items with the top of the stack
    for (int i = 0; i < arr.size(); i++) {
        arr.set(i, stack.pop());
    }
}
```

## Example Stack inversion

Given a stack **s**, write a function to return a new stack that contains all the elements of this stack but in reversed order.

```java
import java.util.*;

class Solution {

    public Stack<Integer> stackInversion(Stack<Integer> s) {

         Stack<Integer> reversedStack = new Stack<>();

        // Transfer elements from original stack to reversed stack

        while (!s.empty()) {

            // Get the top element from the original stack
            int top = s.peek();

  
            // Remove the top element from the original stack
            s.pop();

            // Push the element onto the reversed stack
            reversedStack.push(top);
        }

        // Return the reversed stack
        return reversedStack;
    }
}
```

## Example  Reverse the string

Given a string **s** containing alphanumeric characters, write a function to reverse this string using stack and return the reversed string.

```java
import java.util.*;

class Solution {

    public String reverseTheString(String s) {

        StringBuilder result = new StringBuilder();

        Stack<Character> stack = new Stack<>();

  
        for (char ch : s.toCharArray()) {
            stack.push(ch);
        }

  
        while (!stack.empty()) {
            result.append(stack.pop());
        }
        return result.toString();
    }
}
```

