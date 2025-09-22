
# Introduction the Memory Model
## Overview of program in memory

The compiled/interpreted source code is executed by **loading** it into the computer memory(RAM) as a **process**. A process has executable code that is executed by the CPU. Along with the executable code, the process also has a lot of other information the operating system needs to manage resources properly.

![[Pasted image 20250920152006.png]]

# Understanding memory partitions

```c
#include <iostream>
int y = 2;
int main() {

    int x = 6;

    int *arr = new int [5];

    return 0;

}
```

![[Pasted image 20250920152248.png]]

## Exploring stack memory

The stack memory is a section in the process that stores variables created inside **a function** (including the main function). **==It’s a LIFO, "Last In First Out" structure.==**

When a function declares a new variable, it is "pushed" onto the stack. When the function finishes execution and returns to the calling function, all the variables associated with that function on the stack are deleted, and the memory they use is freed up. This creates the concept of local scope for function variables. The stack memory in the process is automatically managed, so we don’t have to allocate or deallocate memory like in the heap

![[Pasted image 20250920152448.png]]

There is generally a limit on the stack size in a process, which can vary with the operating system (for example, OSX currently has a default stack size of 8MB). **==If a program tries to put too much data on the stack, it will crash with a stack overflow error.==** Stack overflow happens when all the memory in the stack has been allocated, and further allocations begin overflowing into other sections of the process's memory.

```c
#include <iostream>
int y = 2;
int main() {

    int x = 6;

    int *arr = new int [5];

    return 0;

}
```

![[Pasted image 20250920152551.png]]

##  Insights into heap memory

This is the piece of memory that is not automatically managed, which means we have to explicitly allocate (using functions such as `malloc/new`), and deallocate (using functions such as `free/delete`) it before and after its use. It is a large pool of memory that can be used dynamically and is also known as the **free store**.

Failure to free memory when finished using it results in a **memory leak**. This makes the OS think the memory is still "being used" and unavailable for other tasks. Unlike the stack, there are generally no restrictions on the heap size other than the machine's physical memory size. Data items created on the heap are accessible **anywhere** in the program.

```c++
#include <iostream>
void main() {
    // Stored in heap

    int *arr = new int [5];

    int *x = new int();

    *x = 6;

}
```

![[Pasted image 20250920152741.png]]

##  Static memory allocation

Static memory is the process section that **persists** throughout the program's life. On many systems, this variable uses 4 bytes of memory. There are generally two ways to store data in a process's static memory.


### Global variables

If a variable is declared outside of a function, it is considered global, meaning it is accessible anywhere in the program. Global variables are static, with only one copy for the entire program.

```c
#include <iostream>
int x = 2;

int main() {

}
```

## Static variables

Inside a function, the variable is allocated on the stack. It is also possible to force a variable to be static using the `static` keyword in languages like C++ and Java.

```c++
#include <iostream>
int main() {
    static int y = 6;
}
```

![[Pasted image 20250920153318.png]]

##  Delving into the code segment

The text segment, also known as a code segment or simply as text, is the process section containing the executable instructions. It is usually placed below the heap or stack to prevent heap and stack overflows from overwriting it.

Usually, the text segment is sharable, so only a single copy needs to be in memory for frequently executed programs, such as text editors, the C compiler, the shells, and many others. Also, **==the text segment is often read-only to prevent a program from accidentally modifying its instructions.==**


```c++
#include <iostream>
void main() {
    int x = 6;
    std::cout << "Hello World!" << std::endl;
}
```

![[Pasted image 20250920153742.png]]

##  Visualizing the complete picture

 ```cpp
 #include <iostream>
// Stored in static memory
int inStatic1 = 6;

int main() {
    // Stored in static memory
    static int inStatic2 = 7;

    // Stored in stack
    int inStack1 = 1;
    int inStack2 = 4;

    // Stored in heap
    int* inHeap = new int();
    *inHeap = 7;

    std::cout << "Example program";
    return 0;
}
 ```
 ![[Pasted image 20250920153849.png]]

# Nested Functions

 Computer programs do not contain just a single function but multiple functions. The functions call each other constantly, making the code modular and easy to understand. We know that the stack memory of a process is dedicated to storing information about a function.

##  Function call mechanics

