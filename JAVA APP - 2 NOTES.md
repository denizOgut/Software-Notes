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


# CONCURRENCY & MULTITHREADING

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


##  Single-threaded Concurrency

In single-threaded concurrency, a single thread is adept at making progress on multiple tasks by interleaving their execution, eliminating the need for multiple threads. Unlike traditional multithreading where the OS manages task switching between threads, single-threaded concurrency achieves this by internally switching between tasks within the same thread.


###  Classic Multi-threaded Concurrency

typically assign each task to a separate thread for execution. Each thread only executes a single task at a time.
In some designs a new thread will be created for each task, and the thread thus dies once the task is completed. 
In other designs a pool of threads is kept alive which take one task at a time from a task queue, executes it - and then takes another task etc.

Multi-threaded architectures have the advantage that it is relatively easy to distribute the work load across multiple threads and multiple CPUs. However, if the tasks being executed need to share data, a multi-threaded architecture can lead to a lot of concurrency problems such as race conditions, deadlock, starvation, slipped conditions, nested monitor lockout etc.

In general, the more multiple threads share the same data and data structures, the higher the probability is that a concurrency problem may occur.

### Single-threaded or Same-threaded Concurrency

In a single-threaded concurrency design you will have to implement task switching yourself.
You can scale a single-threaded architecture up to use multiple threads, where each thread behaves as if it was a separate, isolated single-threaded system.

###  Single-threaded Concurrency Benefits

- **Full Thread Visibility** 
- **No Race Conditions**: When you only have one thread accessing a data structure shared by multiple tasks you avoid the problems of race conditions.
- **Control Over Task Switching**: manually controlling task switches provides the advantage of ensuring shared resources are left in a consistent state, allowing customization of work increment sizes. This control optimizes CPU utilization by minimizing unnecessary task switching overhead and enables prioritization of tasks based on their assigned work increments.

### Single-threaded Concurrency Challenges

- **Implementation Required**: Having to implement task switching yourself requires that you learn how to implement such designs
- **Blocking Operations Have to be Avoided or Handled in Background Threads**: The thread cannot switch to another task while waiting for the blocking IO operation to complete.
- **A Single Thread Can Only Utilize a Single CPU** 

### Single-threaded Concurrency Designs

#### Thread Loops

Most long-running applications execute in some kind of a loop, where the main application thread is waiting for input from outside the application, processes that input, and then goes back to waiting.

![[Pasted image 20240208202647.png]]

#####  Pausing the Thread Loop

the thread executing the loop is free to "sleep" if it estimates that sleeping a few milliseconds would be okay. That way the CPU time waste can be decreased.

####  Agents

A thread loop typically calls some component which carries out the work of the application.
The life span of an agent may vary

- Run for the entire life-time of your application.
- Run a longer-running job - which eventually finishes.
- Run a one-off task - which finishes quickly.
	
the term agent covers multiple sizes of tasks and responsibility.

#### Thread Loops Call Agents

Thread loops typically call an agent component repeatedly - handing over the actual responsibility of the application to the agent.
The thread loop takes care of looping (repeating the calls to the agent) and detecting when the agent has terminated, and thus terminate the thread loop.
The agent is responsible for executing the application logic itself, but not the looping.

![[Pasted image 20240208203118.png]]


#### Agents May Call Other Agents

An agent may divide its work among other agents. Thus, agents have different levels of responsibility.

![[Pasted image 20240208203201.png]]

#### Single-threaded Task Switching

To enable progress on multiple tasks within a single-threaded system, the tasks must be split into increments.
This allows the thread to switch between tasks, executing one or more increments at each call to an agent. 
By repeatedly calling agents to process these increments, the system can make progress on various tasks without being blocked by the completion of a single lengthy job.

![[Pasted image 20240208203419.png]]                           
![[Pasted image 20240208203439.png]]

#### Increment Size Balancing

If a single thread is to be able to switch between multiple tasks it is imperative that these tasks are not divided into too big increments. In other words, it is the responsibility of each task to help assure fair division of execution time between the tasks.
#### Prioritized Execution

If a single thread is to be able to switch between multiple tasks it is imperative that these tasks are not divided into too big increments. In other words, it is the responsibility of each task to help assure fair division of execution time between the tasks.
#### Agent Parking

If an agent is waiting for some asynchronous operation to finish, e.g. a reply from a remote server, the agent will not be able to make any more progress until the asynchronous operation it is waiting for has finished.
In that case it may not make sense to call that agent over and over again just for the agent to immediately realize that it cannot make any progress and return control immediately to the calling thread.
In such situation it may make sense for an agent to be able to "park" itself so it is no longer being called.
#### Scaling Single-threaded Concurrency

To leverage multiple CPUs in a single-threaded architecture, the solution is to introduce more threads, often aligning with the number of available CPUs.  While technically not single-threaded, each subsystem in this multi-threaded setup is designed and behaves as a single-threaded system. 
#### Event Loops vs. Thread Loops

In an event loop, the loop controls the time between events, limiting application control. 
In contrast, a thread loop allows the application to manage time between events, providing flexibility to prioritize ongoing tasks and decide when to check for new events.

## Concurrency vs. Parallelism

### Concurrency

Concurrency means that an application is making progress on more than one task - at the same time or at least seemingly at the same time (concurrently).

![[Pasted image 20240208204018.png]]

### Parallel Execution

when a computer has more than one CPU or CPU core, and makes progress on more than one task simultaneously. **parallel execution is not parallelism**

![[Pasted image 20240208204123.png]]


### Parallel Concurrent Execution

It is possible to have parallel concurrent execution, where threads are distributed among multiple CPUs. 
Thus, the threads executed on the same CPU are executed concurrently, whereas threads executed on different CPUs are executed in parallel.

![[Pasted image 20240208204338.png]]

### Parallelism

means that an application splits its tasks up into smaller subtasks which can be processed in parallel, for instance on multiple CPUs at the exact same time. To achieve true parallelism your application must have more than one thread running - and each thread must run on separate CPUs

![[Pasted image 20240208204454.png]]

### Concurrency and Parallelism Combinations

To recap, concurrency refers to how a single CPU can make progress on multiple tasks seemingly at the same time Parallelism on the other hand, is related to how an application can parallelize the execution of a single task - typically by splitting the task up into subtasks which can be completed in parallel.	These two execution styles can be combined within the same application
#### Concurrent, Not Parallel

means that it makes progress on more than one task seemingly at the same time (concurrently), but the application switches between making progress on each of the tasks - until the tasks are completed.
There is no true parallel execution of tasks going in parallel threads / CPUs.
#### Parallel, Not Concurrent

means that the application only works on one task at a time, and this task is broken down into subtasks which can be processed in parallel. However, each task (+ subtask) is completed before the next task is split up and executed in parallel.
#### Neither Concurrent Nor Parallel

an application can be neither concurrent nor parallel. This means that it works on only one task at a time, and the task is never broken down into subtasks for parallel execution.
#### Concurrent and Parallel

An application can be both concurrent and parallel by either executing multiple threads concurrently on multiple CPUs or by concurrently working on multiple tasks while breaking each task down into subtasks for parallel execution;  however, careful analysis and measurement are essential as combining these approaches may yield only marginal performance gains or even losses.

## Creating and Starting Java Threads

A Java Thread is like a virtual CPU that can execute your Java code - inside your Java application. 
Java threads are objects like any other Java objects. Threads are instances of class ``java.lang.Thread``, or instances of subclasses of this class In addition to being objects, java threads can also execute code

### Creating and Starting Threads

```java
 Thread thread = new Thread();
 thread.start();
```

There are two ways to specify what code the thread should execute.
The first is to create a subclass of Thread and override the ``run()`` method.
The second method is to pass an object that implements Runnable (``java.lang.Runnable``) to the Thread constructor.

### Thread Subclass

The first way to specify what code a thread is to run, is to create a subclass of Thread and override the ``run()`` method. The ``run()`` method is what is executed by the thread after you call ``start()``.

```java
public class MyThread extends Thread {

    public void run(){
       System.out.println("MyThread running");
    }
  }
```

```java
MyThread myThread = new MyThread();
myTread.start();
```

The ``start()`` call will return as soon as the thread is started. It will not wait until the ``run()`` method is done. The ``run()`` method will execute as if executed by a different CPU. can also create an anonymous subclass of Thread like this:

```java
Thread thread = new Thread(){
    public void run(){
      System.out.println("Thread Running");
    }
  }
  thread.start();
```

### Runnable Interface Implementation

The second way to specify what code a thread should run is by creating a class that implements the ``java.lang.Runnable`` interface. The Runnable interface only has a single method ``run()``.

```java
public interface Runnable() {
    public void run();
}
```

Whatever the thread is supposed to do when it executes must be included in the implementation of the ``run()`` method. There are three ways to implement the Runnable interface:

- **Create a Java class that implements the Runnable interface.**

```java
public class MyRunnable implements Runnable {
    public void run(){
       System.out.println("MyRunnable running");
    }
  }
```

* **Create an anonymous class that implements the Runnable interface.**

```java
Runnable myRunnable =
    new Runnable(){
        public void run(){
            System.out.println("Runnable running");
        }
    }
```

* **Create a Java Lambda that implements the Runnable interface.**

```java
Runnable runnable =
        () -> { System.out.println("Lambda Runnable running"); };
```

#### Starting a Thread With a Runnable

To have the run() method executed by a thread, pass an instance of a class, anonymous class or lambda expression that implements the Runnable interface to a Thread in its constructor.
```java
Runnable runnable = new MyRunnable(); // or an anonymous class, or lambda...
Thread thread = new Thread(runnable);
thread.start();
```

### Subclass or Runnable?

1. **Subclassing Thread:**
    
    When you subclass the `Thread` class, you create a new class that extends `Thread` and overrides its `run()` method. This approach is straightforward, and it involves creating an instance of your custom thread class to start a new thread.
    
    - **Advantages:**
        
        - Simplicity: Creating and starting a thread is a concise process.
        - Direct access to `this`: The thread code has direct access to the instance variables of the class.
    - **Disadvantages:**
        
        - Inheritance limitations: Java supports single inheritance, limiting the ability to extend other classes.
        - Less flexibility: The class is dedicated to being a thread, which might be restrictive in terms of design.
2. **Implementing Runnable:**
    
    When you implement the `Runnable` interface, you create a separate class that defines the `run()` method. This class can then be used to instantiate a `Thread` object.
    
    - **Advantages:**
        
        - Better design: Implementing `Runnable` adheres to the composition over inheritance principle, providing more flexibility in the class hierarchy.
        - Reusability: The same `Runnable` instance can be shared among multiple threads.
        - Stateless: The `Runnable` interface is stateless, which can be beneficial in certain scenarios.
    - **Disadvantages:**
        
        - Slightly more code: The process involves a bit more code compared to subclassing `Thread`.
        - Functional interface: Implementing `Runnable` involves using a functional interface, which can be perceived as an additional layer.

In summary, using `Runnable` is often favored for its better design principles, reusability, and statelessness. It provides a more flexible approach to threading, allowing for improved organization and adaptability in complex applications. However, the choice between the two approaches ultimately depends on the specific requirements of your application and design preferences.

### Common Pitfall: Calling ``run()`` Instead of ``start()``

```java
Thread newThread = new Thread(MyRunnable());
newThread.run();  //should be start();
```

Calling ``run()`` instead of ``start()`` when creating a thread in Java results in the ``run()`` method being executed by the current thread, not the newly created one; to ensure execution by the new thread, ``start()`` should be used.
### Thread Names

When you create a Java thread you can give it a name. The name can help you distinguish different threads from each other. 

```java
Thread thread = new Thread("New Thread") {
      public void run(){
        System.out.println("run by: " + getName());
      }
   };


   thread.start();
   System.out.println(thread.getName());
```

```java
MyRunnable runnable = new MyRunnable();
Thread thread = new Thread(runnable, "New Thread");

thread.start();
System.out.println(thread.getName());
```
### ``Thread.currentThread()``

The ``Thread.currentThread()`` method returns a reference to the Thread instance executing ``currentThread()`` 
This way you can get access to the Java Thread object representing the thread executing a given block of code.

```java
Thread thread = Thread.currentThread();
String threadName = Thread.currentThread().getName();
```
### Pause a Thread

A thread can pause itself by calling the static method ``Thread.sleep()``.  The ``sleep()`` takes a number of milliseconds as parameter. The ``sleep()`` method will attempt to sleep that number of milliseconds before resuming execution. 

```java
try {
    Thread.sleep(10L * 1000L);
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

###  Stop a Thread

Stopping a Java Thread requires careful handling as the deprecated ``stop()`` method can leave shared objects in an unpredictable state.  Instead, it's recommended to implement a thread with a ``doStop()`` method and an internal ``keepRunning()`` method, ensuring a controlled stop.

```java
public class MyRunnable implements Runnable {

    private boolean doStop = false;

    public synchronized void doStop() {
        this.doStop = true;
    }

    private synchronized boolean keepRunning() {
        return this.doStop == false;
    }

