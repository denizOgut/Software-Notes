# DATA STRUCTURES & ALGORITHMS

A sequence of steps leading to the solution of a problem is referred to as an ***algorithm***. However, for some problems, finding an exact solution can be time-consuming. In such cases, settling for a good solution in a short amount of time may be sufficient. The set of steps that do not guarantee an exact solution but offer a promising approach is known as ***heuristic methods*** or simply ***heuristics.***

Algorithm comparison involves two crucial criteria: 
- **speed**  
- **resource usage.** 

However, the predominant criterion is speed. Therefore, when comparing algorithms, it is commonly understood that the default basis for comparison is speed.   The process of examining and comparing algorithms is referred to as ***algorithm analysis***

```java
int[] a = new int[N];
{...}; 

int max, i;
max = a[0];

for (i = 1; i < N; +i) {
    if (max < a[i]) {
        max = a[i];
    }
}
```

In algorithm analysis, the number of operations can be calculated considering three scenarios:

1. **Average case condition**
2. **Worst case condition**
3. **Best case condition**

To compare algorithms in practical terms, asymptotic notations are utilized. Among these, the most commonly used is the ***Big O*** notation.

The Big O notation categorizes algorithms based on their complexities. Algorithms with the same characters in their Big O notation are treated as if there is no difference between them. If an algorithm falls into multiple categories, the worst-case category specifies its actual classification. From best to worst, the Big O categories are as follows:

**O(1):** This category is referred to as "constant complexity." If there are no loops in the algorithm and everything is done with singular operations, the complexity of the algorithm is O(1). Examples include finding the area of a triangle or accessing an element in an array.

**O(log₂N):** This complexity involves a set of input of length N (e.g., an array). The algorithm has a loop, either explicitly or recursively, but this loop iterates not N times, but log₂N times. For example, the "binary search" algorithm has O(log₂N) complexity.

**O(N):** This category is known as "linear complexity." Algorithms in this class may have non-nested loops. If the input length is N, these loops iterate in connection with N (typically N times or N/2 times, etc.), but not logarithmically. Examples include finding the largest number, linear search, adding an element to an array, and finding the sum of array elements.

**O(N * log₂N):** Algorithms in this category have nested loops, with one loop iterating proportionally to N while the other iterates log₂N times. For example, the "quick sort" algorithm has O(N * log N) complexity.

**O(N²):** This is referred to as "quadratic complexity." Algorithms in this category have nested loops, both iterating proportionally to N. Examples include "bubble sort" and "selection sort" algorithms.

**O(N³):** This is called "cubic complexity." Here, there are nested loops proportionally to N, three in total. For example, matrix multiplication requires such a loop structure.

All the categories mentioned above are collectively referred to as ***polynomial complexity***

**O(K^N)** (where K is constant) is also referred to as "exponential complexity." In algorithms within this category, the number of operations grows very rapidly in relation to N. Even with modern computers, algorithms with exponential complexity may take an impractical amount of time for exact solutions. Consequently, computer-based solutions for such algorithms might be unfeasible. Heuristic methods become crucial in these types of algorithms. For instance, the number of subsets of a set with N elements is 2^N. Algorithms that examine all subsets of a set (there are many such algorithms) exhibit exponential complexity.

**O(N!)** is referred to as factorial complexity. This represents the worst-case complexity group. For example, in the traveling salesman problem, the salesman departs from a central node, traverses all cities (nodes), and returns to the starting point. The objective is to find the solution that yields the shortest tour. If there are N nodes in this problem, one needs to calculate (N-1)! / 2 routes. Therefore, the traveling salesman problem is an algorithm with factorial complexity. Job sequencing and scheduling problems also typically fall into this complexity category.

Problems with exponential and factorial complexities are referred to as ***non-polynomial (NP)*** complexity problems. These types of problems are still actively researched, and specialized methods are continuously sought after.

Algorithms can be classified based on various criteria. Typical classification criteria include:

* ***Classification Based on Implementation Forms***: In this classification, algorithms are categorized based on how their codes are written. Typical subcategories include:

	- Recursive Algorithms
	- Logical Algorithms
	- Serial Algorithms
	- Parallel or Distributed Algorithms
	- Deterministic or Non-Deterministic (Probabilistic, Stochastic) Algorithms
	- Algorithms Targeted for Quantum Computers

- ***Classification Based on Design Form***: This classification categorizes algorithms based on their general design. Typical subcategories include:

	- Divide and Conquer Algorithms
	- Algorithms Applying Random Processes
	- Algorithms Seeking Solutions by Reducing Complexity
	- Backtracking Algorithms with Continuous Improvement Structures

- ***Classification Based on Complexity***: In this classification, the algorithm is categorized based on its complexity, which has already been discussed above. Typical subcategories include:

	- Algorithms with O(1) Complexity
	- Algorithms with O(log N) Complexity
	- Algorithms with O(N) Complexity
	- Algorithms with O(N log N) Complexity
	- Algorithms with O(N²) Complexity
	- Algorithms with O(N³) Complexity
	- Algorithms with O(N^k) Complexity
	- Exponential Complexity Algorithms (O(a^N))
	- Factorial Complexity Algorithms (O(N!))


Donald Knuth has classified algorithms in "The Art of Computer Programming" book series as follows:

- **Fundamental Algorithms:** These are basic algorithms encountered in everyday programming.
    
- **Semi-numerical Algorithms:** Algorithms with a numerical aspect that can be encountered in the programming world.
    
- **Sorting and Searching Algorithms:** Algorithms related to searching and sorting operations.
    
- **Graph Algorithms:** Algorithms involving traversal and optimization on graphs.
    
- **Optimization Algorithms:** Algorithms attempting to find the mathematical best values.
    
- **Numerical Algorithms:** Algorithms that focus on numerical operations such as finding roots, solving equations, derivatives, integrals, etc.

## ALGORITHMS

### Recursion
---
**What is Recursion?**   
The process in which a function calls itself directly or indirectly is called recursion and the corresponding function is called a recursive function. A recursive function solves a particular problem by calling a copy of itself and solving smaller subproblems of the original problems. Many more recursive calls can be generated as and when required. It is essential to know that we should provide a certain case in order to terminate this recursion process.

**Properties of Recursion:**

- Performing the same operations multiple times with different inputs.
- In every step, we try smaller inputs to make the problem smaller.
- Base condition is needed to stop the recursion otherwise infinite loop will occur.

#### Algorithm: Steps

The algorithmic steps for implementing recursion in a function are as follows:

```text
Step1 - Define a base case: Identify the simplest case for which the solution is known or trivial. This is the stopping condition for the recursion, as it prevents the function from infinitely calling itself.

Step2 - Define a recursive case: Define the problem in terms of smaller subproblems. Break the problem down into smaller versions of itself, and call the function recursively to solve each subproblem.

Step3 - Ensure the recursion terminates: Make sure that the recursive function eventually reaches the base case, and does not enter an infinite loop.

step4 - Combine the solutions: Combine the solutions of the subproblems to solve the original problem.
```

**How are recursive functions stored in memory?**

Recursion uses more memory, because the recursive function adds to the stack with each recursive call, and keeps the values there until the call is finished. The recursive function uses LIFO (LAST IN FIRST OUT) Structure just like the stack data structure.

**What is the base condition in recursion?**   
In the recursive program, the solution to the base case is provided and the solution to the bigger problem is expressed in terms of smaller problems.

```java
int fact(int n)
{
    if (n < = 1) // base case
        return 1;
    else    
        return n*fact(n-1);    
}
```


**How a particular problem is solved using recursion?**   
The idea is to represent a problem in terms of one or more smaller problems, and add one or more base conditions that stop the recursion. For example, we compute factorial n if we know the factorial of (n-1). The base case for factorial would be n = 0. We return 1 when n = 0. 

**Why Stack Overflow error occurs in recursion?**   
If the base case is not reached or not defined, then the stack overflow problem may arise.

```java
int fact(int n)
{
    // wrong base case (it may cause
    // stack overflow).
    if (n == 100) 
        return 1;

    else
        return n*fact(n-1);
}
```

If the memory is exhausted by these functions on the stack, it will cause a stack overflow error. 

**What is the difference between direct and indirect recursion?**   
A function fun is called direct recursive if it calls the same function fun. A function fun is called indirect recursive if it calls another function say ``fun_new`` and ``fun_new`` calls fun directly or indirectly.

```java
**// An example of direct recursion**
void directRecFun()
{
    // Some code....

    directRecFun();

    // Some code...
}

**// An example of indirect recursion**
void indirectRecFun1()
{
    // Some code...

    indirectRecFun2();

    // Some code...
}
void indirectRecFun2()
{
    // Some code...

    indirectRecFun1();

    // Some code...
}
```

**How memory is allocated to different function calls in recursion?**   
When any function is called from main(), the memory is allocated to it on the stack. A recursive function calls itself, the memory for a called function is allocated on top of memory allocated to the calling function and a different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues.

```java
// A Java program to demonstrate working of
// recursion
class GFG {
	static void printFun(int test)
	{
		if (test < 1)
			return;
		else {
			System.out.printf("%d ", test);
			printFun(test - 1); // statement 2
			System.out.printf("%d ", test);
			return;
		}
	}

	// Driver Code
	public static void main(String[] args)
	{
		int test = 3;
		printFun(test);
	}
}

// This code is contributed by
// Smitha Dinesh Semwal

```


**Output**

```text
3 2 1 1 2 3 
```

**Time Complexity:** O(1)  
**Auxiliary Space:** O(1)

![[Pasted image 20240201111953.png]]

**Recursion VS Iteration**

| **SR No.** | **Recursion** | **Iteration** |
| ---- | ---- | ---- |
| 1) | Terminates when the base case becomes true. | Terminates when the condition becomes false. |
| 2) | Used with functions. | Used with loops. |
| 3) | Every recursive call needs extra space in the stack memory. | Every iteration does not require any extra space. |
| 4) | Smaller code size. | Larger code size. |

### Example:  Real Applications of Recursion in real problems

Recursion is a powerful technique that has many applications in computer science and programming. Here are some of the common applications of recursion:

- **Tree and graph traversal**: Recursion is frequently used for traversing and searching data structures such as trees and graphs. Recursive algorithms can be used to explore all the nodes or vertices of a tree or graph in a systematic way.
- **Sorting algorithms**: Recursive algorithms are also used in sorting algorithms such as quicksort and merge sort. These algorithms use recursion to divide the data into smaller subarrays or sublists, sort them, and then merge them back together.
- **Divide-and-conquer algorithms**: Many algorithms that use a divide-and-conquer approach, such as the binary search algorithm, use recursion to break down the problem into smaller subproblems.
- **Fractal generation**: Fractal shapes and patterns can be generated using recursive algorithms. For example, the Mandelbrot set is generated by repeatedly applying a recursive formula to complex numbers.
- **Backtracking algorithms**: Backtracking algorithms are used to solve problems that involve making a sequence of decisions, where each decision depends on the previous ones. These algorithms can be implemented using recursion to explore all possible paths and backtrack when a solution is not found.
- **Memorization**: Memorization is a technique that involves storing the results of expensive function calls and returning the cached result when the same inputs occur again. Memorization can be implemented using recursive functions to compute and cache the results of subproblems.


```java
import java.io.File;

public class FileLister {

    public static void listFilesRecursive(File directory) {
        // Get all files and subdirectories in the current directory
        File[] files = directory.listFiles();

        if (files != null) {
            // Iterate through the files and directories
            for (File file : files) {
                // If it's a directory, call the function recursively
                if (file.isDirectory()) {
                    System.out.println("Directory: " + file.getName());
                    listFilesRecursive(file);
                } else {
                    // If it's a file, print its name
                    System.out.println("File: " + file.getName());
                }
            }
        }
    }

    public static void main(String[] args) {
        // Replace "your_directory_path" with the path to the directory you want to start from
        File startingDirectory = new File("your_directory_path");

        if (startingDirectory.exists() && startingDirectory.isDirectory()) {
            System.out.println("Listing files and directories in: " + startingDirectory.getAbsolutePath());
            listFilesRecursive(startingDirectory);
        } else {
            System.out.println("Invalid directory path.");
        }
    }
}

```


**Summary of Recursion:**

- There are two types of cases in recursion i.e. recursive case and a base case.
- The base case is used to terminate the recursive function when the case turns out to be true.
- Each recursive call makes a new copy of that method in the stack memory.
- Infinite recursion may lead to running out of stack memory.
- Examples of Recursive algorithms: Merge Sort, Quick Sort, Tower of Hanoi, Fibonacci Series, Factorial Problem, etc.

### Searching Algorithms
---
#### Linear Search

##### What Is Linear Search ?

**Linear Search** is defined as a sequential  that starts at one end and goes through each element of a list until the desired element is found, otherwise the search continues till the end of the data set.

##### How Does Linear Search Algorithm Work?

In Linear Search Algorithm, 

- Every element is considered as a potential match for the key and checked for the same.
- If any element is found equal to the key, the search is successful and the index of that element is returned.
- If no element is found equal to the key, the search returns -1.

```java
public static  int linearSearchIndexOf(int [] a, int val)
{
	for (var i = 0; i < a.length; ++i)
		if (a[i] == val)
			return i;

	return -1;
}
```

##### Complexity Analysis:

**Time Complexity:**

- **Best Case:** In the best case, the key might be present at the first index. So the best case complexity is O(1)
- **Worst Case:** In the worst case, the key might be present at the last index i.e., opposite to the end from which the search has started in the list. So the worst-case complexity is O(N) where N is the size of the list.
- **Average Case:** O(N)

**Auxiliary Space:** O(1) as except for the variable to iterate through the list, no other variable is used.

##### **Advantages of Linear Search:**

- Linear search can be used irrespective of whether the array is sorted or not. It can be used on arrays of any data type.
- Does not require any additional memory.
- It is a well-suited algorithm for small datasets.

##### **Drawbacks of Linear Search:**

- Linear search has a time complexity of O(N), which in turn makes it slow for large datasets.
- Not suitable for large arrays.

##### **When to use Linear Search?**

- When we are dealing with a small dataset.
- When you are searching for a dataset stored in contiguous memory.

--- 
#### Binary Search
##### What Is Binary Search?

***Binary Search*** is defined as a searching algorithm used in a sorted array by ***repeatedly dividing the search interval in half****. The idea of binary search is to use the information that the array is sorted and reduce the time complexity to O(log N).

##### Conditions for when to apply Binary Search in a Data Structure:

To apply Binary Search algorithm:

- The data structure must be sorted.
- Access to any element of the data structure takes constant time.

#####  How Does Binary Search Algorithm Works:

- Divide the search space into two halves by ***finding the middle index "mid"***
- Compare the middle element of the search space with the key. 
- If the key is found at middle element, the process is terminated.
- If the key is not found at middle element, choose which half will be used as the next search space.
    - If the key is smaller than the middle element, then the left side is used for next search.
    - If the key is larger than the middle element, then the right side is used for next search.
- This process is continued until the key is found or the total search space is exhausted.

![[Pasted image 20240128000016.png]]

##### How to Implement Binary Search?

The ***Binary Search Algorithm*** can be implemented in the following two ways

- Iterative Binary Search Algorithm
- Recursive Binary Search Algorithm

  ***Iterative  Binary Search Algorithm:***