Whenever a program has a function call, all the data associated with that function call, like the local variables, function parameters, return address, etc., gets stored in a **stack frame** structure.

```cpp
#include <iostream>
void functionC() {

    // Some code
}

void functionB() {

    functionC();
}

void functionA() {

    functionB();
}

void main() {

    functionA();
}
```

When the program executes, the stack memory is empty until the `main` function is called. When the `main` function is called, a new stack frame for it is created where all the local variables are stored. This stack frame is inserted at the **top** of the stack and will stay there until the `main` function exits. 

As we continue calling more functions in our program, a new stack frame is created for every function call, which is then pushed to the top of the stack. At any given time, the code being executed from the code segment is guaranteed to be from the function at the top of the stack. When a function exits or returns, the associated stack frame is deleted from the top stack of the stack memory.

##  Scope of local variables

Variables that are created inside a function are called local variables. These variables are also stored in the stack frame of the respective function call. Because these variables live in the function's stack frame, their scope is limited to their instance of the function call.

Function arguments and return value are also treated as local variables of the function

![[Pasted image 20250920161411.png]]

```cpp
#include <iostream>

void func2()
{
    int z = 7;
}
void func1()
{
    int y = 6;
    func2();
}
int main()
{
    int x = 5;
    func1();
}
```

## Recursive function calls

> When a function calls itself, it is said to be a recursive function.

![[Pasted image 20250920161636.png]]

### Local Variables

The process executing the code does not differentiate between nested and recursive function calls. This is because every function call is treated independently. When a function makes recursive calls to itself, a stack frame for each instance of the call is created with its own copy of all the local variables and pushed to the top of the stack.

This is why every instance of the function call is only aware of its local variables and is unaffected by the variables that have the same and are from the same function but on different stack frames. This is the magic that makes recursion so powerful. Let us look at a function `foo()` that calls itself.


![[Pasted image 20250920161720.png]]

**When does the recursive function call stop?**

**==Recursive function calls need a stopping condition known as a base condition; otherwise, they will continue infinitely.==** 

```cpp
#include <iostream>
void foo(int count) {
    // Base condition
    if(count == 0)
        return
    foo(count - 1);
}

void main() {
    foo(2);
}
```

## Understanding stack overflow

When the stack memory is exhausted, the program crashes with a runtime error called **stack overflow**. This can happen in one of three ways.

### Nested function calls

This case arises when too many nested function calls keep piling over as stack frames in the stack memory. Since the stack memory is limited in size, there will come a time when there is no more memory to allocate frames for the function calls, leading to a stack overflow error.

```cpp
#include <iostream>
void functionD() {
    // some logic
}

  

void functionC() {
    functionD();
}

  

void functionB() {
    functionC();
}

  

void functionA() {
    functionB();
}

  

int main() {
    functionA();
}
```

> **What is another common cause of stack overflow?**
   A common cause of stack overflow due to nested function calls is when the recursive function calls do not have the correct base condition, and the function recursively calls itself infinitely.

### Huge local variables

Stack overflow may also occur if the program tries to assign too much memory to a variable in a function, like an array of size 1 billion, or if the sum of sizes of all the local variables in that function becomes too huge. This would make the stack frame of the individual function too big to fit in the stack memory available for the process.

To avoid this, huge-size variables should always be allocated in the heap memory using memory allocation functions since the heap has virtually unlimited memory. However, the memory assigned on the heap must always be cleared after use, or it will cause a memory leak.

```cpp
#include <iostreram>
int main() {
    int arr[100000000];
}
```

### Other possible cases

A stack overflow may also occur due to a combination of too many nested function calls and the size of all local variables exceeding the stack memory available. **==This is generally the most common cause of stack overflow errors in well-written and tested computer programs==**.


```cpp
#include <iostream>

void functionC() {
    int arr[10000];
    // some code
}

void functionB() {
    int arr[40000];
    functionC();
}

void functionA() {
    int arr[10000];
    functionB();
}

int main() {
    functionA();
}
```

# Stack Frame

A stack frame is a basic structure that encapsulates all the information for a function call in any computer program. Information is stored in a process's stack memory in units of this structure.

Whenever a function call occurs within the process, a new stack frame is created for that function and pushed to the top of the process's stack memory. This stack frame contains all the information related to that function, including function arguments and local variables defined in that function. When the function finishes execution, this stack frame gets deleted from the stack memory.