    @Override
    public void run() {
        while(keepRunning()) {
            // keep doing what this thread should do.
            System.out.println("Running");

            try {
                Thread.sleep(3L * 1000L);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}
```

```java
public class MyRunnableMain {

    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();

        Thread thread = new Thread(myRunnable);

        thread.start();

        try {
            Thread.sleep(10L * 1000L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        myRunnable.doStop();
    }
}
```

## Virtual Threads

Java virtual threads are different from the original platform threads in that virtual threads are much more lightweight in terms of how many resources (RAM) they demand from the system to run. With more virtual threads running you can do more blocking IO in parallel than with fewer platform threads

### Java Virtual Thread Diagram

- **Application**: The application initiates a JVT.
- **Java Virtual Machine (JVM)**: The JVM manages JVTs, creating and scheduling them according to the task-oriented paradigm.
- **Thread Scheduler**: The Thread Scheduler within the JVM orchestrates the execution of multiple JVTs, allowing for efficient use of system resources.
- **Operating System (OS)**: The OS is not directly involved in managing JVTs. Instead, the JVM handles their execution, making them more lightweight and scalable.
![[Pasted image 20240208214103.png]]

### Virtual Threads are Mounted to Platform Threads

Java virtual threads are executed by platform threads. A platform thread can only execute one virtual thread at a time While the virtual thread is being executed by a platform thread - the virtual thread is said to be mounted to that thread.

New virtual threads are queued up until a platform thread is ready to execute it. When a platform thread becomes ready, it will take a virtual thread and start executing it. A virtual thread that executes some blocking network call (IO) will be unmounted from the platform thread while waiting for the response. In the meantime the platform thread can execute another virtual thread.

#### No Time Slicing Between Virtual Threads

the platform thread does not switch between executing multiple virtual threads - except in the case of blocking network calls. As long as a virtual thread is running code and is not blocked waiting for a network response - the platform thread will keep executing the same virtual thread.

### Virtual Thread Pinning

In Java Virtual Thread (JVT) behavior, a virtual thread remains mounted to a platform thread until it encounters certain blocking operations, such as a network call or a call to a ``BlockingQueue``. However, during blocking file system calls, the virtual thread remains pinned to the platform thread, preventing the execution of other virtual threads.  Additionally, situations like entering a synchronized block may also pin a virtual thread to a platform thread.

### Creating a Java Virtual Thread

use the new ``Thread.ofVirtual()`` factory method, passing an implementation of the Runnable interface.

```java
Runnable runnable = () -> {
    for(int i=0; i<10; i++) {
        System.out.println("Index: " + i);
    }
};
Thread vThread = Thread.ofVirtual().start(runnable);
```

If you do not want the virtual thread to start immediately, you can use the ``unstarted()`` method instead.

```java
Thread vThreadUnstarted = Thread.ofVirtual().unstarted(runnable);
vThreadUnstarted.start();
```

### Join a Virtual Thread

waiting until the virtual thread has finished its work and stopped executing. In other words, the ``join()`` method blocks the calling thread until the virtual thread has finished its work and stopped executing.

```java
Thread vThread = Thread.ofVirtual().start(runnable);
vThread.join();
```

## Race Conditions and Critical Sections

A race condition is a concurrency problem that may occur inside a critical section.
A critical section is a section of code that is executed by multiple threads and where the sequence of execution for the threads makes a difference in the result of the concurrent execution of the critical section.
When the result of multiple threads executing a critical section may differ depending on the sequence in which the threads execute, the critical section is said to contain a race condition.

### Two Types of Race Conditions

Race conditions can occur when two or more threads read and write the same variable according to one of these two patterns:

- Read-modify-write
	two or more threads first read a given variable, then modify its value and write it back to the variable.
	For this to cause a problem, the new value must depend one way or another on the previous value.

- Check-then-act
	involves multiple threads checking a condition concurrently and then taking action based on the result.
	An issue arises when two or more threads simultaneously check and act on the condition, leading to potential conflicts and unexpected outcomes, such as attempting to access the same resource concurrently.

### Read-Modify-Write Critical Sections

```java
public class Counter {

     protected long count = 0;

     public void add(long value){
         this.count = this.count + value;
     }
  }
```

if two threads, A and B, are executing the add method on the same instance of the Counter class. There is no way to know when the operating system switches between the two threads. The code in the ``add()`` method is not executed as a single atomic instruction by the Java virtual machine. Rather it is executed as a set of smaller instructions,

- Read ``this.count`` from memory into register.
- Add value to register.
- Write register to memory.

```java
this.count = 0;

A:  Reads this.count into a register (0)
B:  Reads this.count into a register (0)
B:  Adds value 2 to register
B:  Writes register value (2) back to memory. this.count now equals 2
A:  Adds value 3 to register
A:  Writes register value (3) back to memory. this.count now equals 3
```

#### Race Conditions in Read-Modify-Write Critical Sections

The code in the ``add()`` method in the example earlier contains a critical section. When multiple threads execute this critical section, race conditions occur.

More formally, the situation where two threads compete for the same resource, where the sequence in which the resource is accessed is significant, is called race conditions.  A code section that leads to race conditions is called a critical section.

### Check-Then-Act Critical Sections

If two threads check the same condition, then act upon that condition in a way that changes the condition it can lead to race conditions. If two threads both check the condition at the same time, and then one thread goes ahead and changes the condition, this can lead to the other thread acting incorrectly on that condition.

```java
public class CheckThenActExample {

    public void checkThenAct(Map<String, String> sharedMap) {
        if(sharedMap.containsKey("key")){
            String val = sharedMap.remove("key");
            if(val == null) {
                System.out.println("Value for 'key' was null");
            }
        } else {
            sharedMap.put("key", "value");
        }
    }
}
```

When multiple threads call the ``checkThenAct()`` method on the same object concurrently, a race condition occurs. If two or more threads simultaneously enter the if statement, each may attempt to remove the "key" from the shared map, but only one succeeds, and the others receive a null value. This can lead to unexpected behavior and highlights the need for synchronization mechanisms.

### Preventing Race Conditions

make sure that the critical section is executed as an atomic instruction. That means that once a single thread is executing it, no other threads can execute it until the first thread has left the critical section.
Race conditions can be avoided by proper thread synchronization in critical sections Thread synchronization can be achieved using a synchronized block of Java code. Thread synchronization can also be achieved using other synchronization constructs like locks or atomic variables like ``java.util.concurrent.atomic.AtomicInteger``.

### Critical Section Throughput

For smaller critical sections making the whole critical section a synchronized block may work. 
But, for larger critical sections it may be beneficial to break the critical section into smaller critical sections, to allow multiple threads to execute each a smaller critical section.
This may decrease contention on the shared resource, and thus increase throughput of the total critical section.

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;
    
    public void add(int val1, int val2){
        synchronized(this){
            this.sum1 += val1;   
            this.sum2 += val2;
        }
    }
}
```

To prevent race conditions the summing is executed inside a Java synchronized block. With this implementation only a single thread can ever execute the summing at the same time.
However, since the two sum variables are independent of each other, you could split their summing up into two separate synchronized blocks

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;

    private Integer sum1Lock = new Integer(1);
    private Integer sum2Lock = new Integer(2);

    public void add(int val1, int val2){
        synchronized(this.sum1Lock){
            this.sum1 += val1;   
        }
        synchronized(this.sum2Lock){
            this.sum2 += val2;
        }
    }
}
```

## Thread Safety and Shared Resources

Code that is safe to call by multiple threads simultaneously is called thread safe. If a piece of code is thread safe, then it contains no race conditions.
Race condition only occur when multiple threads update shared resources.

### Local Variables

Local variables are stored in each thread's own stack.
That means that local variables are never shared between threads. That also means that all local primitive variables are thread safe
### Local Object References

The reference itself is not shared. The object referenced however, is not stored in each threads 's local stack. All objects are stored in the shared heap.

If an object created locally never escapes the method it was created in, it is thread safe.  In fact you can also pass it on to other methods and objects as long as none of these methods or objects make the passed object available to other threads.

If an object created within a method (a local object) doesn't extend beyond that method and is not shared with other threads, it is inherently thread-safe because no other threads can access or modify it.

```java
public void someMethod(){

  LocalObject localObject = new LocalObject();

  localObject.callMethod();
  method2(localObject);
}

public void method2(LocalObject localObject){
  localObject.setValue("value");
}
```

``localStringBuilder`` is a local object created within the process() method. Since it doesn't escape the method and is not shared with other threads, it is thread-safe.
### Object Member Variables

Object member variables (fields) are stored on the heap along with the object. Therefore, if two threads call a method on the same object instance and this method updates object member variables, the method is not thread safe.

```java
public class NotThreadSafe{
    StringBuilder builder = new StringBuilder();

    public add(String text){
        this.builder.append(text);
    }
}
```

If two threads call the ``add()`` method simultaneously on the same ``NotThreadSafe`` instance then it leads to race conditions.

```java
NotThreadSafe sharedInstance = new NotThreadSafe();

new Thread(new MyRunnable(sharedInstance)).start();
new Thread(new MyRunnable(sharedInstance)).start();

public class MyRunnable implements Runnable{
  NotThreadSafe instance = null;

  public MyRunnable(NotThreadSafe instance){
    this.instance = instance;
  }

  public void run(){
    this.instance.add("some text");
  }
}
```

the two ``MyRunnable`` instances share the same ``NotThreadSafe`` instance. Therefore, when they call the add() method on the ``NotThreadSafe`` instance it leads to race condition.
However, if two threads call the ``add()`` method simultaneously on "different instances" then it does not lead to race condition.

```java
new Thread(new MyRunnable(new NotThreadSafe())).start();
new Thread(new MyRunnable(new NotThreadSafe())).start();
```

### The Thread Control Escape Rule

The Thread Control Escape Rule states that if a resource is created, used, and disposed within the control of the same thread, without escaping to other threads, its use is considered thread-safe. Disposal involves losing or nullifying the reference to the object. However, if the object points to a shared resource like a file or a database, caution is needed to ensure overall thread safety, as simultaneous operations by multiple threads on the shared resource can lead to potential issues.

## Thread Safety and Immutability

Race conditions occur only if multiple threads are accessing the same resource, and one or more of the threads write to the resource. If multiple threads read the same resource race conditions do not occur.

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }
}
```

We can make sure that objects shared between threads are never updated by any of the threads by making the shared objects immutable, and thereby thread safe. If you need to perform operations on the ``ImmutableValue`` instance you can do so by returning a new instance with the value resulting from the operation.

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }

  **public ImmutableValue add(int valueToAdd){
      return new ImmutableValue(this.value + valueToAdd);
      }**
  
}
```

### The Reference is not Thread Safe!

even if an object is immutable and thereby thread safe, the reference to this object may not be thread safe.

```java
public class Calculator{
  private ImmutableValue currentValue = null;

  public ImmutableValue getValue(){
    return currentValue;
  }

  public void setValue(ImmutableValue newValue){
    this.currentValue = newValue;
  }

  public void add(int newValue){
    this.currentValue = this.currentValue.add(newValue);
  }
}
```

The ``ImmutableValue`` class is thread safe, but the use of it is not. This is something to keep in mind when trying to achieve thread safety through immutability. To make the Calculator class thread safe you could have declared the ``getValue()``,`` setValue()``, and ``add()`` methods synchronized.

## Java Memory Model

specifies how the Java virtual machine works with the computer's memory (RAM). The Java virtual machine is a model of a whole computer so this model naturally includes a memory model - AKA the Java memory model.

>**The statement means that the Java virtual machine (JVM) is designed to emulate the behavior of an entire computer, including its memory management.  The Java memory model, in this context, refers to the rules and specifications that dictate how the JVM interacts with the computer's RAM, ensuring consistency and predictability in handling memory-related operations within Java programs.**

The Java memory model specifies how and when different threads can see values written to shared variables by other threads, and how to synchronize access to shared variables when necessary.

### The Internal Java Memory Model

The Java memory model used internally in the JVM divides memory between thread stacks and the heap
In the Java virtual machine, each thread has its own thread stack, including a "call stack" that tracks method calls and local variables for the methods being executed. 

Local variables of primitive types are fully stored on the thread stack, invisible to other threads. However, objects, including object versions of primitives, are stored in the heap and can be accessed by any thread. 
Each thread has its own version of local variables, promoting thread isolation.

![[Pasted image 20240209131403.png]]

In Java, a local variable can be either of a primitive type, stored entirely on the thread stack, or a reference to an object, where the reference is on the thread stack, but the object itself is stored on the heap.
If an object contains methods with local variables, those variables are also stored on the thread stack.
Member variables of an object, whether of a primitive type or a reference to an object, are stored on the heap with the object.  Static class variables are also stored on the heap.

![[Pasted image 20240209131501.png]]

Objects on the heap are accessible by all threads with a reference to them, allowing access to their member variables.  If multiple threads call a method on the same object simultaneously, they share access to the object's member variables, each having its own copy of local variables.
![[Pasted image 20240209131535.png]]

```java
public class MyRunnable implements Runnable() {

    public void run() {
        methodOne();
    }

    public void methodOne() {
        int localVariable1 = 45;

        MySharedObject localVariable2 =
            MySharedObject.sharedInstance;

        //... do more with local variables.

        methodTwo();
    }

    public void methodTwo() {
        Integer localVariable1 = new Integer(99);

        //... do more with local variable.
    }
}
```

```java
public class MySharedObject {

    //static variable pointing to instance of MySharedObject

    public static final MySharedObject sharedInstance =
        new MySharedObject();


    //member variables pointing to two objects on the heap

    public Integer object2 = new Integer(22);
    public Integer object4 = new Integer(44);