```java
public static  int binarySearchIndexOf(int [] a, int val)
{
	int left = 0;
	int right = a.length - 1;
	int mid;

	while (left <= right) {
		mid = (left + right) / 2;
		if (a[mid] == val)
			return mid;

		if (a[mid] < val)
			left = mid + 1;
		else if (val < a[mid])
			right = mid - 1;
	}

	return -1;
}
```

***Time Complexity:* O(log N)**  
***Auxiliary Space:* O(1)***

 ***Recursive  Binary Search Algorithm:***

```java
public class RecursiveBinarySearch 
{

    public static int binarySearch(int[] array, int target, int low, int high) {
        if (low > high) {
            return -1; // Base case: target not found
        }

        int mid = low + (high - low) / 2;

        if (array[mid] == target) {
            return mid; // Target found
        } else if (array[mid] < target) {
            return binarySearch(array, target, mid + 1, high); // Search in the right half
        } else {
            return binarySearch(array, target, low, mid - 1); // Search in the left half
        }
    }
}

```

##### Complexity Analysis of Binary Search:

- ***Time Complexity:***
    - Best Case: O(1)
    - Average Case: O(log N)
    - Worst Case: O(log N)
- ***Auxiliary Space:*** O(1), If the recursive call stack is considered then the auxiliary space will be O(logN).

##### Advantages of Binary Search:

- Binary search is faster than linear search, especially for large arrays.
- More efficient than other searching algorithms with a similar time complexity, such as interpolation search or exponential search.
- Binary search is well-suited for searching large datasets that are stored in external memory, such as on a hard drive or in the cloud.

##### Drawbacks of Binary Search:

- The array should be sorted.
- Binary search requires that the data structure being searched be stored in contiguous memory locations. 
- Binary search requires that the elements of the array be comparable, meaning that they must be able to be ordered.

##### Applications of Binary Search:

- Binary search can be used as a building block for more complex algorithms used in machine learning, such as algorithms for training neural networks or finding the optimal hyperparameters for a model.
- It can be used for searching in computer graphics such as algorithms for ray tracing or texture mapping.
- It can be used for searching a database.

---

## DATA STRUCTURES

###  Stack
---
####  **What is Stack?**

> A stack is a linear data structure in which the insertion of a new element and removal of an existing element takes place at the same end represented as the top of the stack.

To implement the stack, it is required to maintain the **pointer to the top of the stack**, which is the last element to be inserted because **we can access the elements only on the top of the stack.**

**LIFO( Last In First Out ):**

> This strategy states that the element that is inserted last will come out first.

1. **Browser History:**
    
    - Imagine your web browser's back button functionality. The last page you visited is the first one to be popped off when you press "back."
2. **Stack of Plates:**
    
    - When you stack plates, you typically take the top one when you need to use or wash one. The last plate you put on the stack is the first one to be used.
3. **Undo Feature in Software:**
    
    - Many software applications use a Last In, First Out (LIFO) approach for their undo feature. The last action you performed is the first one you can undo.
4. **Call Stack in Programming:(Recursion)**
    
    - In programming, the call stack is often implemented using LIFO. The last function called is the first one to finish and return control.

#### Basic Operations on Stack

In order to make manipulations in a stack, there are certain operations provided to us.

- **push()** to insert an element into the stack
- **pop()** to remove an element from the stack
- **top()** Returns the top element of the stack.
- **isEmpty()** returns true if stack is empty else false.
- **size()** returns the size of stack.

#### **Understanding stack practically:**

> In web browsers, when you visit a website, the browser stores frequently accessed resources (such as images, stylesheets, or scripts) in a cache. The most recently accessed resources are stored at the top of the cache. When you request a resource, the browser checks the cache first. If the resource is found at the top, it's quickly retrieved (hit), and if not, the cache is updated with the new resource (miss).
>This cache system operates in a Last In, First Out (LIFO) manner. The most recently accessed or added resources are the ones most likely to be reused, reflecting a common principle in caching systems.


#### **Complexity Analysis:**

- **Time Complexity**

|**Operations**|**Complexity**|
|---|---|
|push()|O(1)|
|pop()|O(1)|
|isEmpty()|O(1)|
|size()|O(1)|

#### **Types of Stacks:**

- **Fixed Size Stack**: As the name suggests, a fixed size stack has a fixed size and cannot grow or shrink dynamically. If the stack is full and an attempt is made to add an element to it, an overflow error occurs. If the stack is empty and an attempt is made to remove an element from it, an underflow error occurs.

- **Dynamic Size Stack**: A dynamic size stack can grow or shrink dynamically. When the stack is full, it automatically increases its size to accommodate the new element, and when the stack is empty, it decreases its size. This type of stack is implemented using a linked list, as it allows for easy resizing of the stack.

In addition to these two main types, there are several other variations of Stacks, including:

1. **Infix to Postfix Stack**: This type of stack is used to convert infix expressions to postfix expressions.
2. **Expression Evaluation Stack**: This type of stack is used to evaluate postfix expressions.
3. **Recursion Stack**: This type of stack is used to keep track of function calls in a computer program and to return control to the correct function when a function returns.
4. **Memory Management Stack**: This type of stack is used to store the values of the program counter and the values of the registers in a computer program, allowing the program to return to the previous state when a function returns.
5. **Balanced Parenthesis Stack**: This type of stack is used to check the balance of parentheses in an expression.
6. **Undo-Redo Stack**: This type of stack is used in computer programs to allow users to undo and redo actions.