```cpp
#include <iostream>

// Stored in static memory

int inStatic1 = 6;

void main() {

    // Stored in static memory

    static int inStatic2 = 7;
    // Stored in stack

    int inStack1 = 1;

    int inStack2 = 4;
    // Stored in heap

    int *inHeap = new int();

    *inHeap = 7

    std::cout << "Example program";
}
```

![[Pasted image 20250920164157.png]]

## Understanding the stack pointer

The stack pointer points to the top of the stack memory, i.e., the first offset of the topmost stack frame in the stack memory. Its value can change from time to time, for example, when either a new function is called, or the current function call ends, leading to a new stack frame being created and pushed to the top of the stack or the topmost stack frame being removed, respectively.

```cpp
#include <iostream>
int functionA (int a, int b) {

    int x = 1;

    int y = 2;

    int sum = x + y;

    return sum;

}

int main() {

    std::cout << functionA(3, 4);
    return 0;
}
```

![[Pasted image 20250920164255.png]]

## Understanding the frame pointer

Every stack frame has a data member called the frame pointer, which stores the address of the first offset of its respective stack frame. This is the address where the stack frame for a function begins in the stack memory. The program uses this stack frame pointer behind the scenes to access all the data stored in the respective stack frame

```cpp
#include <iostream>
int functionA (int a, int b) {

    int x = 1;

    int y = 2;

    int sum = x + y;

    return sum;

}

int main() {

    std::cout << functionA(3, 4);

    return 0;

}
```

The frame pointer for `functionA()` will point to the first offset in its own stack frame.

![[Pasted image 20250920164508.png]]

## Storage of local variables

The variables created inside the function, known as local variables, are stored in the stack frame.

```cpp
#include <iostream>
void functionA (int a, int b) {
    int x = 1;
    int y = 2;
}

int main() {
    functionA(3, 4);
    return 0;
}
```

![[Pasted image 20250920164605.png]]

## Storage of function parameters

Whenever a function that takes some arguments is called, the arguments get copied over and stored in a section of the stack frame.

```cpp
#include <iostream>
void functionA (int a, int b) {
    int x = 1;
    int y = 2;
}

int main() {
    functionA(3, 4);
    return 0;
}
```

![[Pasted image 20250920164829.png]]

## Handling the return value

Like the function arguments and local variables, the value that a function returns to the caller, also known as the return value, is stored in the stack frame. The caller generally receives a copy of this value and assigns it to another local variable to its own stack frame.

```cpp
#include <iostream>
int functionA (int a, int b) {

    int x = 1;

    int y = 2;

    int sum = x + y;

    return sum;

}

int main() {
    std::cout << functionA(3, 4);
    return 0;
}
```

![[Pasted image 20250920164929.png]]

## Managing the return address

Whenever a function is called, the address in memory from where it was called in the calling function is also copied over to its stack frame. When the called function finishes its execution, it uses the return address stored in its stack frame to resume the execution from where it was called in the calling function. This is how function calls are linked together, and the program can execute in a linear flow even when the code is split across functions.

```cpp
#include <iostream>

int functionA (int a, int b) {

    int x = 1;

    int y = 2;

    int sum = x + y;

    return sum;

}

int main() {
    std::cout << functionA(3, 4);
    return 0;
}
```

This part of the stack frame stores the address of the calling function, i.e., the function that should be returned execution handle once this function exits and the stack frame for it is deleted from the memory.

![[Pasted image 20250920165028.png]]

# Recursion

Recursion is fundamental to many optimization problems and high-level concepts like memorization and dynamic programming. Understanding recursion is the first step to understanding dynamic programming and divide-and-conquer algorithms.

![[Pasted image 20250920202033.png]]

Simply put, recursion can be defined as solving a problem by solving a smaller version of the same problem or defining a problem in terms of itself. It is not always obvious if a problem can be solved using recursion at first sight. Let's take a real-world example to understand recursion better.

##  Key components of recursion

### Recursive structure

A problem is said to have a recursive structure if it can be broken down into smaller subproblems, solutions to which can be used to solve the bigger problem. These subproblems should be the same as the original problem but on a smaller subset of inputs

### Base case

For a given problem, the base case is the smallest instance of the problem whose answer is already known. The base case is also called the terminating condition or the endpoint of recursion