    public long member1 = 12345;
    public long member2 = 67890;
}
```

``MyRunnable`` is a class implementing the Runnable interface with two methods, ``methodOne`` and ``methodTwo``.
``methodOne`` has two local variables, localVariable1 of type int and localVariable2 of type ``MySharedObject``, which points to the shared instance of ``MySharedObject``. ``methodTwo`` creates a local variable localVariable1 of type Integer. ``MySharedObject`` is a class with a ``sharedInstance`` representing a shared instance accessible to all threads.
``MySharedObject`` has member variables pointing to two objects on the heap (object2 and object4) and two long variables (member1 and member2).

When two threads execute the run() method, each creates its own copy of local variables, like localVariable1 and localVariable2. Primitive variables (localVariable1) are entirely separated on each thread's stack, while object references (localVariable2) may point to the same shared object on the heap.  Member variables of ``MySharedObject`` are stored on the heap, and since they are shared among all threads, changes to them are visible to all. Primitive member variables, like long, are also stored on the heap. Each execution of ``methodTwo()`` creates new Integer objects on the heap, but separate instances for each thread.

### Hardware Memory Architecture

![[Pasted image 20240209131945.png]]

In a modern computer with multiple CPUs, each CPU, having its set of registers, can execute one thread at a time, and CPUs may run threads concurrently. The CPU's internal registers offer faster access than main memory. 
Additionally, CPUs often have a cache memory layer, faster than main memory but slower than registers, which stores frequently accessed data. When a CPU needs to access main memory, it reads part of it into its cache, performs operations, and flushes the results back to main memory.
### Bridging The Gap Between The Java Memory Model And The Hardware Memory Architecture

![[Pasted image 20240209132101.png]]

The hardware memory architecture does not distinguish between thread stacks and heap. On the hardware, both the thread stack and the heap are located in main memory. 
Parts of the thread stacks and heap may sometimes be present in CPU caches and in internal CPU registers.

When objects and variables can be stored in various different memory areas in the computer, certain problems may occur. The two main problems are:

- Visibility of thread updates (writes) to shared variables.
- Race conditions when reading, checking and writing shared variables.

#### Visibility of Shared Objects

When multiple threads share an object without proper volatile declarations or synchronization, changes to the shared object made by one thread may not be visible to others Without synchronization, each thread might have its own copy of the object in different CPU caches, leading to visibility issues.  Using the volatile keyword in Java ensures that the variable is read directly from and written back to main memory, addressing this problem.

#### Race Conditions

Without proper synchronization, two threads updating the same variable can lead to unexpected results, as the increments may not be carried out sequentially. Using a Java synchronized block ensures that only one thread can enter a critical section at a time, preventing race conditions by ensuring proper coordination and visibility of variables between threads.

## Java Happens Before Guarantee

The Java happens before guarantee is a set of rules that govern how the Java VM and CPU is allowed to reorder instructions for performance gains. makes it possible for threads to rely on when a variable value is synchronized to or from main memory, and which other variables have been synchronized at the same time.  centered around access to volatile variables and variables accessed from within synchronized blocks.

### Instruction Reordering

Modern CPUs have the ability to execute instructions in parallel if the instructions do not depend on each other.

```java
a = b + c

d = e + f
```

However, the following two instructions cannot easily be executed in parallel, because the second instruction depends on the result of the first instruction:

```java
a = b + c
d = a + e
```

Imagine the two instructions above were part of a larger set of instructions

```java
a = b + c
d = a + e

l = m + n
y = x + z
```

The instructions could be reordered like below. Then the CPU can execute at least the first 3 instructions in parallel, and as soon as the first instructions is finished, it can start executing the 4th instruction

```java
a = b + c

l = m + n
y = x + z

d = a + e
```

reordering instructions can increase parallel execution of instructions in the CPU. Increased parallelization means increased performance.
### Instruction Reordering Problems in Multi CPU Computers

can introduce unexpected behavior in multithreaded environments, especially when certain assumptions about the order of execution are violated. Consider a scenario where two threads are updating a shared counter variable. The counter is initially set to zero, and each thread increments it by one. Without proper synchronization mechanisms, instruction reordering can lead to a race condition:

```java
// Shared Counter
int counter = 0;

// Thread 1
counter++; // Assume this is instruction 1

// Thread 2
counter++; // Assume this is instruction 2
```

In a non-synchronized environment, the compiler or CPU may decide to reorder the instructions for better performance:

```java
// Possible Reordered Execution
counter++; // Thread 1
counter++; // Thread 2
```

In the above scenario, both threads increment the counter, but the final value may not be what is expected. 
The expected result is 2 (initial value + 1 + 1), but due to instruction reordering, the counter might end up with a value of 1 or some other unexpected result.
### The Java volatile Visibility Guarantee

when a variable is declared as volatile in Java, it ensures that any changes made to that variable by one thread are immediately visible to other threads. Similarly, when one thread reads the value of a volatile variable, it sees the most up-to-date value from main memory.

In essence, volatile helps in keeping the variable's value synchronized across different threads, preventing situations where one thread might not see the latest changes made by another thread due to caching or optimization.

#### The Java volatile Write Visibility Guarantee

When you write to a Java volatile variable, not only is its value guaranteed to be written directly to main memory, but also the values of all other variables that are visible to the writing thread.
####  The Java volatile Read Visibility Guarantee

when you read the value of a Java volatile variable, not only is its value guaranteed to be read directly from memory, but also the values of all other variables that are visible to the reading thread will be refreshed from main memory.

### The Java Volatile Happens Before Guarantee

the Java volatile happens-before guarantee ensures that when a thread writes to a volatile variable, all preceding operations are guaranteed to be completed before the write, and when a thread reads a volatile variable, all subsequent operations are guaranteed to see the effects of the read.

```java
public class FrameExchanger  {

    private long framesStoredCount = 0:
    private long framesTakenCount  = 0;

    private volatile boolean hasNewFrame = false;

    private Frame frame = null;

        // called by Frame producing thread
    public void storeFrame(Frame frame) {
        this.frame = frame;
        this.framesStoredCount++;
        this.hasNewFrame = true;
    }

        // called by Frame drawing thread
    public Frame takeFrame() {
        while( !hasNewFrame) {
            //busy wait until new frame arrives
        }

        Frame newFrame = this.frame;
        this.framesTakenCount++;
        this.hasNewFrame = false;
        return newFrame;
    }

}
```

Without the volatile keyword, the compiler or the CPU might reorder instructions, potentially leading to unexpected behavior.  The use of volatile ensures a consistent and predictable order of operations when dealing with shared variables in a multi-threaded environment.
#### Happens Before Guarantee for Writes to volatile Variables

the volatile write happens-before guarantee ensures that when a non-volatile or volatile variable is written before a write to a volatile variable, the writes will be performed in the specified order.

```java
// called by Frame producing thread
public void storeFrame(Frame frame) {
	this.frame = frame;            // Write to non-volatile variable
	this.framesStoredCount++;      // Another write to non-volatile variable
	this.hasNewFrame = true;       // Write to volatile variable
}
```

The guarantee ensures that the writes to frame and ``framesStoredCount`` (non-volatile variables) before the write to the ``hasNewFrame (volatile variable)`` will always happen before the volatile write. This prevents reordering that could lead to incorrect behavior in multi-threaded scenarios.

#### Happens Before Guarantee for Reads of volatile Variables

A read of a volatile variable will happen before any subsequent reads of both volatile and non-volatile variables.

```java
// called by Frame drawing thread
public Frame takeFrame() {
	while( !hasNewFrame) {
		// busy wait until a new frame arrives
	}

	Frame newFrame = this.frame;    // Read of volatile variable
	this.framesTakenCount++;        // Subsequent read of non-volatile variable
	this.hasNewFrame = false;       // Another subsequent read of non-volatile variable
	return newFrame;
}
```

### The Java Synchronized Visibility Guarantee

In essence, the Java synchronized visibility guarantee ensures that:
- When a thread enters a synchronized block, all variables visible to the thread are refreshed from main memory.
- When a thread exits a synchronized block, all variables visible to the thread are written back to main memory.

This ensures consistent and synchronized visibility of variables between threads.

```java
public class ValueExchanger {
	private int valA;
	private int valB;
	private int valC;
	
	public void set(Values v) {
		this.valA = v.valA;
		this.valB = v.valB;
	
		synchronized(this) {
			this.valC = v.valC;
		}
	}
	
	public void get(Values v) {
		synchronized(this) {
			v.valC = this.valC;
		}
		v.valB = this.valB;
		v.valA = this.valA;
	}
}
```

In the ``set()`` method, the synchronized block at the end ensures that all updated variable values are flushed to the main memory
In the ``get()`` method, the synchronized block at the beginning guarantees that all variables are refreshed from the main memory before they are read.

### Java Synchronized Happens Before Guarantee

provide two happens before guarantees: One guarantee related to the beginning of a synchronized block, and another guarantee related to the end of a synchronized block.
#### Java Synchronized Block Beginning Happens Before Guarantee

The beginning of a Java synchronized block provides the visibility guarantee that when a thread enters a synchronized block all variables visible to the thread will be read in (refreshed from) main memory.

```java
public void get(Values v) {
	synchronized(this) {
		v.valC = this.valC;
	}
	v.valB = this.valB;
	v.valA = this.valA;
	}
	
	
	public void get(Values v) {
	v.valB = this.valB;
	v.valA = this.valA;
	synchronized(this) {
		v.valC = this.valC;
	}
}
```

#### Java Synchronized Block End Happens Before Guarantee

The end of a synchronized block provides the visibility guarantee that all changed variables will be written back to main memory when the thread exits the synchronized block. To be able to uphold that guarantee, a set of restrictions on instruction reordering are necessary

```java
public void set(Values v) {
	this.valA = v.valA;
	this.valB = v.valB;

	synchronized(this) {
		this.valC = v.valC;
	}
}


public void set(Values v) {
	synchronized(this) {
		this.valC = v.valC;
	}
	this.valA = v.valA;
	this.valB = v.valB;
}
```

## Java Synchronized Blocks

A synchronized block in Java can only be executed a single thread at a time (depending on how you use it). 
Java synchronized blocks can thus be used to avoid race conditions.

### The Java synchronized Keyword

Synchronized blocks in Java are marked with the synchronized keyword
All synchronized blocks synchronized on the same object can only have one thread executing inside them at the same time. All other threads attempting to enter the synchronized block are blocked until the thread inside the synchronized block exits the block.

The synchronized keyword can be used to mark four different types of blocks:

- **Instance methods**
- **Static methods**
- **Code blocks inside instance methods**
- **Code blocks inside static methods**

### Synchronized Instance Methods

```java
public class MyCounter {

  private int count = 0;

  public **synchronized** void add(int value){
      this.count += value;
  }
}
```

A synchronized instance method in Java is synchronized on the instance (object) owning the method. 
Thus, each instance has its synchronized methods synchronized on a different object: the owning instance.
One thread per instance. This is true across all synchronized instance methods for the same object (instance). 

### Synchronized Static Methods

```java
public static MyStaticCounter{

  private static int count = 0;

  public **static synchronized** void add(int value){
      count += value;
  }
}
```

Synchronized static methods are synchronized on the class object of the class the synchronized static method belongs to. Since only one class object exists in the Java VM per class, only one thread can execute inside a static synchronized method in the same class.
In case a class contains more than one static synchronized method, only one thread can execute inside any of these methods at the same time.

```java
public static MyStaticCounter{

  private static int count = 0;

  public **static synchronized** void add(int value){
    count += value;
  }

  public **static synchronized** void subtract(int value){
    count -= value;
  }
}
```

If the static synchronized methods are located in different classes, then one thread can execute inside the static synchronized methods of each class. One thread per class regardless of which static synchronized method it calls.

### Synchronized Blocks in Instance Methods

Sometimes it is preferable to synchronize only part of a method. Java synchronized blocks inside methods makes this possible.
```java
public void add(int value){

    synchronized(this){
       this.count += value;   
    }
  }
```

This code will now execute as if it was a synchronized method.
A synchronized instance method uses the object it belongs to as monitor object.
Only one thread can execute inside a Java code block synchronized on the same monitor object.

```java
public class MyClass {
  
    public synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public void log2(String msg1, String msg2){
       synchronized(this){
          log.writeln(msg1);
          log.writeln(msg2);
       }
    }
  }
```

Thus only a single thread can execute inside either of the two synchronized blocks 
Had the second synchronized block been synchronized on a different object than this, then one thread at a time had been able to execute inside each method.
### Synchronized Blocks in Static Methods

Synchronized blocks can also be used inside of static methods. Only one thread can execute inside any of these two methods at the same time.

```java
public class MyClass {

    public static synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public static void log2(String msg1, String msg2){
       synchronized(MyClass.class){
          log.writeln(msg1);
          log.writeln(msg2);  
       }
    }
  }
```

###  Synchronized Blocks in Lambda Expressions

```java
import java.util.function.Consumer;

public class SynchronizedExample {