####  **Applications of the stack:**

1. **Expression Conversion:**
    
    - Used in converting infix to postfix/prefix expressions.
2. **Redo-Undo Features:**
    
    - Implemented in editors, Photoshop, and similar tools for managing editing history.
3. **Navigation in Web Browsers:**
    
    - Enables forward and backward features in web browsers.
4. **Algorithmic Problems:**
    
    - Utilized in various algorithms such as Tower of Hanoi, tree traversals, stock span, and histogram problems.
5. **Backtracking:**
    
    - Essential for backtracking algorithms like Knight-Tour, N-Queen, maze-solving, and game scenarios like chess or checkers.
6. **Graph Algorithms:**
    
    - Applied in graph algorithms like Topological Sorting and Strongly Connected Components.
7. **Memory Management:**
    
    - Used in computer memory management, with each running program having its own memory allocations.
8. **String Reversal:**
    
    - Reversing strings by pushing each character onto the stack and then popping them.
9. **Function Call Implementation:**
    
    - Facilitates implementing function calls in computers, ensuring the last-called function completes first.
10. **Undo/Redo in Text Editors:**
    
    - Employed in text editors for implementing undo and redo operations.


#### Implementation of Stack:

- **Array-based:** Uses an array to push and pop elements. Push increments the top index, while pop decrements it.
    
- **Linked List-based:** Utilizes a linked list, pushing involves creating a new node with the new element, adjusting pointers.
    

**Applications of Stacks:**

- **Expression Evaluation:** Stacks store operands and operators during expression processing.
    
- **Function Calls:** Tracks the order of function calls and facilitates proper return control.
    
- **Memory Management:** Utilizes stacks to store program counter and register values, allowing efficient return to the previous state.
    

**Conclusion:**

- **Linear Data Structure:** Follows Last In, First Out (LIFO) principle.
- **Implementation Choices:** Can be implemented using an array or a linked list.
- **Key Operations:** Basic operations include push, pop, and peek.
- **Versatile Usage:** Widely applied in computer science for expression evaluation, function calls, and memory management.

#### **Implementing Stack using Arrays:**

```java
/* Java program to implement basic stack 
operations */
class Stack { 
	static final int MAX = 1000; 
	int top; 
	int a[] = new int[MAX]; // Maximum size of Stack 

	boolean isEmpty() 
	{ 
		return (top < 0); 
	} 
	Stack() 
	{ 
		top = -1; 
	} 

	boolean push(int x) 
	{ 
		if (top >= (MAX - 1)) { 
			System.out.println("Stack Overflow"); 
			return false; 
		} 
		else { 
			a[++top] = x; 
			System.out.println(x + " pushed into stack"); 
			return true; 
		} 
	} 

	int pop() 
	{ 
		if (top < 0) { 
			System.out.println("Stack Underflow"); 
			return 0; 
		} 
		else { 
			int x = a[top--]; 
			return x; 
		} 
	} 

	int peek() 
	{ 
		if (top < 0) { 
			System.out.println("Stack Underflow"); 
			return 0; 
		} 
		else { 
			int x = a[top]; 
			return x; 
		} 
	} 
	
	void print(){ 
	for(int i = top;i>-1;i--){ 
	System.out.print(" "+ a[i]); 
	} 
} 
} 

// Driver code 
class Main { 
	public static void main(String args[]) 
	{ 
		Stack s = new Stack(); 
		s.push(10); 
		s.push(20); 
		s.push(30); 
		System.out.println(s.pop() + " Popped from stack"); 
		System.out.println("Top element is :" + s.peek()); 
		System.out.print("Elements present in stack :"); 
		s.print(); 
	} 
} 
```

**Output**

```text
10 pushed into stack
20 pushed into stack
30 pushed into stack
30 Popped from stack
Top element is : 20
Elements present in stack : 20 10
```

**CSD IntArrayStack Implementation**

```java
/**  
 * * Fixed stack that stores int values. Stack capacity does not grow. It is fixed * @author JavaApp2-Jan-2024 group  
 */public class IntArrayStack {  
    private final int [] m_values;  
    private int m_index;  
  
    /**  
     * Creates a fixed stack     * @param count capacity of the stack  
     */    public IntArrayStack(int count)  
    {  
        m_values = new int[count];  
    }  
  
    /**  
     * Pushes a value to the stack if available     * @param value for push  
     * @return true if stack is available, false if stack full  
     */    public boolean push(int value)  
    {  
        var result = m_index != m_values.length;  
  
        if (result)  
            m_values[m_index++] = value;  
  
        return result;  
    }  
  
    /**  
     * Peek the last element from stack     * @return last element from stack, zero if stack is empty  
     */    public int peek()  
    {  
        return m_index != 0 ? m_values[m_index - 1] : 0;  
    }  
  
    /**  
     * Pops a last value from stack if stack is not empty     * @return true if stack is available, false if stack is empty  
     */    public boolean pop()  
    {  
        var result = m_index != 0;  
  
        if (m_index != 0)  
            --m_index;  
  
        return result;  
    }  
  
    /**  
     *  Check if stack is empty     * @return true if stack is empty, otherwise false  
     */    public boolean isEmpty()  
    {  
        return m_index == 0;  
    }  
  
    /**  
     * Gets the size of the elements int the stack     *     * @return size of the elements int the stack  
     */    public int size()  
    {  
        return m_index;  
    }  
  
    /**  
     * Gets the capacity of the elements int the stack     *     * @return capacity of the elements int the stack  
     */    public int capacity()  
    {  
        return m_values.length;  
    }  
}
```