### Recursive relation

Recursion is just the execution of a recursive relation. A recursive relation is the mathematical representation of recursion.

Recursive Relation

> A recursive relation is a relation that can be represented in its own terms and has a base case whose value is already known. It is also known as a recursive equation or recursive formula.

![[Pasted image 20250920203057.png]]

Here `F(n)`  is the solution to a problem with input `n` and `G` is a function that is used to calculate the solution using the result of `F(n-1)`.

![[Pasted image 20250920203122.png]]

>**Why is it called a tree when it is just a straight line?**  
  The atm queue example we used has a simple recursive relation. Hence, the recursion tree has no branches. Other more complex recursive relations branch out more and look like trees, as we will learn later in this course.

## Implementing recursive algorithms

 a recursive function calls itself instead of calling some other function. Now that we know about stack frames and stack memory, it is easy to visualize how these recursive function calls work under the hood.

```java
public class Main {

    static int findPosition(int n) {
        // Base case
        if (n == 1) {
            return 1;
        }

        return 1 + findPosition(n - 1);
    }

    public static void main(String[] args) {
        System.out.println(findPosition(4));
    }
}

```

1. Function Calls
2. Base Case
3. Stack Unwinding

### 1. Function calls

The recursive solution starts with the first function call, also called the **top level** function call, which is made to get the results for an input. This function call creates a stack frame in the process's stack memory and, during its execution, calls the same function again with different inputs.

Though these two functions are exactly the same, for the process executing it, every function call is different and it creates a new stack frame for this second call to the same function.

These two functions have their own **copy** of all the local variables. During its execution, this second function call calls the same function again with a different input, and just like before, a new stack frame is created for this call. This process continues until the function is called for the base case.

### 2. Base case

The process of repeatedly calling the same function and creating new stack frames for each call in the stack memory finally stops when the recursive function is called with the base case. We already know the answer to the base case, so there are no more subsequent function calls, and some value is returned from the function. As this final function call returns the value to the caller, the stack frame associated with it is also deleted from the process's stack memory.

![[Pasted image 20250920203806.png]]

It is quite easy to see that if there was no base case, the recursive function calls would go on and on forever and would cause the program to crash due to stack overflow

### 3. Stack unwinding

The return of execution from the base cases starts **stack unwinding**. The stack frame associated with the function call that called the base case can now compute the result for itself and return it to the function that, in turn, called it. Once it returns the results, the stack frame associated with this instance of the function call will also be deleted. This process will go on and on until the execution reaches the **top level** function call, where we get back the result to our **original** input.

# Direct Recursion

In direct recursion, a function solves a problem by calling itself with a modified parameter until a base condition is met. The base condition ensures the recursion terminates. The primary components of a recursive function are:

> - **Base Case:** A condition that stops the recursion to prevent infinite loops.
> - **Recursive Case:** The part of the function where the function calls itself with a different argument.

Calculating a number's factorial is the most commonly known direct recursive relation. `N` is the product of all numbers starting from `1` to `N`. For, e.g., the factorial of `3` is `(1*2*3) = 6`.

```java
class Solution {

    public int recursivelyCalculateFactorial(int N) {
        // Base case: If N is 0, the factorial is 1
        if (N == 0) {
            return 1;
        }

        // Multiply N with the factorial of (N - 1) by making a recursive call
        return N * recursivelyCalculateFactorial(N - 1);
    }

}
```

## Example  Recursively calculate factorial

Given a positive integer **N**, write a recursive function to return the factorial of N.

```java
class Solution {

    public int solution(int N) {
        if(N <= 1)
            return 1;
            return N * solution(N - 1);
    }
}
```


# Head Recursion

Head recursion is a specific type of recursion where a function makes its recursive call as the first operation. This means **==the recursive call is made before any other processing happens in the function, and once the base case is reached, the function processes the data to back up the call stack==**. The primary components of a head recursive function are:

> - **Base Case:** A condition that stops the recursion to prevent infinite loops.
> - **Recursive Case:** The part of the function where the function calls itself first, then processes the data after returning from the recursive call.

## Example 

The recursive relation to print numbers is simple. No computation is involved. We print the given value at every step.