  public static void main(String[] args) {

    Consumer<String> func = (String param) -> {

      synchronized(SynchronizedExample.class) {

        System.out.println(
            Thread.currentThread().getName() +
                    " step 1: " + param);

        try {
          Thread.sleep( (long) (Math.random() * 1000));
        } catch (InterruptedException e) {
          e.printStackTrace();
        }

        System.out.println(
            Thread.currentThread().getName() +
                    " step 2: " + param);
      }

    };


    Thread thread1 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 1");

    Thread thread2 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 2");

    thread1.start();
    thread2.start();
  }
}
```

the choice of the object for synchronization is crucial to achieve the desired level of coordination between threads. Using a class object is common, but in some cases, a dedicated lock object may be more appropriate.

### Synchronized and Data Visibility

Without the use of the synchronized keyword (or the Java volatile keyword) there is no guarantee that when one thread changes the value of a variable shared with other threads that the other threads can see the changed value. There are no guarantees about when a variable kept in a CPU register by one thread is "committed" to main memory, and there is no guarantee about when other threads "refresh" a variable kept in a CPU register from main memory.

The synchronized keyword changes that.
- When a thread enters a synchronized block it will refresh the values of all variables visible to the thread.
- When a thread exits a synchronized block all changes to variables visible to the thread will be committed to main memory.

### Synchronized and Instruction Reordering

The Java compiler and Java Virtual Machine are allowed to reorder instructions in your code to make them execute faster, typically by enabling the reordered instructions to be executed in parallel by the CPU.
Instruction reordering could potentially cause problems in code that is executed by multiple threads at the same time.  For instance, if a write to a variable happening inside of a synchronized block was reordered to happen outside of the synchronized block.

To fix this problem the Java synchronized keyword places some restrictions on reordering of instructions before, inside and after synchronized blocks.
The end result is, that you can be sure that your code works correctly - that no instruction reordering is taking place that ends up making the code behave differently than what was to be expected from the code you wrote.

### What Objects to Synchronize On

When using synchronized blocks in Java, it's advisable not to synchronize on String or primitive type wrapper objects, as the compiler might optimize them, leading to unexpected behavior.

To ensure consistent synchronization, it's recommended to synchronize on this or a new Object() to avoid potential issues with object reuse and caching.

### Synchronized Block Limitations and Alternatives

Synchronized blocks in Java have limitations; they allow only one thread at a time.
For scenarios with shared read-only access, consider alternatives like Read/Write Lock or Semaphores (Java provides ``ReadWriteLock`` and Semaphore). For simultaneous access by multiple threads, Semaphores can help.

Synchronized blocks lack order guarantees for granting access to waiting threads. To enforce order, you must implement fairness. In cases with a single writing thread and multiple reading threads, using a volatile variable for the shared data might be sufficient. Volatile ensures visibility of changes across threads without the need for additional synchronization.

### Synchronized Block Performance Overhead

Entering and exiting synchronized blocks in Java incurs a small performance overhead. 
Though modern Java versions have minimized this overhead, it remains a concern when frequent synchronization occurs, especially within tight loops.

To mitigate this, it's crucial to keep synchronized blocks as small as possible. 
Synchronize only the essential operations to prevent unnecessary blocking of threads. 
Restrict synchronization to the absolutely necessary instructions within the blocks to enhance code parallelism.

### Synchronized Block Reentrance

When a thread enters a synchronized block, it holds the lock for the associated object. 
If the thread calls another method that reenters the same synchronized block, it's allowed to do so, as long as the thread itself is holding the lock.  This is to prevent blocking when a thread calls back into its own synchronized block.

## Java Volatile Keyword

is used to mark a Java variable as "being stored in main memory".
More precisely that means, that every read of a volatile variable will be read from the computer's main memory, and not from the CPU registers, and that every write to a volatile variable will be written to main memory

## Variable Visibility Problems

In a multithreaded application where the threads operate on non-volatile variables, each thread may copy variables from main memory into a CPU registers while working on them, for performance reasons. If your computer contains more than one CPU, each thread may run on a different CPU. That means, that each thread may copy the variables into the CPU registers of different CPUs.

![[Pasted image 20240209175343.png]]

With non-volatile variables there are no guarantees about when the Java Virtual Machine (JVM) reads data from main memory into CPU registers, or writes data from CPU registers to main memory. Imagine a situation in which two or more threads have access to a shared object which contains a counter variable

```java
public class SharedObject {

    public int counter = 0;

}
```

Imagine too, that only Thread 1 increments the counter variable, but both Thread 1 and Thread 2 may read the counter variable from time to time. If the counter variable is not declared volatile there is no guarantee about when the value of the counter variable is written from the CPU registers back to main memory.
This means, that the counter variable value in the CPU register may not be the same as in main memory
The problem with threads not seeing the latest value of a variable because it has not yet been written back to main memory by another thread, is called a "visibility" problem. The updates of one thread are not visible to other threads.

![[Pasted image 20240209175454.png]]

### The Java volatile Visibility Guarantee

volatile keyword is intended to address variable visibility problems.
By declaring the counter variable volatile all writes to the counter variable will be written back to main memory immediately. Also, all reads of the counter variable will be read directly from main memory.

```java
public class SharedObject {

    public **volatile** int counter = 0;

}
```

Declaring a variable volatile thus guarantees the visibility for other threads of writes to that variable.

#### Full volatile Visibility Guarantee

The visibility guarantee is as follows:

If Thread A writes to a volatile variable and Thread B subsequently reads the same volatile variable, 
then all variables visible to Thread A before writing the volatile variable, will also be visible to Thread B after it has read the volatile variable.

If Thread A reads a volatile variable, then all all variables visible to Thread A when reading the volatile variable will also be re-read from main memory.

```java
public class MyClass {
	private int years;
	private int months
	private volatile int days;


	public void update(int years, int months, int days){
		this.years  = years;
		this.months = months;
		this.days   = days;
	}
}
```

The full volatile visibility guarantee means, that when a value is written to days, then all variables visible to the thread are also written to main memory.  That means, that when a value is written to days, the values of years and months are also written to main memory.

```java
public class MyClass {
	private int years;
	private int months
	private volatile int days;

	public int totalDays() {
		int total = this.days;
		total += months * 30;
		total += years * 365;
		return total;
	}

	public void update(int years, int months, int days){
		this.years  = years;
		this.months = months;
		this.days   = days;
	}
}
```

the ``totalDays()`` method starts by reading the value of days into the total variable. When reading the value of days, the values of months and years are also read into main memory.
Therefore you are guaranteed to see the latest values of days, months and years with the above read sequence.

### Instruction Reordering Challenges

The Java VM and the CPU are allowed to reorder instructions in the program for performance reasons, as long as the semantic meaning of the instructions remain the same

```java
int a = 1;
int b = 2;

a++;
b++;
```

These instructions could be reordered to the following sequence without losing the semantic meaning of the program:

```java
int a = 1;
a++;

int b = 2;
b++;
```

instruction reordering presents a challenge when one of the variables is a volatile variable.

```java
public class MyClass {
	private int years;
	private int months
	private volatile int days;


	public void update(int years, int months, int days){
		this.years  = years;
		this.months = months;
		this.days   = days;
	}
}
```

Once the ``update()`` method writes a value to days, the newly written values to years and months are also written to main memory. But, what if the Java VM reordered the instructions

```java
public void update(int years, int months, int days){
	this.days   = days;
	this.months = months;
	this.years  = years;
}
```

The values of months and years are still written to main memory when the days variable is modified, but this time it happens before the new values have been written to months and years. 
The new values are thus not properly made visible to other threads. The semantic meaning of the reordered instructions has changed.

### The Java volatile Happens-Before Guarantee

To address the instruction reordering challenge, the Java volatile keyword gives a "happens-before" guarantee, in addition to the visibility guarantee. The happens-before guarantee guarantees that:

- Before and After Write to Volatile:
	Operations before a write to a volatile variable are guaranteed to happen before that write.
	Operations after a write to a volatile variable may be reordered to occur before, but not the other way around.

- Before and After Read of Volatile:
     Operations before a read of a volatile variable may be reordered to occur after, but not the other way around. Operations after a read of a volatile variable are guaranteed to happen after that read. 

### Volatile is Not Always Enough

using the volatile keyword ensures that reads and writes of a variable are directly performed in main memory.
However, when multiple threads need to read the current value of a volatile variable, calculate a new value based on that, and then update the variable, a race condition can occur. In this scenario, different threads might read the same initial value, perform independent calculations, and overwrite each other's results when writing back to main memory. 

This situation can lead to incorrect and unpredictable variable values, making volatile alone insufficient for scenarios where multiple threads modify a shared variable based on its current state.

### When is volatile Enough?

To ensure atomicity when both reading and writing to a shared variable by multiple threads, the volatile keyword alone is not sufficient. In such cases, using synchronized blocks is necessary to guarantee atomic operations, preventing potential race conditions. Unlike reading or writing a volatile variable, the synchronized keyword provides a mechanism for blocking threads during critical sections.

However, if only one thread writes to a volatile variable, and other threads solely read the variable, the volatile keyword ensures that reading threads see the latest written value. This guarantee is crucial for scenarios where multiple threads read a shared variable, and making the variable volatile is essential to ensure the latest value is visible to all reading threads.

### Performance Considerations of volatile

The use of volatile variables in Java incurs a performance cost due to the necessity of reading or writing to main memory, which is more expensive than accessing CPU registers. it is advisable to use volatile variables only when there's a genuine need to enforce visibility of variables.

In practice, CPU register values are typically written to the CPU L1 cache, which is reasonably fast—though not as fast as writing to a CPU register. The synchronization process from the L1 cache down through L2 and L3 cache, and back to main memory (RAM), involves separate chips than the CPU, relieving the CPU of this burden.

Despite the optimization in modern systems, it's essential to use volatile variables judiciously, limiting their use to situations where visibility enforcement is crucial. This approach encourages a detailed understanding of how Java volatile variables operate.

## CPU Cache Coherence in Java Concurrency

In Java, when variables stored in CPU registers need to be synchronized, they are flushed to main memory (RAM).  This process may involve storing the variables in the CPU cache, with the CPU and motherboard employing cache coherence methods to ensure visibility across all CPU caches.

The hardware might optimize this process by keeping the variables in the CPU cache until it's needed for other data, at which point it can be flushed to main memory. However, from the perspective of the executing code on the CPU, whether the data is in the CPU cache or main RAM is transparent as long as it's retrieved as needed.

![[Pasted image 20240209180614.png]]

**Key points:**

- **Synchronization involves flushing variables from CPU registers to main memory.**
- **CPU cache coherence methods ensure visibility across CPU caches.**
- **Optimization may involve temporarily keeping variables in the CPU cache.**
- **The specifics of CPU cache coherence are handled by the hardware, and from the code's perspective, data retrieval remains consistent.**

## False Sharing in Java

False sharing in Java occurs when two threads running on two different CPUs write to two different variables which happen to be stored within the same CPU cache line. When the first thread modifies one of the variables - the whole CPU cache line is invalidated in the CPU caches of the other CPU where the other thread is running
This means, that the other CPUs need to reload the content of the invalidated cache line - even if they don't really need the variable that was modified within that cache line.

![[Pasted image 20240209180802.png]]

### Cache Lines

When the CPU caches are reading data from lower level caches or main RAM they don't just read a single byte at a time. That would be inefficient. Instead they read a cache line. A cache line typically consists of 64 bytes. 
Thus, the caches read 64 bytes at a time from lower level caches or main RAM.

Because a cache line consist of multiple bytes, a single cache line will often store more than one variable.
If the same CPU needs to access more of the variables stored within the same cache line - this is an advantage.
If multiple CPUs need to access the variables stored within the same cache line, false sharing can occur.

### Cache Line Invalidation

When a CPU writes to memory address in a cache line, typically because the CPU is writing to a variable, the cache line becomes dirty. The cache line then needs to be synchronized to other CPUs that also have that cache line in their CPU caches. The same cache line stored in the other CPU caches thus becomes invalid - they need to be refreshed

Cache refreshing after cache invalidation can happen either via cache coherence mechanisms, or by reloading the cache line from main RAM. The CPU is not allowed to access that cache line until it has been refreshed.

### False Sharing Results in a Performance Penalty

False sharing occurs when multiple CPUs write to variables within the same cache line, even if each CPU doesn't depend on the values written by the other. This leads to continuous cache line invalidation and refreshing between CPUs, causing performance degradation as each CPU waits for cache line refreshes, resulting in fewer executed instructions.

To address false sharing, it's essential to restructure data so that independent variables used by CPUs are not stored within the same cache line. This prevents unnecessary cache line invalidation and refresh cycles.

**Key Points**

- **False sharing involves multiple CPUs writing to variables in the same cache line.**
- **CPUs continuously invalidate and refresh the cache line, leading to performance degradation.**
- **Restructuring data to separate independent variables can mitigate false sharing and improve performance.**

```java
public class Counter {

    public volatile long count1 = 0;
    public volatile long count2 = 0;

}
```

```java
public class FalseSharingExample {

    public static void main(String[] args) {

        Counter counter1 = new Counter();
        Counter counter2 = counter1;

        long iterations = 1_000_000_000;

        Thread thread1 = new Thread(() -> {
            long startTime = System.currentTimeMillis();
            for(long i=0; i<iterations; i++) {
                counter1.count1++;
            }
            long endTime = System.currentTimeMillis();
            System.out.println("total time: " + (endTime - startTime));
        });
        Thread thread2 = new Thread(() -> {
            long startTime = System.currentTimeMillis();
            for(long i=0; i<iterations; i++) {
                counter2.count2++;
            }
            long endTime = System.currentTimeMillis();
            System.out.println("total time: " + (endTime - startTime));
        });

        thread1.start();
        thread2.start();
    }
}
```

```java
// To fix this 			
Counter counter2 = new Counter();
```

#### Fixing False Sharing Problems

The way to fix a false sharing problem is to design your code so that different variables used by different threads do not end up being stored within the same CPU cache line. storing the variables in different objects is one way to do so

## Java ``ThreadLocal``

enables you to create variables that can only be read and written by the same thread.  Thus, even if two threads are executing the same code, and the code has a reference to the same ThreadLocal variable, the two threads cannot see each other's ThreadLocal variables.  Thus, the Java ThreadLocal class provides a simple way to make code thread safe that would not otherwise be so.

### Creating a ThreadLocal

```java
private ThreadLocal threadLocal = new ThreadLocal();
threadLocal.set("A thread local value");
String threadLocalValue = (String) threadLocal.get();

threadLocal.remove();
```

### Generic ThreadLocal

Using a generic type only objects of the generic type can be set as value on the ThreadLocal.
Additionally, you do not have to typecast the value returned by ``get()``.

```java
private ThreadLocal<String> myThreadLocal = new ThreadLocal<String>();
myThreadLocal.set("Hello ThreadLocal");
String threadLocalValue = myThreadLocal.get();
```

### Initial ThreadLocal Value

It is possible to set an initial value for a Java ThreadLocal which will get used the first time ``get()`` is called - before ``set()`` has been called with a new value.		

- Create a ThreadLocal subclass that overrides the ``initialValue()`` method.
- Create a ThreadLocal with a Supplier interface implementation.

#### Override ``initialValue()``

create a subclass of ThreadLocal which overrides its ``initialValue()`` method.
The easiest way to create a subclass of ThreadLocal is to simply create an anonymous subclass, right where you create the ThreadLocal variable.

```java
private ThreadLocal myThreadLocal = new ThreadLocal<String>() {
	@Override protected String initialValue() {
		return String.valueOf(System.currentTimeMillis());
	}
};
```

different threads will still see different initial values.
Each thread will create its own initial value.  Only if you return the exact same object from the ``initialValue()`` method, will all threads see the same object. However, the whole point of using a ThreadLocal in the first place is to avoid the different threads seeing the same instance.

#### Provide a Supplier Implementation

to use its static factory method ``withInitial(Supplier)`` passing a Supplier interface implementation as parameter. This Supplier implementation supplies the initial value for the ThreadLocal.

```java
ThreadLocal<String> threadLocal = ThreadLocal.withInitial(new Supplier<String>() {
		@Override
		public String get() {
			return String.valueOf(System.currentTimeMillis());
		}
	});
	
	
	ThreadLocal threadLocal = ThreadLocal.withInitial(
	() -> { return String.valueOf(System.currentTimeMillis()); } );
	