#### Advantages of array implementation:

- Easy to implement.
- Memory is saved as pointers are not involved.

#### Disadvantages of array implementation:

- It is not dynamic i.e., it doesn’t grow and shrink depending on needs at runtime. 
- The total size of the stack must be defined beforehand.


#### **Implementing Stack using Linked List:**

```java
// Java Code for Linked List Implementation 

public class StackAsLinkedList { 

	StackNode root; 

	static class StackNode { 
		int data; 
		StackNode next; 

		StackNode(int data) { this.data = data; } 
	} 

	public boolean isEmpty() 
	{ 
		if (root == null) { 
			return true; 
		} 
		else
			return false; 
	} 

	public void push(int data) 
	{ 
		StackNode newNode = new StackNode(data); 

		if (root == null) { 
			root = newNode; 
		} 
		else { 
			StackNode temp = root; 
			root = newNode; 
			newNode.next = temp; 
		} 
		System.out.println(data + " pushed to stack"); 
	} 

	public int pop() 
	{ 
		int popped = Integer.MIN_VALUE; 
		if (root == null) { 
			System.out.println("Stack is Empty"); 
		} 
		else { 
			popped = root.data; 
			root = root.next; 
		} 
		return popped; 
	} 

	public int peek() 
	{ 
		if (root == null) { 
			System.out.println("Stack is empty"); 
			return Integer.MIN_VALUE; 
		} 
		else { 
			return root.data; 
		} 
	} 

	// Driver code 
	public static void main(String[] args) 
	{ 

		StackAsLinkedList sll = new StackAsLinkedList(); 

		sll.push(10); 
		sll.push(20); 
		sll.push(30); 

		System.out.println(sll.pop() 
						+ " popped from stack"); 

		System.out.println("Top element is " + sll.peek()); 
	} 
}
```

**Output**

```text
10 pushed to stack
20 pushed to stack
30 pushed to stack
30 popped from stack
Top element is 20
Elements present in stack : 20 10
```

#### Advantages of Linked List implementation:

- The linked list implementation of a stack can grow and shrink according to the needs at runtime.
- It is used in many virtual machines like JVM.

#### Disadvantages of Linked List implementation:

- Requires extra memory due to the involvement of pointers.
- Random accessing is not possible in stack.


# Concurrency and Multithreading

## What is Multithreading?

Multithreading means that you have multiple _threads of execution_ inside the same application. A thread is like a separate CPU executing your application. Thus, a multithreaded application is like an application that has multiple CPUs executing different parts of the code at the same time. Usually a single CPU will share its execution time among multiple threads, switching between executing each of the threads for a given amount of time.

![[Pasted image 20240208092843.png]]

## Why Multithreading?

There are several reasons as to why one would use multithreading in an application. Some of the most common reasons for multithreading are:

- **Better CPU Utilization:** Enables more efficient use of CPU resources, especially on multi-core processors.
    
- **Simpler Program Design:** Facilitates simpler program architecture in certain scenarios, allowing for more streamlined code organization.
    
- **More Responsive Programs:** Enhances program responsiveness by concurrently handling tasks, preventing delays during resource-intensive operations.
    
- **Fair Division of CPU Resources:** Ensures a fair distribution of CPU resources among different tasks, preventing resource monopolization and promoting equitable performance

## Multithreading Benefits
### Better CPU Utilization

Multithreading improves CPU utilization by allowing a program to execute multiple threads simultaneously. In traditional single-threaded applications, the CPU may not be fully engaged while waiting for certain tasks to complete, leading to underutilization of processing power. With multithreading, different threads can execute independently, enabling better exploitation of available CPU resources. This is particularly advantageous on multi-core processors, where each core can handle a separate thread, leading to parallel execution and overall increased efficiency.

### Simpler Program Design

Multithreading can contribute to simpler program design in certain situations by allowing developers to modularize and separate tasks that can run concurrently. This modularization often leads to cleaner and more maintainable code. Instead of having complex, intertwined code for various tasks, developers can isolate different functionalities into separate threads, making it easier to understand, debug, and modify specific components of the program. However, it's important to note that while multithreading can simplify design in some cases, it also introduces challenges such as thread synchronization and communication, which need careful consideration during the development process.

### More Responsive Programs

Multithreading enhances program responsiveness by allowing a program to continue executing other tasks while waiting for certain operations to complete. In a single-threaded application, if one task takes a significant amount of time (e.g., file I/O, network communication), the entire program might become unresponsive during that period. With multithreading, other threads can continue executing, ensuring that the program remains responsive to user input or other external events. This is particularly beneficial in applications where user interaction is critical, providing a smoother and more interactive experience for the end user.

### More Fair Distribution of CPU Resources