Nothing is done during the successive recursive function calls because the recursive function call is at the beginning. The work is done **after** the smaller problems return the result during the **stack unwinding** phase of recursion

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    private void helper(int N, List<Integer> result) {
        // Base case: If N is less than or equal to 0, stop recursion
        if (N <= 0) {
            return;
        }

        // Recursive call with N-1
        helper(N - 1, result);

        // Add current number after recursive call
        result.add(N);
    }

    public List<Integer> recursivelyPrintNumbersFrom1ToN(int N) {
        List<Integer> result = new ArrayList<>();
        helper(N, result);
        return result;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        List<Integer> numbers = solution.recursivelyPrintNumbersFrom1ToN(5);
        System.out.println(numbers); // Output: [1, 2, 3, 4, 5]
    }
}

```

## Example Recursively reverse a stack

Given a stack **s**, reverse the contents of this stack **using recursion**. You do not need to return a new reversed stack but reverse the contents of the input stack itself.

```java
class Solution {
    // Function to insert an element at the bottom of the stack

    public void insertAtBottom(Stack<Integer> stack, int elem) {

        // Base case: If stack is empty, push the element

        if (stack.isEmpty()) {
            stack.push(elem);
        } else {
            // Save the top element of the stack
            int top = stack.pop();
            // Recursively insert the element at the bottom
            insertAtBottom(stack, elem);
            // Push the saved top element back to the stack
            stack.push(top);
        }
    }

    public void recursivelyReverseAStack(Stack<Integer> s) {

        // Base case: If stack has one or less elements

        if (s.size() <= 1) {
            return;
        }

        // Save the top element of the stack
        int top = s.peek();
        
        // Pop the top element
        s.pop();

        // Recursively reverse the remaining stack
        recursivelyReverseAStack(s);

        // Insert the saved top element at the bottom
        insertAtBottom(s, top);
    }
}
```

# Tail Recursion

**==In tail recursion, a function performs its recursive call as the final action before returning a result. This allows the current function frame to replace the next one.==** This is significant because many compilers and interpreters can optimize tail-recursive functions to prevent excessive use of the call stack, thus improving performance and avoiding stack overflow errors. The key components of a tail-recursive function are:

> - **Base Case:** A condition that stops the recursion to prevent infinite loops.
> - **Recursive Case:** The part of the function where the function calls itself as the last operation, often passing along an accumulator or additional parameters to maintain state.

Consider printing all the numbers from 1 to N in reverse order. This problem is similar to printing numbers from `1` to `N` and is an excellent example of the difference between head and tail recursion. 

> Given a number `N`, recursively print all the numbers from `1` to `N` in **reverse** order.

The recursive relation to print numbers in reverse is very similar to printing them from 1 to N. We need to print the given number **before** printing the smaller number. This means we need to solve the problem for the given problem **before** solving it for the smaller problem.

**==Unlike head recursion, because the recursive function call is at the end, the actual work is done during the first phase (recursive calls) of recursion, and nothing is done after the smaller problems return the result during the stack unwinding phase.==**

```java
import java.util.*;

class Solution {
    public void helper(int N, List<Integer> result) {
        // Base case: If N is less than or equal to 0, we have reached
        // the end of recursion
        if (N <= 0) {
            // Exit the function, as there are no more numbers to add
            return;
        }

        // First, add the current number N to the result list
        result.add(N);

        // Recursive call to the helper method with N-1, to move towards
        // the base case
        helper(N - 1, result);
    }

    public List<Integer> recursivelyPrintNumbersFromNTo1(int N) {
        // Initialize an empty list to store the result
        List<Integer> result = new ArrayList<>();

        // Call the helper method to populate the result list with
        // numbers from N to 1
        helper(N, result);

        // Return the generated list containing numbers from N to 1
        return result;
    }
}
```

## Example  Recursively reverse a queue

Given a queue **q**, reverse the contents of this stack **using recursion**. You do not need to return a new reversed queue but reverse the contents of the input queue itself.

```java
class Solution {

    public void recursivelyReverseAQueue(Queue<Integer> q) {

        // Base case: Queue is empty or has only one element

        if (q.isEmpty() || q.size() == 1) {
            return;
        }

        // Dequeue the front element
        int frontElement = q.poll();

        // Reverse the remaining queue
        recursivelyReverseAQueue(q);

        // Enqueue the front element to the rear
        q.add(frontElement);
    }
}
```