	ThreadLocal threadLocal3 = ThreadLocal.withInitial(
	() -> String.valueOf(System.currentTimeMillis()) );
```

### Lazy Setting of ThreadLocal Value

In some situations you cannot use the standard ways of setting an initial value For instance, perhaps you need some configuration information which is not available at the time you create the ThreadLocal variable.  In that case you can set the initial value lazily.

```java
public class MyDateFormatter {
	private ThreadLocal<SimpleDateFormat> simpleDateFormatThreadLocal = new ThreadLocal<>();

	public String format(Date date) {
		SimpleDateFormat simpleDateFormat = getThreadLocalSimpleDateFormat();
		return simpleDateFormat.format(date);
	}
	
	
	private SimpleDateFormat getThreadLocalSimpleDateFormat() {
		SimpleDateFormat simpleDateFormat = simpleDateFormatThreadLocal.get();
		if(simpleDateFormat == null) {
			simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
			simpleDateFormatThreadLocal.set(simpleDateFormat);
		}
		return simpleDateFormat;
	}
}
```

### Using a ThreadLocal with a Thread Pool or ``ExecutorService``

a Java ThreadLocal from inside a task passed to a Java Thread Pool or a Java ``ExecutorService``, keep in mind that you do not have any guarantees which thread will execute your task. However, if all you need is to make sure that each thread uses its own instance of some object, this is not a problem. Then you can use a Java ThreadLocal with a thread pool or ``ExecutorService`` just fine.
### Inheritable ThreadLocal

The ``InheritableThreadLocal`` class is a subclass of ThreadLocal. Instead of each thread having its own value inside a ThreadLocal, the ``InheritableThreadLocal`` grants access to values to a thread and all child threads created by that thread

```java
public class InheritableThreadLocalBasicExample {

    public static void main(String[] args) {

        ThreadLocal<String> threadLocal = new ThreadLocal<>();
        InheritableThreadLocal<String> inheritableThreadLocal =
                new InheritableThreadLocal<>();

        Thread thread1 = new Thread(() -> {
            System.out.println("===== Thread 1 =====");
            threadLocal.set("Thread 1 - ThreadLocal");
            inheritableThreadLocal.set("Thread 1 - InheritableThreadLocal");

            System.out.println(threadLocal.get());
            System.out.println(inheritableThreadLocal.get());

            Thread childThread = new Thread( () -> {
                System.out.println("===== ChildThread =====");
                System.out.println(threadLocal.get());
                System.out.println(inheritableThreadLocal.get());
            });
            childThread.start();
        });

        thread1.start();

        Thread thread2 = new Thread(() -> {
            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println("===== Thread2 =====");
            System.out.println(threadLocal.get());
            System.out.println(inheritableThreadLocal.get());
        });
        thread2.start();
    }
}
```

```java
===== Thread 1 =====
Thread 1 - ThreadLocal
Thread 1 - InheritableThreadLocal
===== ChildThread =====
null
Thread 1 - InheritableThreadLocal
===== Thread2 =====
null
null
```

## Thread Signaling

Java contains a set of features that enable thread to send signals to each other, and for threads to wait for such signals. The thread signaling features in Java are implemented via the wait(), notify() and notifyAll() methods that are part of the the Object class which all Java classes extend.

### ``wait()``, ``notify()`` and ``notifyAll()``

Java has a built-in wait mechanism that enable threads to become inactive while waiting for signals from other threads. A thread that calls wait() on any object becomes inactive until another thread calls notify() or notifyAll() on that object. In order to call either wait(), notify() or notifyAll(), the calling thread must first obtain the lock on that object. In other words, the calling thread must call wait() or notify() from inside a synchronized block that is synchronized on that object.

```java
public class MonitorObject{
}

public class MyWaitNotify{

  MonitorObject myMonitorObject = new MonitorObject();

  public void doWait(){
    synchronized(myMonitorObject){
      try{
        myMonitorObject.wait();
      } catch(InterruptedException e){...}
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      myMonitorObject.notify();
    }
  }
}
```

``doWait()`` pauses a thread until signaled by another thread using ``doNotify()``.
Both methods synchronize on the same ``MonitorObject``. Exception handling is provided for potential interruptions during the wait.

Multiple threads can call wait() on the same monitor object - and thus become blocked waiting for a notify() or ``notifyAll()`` call. Calling notify() will only awaken a single waiting thread. Calling notifyAll() will awaken all waiting threads.

A thread cannot call wait(), notify() or notifyAll() without holding the synchronization lock on the object the method is called on. If it does, an ``IllegalMonitorStateException`` is thrown.

![[Pasted image 20240209191802.png]]

### Missed Signals

The methods notify() and notifyAll() do not save the method calls to them in case no threads are waiting when they are called.  The notify signal is then just lost.
Therefore, if a thread calls notify() before the thread to signal has called wait(), the signal will be missed by the waiting thread. in some cases this may result in the waiting thread waiting forever, never waking up, because the signal to wake up was missed.

To avoid losing signals they should be stored inside the signal class.

```java
public class MyWaitNotify2{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      if(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

### Spurious Wakeups

For inexplicable reasons it is possible for threads to wake up even if notify() and notifyAll() has not been called.
This is known as "spurious wakeups". Wakeups without any reason.

If a spurious wakeup occurs in the MyWaitNofity2 class's ``doWait()`` method the waiting thread may continue processing without having received a proper signal to do so!  To guard against spurious wakeups the signal member variable is checked inside a while loop instead of inside an if-statement. Such a while loop is also called a spin lock. The thread awakened spins around until the condition in the spin lock (while loop) becomes false. 

```java
public class MyWaitNotify3{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      while(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

### Multiple Threads Waiting for the Same Signals

The while loop is also a nice solution if you have multiple threads waiting, which are all awakened using notifyAll(), but only one of them should be allowed to continue Only one thread at a time will be able to obtain the lock on the monitor object, meaning only one thread can exit the wait() call and clear the ``wasSignalled`` flag. Once this thread then exits the synchronized block in the ``doWait()`` method, the other threads can exit the wait() call and check the ``wasSignalled`` member variable inside the while loop. However, this flag was cleared by the first thread waking up, so the rest of the awakened threads go back to waiting, until the next signal arrives.

### Don't call ``wait()`` on constant String's or global objects

risk of spurious wakeups and missed signals when using notify() on shared objects. The recommendation is to avoid using global objects or constants as monitor objects.  Instead, each instance of the class should have its own unique monitor object to prevent unintended interference. The choice between notify() and notifyAll() should consider the trade-off between correctness and performance, as notifyAll() wakes up all waiting threads, while notify() wakes up only one.

## Deadlock

### Thread Deadlock

A deadlock is when two or more threads are blocked waiting to obtain locks that some of the other threads in the deadlock are holding. Deadlock can occur when multiple threads need the same locks, at the same time, but obtain them in different order.
### Deadlock Example

Thread 1 holds the key to Door A and is waiting for the key to Door B.
Thread 2 holds the key to Door B and is waiting for the key to Door A.

Neither thread can proceed, and they are stuck indefinitely, each waiting for the other to release the key they need. This deadlock leaves both threads blocked, and they will remain so forever. It's like a stand-off where neither friend can enter their desired door.

```java
Thread 1  locks A, waits for B
Thread 2  locks B, waits for A
```

```java
public class TreeNode {
 
  TreeNode parent   = null;  
  List     children = new ArrayList();

  public synchronized void addChild(TreeNode child){
    if(!this.children.contains(child)) {
      this.children.add(child);
      child.setParentOnly(this);
    }
  }
  
  public synchronized void addChildOnly(TreeNode child){
    if(!this.children.contains(child){
      this.children.add(child);
    }
  }
  
  public synchronized void setParent(TreeNode parent){
    this.parent = parent;
    parent.addChildOnly(this);
  }

  public synchronized void setParentOnly(TreeNode parent){
    this.parent = parent;
  }
}
```

```java
// pseudo code
				
Thread 1: parent.addChild(child); //locks parent
--> child.setParentOnly(parent);

Thread 2: child.setParent(parent); //locks child
  --> parent.addChildOnly()
```

### More Complicated Deadlocks

```java
Thread 1  locks A, waits for B
Thread 2  locks B, waits for C
Thread 3  locks C, waits for D
Thread 4  locks D, waits for A
```

### Database Deadlocks

A more complicated situation in which deadlocks can occur, is a database transaction.
A database transaction may consist of many SQL update requests. If multiple transactions are running at the same time that need to update the same records, there is a risk of them ending up in a deadlock.

```java
Transaction 1, request 1, locks record 1 for update
Transaction 2, request 1, locks record 2 for update
Transaction 1, request 2, tries to lock record 2 for update.
Transaction 2, request 2, tries to lock record 1 for update.
```

## Deadlock Prevention

### Lock Ordering

Lock ordering is a strategy to maintain consistency in the order in which locks are acquired to prevent deadlocks and ensure a reliable multithreading environment.  It involves establishing a global lock order or lock hierarchies and ensuring that all threads follow this order when acquiring multiple locks. If you make sure that all locks are always taken in the same order by any thread, deadlocks cannot occur.

```java
Thread 1:

  lock A 
  lock B


Thread 2:

   wait for A
   lock C (when A locked)


Thread 3:

   wait for A
   wait for B
   wait for C
```

### Lock Timeout

refers to the concept of setting a maximum time limit for acquiring a lock in a multithreading or concurrent programming environment.  When a thread attempts to acquire a lock and the lock is currently held by another thread, the thread can either wait indefinitely for the lock to be released or wait for a specified period, after which it gives up trying to acquire the lock.

```java
Lock lock = new ReentrantLock();
boolean lockAcquired = lock.tryLock(500, TimeUnit.MILLISECONDS);
if (lockAcquired) {
	try {
		// Code protected by the lock
	} finally {
		lock.unlock();
	}
} else {
	// Handle lock acquisition timeout
}
```

lock timeout is a mechanism to limit the amount of time a thread is willing to wait to acquire a lock, helping prevent deadlocks, improving system responsiveness, and enabling effective error handling in concurrent programming scenarios.

```java
Thread 1 locks A
Thread 2 locks B

Thread 1 attempts to lock B but is blocked
Thread 2 attempts to lock A but is blocked

Thread 1's lock attempt on B times out
Thread 1 backs up and releases A as well
Thread 1 waits randomly (e.g. 257 millis) before retrying.

Thread 2's lock attempt on A times out
Thread 2 backs up and releases B as well
Thread 2 waits randomly (e.g. 43 millis) before retrying.
```

A problem with the lock timeout mechanism is that it is not possible to set a timeout for entering a synchronized block in Java You will have to create a custom lock class or use one of the Java 5 concurrency constructs in the ``java.util.concurrency`` package.
### Deadlock Detection

is a heavier deadlock prevention mechanism aimed at cases in which lock ordering isn't possible, and lock timeout isn't feasible. Every time a thread takes a lock it is noted in a data structure (map, graph etc.) of threads and locks. Additionally, whenever a thread requests a lock this is also noted in this data structure.

deadlock detection involves periodically examining resource allocation graphs, specifically wait-for graphs, to identify cycles indicating potential deadlocks.  Once a deadlock is detected, corrective actions can be taken to recover from or mitigate the deadlock and restore system functionality.

![[Pasted image 20240209201856.png]]

what do the threads do if a deadlock is detected?

One possible action is to release all locks, backup, wait a random amount of time and then retry. 

- A better option is to determine or assign a priority of the threads so that only one (or a few) thread backs up. The rest of the threads continue taking the locks they need as if no deadlock had occurred.

- If the priority assigned to the threads is fixed, the same threads will always be given higher priority. To avoid this you may assign the priority randomly whenever a deadlock is detected.

## Starvation and Fairness

If a thread is not granted CPU time because other threads grab it all, it is called "starvation". The thread is "starved to death" because other threads are allowed the CPU time instead of it.
### Causes of Starvation in Java

Threads with high priority swallow all CPU time from threads with lower priority.
Threads are blocked indefinitely waiting to enter a synchronized block, because other threads are constantly allowed access before it.
Threads waiting on an object (called wait() on it) remain waiting indefinitely because other threads are constantly awakened instead of it.

#### Threads with high priority swallow all CPU time from threads with lower priority.

You can set the thread priority of each thread individually. The higher the priority the more CPU time the thread is granted. -> **between 1 and 10**.

#### Threads are blocked indefinitely waiting to enter a synchronized block

synchronized code blocks can be another cause of starvation Java's synchronized code block makes no guarantee about the sequence in which threads waiting to enter the synchronized block are allowed to enter. This means that there is a theoretical risk that a thread remains blocked forever trying to enter the block, because other threads are constantly granted access before it.

#### Threads waiting on an object (called ``wait()`` on it) remain waiting indefinitely

The ``notify()`` method makes no guarantee about what thread is awakened if multiple thread have called wait() on the object ``notify()`` is called on. It could be any of the threads waiting. Therefore there is a risk that a thread waiting on a certain object is never awakened because other waiting threads are always awakened instead of it.

### Implementing Fairness in Java

it is not possible to implement 100% fairness in Java

```java
public class Synchronizer{

  public synchronized void doSynchronized(){
    //do a lot of work which takes a long time
  }

}
```

If more than one thread call the ``doSynchronized()`` method, some of them will be blocked until the first thread granted access has left the method.
If more than one thread are blocked waiting for access there is no guarantee about which thread is granted access next.

#### Using Locks Instead of Synchronized Blocks

To increase the fairness of waiting threads first we will change the code block to be guarded by a lock rather than a synchronized block:

```java
public class Synchronizer{
  Lock lock = new Lock();

  public void doSynchronized() throws InterruptedException{
    this.lock.lock();
      //critical section, do a lot of work which takes a long time
    this.lock.unlock();
  }

}
```

the ``doSynchronized()`` method is no longer declared synchronized. Instead the critical section is guarded by the ``lock.lock()`` and ``lock.unlock()`` calls.

```java
public class Lock{
  private boolean isLocked      = false;
  private Thread  lockingThread = null;

  public synchronized void lock() throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked      = true;
    lockingThread = Thread.currentThread();
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    notify();
  }
}
```

the Lock class implements a locking mechanism using the wait() and notify() methods.
When multiple threads attempt to acquire the lock simultaneously, they may end up waiting in the wait() call inside the lock() method. If the critical section within the lock takes a long time to execute, most of the waiting time is spent inside the wait() call.

The current implementation doesn't guarantee fairness, similar to synchronized blocks.  However, fairness can be introduced by having each thread call wait() on a separate object. This way, the Lock class can selectively call notify() on a specific object, determining which thread to awaken. 
### A Fair Lock

```java
public class FairLock {
    private boolean           isLocked       = false;
    private Thread            lockingThread  = null;
    private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject           = new QueueObject();
    boolean     isLockedForThisThread = true;
    synchronized(this){
        waitingThreads.add(queueObject);
    }

    while(isLockedForThisThread){
      synchronized(this){
        isLockedForThisThread =
            isLocked || waitingThreads.get(0) != queueObject;
        if(!isLockedForThisThread){
          isLocked = true;
           waitingThreads.remove(queueObject);
           lockingThread = Thread.currentThread();
           return;
         }
      }
      try{
        queueObject.doWait();
      }catch(InterruptedException e){
        synchronized(this) { waitingThreads.remove(queueObject); }
        throw e;
      }
    }
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    if(waitingThreads.size() > 0){
      waitingThreads.get(0).doNotify();
    }
  }
}
```

The FairLock class implements a fair locking mechanism using a queue of waiting threads. 
Each thread calling lock() enqueues a ``QueueObject``. The first thread in the queue is allowed to lock the ``FairLock`` instance, while others wait until their turn.

```java
public class QueueObject {