Multithreading promotes a more fair distribution of CPU resources among different tasks by preventing one thread from monopolizing the processor. In a single-threaded environment, a resource-intensive task could dominate the CPU, leading to delays for other tasks and potentially causing an unresponsive system. With multithreading, the operating system or the program itself can allocate CPU time more evenly among various threads, ensuring that each task gets a fair share of processing power. This prevents one thread from starving others and contributes to a more equitable division of resources, enhancing overall system stability and performance.

## Multithreading Costs

- **More Complex Design:** Multithreading can introduce complexity to program design due to the need for synchronization mechanisms to manage shared resources among threads. Coordination between threads must be carefully handled to avoid issues like data corruption and race conditions.
    
- **Context Switching Overhead:** Switching between threads (context switching) comes with an overhead. When the operating system transitions from one thread to another, it needs to save and restore the state of the CPU, which consumes additional processing time. Excessive context switching can impact overall performance.
    
- **Increased Resource Consumption:** Each thread requires its own stack and resources, leading to increased memory consumption. While this may not be a significant concern for lightweight threads, a large number of threads or resource-intensive threads can lead to higher overall resource usage.

## Concurrency Models

A _concurrency model_ specifies how threads in the the system collaborate to complete the tasks they are are given. Different concurrency models split the tasks in different ways, and the threads may communicate and collaborate in different ways.

### Concurrency Models and Distributed System Similarities

In a concurrent system different threads communicate with each other. In a distributed system different processes communicate with each other (possibly on different computers). Threads and processes are quite similar to each other in nature. That is why the different concurrency models often look similar to different distributed system architectures.

Because concurrency models are similar to distributed system architectures, they can often borrow ideas from each other. For instance, models for distributing work among workers (threads) are often similar to models of load balancing in distributed systems. The same is true of error handling techniques like logging, fail-over, idempotency of tasks etc.
###  Shared State vs. Separate State

One important aspect of a concurrency model is, whether the components and threads are designed to share state among the threads, or to have separate state which is never shared among the threads.

***Shared state*** means that the different threads in the system will share some state among them. By state is meant some data, typically one or more objects or similar. When threads share state, problems like **race conditions** and **deadlock** etc. may occur. It depends on how the threads use and access the shared objects, of course.

![[Pasted image 20240208095557.png]]

**_Separate state_** means that the different threads in the system do not share any state among them. In case the different threads need to communicate, they do so either by exchanging immutable objects among them, or by sending copies of objects (or data) among them. Thus, when no two threads write to the same object (data / state), you can avoid most of the common concurrency problems.

![[Pasted image 20240208100716.png]]

###  Parallel Workers

The Parallel Workers concurrency model involves independent workers executing tasks simultaneously, enabling parallel processing and efficient utilization of resources. Each worker operates concurrently, handling different aspects of a task, and their results are often combined to achieve the overall goal. This model is particularly effective for parallelizable tasks on multi-core processors, enhancing performance by dividing the workload among multiple workers.

![[Pasted image 20240208101201.png]]

#### Parallel Workers Advantages

- **Increased Performance:** Parallel Workers concurrency allows tasks to be executed simultaneously, leveraging multiple processors or cores, leading to faster overall processing.
    
- **Efficient Resource Utilization:** This model efficiently utilizes available resources by distributing tasks among independent workers, maximizing the use of multi-core processors.
    
- **Scalability:** As the workload increases, additional workers can be added to scale performance, making it adaptable to varying computational demands.
    
- **Improved Responsiveness:** Tasks can progress independently, enhancing the system's responsiveness by avoiding bottlenecks that may occur in a sequential execution model.
    
- **Enhanced Throughput:** Parallel processing can lead to higher throughput, enabling the system to handle more tasks or data in a given timeframe.

#### Parallel Workers Disadvantages

- **Complexity:** Implementing and managing parallel workers can introduce complexity to the design and programming of the system. Coordinating independent workers and ensuring proper synchronization can be challenging.
    
- **Potential for Race Conditions:** Concurrent execution may introduce race conditions, where multiple workers access shared resources simultaneously, leading to unpredictable behavior and data corruption.
    
- **Difficulty in Debugging:** Identifying and resolving issues in a parallel environment can be more challenging than in a sequential one. Debugging tools and techniques must handle the complexities of parallel execution.
    
- **Overhead of Coordination:** Coordinating the activities of parallel workers introduces overhead due to synchronization mechanisms. This overhead may impact the overall performance gain achieved through parallelism.
    
- **Limited Applicability:** Not all tasks can be effectively parallelized. Some algorithms and processes inherently depend on sequential execution, limiting the benefits of parallel workers in certain scenarios.

### Assembly Line

The Assembly Line concurrency model involves breaking down a task into sequential stages, each handled by a dedicated worker or thread. Each stage processes a specific aspect of the task, and work progresses in a linear fashion from one stage to the next. This model is efficient for tasks that can be divided into discrete steps and is particularly useful for optimizing throughput and resource utilization.

![[Pasted image 20240208103053.png]]

Systems using the assembly line concurrency model are usually designed to use non-blocking IO. Non-blocking IO means that when a worker starts an IO operation (e.g. reading a file or data from a network connection) the worker does not wait for the IO call to finish. IO operations are slow, so waiting for IO operations to complete is a waste of CPU time. The CPU could be doing something else in the meanwhile. When the IO operation finishes, the result of the IO operation ( e.g. data read or status of data written) is passed on to another worker.