  private boolean isNotified = false;

  public synchronized void doWait() throws InterruptedException {
    while(!isNotified){
        this.wait();
    }
    this.isNotified = false;
  }

  public synchronized void doNotify() {
    this.isNotified = true;
    this.notify();
  }

  public boolean equals(Object o) {
    return this == o;
  }
}
```

## How Nested Monitor Lockout Occurs

Nested Monitor Lockout occurs when a thread attempts to acquire a lock that it already holds.  when a thread holds a lock and tries to enter a synchronized block or method that requires the same lock, it will succeed in acquiring the lock without blocking itself.

```java
Thread 1 synchronizes on A
Thread 1 synchronizes on B (while synchronized on A)
Thread 1 decides to wait for a signal from another thread before continuing
Thread 1 calls B.wait() thereby releasing the lock on B, but not A.

Thread 2 needs to lock both A and B (in that sequence)
        to send Thread 1 the signal.
Thread 2 cannot lock A, since Thread 1 still holds the lock on A.
Thread 2 remain blocked indefinately waiting for Thread1
        to release the lock on A

Thread 1 remain blocked indefinately waiting for the signal from
        Thread 2, thereby
        never releasing the lock on A, that must be released to make
        it possible for Thread 2 to send the signal to Thread 1, etc.
```

```java
//lock implementation with nested monitor lockout problem

public class Lock{
  protected MonitorObject monitorObject = new MonitorObject();
  protected boolean isLocked = false;

  public void lock() throws InterruptedException{
      synchronized(this){
      while(isLocked){
        synchronized(this.monitorObject){
            this.monitorObject.wait();
        }
      }
      isLocked = true;
    }
  }

  public void unlock(){
    synchronized(this){
      this.isLocked = false;
      synchronized(this.monitorObject){
        this.monitorObject.notify();
      }
    }
  }
}
```

### Nested Monitor Lockout vs. Deadlock

The threads involved end up blocked forever waiting for each other.
The two situations are not equal though a deadlock occurs when two threads obtain locks in different order.

a nested monitor lockout occurs exactly by two threads taking the locks in "the same order".

- In deadlock, two threads are waiting for each other to release locks.

- In nested monitor lockout, Thread 1 is holding a lock A, and waits
	for a signal from Thread 2. Thread 2 needs the lock A to send the
	signal to Thread 1.

##  Locks in Java

A lock is a thread synchronization mechanism like synchronized blocks except locks can be more sophisticated
### A Simple Lock

```JAVA
public class Counter{

  private int count = 0;

  public int inc(){
    synchronized(this){
      return ++count;
    }
  }
}
```

The Counter class could have been written like this instead, using a Lock instead of a synchronized block:

```java
public class Counter{

  private Lock lock = new Lock();
  private int count = 0;

  public int inc(){
    lock.lock();
    int newCount = ++count;
    lock.unlock();
    return newCount;
  }
}
```

```java
public class Lock{

  private boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
	while(isLocked){
	  wait();
	}
	isLocked = true;
  }

  public synchronized void unlock(){
	isLocked = false;
	notify();
  }
}
```

When the thread is done with the code in the critical section (the code between ``lock()`` and ``unlock()``), the thread calls ``unlock()``.  Executing ``unlock()`` sets ``isLocked`` back to false, and notifies (awakens) one of the threads waiting in the ``wait()`` call in the ``lock()`` method, if any.

### Lock Reentrance

Synchronized blocks in Java are reentrant.
This means, that if a Java thread enters a synchronized block of code, and thereby take the lock on the monitor object the block is synchronized on, the thread can enter other Java code blocks synchronized on the same monitor object.

 >**When a Java thread enters a synchronized block of code and acquires the lock on the associated monitor object, it gains the ability to enter other synchronized code blocks that also use the same monitor object for synchronization.** 
 >**This is because the thread already holds the lock for that monitor object, allowing it to proceed into any synchronized block that shares the same monitor.** 
  >**In essence, the lock on the monitor object provides exclusive access to all synchronized blocks synchronized on that particular object.**
  
```java
public class ReentrantExample {

	public synchronized void outer() {
		inner();
	}
	
	public synchronized void inner() {
		// do something
	}
}
```

both ``outer()`` and ``inner()`` methods are synchronized, and they use the same monitor object (this). If a thread calls ``outer()``, it can freely call ``inner()`` without any issues, thanks to reentrancy. However, in contrast, the Lock class shown earlier is not inherently reentrant. Here's a modified version of the Lock class to make it reentrant:

```java
public class ReentrantLock {
	private boolean isLocked = false;
	private Thread lockedBy = null;
	private int lockedCount = 0;

	public synchronized void lock() throws InterruptedException {
		Thread callingThread = Thread.currentThread();
		while (isLocked && lockedBy != callingThread) {
			wait();
		}
		isLocked = true;
		lockedCount++;
		lockedBy = callingThread;
	}

	public synchronized void unlock() {
		if (Thread.currentThread() == lockedBy) {
			lockedCount--;

			if (lockedCount == 0) {
				isLocked = false;
				notify();
			}
		}
	}
}
```

This modified Lock class checks whether the calling thread is the one that locked it, making it reentrant.
Additionally, it keeps track of the number of times the lock has been acquired, ensuring it is properly released when the thread calls ``unlock()`` an equal number of times.
### Lock Fairness

synchronized blocks do not guarantee the order in which threads are granted access.  This lack of order can lead to a situation called "starvation," where some threads may be consistently denied access to a synchronized block, always losing to other threads competing for the same resource. Fairness in a lock ensures that threads are granted access in a more orderly manner.

The Lock implementations here, which use synchronized blocks internally, do not guarantee fairness. As a result, there's a risk of potential starvation when multiple threads contend for the same lock.
### Calling ``unlock()`` From a finally-clause

When using a Lock to guard a critical section in Java, especially when the critical section may throw exceptions, it's crucial to call the ``unlock()`` method from within a finally clause.  This ensures that the Lock is always unlocked, allowing other threads to acquire it.

```java
lock.lock();
try {
  // Critical section code that may throw exceptions
} finally {
  lock.unlock();
}
```

By employing this pattern, even if an exception occurs within the critical section, the ``unlock()`` method is guaranteed to be called, preventing the Lock from remaining locked indefinitely.  Without the finally clause, an exception could lead to the Lock staying locked, causing all subsequent threads attempting to ``lock()`` on that instance to become blocked indefinitely.

## Read / Write Locks in Java

In scenarios where reading a resource is more frequent than writing to it, a read/write lock provides an efficient solution. Multiple threads can simultaneously read the resource without causing conflicts, but exclusive access is ensured when a single thread wants to write to the resource.

The key idea is to allow concurrent reads while ensuring exclusive access for writing, balancing efficiency and consistency.

### Read / Write Lock Java Implementation

- **Read Access**:   	If no threads are writing, and no threads have requested write access.
- **Write Access**:   	If no threads are reading or writing.

In a read/write lock scenario, a thread seeking to read a resource is allowed if no threads are currently writing to it or have requested write access. Giving priority to write-access requests assumes that write requests are more critical than read requests. Additionally, prioritizing writes helps prevent potential starvation issues.

If read requests are continually granted without prioritizing writes, threads waiting for write access could be blocked indefinitely, leading to starvation.

For a thread to be granted read access, there must be no ongoing write operations, and no threads should have requested the lock for writing. On the other hand, a thread seeking write access can be granted if no threads are currently reading or writing to the resource.  The sequence or number of threads requesting write access is generally not a concern, unless fairness between such threads is a priority.

```java
public class SharedResource {
	private int data = 0;
	private ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

	public int readData() {
		readWriteLock.readLock().lock();
		try {
			// Reading from the shared resource
			return data;
		} finally {
			readWriteLock.readLock().unlock();
		}
	}

	public void writeData(int newValue) {
		readWriteLock.writeLock().lock();
		try {
			// Writing to the shared resource
			data = newValue;
		} finally {
			readWriteLock.writeLock().unlock();
		}
	}
}
```

## Reentrance Lockout

Reentrance lockout is a situation similar to deadlock and nested monitor lockout. Reentrance lockout may occur if a thread reenters a Lock, ``ReadWriteLock`` or some other synchronizer that is not reentrant. Reentrant means that a thread that already holds a lock can retake it.

```java
public class ReentrantLockoutExample {

	private final Object lock = new Object();

	public void outer() {
		synchronized (lock) {
			inner();  // calling another synchronized method
		}
	}

	public void inner() {
		synchronized (lock) {
			// Some critical section code
		}
	}

	public static void main(String[] args) {
		ReentrantLockoutExample example = new ReentrantLockoutExample();

		// Create two threads calling outer method
		Thread thread1 = new Thread(() -> example.outer());
		Thread thread2 = new Thread(() -> example.outer());

		// Start the threads
		thread1.start();
		thread2.start();
	}
}
```

## Semaphores

A semaphore is a synchronization construct used in concurrent programming to control access to a shared resource. It maintains a set of permits, and threads that need access to the resource must acquire a permit before proceeding. Once the thread is done with the resource, it releases the permit, making it available for other threads.

### Key concepts:

- **Permits**: Semaphores have a fixed number of permits, which control the number of threads that can concurrently access the shared resource.

- **Acquiring and Releasing Permits**
	- **``Acquire()``**: A thread requests a permit from the semaphore. If a permit is available, it's granted, and the thread continues. If not, the thread may be blocked or put into a waiting state until a permit becomes available.
	- **``Release()``**: When a thread is done using the resource, it releases the permit, making it available for other threads.
- **Counting Semaphores**: Semaphores can be either counting semaphores or binary semaphores.
	- **Counting Semaphore**: Permits can be any non-negative integer, allowing multiple threads to access the resource simultaneously, up to the total number of permits. 
	- **Binary Semaphore (Mutex)**: Limited to two states (0 or 1), essentially acting as a mutual exclusion mechanism, allowing only one thread to access the resource at a time.
- **Uses**
	- **Resource Management**: Semaphores are often used to control access to a pool of resources.
	- **Thread Synchronization**: Ensuring that certain sections of code are accessed by a limited number of threads simultaneously.

```java
import java.util.concurrent.Semaphore;
public class SemaphoreExample {
	public static void main(String[] args) {
		// Creating a counting semaphore with 3 permits
		Semaphore semaphore = new Semaphore(3);

		// Creating and starting 5 threads
		for (int i = 1; i <= 5; i++) {
			Thread thread = new Thread(new Worker(semaphore, i));
			thread.start();
		}
	}

	static class Worker implements Runnable {
		private final Semaphore semaphore;
		private final int workerId;

		Worker(Semaphore semaphore, int workerId) {
			this.semaphore = semaphore;
			this.workerId = workerId;
		}

		@Override
		public void run() {
			try {
				System.out.println("Worker " + workerId + " is trying to acquire a permit.");
				semaphore.acquire();
				System.out.println("Worker " + workerId + " has acquired a permit.");
				
				// Simulating some work being done
				Thread.sleep(2000);
				
				System.out.println("Worker " + workerId + " is releasing the permit.");
				semaphore.release();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

## Blocking Queues

is a queue that blocks when you try to dequeue from it and the queue is empty, or if you try to enqueue items to it and the queue is already full. A thread trying to dequeue from an empty queue is blocked until some other thread inserts an item into the queue.  A thread trying to enqueue an item in a full queue is blocked until some other thread makes space in the queue, either by dequeuing one or more items or clearing the queue completely.

![[Pasted image 20240210153154.png]]

```java
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

public class BlockingQueueExample {

	public static void main(String[] args) {
		// Creating a LinkedBlockingQueue with a maximum capacity of 5
		BlockingQueue<String> blockingQueue = new LinkedBlockingQueue<>(5);

		// Creating and starting producer and consumer threads
		Thread producerThread = new Thread(new Producer(blockingQueue));
		Thread consumerThread = new Thread(new Consumer(blockingQueue));

		producerThread.start();
		consumerThread.start();
	}

	// Producer thread that adds elements to the blocking queue
	static class Producer implements Runnable {
		private final BlockingQueue<String> blockingQueue;

		Producer(BlockingQueue<String> blockingQueue) {
			this.blockingQueue = blockingQueue;
		}

		@Override
		public void run() {
			try {
				for (int i = 1; i <= 10; i++) {
					String message = "Message " + i;
					blockingQueue.put(message); // Blocking if the queue is full
					System.out.println("Produced: " + message);
					Thread.sleep(1000);
				}
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}

	// Consumer thread that removes elements from the blocking queue
	static class Consumer implements Runnable {
		private final BlockingQueue<String> blockingQueue;

		Consumer(BlockingQueue<String> blockingQueue) {
			this.blockingQueue = blockingQueue;
		}

		@Override
		public void run() {
			try {
				while (true) {
					String message = blockingQueue.take(); // Blocking if the queue is empty
					System.out.println("Consumed: " + message);
				}
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

the Producer thread produces messages (strings) and puts them into the blocking queue. The Consumer thread consumes messages by taking them from the blocking queue. The put and take methods on the blocking queue ensure that the producer blocks when the queue is full and the consumer blocks when the queue is empty.

## The Producer Consumer Pattern

is a concurrency design pattern where one or more producer threads produce objects which are queued up, and then consumed by one or more consumer threads. The objects enqueued often represent some work that needs to be done. Decoupling the detection of work from the execution of work means you can control how many threads at a time that are engaged in detecting or executing the work.

![[Pasted image 20240210153339.png]]

### Use Cases

Most common ones:
- **Reduce foreground thread latency.**
- **Load balance work between different threads.**
- **Backpressure management.**

#### Reduce Foreground Thread Latency

In some systems you have a single foreground thread which has the communication with the outside world.
In a server it could be the thread accepting the incoming connections from clients. In a desktop app that could be the UI thread.

In order to not make the foreground thread busy with tasks - whatever tasks the foreground thread receives from the outside world are offloaded to one or more background threads.  In a server it could be processing the data that is received via the inbound connections.

#### Load Balance Work Between Threads

is to load balance work between a set of worker threads.  Actually, this load balancing happens pretty much automatically, as long as the worker threads take new task objects from the queue as soon as they have time to process them. This will result in load balancing the tasks between the worker threads.

#### Backpressure Management

If the queue between the producer and consumer threads is a Java ``BlockingQueue``, then you can use the queue for backpressure management. Backpressure means, that if the producer thread(s) produce more work than the consumer threads are able to handle - the tasks will queue up in the queue.  At some point the ``BlockingQueue`` will become full, and the producer threads will be blocked trying to insert new tasks / work objects into the queue.  This phenomenon is called "backpressure".

The system presses back against the producers - towards the beginning of the "pipeline" - preventing more work from coming in. The backpressure will "spill out" of the queue, and slow down the producer thread(s).
Thus, they too could propagate the pressure back up the work pipeline, if there are any earlier steps in the total pipeline.

## Thread Pools

is a pool threads that can be "reused" to execute tasks, so that each thread may execute more than one task.
A thread pool is an alternative to creating a new thread for each task you need to execute.

Creating a new thread comes with a performance overhead compared to reusing a thread that is already created.  That is why reusing an existing thread to execute a task can result in a higher total throughput than creating a new thread per task.

Additionally, using a thread pool can make it easier to control how many threads are active at a time.
Each thread consumes a certain amount of computer resources, such as memory (RAM).

![[Pasted image 20240210153722.png]]
### How a Thread Pool Works

Instead of starting a new thread for every task to execute concurrently, the task can be passed to a thread pool.
As soon as the pool has any idle threads the task is assigned to one of them and executed. Internally the tasks are inserted into a Blocking Queue which the threads in the pool are dequeuing from.

When a new task is inserted into the queue one of the idle threads will dequeue it successfully and execute it.
The rest of the idle threads in the pool will be blocked waiting to dequeue tasks.
### Thread Pool Use Cases

Thread pools are often used in multi threaded servers.
Each connection arriving at the server via the network is wrapped as a task and passed on to a thread pool.
The threads in the thread pool will process the requests on the connections concurrently.

### Thread Pool Example

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {

	public static void main(String[] args) {
		// Create a thread pool with three worker threads
		ExecutorService executorService = Executors.newFixedThreadPool(3);

		// Submit tasks to the thread pool
		for (int i = 1; i <= 5; i++) {
			final int taskId = i;
			executorService.submit(() -> {
				// Task execution logic
				System.out.println("Task " + taskId + " is being processed by thread: " +
						Thread.currentThread().getName());
			});
		}

		// Shutdown the thread pool when tasks are completed
		executorService.shutdown();
	}
}
```

## Thread Congestion in Java

Thread congestion can occur when two or more threads are trying to access the same, guarded data structure at the same time. By "guarded" means that the data structure is guarded using synchronized blocks or a concurrent data structure (Lock, ``BlockingQueue`` etc.) so that the data structure is thread safe.

The resulting thread congestion means that the threads trying to access the shared data structure are spending a high amount of time waiting in line to access the data structure - wasting valuable execution time on waiting.

![[Pasted image 20240210153931.png]]

### Thread Blocking Data Structures May Cause Thread Congestion

A data structure which blocks threads from accessing it - depending on what other threads are currently accessing it - may cause thread congestion. If more than one thread accesses such a data structure at the same time, one or more of the threads may be queued up waiting to access the data structure.

This queuing up is not visible in your code. The queuing up happens inside the Java VM. Therefore thread congestion is not so easy to spot simply by looking at your code. may need profiling tools to detect thread congestion
### A Blocked Thread Loses Execution Time

While a thread is blocked trying to execute a blocking data structure, it cannot do anything.
Thus, while being blocked the thread loses possible execution time. The longer the thread is blocked, the more potential execution time it loses.
### The More Threads - The Higher Congestion

The more threads that attempt to access a shared, blocking data structure, the higher the risk is of thread congestion occurring, and the higher the congestion may be
### Alleviating Thread Congestion

To alleviate thread congestion you must reduce the number of threads trying to access the blocking data structure at exactly the same time.

#### Multiple Data Structures

One way to alleviate thread congestion - at least around blocking queues - is to give each consuming thread its own queue, and have the producing thread distribute the objects (e.g. tasks) among these blocking queues. 
This way, only 2 threads are ever accessing each queue: The producing thread and the consuming thread.

![[Pasted image 20240210154151.png]]

#### Non-blocking Concurrency Algorithms

Another way is to use non-blocking concurrency algorithms where the threads accessing the data structure are never blocked.

## Compare and Swap

is a technique used when designing concurrent algorithms. Basically, compare and swap compares the value of a variable with an expected value, and if the values are equal then swaps the value of the variable for a new value.
### Compare and Swap for Check Then Act Cases

A commonly occurring pattern in concurrent algorithms is the check then act pattern The check then act pattern occurs when the code first checks the value of a variable and then acts based on that value.

```java
import java.util.concurrent.atomic.AtomicBoolean;

public class SafeLock {

	private final AtomicBoolean locked = new AtomicBoolean(false);

	public void lock() {
		while (!locked.compareAndSet(false, true)) {
			// busy wait - until locked is false
		}
	}

	public void unlock() {
		locked.set(false);
	}
}
```

The ``lock()`` method checks if locked is false and, if true, sets it to true.
In a multi-threaded scenario, multiple threads might simultaneously check and set the locked variable.
This creates a race condition where multiple threads can enter the critical section concurrently, defeating the purpose of the lock.

### Check Then Act - Must Be Atomic

In a multithreaded application, for check-then-act operations to be thread-safe and avoid race conditions, the operations must be atomic.  Atomicity ensures that both the check and act actions are executed without interference from other threads. One way to achieve atomicity in Java is by using the synchronized keyword to create a synchronized block of code.

```java
public class ProblematicLock {
	private volatile boolean locked = false;

	public synchronized void lock() {
		while(this.locked) {
			// busy wait - until this.locked == false
		}
		this.locked = true;
	}

	public void unlock() {
		this.locked = false;
	}
}
```

the ``lock()`` method is effectively atomic, ensuring that only one thread can execute it at a time on the same ``ProblematicLock`` instance.

### Blocking Threads is Expensive

When two threads try to enter a synchronized block in Java at the same time, one of the threads will be blocked, and the other thread will allowed to enter the synchronized block.  When the thread that entered the synchronized block exits the block again, a waiting thread will be allowed to enter the block.

Entering a synchronized block is not that expensive - if the thread is allowed access. But if the thread is blocked because another thread is already executing inside the synchronized block - the blocking of the thread is expensive.

Additionally, you do not have any guarantee about exactly when a blocked thread is unblocked when the synchronized block is free again.  This is typically up to the OS or execution platform to coordinate the unblocking of blocked threads.

Of course it will not take seconds or minutes before a blocked thread is unblocked and allowed to enter, but some amount of time can be wasted for the blocked thread where it could have accessed the shared data structure.

### Hardware Provided Atomic Compare And Swap Operations

Modern CPUs offer built-in support for atomic compare-and-swap operations, providing a way to replace synchronized blocks or other blocking data structures. With compare-and-swap, the CPU ensures that only one thread can execute the operation at a time, even across CPU cores. This eliminates the need for the operating system or execution platform to handle thread blocking and unblocking.

In situations where hardware-provided compare-and-swap functionality is used, the thread attempting to access a shared data structure is not fully blocked. Instead, it continuously tries to execute the compare-and-swap operation until it succeeds, minimizing the delay before accessing the shared data structure This results in shorter waiting times, less congestion, and higher throughput

### Compare and Swap in Java

The advantage of using the compare and swap features that comes with Java 5+ rather than implementing your own is that  the compare and swap features built into Java 5+ lets you utilize the underlying compare and swap features of the CPU your application is running on. This makes your compare and swap code faster.

### Compare And Swap as Guard

It is also possible to use compare and swap functionality as an optimistic locking mechanism. An optimistic locking mechanism allows more than one thread to enter a critical section at a time, but only allows one of the threads to commit its work at the end of the critical section.

```java
import java.util.concurrent.atomic.AtomicLong;

public class OptimisticLockCounter {

	private AtomicLong count = new AtomicLong();

	public void inc() {
		boolean incSuccessful = false;
		while (!incSuccessful) {
			long value = this.count.get();
			long newValue = value + 1;

			incSuccessful = this.count.compareAndSet(value, newValue);
		}
	}

	public long getCount() {
		return this.count.get();
	}
}
```
## Anatomy of a Synchronizer

Even if many synchronizers (locks, semaphores, blocking queue etc.) are different in function, they are often not that different in their internal design. they consist of the same (or similar) basic parts internally.
### State

The state of a synchronizer is used by the access condition to determine if a thread can be granted access.
- In a Lock the state is kept in a boolean saying whether the Lock is locked or not. 
- In a Bounded Semaphore the internal state is kept in a counter (int) and an upper bound (int) which state the current number of "takes" and the maximum number of "takes".
-  In a Blocking Queue the state is kept in the List of elements in the queue and the maximum queue size (int) member (if any).

### Access Condition

The access conditions is what determines if a thread calling a test-and-set-state method can be allowed to set the state or not.  The access condition is typically based on the state of the synchronizer. The access condition is typically checked in a while loop to guard against Spurious Wakeups. When the access condition is evaluated it is either true or false.

In a Lock the access condition simply checks the value of the ``isLocked`` member variable. In a Bounded Semaphore there are actually two access conditions depending on whether you are trying to "take" or "release" the semaphore. If a thread tries to take the semaphore the signals variable is checked against the upper bound.
If a thread tries to release the semaphore the signals variable is checked against 0.

### State Changes

Once a thread gains access to the critical section it has to change the state of the synchronizer to (possibly) block other threads from entering it.
In other words, the state needs to reflect the fact that a thread is now executing inside the critical section.
This should affect the access conditions of other threads attempting to gain access.

In a Lock the state change is the code setting ``isLocked = true``. In a semaphore it is either the code signals-- or signals++
### Notification Strategy

Once a thread has changed the state of a synchronizer it may sometimes need to notify other waiting threads about the state change. Perhaps this state change might turn the access condition true for other threads.
Notification Strategies typically fall into three categories.

- Notify all waiting threads.
-  Notify 1 random of N waiting threads.
- Notify 1 specific of N waiting thread.
	
Notifying all waiting threads is pretty easy. All waiting threads call wait() on the same object. Once a thread want to notify the waiting threads it calls notifyAll() on the object the waiting threads called wait() on.

Notifying a single random waiting thread is also pretty easy. Just have the notifying thread call notify() on the object the waiting threads have called wait() on. Calling notify makes no guarantee about which of the waiting threads will be notified. Hence the term "random waiting thread".

Sometimes you may need to notify a specific rather than a random waiting thread. For instance if you need to guarantee that waiting threads are notified in a specific order, be it the order they called the synchronizer in, or some prioritized order. To achieve this each waiting thread must call wait() on its own, separate object. When the notifying thread wants to notify a specific waiting thread it will call notify() on the object this specific thread has called ``wait()`` on.
### Test and Set Method

Synchronizer most often have two types of methods of which test-and-set is the first type (set is the other).
Test-and-set means that the thread calling this method tests the internal state of the synchronizer against the access condition. If the condition is met the thread sets the internal state of the synchronizer to reflect that the thread has gained access.

The state transition usually results in the access condition turning false for other threads trying to gain access, but may not always do so It is imperative that the test-and-set operations are executed atomically meaning no other threads are allowed to execute in the test-and-set method in between the test and the setting of the state.

The program flow of a test-and-set method is usually something along the lines of:

- Set state before test if necessary
- Test state against access condition
- If access condition is not met, wait
- If access condition is met, set state, and notify waiting threads if necessary

### Set Method

The set method is the second type of method that synchronizers often contain. The set method just sets the internal state of the synchronizer without testing it first. A typical example of a set method is the ``unlock()`` method of a Lock class. A thread holding the lock can always unlock it without having to test if the Lock is unlocked.
The program flow of a set method is usually along the lines of:

- Set internal state
- Notify waiting threads

## Non-blocking Algorithms

in the context of concurrency are algorithms that allows threads to access shared state (or otherwise collaborate or communicate) without blocking the threads involved. In more general terms, an algorithm is said to be non-blocking if the suspension of one thread cannot lead to the suspension of other threads involved in the algorithm.
### Blocking Concurrency Algorithms

is an algorithm which either:

- A: Performs the action requested by the thread - OR
- B: Blocks the thread until the action can be performed safely

Many types of algorithms and concurrent data structures are blocking.

![[Pasted image 20240211103420.png]]

### Non-blocking Concurrency Algorithms

is an algorithm which either:

- A: Performs the action requested by the thread - OR
- B: Notifies the requesting thread that the action could not be performed

![[Pasted image 20240211103533.png]]

### Non-blocking vs Blocking Algorithms

- Blocking algorithms block the thread until the requested action can be performed, potentially leading to indefinite blocking if conditions are not met. 
- Non-blocking algorithms, on the other hand, notify the requesting thread that the action cannot be performed, allowing the thread to handle the situation without waiting indefinitely.

### Non-blocking Concurrent Data Structures

In a multithreaded system, threads communicate through various data structures, ranging from simple variables to complex structures like queues and maps. For proper concurrent access, these data structures require guarding by concurrent algorithms.  If the guarding algorithm involves thread suspension, it is considered a blocking algorithm, resulting in a blocking concurrent data structure.

Conversely, if the guarding algorithm is non-blocking, it is a non-blocking algorithm, leading to a non-blocking concurrent data structure. The choice of a concurrent data structure depends on communication needs, and the following sections will explore non-blocking concurrent data structures, providing insights into their design and implementation.

### Volatile Variables

Java volatile variables ensure that their values are always read directly from main memory. 
When a new value is assigned to a volatile variable, it is immediately written to main memory, guaranteeing that the latest value is visible to other threads running on different CPUs.  This eliminates the reliance on CPU caches and ensures consistent visibility across threads.

Volatile variables offer non-blocking behavior, as writing a value to a volatile variable is an atomic operation, preventing interruptions.  However, a read-update-write sequence on a volatile variable is not atomic.

```java
volatile myVar = 0;

...
int temp = myVar;
temp++;
myVar = temp;
```

the value of the volatile variable ``myVar`` is read into a temporary variable, incremented, and then written back to main memory. If two threads execute this code concurrently, there is a risk of a race condition, where both threads read, increment, and write back the same value, potentially resulting in an incorrect final value. This scenario is analogous to the more concise expression ``myVar++``.
#### The Single Writer Case

In scenarios where only a single thread is responsible for updating a shared variable, and multiple threads are involved in reading its value, race conditions can be avoided.  In such cases, using a volatile variable is appropriate, as the visibility guarantees provided by volatile variables are sufficient to maintain consistency when there is only one writer.

```java
public class SingleWriterCounter {

    private volatile long count = 0;

    /**
     * Only one thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void inc() {
        this.count++;
    }


    /**
     * Many reading threads may call this method
     * @return
     */
    public long count() {
        return this.count;
    }
}
```

Multiple threads can access the same instance of this counter, as long as only one thread calls ``inc()``. The ``count()`` method can be called by multiple threads without causing race conditions. The use of the volatile keyword ensures that the latest value of the count variable is always visible to reading threads, even if there is only one writing thread.

![[Pasted image 20240211104029.png]]

#### More Advanced Data Structures Based on Volatile Variables

In scenarios where multiple threads need to communicate through non-blocking means, it is possible to design data structures using combinations of volatile variables. Each volatile variable is written by a single thread and read by multiple threads, providing a mechanism for threads to exchange information without blocking.

```java
public class DoubleWriterCounter {

    private volatile long countA = 0;
    private volatile long countB = 0;

    /**
     * Only one (and the same from thereon) thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void incA() { this.countA++;  }


    /**
     * Only one (and the same from thereon) thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void incB() { this.countB++;  }


    /**
     * Many reading threads may call this method
     */
    public long countA() { return this.countA; }


    /**
     * Many reading threads may call this method
     */
    public long countB() { return this.countB; }
}
```

``incA()`` and ``incB()`` methods are meant to be called by a single thread each, preventing race conditions. Multiple threads are allowed to call ``countA()`` and ``countB()`` without causing race conditions. This design enables two threads to communicate by exchanging counts. It's worth noting that, in practice, using separate instances of a single writer counter class might achieve a similar effect.

![[Pasted image 20240211104346.png]]

### Optimistic Locking With Compare and Swap

In scenarios where exclusive access to a shared variable is needed, using a volatile variable alone is insufficient. 
Exclusive access can be achieved using synchronized blocks,

```java
public class SynchronizedCounter {
    long count = 0;

    public void inc() {
        synchronized(this) {
            count++;
        }
    }

    public long count() {
        synchronized(this) {
            return this.count;
        }
    }
}
```

In the above example, both the ``inc()`` and ``count()`` methods contain synchronized blocks. However, to avoid the use of synchronized blocks, an alternative approach is to use an atomic variable, such as ``AtomicLong``

```java
import java.util.concurrent.atomic.AtomicLong;

public class AtomicCounter {
	private AtomicLong count = new AtomicLong(0);

	public void inc() {
		boolean updated = false;
		while (!updated) {
			long prevCount = this.count.get();
			updated = this.count.compareAndSet(prevCount, prevCount + 1);
		}
	}

	public long count() {
		return this.count.get();
	}
}
```

In this version, the ``inc()`` method no longer contains a synchronized block. Instead, it utilizes the ``compareAndSet()`` method provided by ``AtomicLong`` This method performs an atomic compare-and-swap operation, which avoids the need for synchronization and thread suspension The ``compareAndSet()`` method is typically supported by atomic instructions in the CPU.

The ``inc()`` method checks whether the update was successful through a while loop.  If another thread modifies the ``AtomicLong`` between reading the previous count and attempting to update it, the ``compareAndSet()`` call will fail, and the loop will be repeated.  This ensures that only one thread successfully increments the counter at a time, avoiding race conditions.
#### Why is it Called Optimistic Locking?

because it operates under the optimistic assumption that conflicts or contention for shared resources will be infrequent. In this approach, threads are optimistic that they can proceed with their modifications to shared memory without the need for blocking or obtaining exclusive locks. The term "optimistic" reflects the positive outlook that conflicts will be rare.

In contrast, traditional or pessimistic locking involves blocking access to shared memory using locks or synchronized blocks, even for read operations. Pessimistic locking assumes that conflicts are likely, and therefore, it takes a more conservative approach by blocking threads to prevent concurrent modifications.

Optimistic locking allows multiple threads to independently make copies of shared data, modify their copies, and then attempt to update the shared data without immediate synchronization. This approach is suitable when contention is expected to be low or infrequent. However, if contention is high, and multiple threads are likely to modify the shared data simultaneously, optimistic locking may result in wasted effort as threads may need to retry updating the shared data.

#### Optimistic Locking is Non-blocking

In an optimistic locking approach, threads are allowed to perform operations on shared data independently without immediately acquiring locks or causing blocking for other threads. Contrastingly, in traditional locking paradigms (e.g., using synchronized blocks or locks), when a thread acquires a lock, it prevents other threads from accessing the same locked resource until the lock is released. If the thread holding the lock gets blocked or delayed for some reason, it can lead to potential contention and increased wait times for other threads attempting to access the same resource.

The non-blocking nature of optimistic locking allows threads to proceed with their operations independently, minimizing contention and enabling concurrency. Even if a thread encounters a conflict during the attempt to update shared data, it can retry without causing blockages for other threads.

This non-blocking characteristic is one of the advantages of optimistic locking in scenarios where contention is expected to be low, and conflicts are assumed to be infrequent. It can lead to better overall system throughput and responsiveness compared to traditional blocking approaches in certain situations.

### Non-swappable Data Structures

Non-swappable data structures are those where replacing the entire structure during updates is impractical.
In these cases, non-blocking strategies are employed to enable concurrent updates without copying the entire structure.  This is achieved by using atomic operations on specific elements or references within the structure, allowing independent updates without blocking the entire data set. The key is to design these structures carefully to minimize contention and avoid unnecessary overhead during modifications.

#### Completable Intended Modifications

In a non-blocking algorithm using completable intended modifications, each submitted modification must contain sufficient information for another thread to complete it.  This design ensures that if the original thread doesn't complete the modification, another thread can step in and finish it.  The completion process involves one or more compare-and-swap operations, ensuring that only one thread can successfully execute these operations.

The blueprint of this non-blocking algorithm involves submitting intended modifications, which can be completed by other threads through compare-and-swap operations.  This approach prevents a single modification from locking the shared data structure, allowing multiple threads to work concurrently.

### The A-B-A Problem

This problem occurs when a variable is changed from A to B and then back to A again, making it challenging for another thread to detect the change.  if thread A is suspended after checking for ongoing updates and copying data, thread B may perform a full update in the meantime.

If thread B successfully updates the data structure and removes its intended modification, when thread A resumes, it might not detect any modification since it copied the data structure.  However, a modification did occur during the suspension of thread A. Consequently, when thread A continues its update based on the outdated copy, it unintentionally undoes the modification made by thread B
#### A-B-A Solutions

a common solution is to use a combination of a pointer and a counter.  This involves swapping a pointer to an intended modification object along with a counter using a single compare-and-swap operation. In Java, where you cannot directly merge a reference and a counter into a single variable, the ``AtomicStampedReference`` class is provided.  This class allows you to atomically swap a reference and a stamp (counter) using a compare-and-swap operation, preventing the A-B-A problem.
### A Non-blocking Algorithm Template

Non-blocking algorithms are designed to allow multiple threads to operate concurrently on shared data structures without the need for locks or other blocking mechanisms.  The key idea is to enable progress even when contention or conflicts occur among threads.

#### Optimistic Concurrency Control

Non-blocking algorithms often employ optimistic concurrency control, where threads perform operations assuming that there will be no interference from other threads. Threads make modifications locally and then use atomic operations, such as compare-and-swap, to apply changes to shared data structures.

#### Compare-and-Swap (CAS)

CAS is a fundamental atomic operation in non-blocking algorithms. It involves comparing the current value of a variable with an expected value and, if they match, updating the variable to a new value. The operation is atomic and helps avoid race conditions.

#### A-B-A Problem

where a variable changes from A to B and back to A, making it difficult for a thread to detect changes.
Techniques like using version numbers or stamps in conjunction with CAS are employed to address the A-B-A problem.

#### Completable Intended Modifications

modifications to shared data structures are often represented as "intended modifications" that can be completed by one or more threads. This approach allows a thread to submit a modification request without blocking and enables other threads to assist in completing the modification.

#### ``AtomicStampedReference``

Some programming languages, like Java, provide atomic classes like ``AtomicStampedReference`` to combine a reference with a stamp (version number) in a single atomic variable, helping address the A-B-A problem.

#### Testing and Validation

Due to the complexity of non-blocking algorithms, thorough testing and validation are crucial to ensure correctness and identify potential race conditions or other concurrency issues.

### Non-blocking Algorithms are Difficult to Implement

they require managing concurrency without traditional locks.
Ensuring correctness amid simultaneous operations by multiple threads, avoiding race conditions, and addressing A-B-A problems demand intricate designs and careful handling of atomic operations like compare-and-swap.  Testing and validation are crucial due to the complexity, making non-blocking algorithms harder to develop compared to their blocking counterparts.

### The Benefit of Non-blocking Algorithms

#### Choice

threads are given a choice about what to do when their requested action cannot be performed.
Instead of just being blocked, the request thread has a choice about what to do. Sometimes there is nothing a thread can do In that case it can choose to block or wait itself, thus freeing up the CPU for other tasks. But at least the requesting thread is given a choice.

#### No Deadlocks

the suspension of one thread cannot lead to the suspension of other threads.
This means that deadlock cannot occur. Two threads cannot be blocked waiting for each other to release a lock they want. Since threads are not blocked when they cannot perform their requested action, they cannot be blocked waiting for each other.

#### No Thread Suspension

Suspending and reactivating a thread is costly. However, there is still a high price to pay for thread suspension and reactivation.

Whenever a thread is blocked it is suspended, thus incurring the overhead of thread suspension and reactivation.
Since threads are not suspended by non-blocking algorithms, this overhead does not occur. This means that the CPUs can potentially spend more time performing actual business logic instead of context switching.

On a multi CPU system blocking algorithms can have more significant impact on the overall performance.

#### Reduced Thread Latency

Latency in this context means the time between a requested action becomes possible and the thread actually performs it. Since threads are not suspended in non-blocking algorithms they do not have to pay the expensive, slow reactivation overhead. That means that when a requested action becomes possible threads can respond faster and thus reduce their response latency.

The non-blocking algorithms often obtain the lower latency by busy-waiting until the requested action becomes possible.