With non-blocking IO, the IO operations determine the boundary between workers. A worker does as much as it can until it has to start an IO operation. Then it gives up control over the job. When the IO operation finishes, the next worker in the assembly line continues working on the job, until that too has to start an IO operation etc.

![[Pasted image 20240208103325.png]]

In reality, the jobs may not flow along a single assembly line. Since most systems can perform more than one job, jobs flows from worker to worker depending on what part of the job that needs to be executed next. In reality there could be multiple different virtual assembly lines running on at the same time.

![[Pasted image 20240208103730.png]]

Jobs may even be forwarded to more than one worker for concurrent processing. For instance, a job may be forwarded to both a job executor and a job logger.

![[Pasted image 20240208103813.png]]

####  Assembly Line Advantages

- **Optimized Throughput:** The Assembly Line concurrency model is designed for efficient task processing, leading to optimized throughput as each stage works on a specific aspect of the task simultaneously.
    
- **Clear Task Division:** Breaking down a task into sequential stages provides a clear and modular division of labor, making it easier to understand, implement, and maintain the code.
    
- **Resource Utilization:** This model can make effective use of available resources, as each stage can be assigned to a dedicated worker or thread, enabling parallel execution on multi-core processors.
    
- **Predictable Execution:** The linear progression of tasks in the Assembly Line model facilitates predictability in execution, simplifying debugging and performance tuning.
    
- **Scalability:** As the workload increases, additional stages or workers can be added to the assembly line, allowing for scalability and adaptability to varying computational demands.

#### Assembly Line Disadvantages

- **Limited Parallelism:** While the Assembly Line model is efficient for tasks with clear sequential stages, it may not fully exploit parallelism in situations where stages are not entirely independent or where dependencies are complex.
    
- **Rigid Structure:** The fixed linear structure of the assembly line can be restrictive, making it less suitable for tasks that don't neatly fit into a sequential workflow.
    
- **Uneven Work Distribution:** If certain stages of the assembly line take significantly longer than others, it can lead to uneven work distribution and potential idle time for some workers.
    
- **Challenge with Dynamic Workloads:** Adapting the Assembly Line model to dynamic workloads or tasks with unpredictable variations in processing requirements can be challenging.
    
- **Complexity in Stage Interaction:** Coordinating and managing interactions between stages, especially when there are dependencies or shared resources, can introduce complexities and potential bottlenecks.

###  Functional Parallelism

The Functional Parallelism concurrency model involves dividing a task into smaller, independent functions that can be executed concurrently. Each function operates on distinct data, and parallel processing is achieved by simultaneously executing these functions. This model aligns well with functional programming principles and is effective for tasks that can be decomposed into parallelizable functions.

## Same-threading

Same-threading is a concurrency model that scales out by replicating single-threaded systems N times, resulting in N independent single-threaded systems running concurrently in parallel.

###  Why Single-threaded Systems?

Single-threaded systems are often chosen for simplicity, ease of programming, and predictable execution, but they can be scaled out in a same-threading model to achieve parallelism and handle increased workloads.

Single-threaded systems have gained popularity because their concurrency models are much simpler than multi-threaded systems. Single-threaded systems do not share any state (objects / data) with other threads. This enables the single thread to use non-concurrent data structures, and utilize the CPU and CPU caches better.

### Same-threading: Single-threading Scaled Out

In order to utilize all the cores in the CPU, a single-threaded system can be scaled out to utilize the whole computer.

### No Shared State

A same-threaded system looks similar to a traditional multi-threaded system, since a same-threaded system has multiple threads running inside it. But there is a subtle difference.

**The difference between a same-threaded and a traditional multi-threaded system is that the threads in a same-threaded system do not share state.** There is no shared memory which the threads access concurrently. No concurrent data structures etc. via which the threads share data.

![[Pasted image 20240208111557.png]]

The lack of shared state is what makes each thread behave as it if was a single-threaded system. 
Same-threaded basically means that data processing stays within the same thread, and that no threads in a same-threaded system share data concurrently. Sometimes this is also referred to just as ***no shared state concurrency***, or ***separate state-concurrency***.

### Load Distribution

If only one thread gets any work, the system would in effect be single-threaded.
Exactly how you distribute the load over the different threads depend on the design of your system

#### Single-threaded Microservices

If your system consists of multiple microservices, each microservice can run in single-threaded mode. When you deploy multiple single-threaded microservices to the same machine, each microservice can run a single thread on a single CPU.

Microservices do not share any data by nature, so microservices is a good use case for a same-threaded system.

#### Services With Sharded Data

If your system does actually need to share data, or at least a database, you may be able to shard the database. Sharding means that the data is divided among multiple databases. The data is typically divided so that all data related to each other is located together in the same database. For instance, all data belonging to some "owner" entity will be inserted into the same database.

### Thread Communication

If the threads in a same-threaded system need to communicate, they do so by message passing. If Thread A wants to send a message to Thread B, Thread A can do so by generating a message (a byte sequence). Thread B can then copy that message (byte sequence) and read it. By copying the message Thread B makes sure that Thread A cannot modify the message while Thread B reads it. Once copied, the message copy is inaccessible for Thread A.

![[Pasted image 20240208113246.png]]

The thread communication can take place via queues, pipes, unix sockets, TCP sockets etc. Whatever fits your system.













