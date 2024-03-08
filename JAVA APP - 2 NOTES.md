# DATA STRUCTURES & ALGORITHMS

## ALGORITHMS #CSD_NOTES

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

### Queue
---

#### **What is Queue Data Structure?***

A ***Queue*** is defined as a linear data structure that is open at both ends and the operations are performed in ***First In First Out (FIFO)*** order.


![[Pasted image 20240221222130.png]]


define a queue to be a list in which all additions to the list are made at one end, and all deletions from the list are made at the other end.  The element which is first pushed into the order, the operation is first performed on that.

#### ***FIFO Principle of Queue:***

- A Queue is like a line waiting to purchase tickets, where the first person in line is the first person served. (i.e. First come first serve).
- Position of the entry in a queue ready to be served, that is, the first entry that will be removed from the queue, is called the ****front**** of the queue(sometimes, ****head**** of the queue), similarly, the position of the last entry in the queue, that is, the one most recently added, is called the ***rear*** (or the ***tail***) of the queue.

#### ***Characteristics of Queue:***

- Queue can handle multiple data.
- We can access both ends.
- They are fast and flexible.

#### Basic Operations of Queue

A queue is an object (an abstract data structure - ADT) that allows the following operations:

- **Enqueue**: Add an element to the end of the queue
- **Dequeue**: Remove an element from the front of the queue
- **IsEmpty**: Check if the queue is empty
- **IsFull**: Check if the queue is full
- **Peek**: Get the value of the front of the queue without removing it

#### Applications of Queue

- CPU scheduling, Disk Scheduling
- When data is transferred asynchronously between two processes.The queue is used for synchronization. For example: IO Buffers, pipes, file IO, etc
- Handling of interrupts in real-time systems.
- Call Center phone systems use Queues to hold people calling them in order.

#### Queue Representation:

Like stacks, Queues can also be represented in an array: In this representation, the Queue is implemented using the array. Variables used in this case are

- ***Queue:*** the name of the array storing queue elements.
- ***Front***: the index where the first element is stored in the array representing the queue.
- ***Rear:*** the index where the last element is stored in an array representing the queue.

```java
public class Queue {
  int SIZE = 5;
  int items[] = new int[SIZE];
  int front, rear;

  Queue() {
    front = -1;
    rear = -1;
  }

  boolean isFull() {
    if (front == 0 && rear == SIZE - 1) {
      return true;
    }
    return false;
  }

  boolean isEmpty() {
    if (front == -1)
      return true;
    else
      return false;
  }

  void enQueue(int element) {
    if (isFull()) {
      System.out.println("Queue is full");
    } else {
      if (front == -1)
        front = 0;
      rear++;
      items[rear] = element;
      System.out.println("Inserted " + element);
    }
  }

  int deQueue() {
    int element;
    if (isEmpty()) {
      System.out.println("Queue is empty");
      return (-1);
    } else {
      element = items[front];
      if (front >= rear) {
        front = -1;
        rear = -1;
      } /* Q has only one element, so we reset the queue after deleting it. */
      else {
        front++;
      }
      System.out.println("Deleted -> " + element);
      return (element);
    }
  }

  void display() {
    /* Function to display elements of Queue */
    int i;
    if (isEmpty()) {
      System.out.println("Empty Queue");
    } else {
      System.out.println("\nFront index-> " + front);
      System.out.println("Items -> ");
      for (i = front; i <= rear; i++)
        System.out.print(items[i] + "  ");

      System.out.println("\nRear index-> " + rear);
    }
  }

  public static void main(String[] args) {
    Queue q = new Queue();

    // deQueue is not possible on empty queue
    q.deQueue();

    // enQueue 5 elements
    q.enQueue(1);
    q.enQueue(2);
    q.enQueue(3);
    q.enQueue(4);
    q.enQueue(5);

    // 6th element can't be added to because the queue is full
    q.enQueue(6);

    q.display();

    // deQueue removes element entered first i.e. 1
    q.deQueue();

    // Now we have just 4 elements
    q.display();

  }
}
```

### Circular Queue
---

#### What is a Circular Queue?

> A Circular Queue is an extended version of a normal queue where the last element of the queue is connected to the first element of the queue forming a circle.

The operations are performed based on FIFO (First In First Out) principle. It is also called **‘Ring Buffer’**.

![[Pasted image 20240222212116.png]]

The circular queue solves the major limitation of the normal queue. In a normal queue, after a bit of insertion and deletion, there will be non-usable empty space.

#### How Circular Queue Works

Circular Queue works by the process of circular increment i.e. when we try to increment the pointer and we reach the end of the queue, we start from the beginning of the queue.

```java
if REAR + 1 == 5 (overflow!), REAR = (REAR + 1)%5 = 0 (start of queue)
```

#### Operations on Circular Queue:

- **Front:** Get the front item from the queue.
- **Rear:** Get the last item from the queue.
- **``enQueue(value)``** This function is used to insert an element into the circular queue. In a circular queue, the new element is always inserted at the rear position.   
    - Check whether the queue is full – (i.e., the rear end is in just before the front end in a circular manner].
    - If it is full then display Queue is full. 
        - If the queue is not full then,  insert an element at the end of the queue.
- **``deQueue()``** This function is used to delete an element from the circular queue. In a circular queue, the element is always deleted from the front position.   
    - Check whether the queue is Empty.
    - If it is empty then display Queue is empty.
        - If the queue is not empty, then get the last element and remove it from the queue.


##### Illustration of Circular Queue Operations

![[Pasted image 20240222212605.png]]


#### How to Implement a Circular Queue?
A circular queue can be implemented using two data structures:

- Array
- Linked List

##### Implement Circular Queue using Array:

1. Initialize an array queue of size **n**, where n is the maximum number of elements that the queue can hold.
2. Initialize two variables front and rear to -1.
3. **Enqueue:** To enqueue an element **x** into the queue, do the following:
    - Increment rear by 1.
        - If **rear** is equal to n, set **rear** to 0.
    - If **front** is -1, set **front** to 0.
    - Set queue[rear] to x.
4. **Dequeue:** To dequeue an element from the queue, do the following:
    - Check if the queue is empty by checking if **front** is -1. 
        - If it is, return an error message indicating that the queue is empty.
    - Set **x** to queue[front].
    - If **front** is equal to **rear**, set **front** and **rear** to -1.
    - Otherwise, increment **front** by 1 and if **front** is equal to n, set **front** to 0.
    - Return x.

```java
// Java program for insertion and
// deletion in Circular Queue
import java.util.ArrayList;

class CircularQueue {

    // Declaring the class variables.
    private int size, front, rear;

    // Declaring array list of integer type.
    private ArrayList<Integer> queue = new ArrayList<Integer>();

    // Constructor
    CircularQueue(int size) {
        this.size = size;
        this.front = this.rear = -1;
    }

    // Method to insert a new element in the queue.
    public void enQueue(int data) {

        // Condition if queue is full.
        if ((front == 0 && rear == size - 1) ||
            (rear == (front - 1) % (size - 1))) {
            System.out.print("Queue is Full");
        }

        // condition for empty queue.
        else if (front == -1) {
            front = 0;
            rear = 0;
            queue.add(rear, data);
        }

        else if (rear == size - 1 && front != 0) {
            rear = 0;
            queue.set(rear, data);
        }

        else {
            rear = (rear + 1);

            // Adding a new element if
            if (front <= rear) {
                queue.add(rear, data);
            }

            // Else updating old value
            else {
                queue.set(rear, data);
            }
        }
    }

    // Function to dequeue an element
    // form the queue.
    public int deQueue() {
        int temp;

        // Condition for empty queue.
        if (front == -1) {
            System.out.print("Queue is Empty");

            // Return -1 in case of an empty queue
            return -1;
        }

        temp = queue.get(front);

        // Condition for only one element
        if (front == rear) {
            front = -1;
            rear = -1;
        }

        else if (front == size - 1) {
            front = 0;
        } else {
            front = front + 1;
        }

        // Returns the dequeued element
        return temp;
    }

    // Method to display the elements of the queue
    public void displayQueue() {

        // Condition for an empty queue.
        if (front == -1) {
            System.out.print("Queue is Empty");
            return;
        }

        // If rear has not crossed the max size
        // or queue rear is still greater than
        // front.
        System.out.print("Elements in the " +
                "circular queue are: ");

        if (rear >= front) {

            // Loop to print elements from
            // front to rear.
            for (int i = front; i <= rear; i++) {
                System.out.print(queue.get(i));
                System.out.print(" ");
            }
            System.out.println();
        }

        // If rear crossed the max index and
        // indexing has started in loop
        else {

            // Loop for printing elements from
            // front to max size or last index
            for (int i = front; i < size; i++) {
                System.out.print(queue.get(i));
                System.out.print(" ");
            }

            // Loop for printing elements from
            // 0th index till rear position
            for (int i = 0; i <= rear; i++) {
                System.out.print(queue.get(i));
                System.out.print(" ");
            }
            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args) {

        // Initializing a new object of
        // CircularQueue class.
        CircularQueue q = new CircularQueue(5);

        q.enQueue(14);
        q.enQueue(22);
        q.enQueue(13);
        q.enQueue(-6);

        q.displayQueue();

        int x = q.deQueue();

        // Checking for an empty queue.
        if (x != -1) {
            System.out.print("Deleted value = ");
            System.out.println(x);
        }

        x = q.deQueue();

        // Checking for an empty queue.
        if (x != -1) {
            System.out.print("Deleted value = ");
            System.out.println(x);
        }

        q.displayQueue();

        q.enQueue(9);
        q.enQueue(20);
        q.enQueue(5);

        q.displayQueue();

        q.enQueue(20);
    }
}
```

**Output**

```text
Elements in Circular Queue are: 14 22 13 -6 
Deleted value = 14
Deleted value = 22
Elements in Circular Queue are: 13 -6 
Elements in Circular Queue are: 13 -6 9 20 5 
Queue is Full
```

#### Complexity Analysis of Circular Queue Operations:

- **Time Complexity:** 
    - Enqueue: O(1) because no loop is involved for a single enqueue.
    - Dequeue: O(1) because no loop is involved for one dequeue operation.
- **Auxiliary Space:** O(N) as the queue is of size N.

#### Applications of Circular Queue:

1. **Memory Management:** The unused memory locations in the case of ordinary queues can be utilized in circular queues.
2. **Traffic system:** In computer controlled traffic system, circular queues are used to switch on the traffic lights one by one repeatedly as per the time set.
3. **CPU Scheduling:** Operating systems often maintain a queue of processes that are ready to execute or that are waiting for a particular event to occur.


# CONCURRENCY & MULTITHREADING

**[Concurrency](https://en.wikipedia.org/wiki/Concurrency_%28computer_science%29)** is the ability to run several programs or several parts of a program in parallel. Concurrency enables a program to achieve high performance and throughput by utilizing the untapped capabilities of the underlying operating system and machine hardware.

The backbone of **java concurrency** is threading. A thread is a lightweight process that has its own call stack but can access shared data of other threads in the same process. A Java application runs by default in one process.

## Thread Safety

Thread safety is the concept of correctness. 

> **Correctness means that a class conforms to its specification.**

> **A class is thread-safe if it behaves correctly when accessed from multiple threads, regardless of the scheduling or interleaving of the execution of those threads by the runtime environment, and with no additional synchronization or other coordination on the part of the calling code.**

Thread-safe classes encapsulate any needed synchronization so that clients need not provide their own.

## Lifecycle and States of a Thread

A thread in Java at any point of time exists in any one of the following states. A thread lies only in one of the shown states at any instant:

1. New State
2. Runnable State
3. Blocked State
4. Waiting State
5. Timed Waiting State
6. Terminated State

![[Pasted image 20240227095944.png]]

1. ***New Thread:*** When a new thread is created, it is in the new state. The thread has not yet started to run when the thread is in this state. When a thread lies in the new state, its code is yet to be run and hasn’t started to execute.
2. ***Runnable State:*** A thread that is ready to run is moved to a runnable state. In this state, a thread might actually be running or it might be ready to run at any instant of time. It is the responsibility of the thread scheduler to give the thread, time to run.   
    A multi-threaded program allocates a fixed amount of time to each individual thread. Each and every thread runs for a short while and then pauses and relinquishes the CPU to another thread so that other threads can get a chance to run. When this happens, all such threads that are ready to run, waiting for the CPU and the currently running thread lie in a runnable state.
3. ***Blocked:*** The thread will be in blocked state when it is trying to acquire a lock but currently the lock is acquired by the other thread. The thread will move from the blocked state to runnable state when it acquires the lock.
4. ***Waiting state:*** The thread will be in waiting state when it calls wait() method or join() method. It will move to the runnable state when other thread will notify or that thread will be terminated.
5. ***Timed Waiting:*** A thread lies in a timed waiting state when it calls a method with a time-out parameter. A thread lies in this state until the timeout is completed or until a notification is received. For example, when a thread calls sleep or a conditional wait, it is moved to a timed waiting state.
6. ***Terminated State:*** A thread terminates because of either of the following reasons:   
    - Because it exits normally. This happens when the code of the thread has been entirely executed by the program.
    - Because there occurred some unusual erroneous event, like a segmentation fault or an unhandled exception.


```java
// Java program to demonstrate thread states
class thread implements Runnable {
	public void run()
	{
		// moving thread2 to timed waiting state
		try {
			Thread.sleep(1500);
		}
		catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println(
			"State of thread1 while it called join() method on thread2 -"
			+ Test.thread1.getState());
		try {
			Thread.sleep(200);
		}
		catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
}

public class Test implements Runnable {
	public static Thread thread1;
	public static Test obj;

	public static void main(String[] args)
	{
		obj = new Test();
		thread1 = new Thread(obj);

		// thread1 created and is currently in the NEW
		// state.
		System.out.println(
			"State of thread1 after creating it - "
			+ thread1.getState());
		thread1.start();

		// thread1 moved to Runnable state
		System.out.println(
			"State of thread1 after calling .start() method on it - "
			+ thread1.getState());
	}

	public void run()
	{
		thread myThread = new thread();
		Thread thread2 = new Thread(myThread);

		// thread1 created and is currently in the NEW
		// state.
		System.out.println(
			"State of thread2 after creating it - "
			+ thread2.getState());
		thread2.start();

		// thread2 moved to Runnable state
		System.out.println(
			"State of thread2 after calling .start() method on it - "
			+ thread2.getState());

		// moving thread1 to timed waiting state
		try {
			// moving thread1 to timed waiting state
			Thread.sleep(200);
		}
		catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(
			"State of thread2 after calling .sleep() method on it - "
			+ thread2.getState());

		try {
			// waiting for thread2 to die
			thread2.join();
		}
		catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(
			"State of thread2 when it has finished it's execution - "
			+ thread2.getState());
	}
}
```

```shell
State of thread1 after creating it - NEW
State of thread1 after calling .start() method on it - RUNNABLE
State of thread2 after creating it - NEW
State of thread2 after calling .start() method on it - RUNNABLE
State of thread2 after calling .sleep() method on it - TIMED_WAITING
State of thread1 while it called join() method on thread2 - WAITING
State of thread2 when it has finished its execution - TERMINATED
```

When a new thread is created, the thread is in the NEW state. When the start() method is called on a thread, the thread scheduler moves it to the Runnable state. Whenever the join() method is called on a thread instance, the current thread executing that statement will wait for this thread to move to the Terminated state. So, before the final statement is printed on the console, the program calls join() on thread2 making the thread1 wait while thread2 completes its execution and is moved to the Terminated state. thread1 goes to the Waiting state because it is waiting for thread2 to complete its execution as it has called join on thread2.

## Thread Priority in Multithreading

Whenever we create a thread in Java, it always has some priority assigned to it. Priority can either be given by JVM while creating the thread or it can be given by the programmer explicitly.

Priorities in threads is a concept where each thread is having a priority which in layman’s language one can say every object is having priority

- The default priority is set to 5 as excepted.
- Minimum priority is set to 1.
- Maximum priority is set to 10.

3 constants are defined in it namely as follows:

1. **``public static int NORM_PRIORITY``**
2. **``public static int MIN_PRIORITY``**
3. **``public static int MAX_PRIORITY``**


```java
// Java Program to Illustrate Priorities in Multithreading
// via help of getPriority() and setPriority() method

// Importing required classes
import java.lang.*;

// Main class
class ThreadDemo extends Thread {

	// Method 1
	// run() method for the thread that is called
	// as soon as start() is invoked for thread in main()
	public void run()
	{
		// Print statement
		System.out.println("Inside run method");
	}

	// Main driver method
	public static void main(String[] args)
	{
		// Creating random threads
		// with the help of above class
		ThreadDemo t1 = new ThreadDemo();
		ThreadDemo t2 = new ThreadDemo();
		ThreadDemo t3 = new ThreadDemo();

		// Thread 1
		// Display the priority of above thread
		// using getPriority() method
		System.out.println("t1 thread priority : "
						+ t1.getPriority());

		// Thread 1
		// Display the priority of above thread
		System.out.println("t2 thread priority : "
						+ t2.getPriority());

		// Thread 3
		System.out.println("t3 thread priority : "
						+ t3.getPriority());

		// Setting priorities of above threads by
		// passing integer arguments
		t1.setPriority(2);
		t2.setPriority(5);
		t3.setPriority(8);

		// t3.setPriority(21); will throw
		// IllegalArgumentException

		// 2
		System.out.println("t1 thread priority : "
						+ t1.getPriority());

		// 5
		System.out.println("t2 thread priority : "
						+ t2.getPriority());

		// 8
		System.out.println("t3 thread priority : "
						+ t3.getPriority());

		// Main thread

		// Displays the name of
		// currently executing Thread
		System.out.println(
			"Currently Executing Thread : "
			+ Thread.currentThread().getName());

		System.out.println(
			"Main thread priority : "
			+ Thread.currentThread().getPriority());

		// Main thread priority is set to 10
		Thread.currentThread().setPriority(10);

		System.out.println(
			"Main thread priority : "
			+ Thread.currentThread().getPriority());
	}
}
```

```shell
t1 thread priority : 5
t2 thread priority : 5
t3 thread priority : 5
t1 thread priority : 2
t2 thread priority : 5
t3 thread priority : 8
Currently Executing Thread : main
Main thread priority : 5
Main thread priority : 10
```

- Thread with the highest priority will get an execution chance prior to other threads. Suppose there are 3 threads t1, t2, and t3 with priorities 4, 6, and 1. So, thread t2 will execute first based on maximum priority 6 after that t1 will execute and then t3.
- The default priority for the main thread is always 5, it can be changed later. The default priority for all other threads depends on the priority of the parent thread.
-  If two threads have the same priority then we can’t expect which thread will execute first. It depends on the thread scheduler’s algorithm(Round-Robin, First Come First Serve, etc)
- If we are using thread priority for thread scheduling then we should always keep in mind that the underlying platform should provide support for scheduling based on thread priority.

## How to Create and Start a New Thread

In Java, we can create a _Thread_ in following ways:

- By extending _[Thread](https://howtodoinjava.com/java/multi-threading/java-runnable-vs-thread/)_ class
- By implementing _Runnable_ interface
- Using Lambda expressions

###  By Extending _Thread_ Class

To create a new thread, extend the class with _Thread_ and override the `run()` method.

```java
class SubTask extends Thread {
  public void run() {
    System.out.println("SubTask started...");
  }
}
```

**CSD EXAMPLE**
```java
public class RandomTextGeneratorThread extends Thread {  
    private final Random m_random = new Random();  
    private final int m_count;  
    private final int m_min;  
    private final int m_bound;  
  
    public RandomTextGeneratorThread(String name, int count, int min, int bound)  
    {  
        super(name);  
        m_count = count;  
        m_min = min;  
        m_bound = bound;  
    }  
  
    @Override  
    public void run()  
    {  
        for (var i = 0; i < m_count; ++i) {  
            var text = StringUtil.getRandomTextEN(m_random, m_random.nextInt(m_min, m_bound));  
  
            System.out.printf("%s -> %s%n", getName(), text);  
            //ThreadUtil.sleep(m_random.nextLong(300, 501));  
        }  
    }  
}
```

```java
class Application {  
    public static void run(String[] args)  
    {  
        var self = Thread.currentThread();  
  
        var nThreads = Console.readInt("Input number of threads:");  
        var count = Console.readInt("Input count:");  
  
        System.out.printf("Name:%s%n", self.getName());  
  
        for (var i = 0; i < nThreads; ++i) {  
            var thread = new RandomTextGeneratorThread("Generator-" + (i + 1), count, 5, 15);  
  
            thread.start();  
        }  
  
        System.out.println("main ends!...");  
    }  
}
```

### By Implementing _Runnable_ Interface

Implementing the _Runnable_ interface is considered a better approach because, in this way, the thread class can extend any other class. Remember, in Java, a class can extend only one class but implement multiple interfaces.

```java
class SubTaskWithRunnable implements Runnable {  public void run() {    System.out.println("SubTaskWithRunnable started...");  }}
```

**CSD EXAMPLE**
```java
public class RandomTextGeneratorThread implements Runnable {  
    private final Random m_random = new Random();  
    private final int m_count;  
    private final int m_min;  
    private final int m_bound;  
  
    public RandomTextGeneratorThread(int count, int min, int bound)  
    {  
        m_count = count;  
        m_min = min;  
        m_bound = bound;  
    }  
  
    @Override  
    public void run()  
    {  
        var name = Thread.currentThread().getName();  
  
        for (var i = 0; i < m_count; ++i) {  
            var text = StringUtil.getRandomTextEN(m_random, m_random.nextInt(m_min, m_bound));  
  
            System.out.printf("%s -> %s%n", name, text);  
        }  
    }  
}
```

### Using Lambda Expressions

Lambda expressions help create inline instances of functional interfaces and can help reduce the boilerplate code.

```java
Runnable subTaskWithLambda = () ->
{
  System.out.println("SubTaskWithLambda started...");
};
```

### Difference between Runnable vs Thread

#### Key Points

1. ``Runnable`` is an interface with a single ``run()`` method that needs to be implemented to define the task that will execute in the thread.

2. ``Thread`` is a class that can be extended to create a new thread and override the ``run()`` method to define its task.

3. Creating a thread with ``Runnable`` allows you to extend another class, but extending  ``Thread`` does not.

4. Using ``Runnable`` is the preferred way to create a thread because it supports the Object-Oriented principle of composition over inheritance.

#### Difference

| Runnable                                    | Thread                                       |
|---------------------------------------------|----------------------------------------------|
| An interface to be implemented by any class | A class that is to be extended when creating |
| whose instances are intended to be executed | a new thread.                                |
| by a thread.                                |                                              |
| Allows extending another class and          | Extending Thread means you cannot extend    |
| implementing Runnable.                      | any other class.                            |
| You need to pass an instance of a Runnable  | You can directly create a Thread object by  |
| to a Thread object.                         | extending from the Thread class.           |

####  When To Use ? 

- Use ``Runnable`` when you want to separate the task's logic from thread control, or when you need to implement multiple interfaces.

- Use ``Thread`` when you need to manage or control thread-specific behavior and do not require the ability to extend another class.


### Difference between Runnable vs Callable

| **Runnable interface**                                                                                    | **Callable interface**                                                                                                            |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| It cannot return the result of computation.                                                               | It can return the result of the parallel processing of a task.                                                                    |
| It cannot throw a checked Exception.                                                                      | It can throw a checked Exception.                                                                                                 |
| In a runnable interface, one needs to override the run() method in Java.                                  | In order to use Callable, you need to override the call()                                                                         |

### Starting a New Thread

####  Using *``Thread.start()``*

The ``start()`` method is responsible for registering the thread with the platform thread scheduler and doing all the other mandatory activities such as resource allocations.

```JAVA
class SubTask extends Thread {
  public void run() {
    System.out.println("SubTask started...");
  }
}
Thread subTask = new SubTask();
subTask.start();
```

**What happens when a function is called?**   
When a function is called the following operations take place:   
 

1. The arguments are evaluated.
2. A new stack frame is pushed into the call stack.
3. Parameters are initialized.
4. Method body is executed.
5. Value is returned and current stack frame is popped from the call stack.

  
**The purpose of start() is to create a separate call stack for the thread. A separate call stack is created by it, and then run() is called by JVM.**

```java
// Java code to see that all threads are
// pushed on the same stack if we use run()
// instead of start().
class ThreadTest extends Thread {
    public void run() {
        try {
            // Displaying the thread that is running
            System.out.println("Thread " +
                    Thread.currentThread().getId() +
                    " is running");

        } catch (Exception e) {
            // Throwing an exception
            System.out.println("Exception is caught");
        }
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        int n = 8;
        for (int i = 0; i < n; i++) {
            ThreadTest object = new ThreadTest();

            // start() is replaced with run() for
            // seeing the purpose of start
            object.run();
        }
    }
}
```

```shell
Thread 1 is running
Thread 1 is running
Thread 1 is running
Thread 1 is running
Thread 1 is running
Thread 1 is running
Thread 1 is running
Thread 1 is running
```

```java
// Java code to see that all threads are
// pushed on same stack if we use run()
// instead of start().
class ThreadTest extends Thread
{
    public void run()
    {
        try
        {
            // Displaying the thread that is running
            System.out.println ("Thread " +
                                Thread.currentThread().getId() +
                                " is running");

        }
        catch (Exception e)
        {
            // Throwing an exception
            System.out.println ("Exception is caught");
        }
    }
}

// Main Class
public class Main
{
    public static void main(String[] args)
    {
        int n = 8;
        for (int i=0; i<8; i++)
        {
            ThreadTest object = new ThreadTest();

            object.start();
        }
    }
}
```

```shell
Thread 15 is running
Thread 16 is running
Thread 13 is running
Thread 14 is running
Thread 11 is running
Thread 12 is running
Thread 17 is running
Thread 18 is running
```

##### Difference between ``Thread.start()``  and ``Thread.run()``

|start()|run()|
|---|---|
|Creates a new thread and the run() method is executed on the newly created thread.|No new thread is created and the run() method is executed on the calling thread itself.|
|Can’t be invoked more than one time otherwise throws _java.lang.IllegalStateException_|Multiple invocation is possible|
|Defined in _java.lang.Thread_ class.|Defined in _java.lang.Runnable_ interface and must be overridden in the implementing class.|

#### Using _``ExecutorService``_

Creating a new _Thread_ is resource intensive. So, creating a new Thread, for every subtask, decreases the performance of the application. To overcome these problems, we should use _thread pools_

A **_thread pool_ is a pool of already created _Threads_ ready to do our task**. In Java, _``ExecutorService``_ is the backbone of creating and managing thread pools. We can submit either a **_Runnable_** or a **_Callable_** task in the _``ExecutorService``,_ and it executes the submitted task using the one of the threads in the pool.

```java
Runnable subTaskWithLambda = () -> {
  System.out.println("SubTaskWithLambda started...");
};
ExecutorService executorService = Executors.newFixedThreadPool(10);
executorService.execute(subTaskWithLambda);
```

**CSD EXAMPLE**

```java
public class StringGenerator {  
    private final List<String> m_list;  
    private final int m_count;  
    private final int m_nThreads;  
    private final RandomGenerator m_randomGenerator;  
    private final ExecutorService m_threadPool;  
  
    private void generateCallback()  
    {  
        var self = Thread.currentThread();  
  
        for (var i = 0; i < m_count; ++i)  
            synchronized (this) {  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(5, 15))));  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(1, 15))));  
            }  
    }  
  
    public StringGenerator(List<String> list, int count, int nThreads, RandomGenerator randomGenerator)  
    {  
        m_list = list;  
        m_count = count;  
        m_randomGenerator = randomGenerator;  
        m_nThreads = nThreads;  
        m_threadPool = Executors.newFixedThreadPool(m_nThreads);  
    }  
  
    public int size()  
    {  
        return m_list.size();  
    }  
  
    public void run()  
    {  
        Future<?> [] futures = new Future[m_nThreads];  
  
        for (var i = 0; i < m_nThreads; ++i)  
            futures[i] = m_threadPool.submit(this::generateCallback);  
  
        for (var future : futures)  
            try {  
                future.get();  
            }  
            catch (ExecutionException | InterruptedException ignore) {  
  
            }  
  
        for (var str : m_list)  
            Console.writeLine(str);  
  
        m_threadPool.shutdown();  
    }  
}
```

```java
class Application {  
    public static void run(String[] args)  
    {  
        var stringGenerator = new StringGenerator(new ArrayList<>(), Console.readInt("Input count:"), Console.readInt("Input number of threads:"), new Random());  
  
        stringGenerator.run();  
        System.out.printf("Size:%d%n", stringGenerator.size());  
    }  
}
```

#### Delayed Execution with _``ScheduledExecutorService``_

When we submit a task to the executor, it executes as soon as possible. But suppose we want to **execute a task after a certain amount of time or to run the task periodically then we can use** _``ScheduledExecutorService``._

```java
ScheduledExecutorService executor = Executors.newScheduledThreadPool(2);
ScheduledFuture<String> result = executor.schedule(() -> {
	System.out.println("Thread is executing the job");
	return "completed";
}, 10, TimeUnit.SECONDS);
System.out.println(result.get());
```

**CSD EXAMPLE**

```java
public class DigitalClock {  
    private final DateTimeFormatter m_formatter;  
    private final ScheduledExecutorService m_scheduledExecutorService;  
  
    public DigitalClock()  
    {  
        m_formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH.mm.ss");  
        m_scheduledExecutorService = Executors.newSingleThreadScheduledExecutor();  
    }  
  
    public void run()  
    {  
        var future = m_scheduledExecutorService.scheduleAtFixedRate(() -> Console.write("%s\r", m_formatter.format(LocalDateTime.now())), 0, 1, TimeUnit.SECONDS);  
  
        Console.readLine();  
        future.cancel(false);  
        m_scheduledExecutorService.shutdown();  
    }  
}
```

```java
class Application {  
    public static void run(String[] args)  
    {  
        var clock = new DigitalClock();  
  
        clock.run();  
    }  
}
```

## Different Ways to Kill a Thread

There is **no official method to kill a thread in Java**. Stopping a thread is entirely managed by the JVM. Although Java provides several ways to manage the thread lifecycle such as a _start()_, _sleep()_, _stop()_ , etc. but does not provide any method to kill a thread and free the resources cleanly.

**Oracle specified** the reason for deprecating the stop() method as _It is inherently unsafe. Stopping a thread causes it to unlock all its locked monitors._ 

### Two Ways to Kill a Thread

**Effectively, we can only signal the thread to stop itself and let the thread clean up the resources and terminate itself.** In Java, we can send a signal to a thread in two ways:

- By periodically checking a _boolean_ flag
- By interrupting the thread using  _``Thread.interrupt()``_  method

#### By Checking a Flag

In this method, we check a _boolean_ flag periodically, or after every step in the task. Initially, the flag is set to _false_. To stop the thread, set the flag to _true_. Inside the thread, when the code checks the flag’s value to _true_, it destroys itself gracefully and returns.

Note that in this design, generally, there are two threads. One thread sets the _flag_ value to _true_, and another thread checks the _flag_ value. To **ensure that both threads see the same value** all the time, we must make the _flag_ variable _**volatile**_. Or we can use **``AtomicBoolean``** class that **supports atomic operations on an underlying _volatile_ _boolean_ variable**.

```java
Checking flag periodicallypublic class CustomTask implements Runnable {
  private volatile boolean flag = false;
  private Thread worker;
  public void start() {
    worker = new Thread(this);
    worker.start();
  }
  public void stop() {
    flag = true;
  }
  @Override
  public void run() {
    while (!flag) {
      try {
        Thread.sleep(500);
        System.out.println(Thread.currentThread().getName() + " Running...");
      } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
        System.out.println("Thread was interrupted," + e.getMessage());
      }
    }
    System.out.println(Thread.currentThread().getName() + " Stopped");
    return;
  }
}
```

```java
CustomTask task1 = new CustomTask();
CustomTask task2 = new CustomTask();
task1.start();
task2.start();
try {
  Thread.sleep(1000);
  task1.stop();
  task2.stop();
} catch (InterruptedException e) {
  System.out.println("Caught:" + e);
}
```

```shell
OutputThread-0 Running...
Thread-1 Running...
Thread-1 Running...
Thread-0 Running...
Thread-1 Stopped
Thread-0 Stopped
```

**CSD EXAMPLE**

```java
class Application {  
    private static boolean ms_flag = true;  
  
    private static void threadCallback()  
    {  
        var a = 0L;  
  
        while (ms_flag)  
            Console.writeLine(a++);  
    }  
  
    public static void run(String[] args)  
    {  
        var t = new Thread(Application::threadCallback);  
  
        t.start();  
  
        ThreadUtil.sleep(3, TimeUnit.SECONDS);  
        ms_flag = false;  
    }  
}
```

#### By Interrupting the Thread

The only difference is that we will **interrupt the thread instead of setting the flag to _false_**.

So inside the thread, we will keep checking the _thread’s interrupt status_, and when the thread is interrupted, we will stop the thread gracefully. To check the status of the interrupted thread, we can use the _**``Thread.isInterrupted()``**_ method. It returns either _true_ or _false_ based on the thread’s interrupt status.

```java
Using Interrupt Statuspublic class CustomTaskV2 implements Runnable {
  private Thread worker;
  public void start() {
    worker = new Thread(this);
    worker.start();
  }
  public void interrupt() {
    worker.interrupt();
  }
  @Override
  public void run() {
    while (!Thread.currentThread().isInterrupted()) {
      try {
        Thread.sleep(500);
        System.out.println(Thread.currentThread().getName() + " Running...");
      } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
        System.out.println("Thread was interrupted with reason : " + e.getMessage());
      }
    }
    System.out.println(Thread.currentThread().getName() + " Stopped");
    return;
  }
}
```

```java
CustomTaskV2 task1 = new CustomTaskV2();
CustomTaskV2 task2 = new CustomTaskV2();
task1.start();
task2.start();
try {
  Thread.sleep(1100);isInterrupted
  task1.interrupt();
  task2.interrupt();
} catch (InterruptedException e) {
  System.out.println("Caught:" + e);
}
```

```shell
OutputThread-0 Running...
Thread-1 Running...
Thread-1 Running...
Thread-0 Running...
Thread was interrupted with reason : sleep interrupted
Thread was interrupted with reason : sleep interrupted
Thread-0 Stopped
Thread-1 Stopped
```

**CSD EXAMPLE**

```java
class Application {  
    private static void threadCallback1()  
    {  
        var a = 0L;  
        var self = Thread.currentThread();  
  
        while (!self.isInterrupted())  
            Console.writeLine("t1->First:%d", a++);  
  
        while (!self.isInterrupted())  
            Console.writeLine("t1->Second:%d", a++);  
    }  
  
    private static void threadCallback2()  
    {  
        var a = 0L;  
  
        while (!Thread.interrupted())  
            Console.writeLine("t2->First:%d", a++);  
  
        while (!Thread.interrupted())  
            Console.writeLine("t2->Second:%d", a++);  
    }  
  
    public static void run(String[] args)  
    {  
        var t1 = new Thread(Application::threadCallback1);  
        var t2 = new Thread(Application::threadCallback2);  
  
        t1.start();  
        t2.start();  
  
        ThreadUtil.sleep(3, TimeUnit.SECONDS);  
        t1.interrupt();  
        t2.interrupt();  
        ThreadUtil.sleep(3, TimeUnit.SECONDS);  
        t2.interrupt();  
    }  
}
```

### ``Interrupt()``, ``Interrupted()`` And ``IsInterrupted()`` difference

- **`interrupt()` method:**
    
    - Invoked on a Thread object to interrupt it.
    - Sets the interrupt flag for the thread.
    - Does not necessarily stop the thread but indicates that it should check for interruption.
- **`isInterrupted()` method:**
    
    - Checks the interrupt status of the current thread or a specified thread.
    - Does not clear the interrupt flag; returns the current status.
    - Can be used to determine if the thread has been interrupted.
- **`interrupted()` method:**
    
    - A static method that checks the interrupt status of the current thread.
    - Clears the interrupt status, setting it to false.
    - Provides a way to check and clear the interrupt status in a single atomic operation.


##  Join Threads

If we have a requirement where **the first _Thread_ _must_ wait until the second _Thread_ completes its execution** then we should join these 2 Threads.

![[Pasted image 20240227125046.png]]

- The wedding cards distribution activity starts once the wedding cards printing activity completes and the wedding cards printing activity starts once we fix the venue for the wedding.
- We can say that in this case, _Thread-3_ has to wait until _Thread-2_ completes and also _Thread-2_ has to wait until _Thread-1_ completes its execution.
- **_Thread-2_ has to call _Thread-1.join()_, and _Thread-3_ has to call _Thread-2.join()_** so that they will wait until the completion of the other thread.

###  Java ``Thread.join()`` API

**The _join()_ method makes a calling _Thread_ enters into waiting for the state until the _Thread_ on which _join()_ is called completes its execution.**

- A _Thread_ `'t1'` wants to wait until another _Thread_ `'t2'` completes its execution then t1 has to call the _join()_ method on t2,
- _t2.join()_ called by t1.
- When t1 executes t2.join() then **t1 enters into waiting state immediately and continues to wait until t2 completes** its execution and terminates.
- Once t2 completes then only t1 continues its execution again.

![[Pasted image 20240227125528.png]]

####  Joining without Timeout

The default _join()_ method makes the current _Thread_ wait indefinitely until the _Thread_ on which it is called is completed. If the _Thread_ is interrupted then it will throw _[InterruptedException](https://docs.oracle.com/javase/7/docs/api/java/lang/InterruptedException.html)._

```java
public final void join() throws InterruptedException
```

```java
public class ChildThread extends Thread
{
         public void run()
         {
              for(int i=1; i<=4; i++)
              {
                 try{
                         Thread.sleep(500);
                      } catch(Exception e){
                          System.out.println(e);
                      }
                 System.out.println(“child thread execution - ” + i);
              }
         }
}
```

```java
ChildThread th1 = new ChildThread();
// Starting child Thread
th1.start();
// main thread joining the child thread
th1.join();
// main Thread printing statements
System.out.println(“main thread completed”);
```

The **main thread is calling _join()_ method on child thread** and waiting for its completion so after calling _join()_. So, all the statements from the child thread print before the main thread statements.

```shell
child thread execution - 1
child thread execution - 2
child thread execution - 3
child thread execution – 4
main thread completed
```

**CSD EXAMPLE**

```java
public class ThreadParam {  
    private final int m_count;  
    private final int m_min;  
    private final int m_bound;  
  
    private long m_result;  
  
    public ThreadParam(int count, int min, int bound)  
    {  
        m_count = count;  
        m_min = min;  
        m_bound = bound;  
    }  
  
    public int getCount()  
    {  
        return m_count;  
    }  
  
    public int getMin()  
    {  
        return m_min;  
    }  
  
    public int getBound()  
    {  
        return m_bound;  
    }  
  
    public long getResult()  
    {  
        return m_result;  
    }  
  
    public void add(long value)  
    {  
        m_result += value;  
    }  
  
    //...  
}
```

```java
class Application {  
    private static void join(Thread thread)  
    {  
        try {  
            thread.join();  
        }  
        catch (InterruptedException ignore) {  
  
        }  
    }  
  
    private static void generateAndFindTotalThreadCallback(ThreadParam param)  
    {  
        var self = Thread.currentThread();  
        var random = new Random();  
        var count = param.getCount();  
        var min = param.getMin();  
        var bound = param.getBound();  
  
        for (var i = 0; i < count; ++i) {  
            var val = random.nextInt(min, bound);  
  
            //Console.writeLine("%s:%d", self.getName(), val);  
            param.add(val);  
        }  
    }  
  
    public static void run(String[] args)  
    {  
        if (args.length != 4) {  
            Console.Error.writeLine("Wrong number of arguments!...");  
            System.exit(1);  
        }  
  
        try {  
            var nThreads = Integer.parseInt(args[0]);  
            var threads = new Thread[nThreads];  
            var threadParams = new ThreadParam[nThreads];  
  
            for (var i = 0; i < nThreads; ++i) {  
                int idx = i;  
  
                threadParams[idx] = new ThreadParam(parseInt(args[1]), parseInt(args[2]), parseInt(args[3]));  
                threads[i] =new Thread(() -> generateAndFindTotalThreadCallback(threadParams[idx]), "Thread-" + (i + 1));  
                threads[i].start();  
            }  
  
            for (var t : threads)  
                join(t);  
  
            for (var tp : threadParams)  
                Console.writeLine("Result:%d", tp.getResult());  
        }  
        catch (NumberFormatException ignore) {  
            Console.writeLine("Invalid arguments!...");  
        }  
    }  
}
```

####  Joining with Timeout

- `join(long millis):` It makes the current _Thread_ wait until the _Thread_ on which it is called is completed or the time specified in milliseconds has expired.
- `join(long millis, int nanos):` It makes the current _Thread_ wait until the _Thread_ on which it is called is completed or the time specified in milliseconds + nanoseconds has expired.

```java
public final synchronized void join(long millis) throws InterruptedException
public final synchronized void join(long millis, int nanos) throws InterruptedException
```

```java
// Creating child Thread Object
ChildThread th1 = new ChildThread();
// Starting child Thread
th1.start();
//main thread joining the child thread with 1000ms expiration time
th1.join(1000);
// main Thread printing statements
System.out.println(“main thread completed”);
```

When the program executes, the main thread will wait at max 1000ms and will be invoked anytime after that.

```shell
child thread execution - 1
main thread completed
child thread execution - 2
child thread execution - 3
child thread execution - 4
```

**CSD EXAMPLE**

```java
public class ThreadParam {  
    private final int m_count;  
    private final int m_min;  
    private final int m_bound;  
  
    private long m_result;  
  
    public ThreadParam(int count, int min, int bound)  
    {  
        m_count = count;  
        m_min = min;  
        m_bound = bound;  
    }  
  
    public int getCount()  
    {  
        return m_count;  
    }  
  
    public int getMin()  
    {  
        return m_min;  
    }  
  
    public int getBound()  
    {  
        return m_bound;  
    }  
  
    public long getResult()  
    {  
        return m_result;  
    }  
  
    public void add(long value)  
    {  
        m_result += value;  
    }  
  
    //...  
}
```

```java
class Application {  
    private static void join(Future<?> future)  
    {  
        try {  
            future.get();  
        }  
        catch (ExecutionException | InterruptedException ignore) {  
  
        }  
    }  
  
    private static void doCalculate(int nThreads, int count, int min, int bound)  
    {  
            var threadPool = Executors.newFixedThreadPool(nThreads);  
            var futures = new Future<?>[nThreads];  
            var threadParams = new ThreadParam[nThreads];  
  
            for (var i = 0; i < nThreads; ++i) {  
                int idx = i;  
  
                threadParams[idx] = new ThreadParam(count, min, bound);  
                futures[i] = threadPool.submit(() -> generateAndFindTotalThreadCallback(threadParams[idx]));  
            }  
  
            for (var future : futures)  
                join(future);  
  
            for (var tp : threadParams)  
                Console.writeLine("Result:%d", tp.getResult());  
  
            threadPool.shutdown();  
    }  
  
    private static void generateAndFindTotalThreadCallback(ThreadParam param)  
    {  
        try {  
            var random = new Random();  
            var count = param.getCount();  
            var min = param.getMin();  
            var bound = param.getBound();  
  
            for (var i = 0; i < count; ++i) {  
                var val = random.nextInt(min, bound);  
  
                //Console.writeLine("%s:%d", self.getName(), val);  
                param.add(val);  
            }  
        }  
        catch (Throwable ex) {  
  
        }  
    }  
  
    public static void run(String[] args)  
    {  
        if (args.length != 4) {  
            Console.Error.writeLine("Wrong number of arguments!...");  
            System.exit(1);  
        }  
  
        try {  
            doCalculate(parseInt(args[0]), parseInt(args[1]), parseInt(args[2]), parseInt(args[3]));  
        }  
        catch (NumberFormatException ignore) {  
            Console.writeLine("Invalid arguments!...");  
        }  
    }  
}
```

###  Interrupting a Joined _Thread_

A waiting _Thread_ can be interrupted by another _Thread_ using the _interrupt()_ method. Once the waiting _Thread_ is interrupted, it immediately comes out of the waiting state and moves into _Ready/Runnable_ state and waits for the _Thread Scheduler_ to allocate the processor to begin the execution again.

```java
public class ThreadJoiningInterrupt {
  public static void main(String[] args) {
    ChildThread childThread = new ChildThread(Thread.currentThread());
    childThread.start();
    try {
      childThread.join();   //Joined
    } catch (InterruptedException ie) {
      System.out.println("main Thread is interrupted");
    }
    for (int i = 1; i <= 4; i++) {
      System.out.println("main Thread Execution - " + i);
    }
  }
}
class ChildThread extends Thread {
  private static Thread parentThreadRef;
  public ChildThread(Thread parentThreadRef) {
    this.parentThreadRef = parentThreadRef;
  }
  public void run() {
    parentThreadRef.interrupt();   //Interrupted
    for (int i = 1; i <= 4; i++) {
      System.out.println("Child Thread Execution - " + i);
    }
  }
}
```

once the child thread interrupts the joined main thread then both thread executes simultaneously.

```java
Child Thread Execution - 1
main Thread is interrupted
Child Thread Execution - 2
main Thread Execution - 1
main Thread Execution - 2
main Thread Execution - 3
main Thread Execution - 4
Child Thread Execution - 3
Child Thread Execution – 4
```

###  Watch out for Deadlocks

If **two Threads call the _join()_ method on each other then both threads enter into waiting for state and wait for each other forever**.

Similarly, if a thread, by mistake, joins itself then it will be blocked forever, and JVM must be shutdown to recover.

```java
class Threadjoindemo
{
	public static void main(String[] args)
	{
	    // main thread calling join() on itself
	    Thread.currentThread().join(); // Program gets stuck, Deadlock suitation
	}
}
```

###  Difference between ``yield()`` and ``join()``

- Java virtual machine implements a preemptive, priority-based scheduler for its threads, assigning each thread a priority within a defined range.
- Thread priority can be changed by developers, but the virtual machine doesn't automatically adjust it.
- The highest-priority thread is generally chosen by the operating system to run, but this is not an absolute guarantee.
- Java doesn't mandate time-slicing for threads, though many operating systems implement it.
- Thread priorities range from 1 to 10, with 10 being the highest, 1 the lowest, and 5 the normal priority.
- The thread scheduler determines which thread to execute, and priorities should be set before the thread's start method is invoked.
- The `yield()` method is a static and native method in Java, allowing a thread to indicate its willingness to give up the processor to other threads with equal priority.
- `yield()` does not guarantee an immediate transition to the runnable state and only moves a thread from running to runnable state, not from wait or blocked state.
- `Thread.yield()` is often used to improve relative progression between threads in the thread pool.
- The `join()` method is used to make one thread wait for the completion of another. The calling thread will block until the thread it joins with has finished executing.
- Adding a timeout within `join()` allows the waiting thread to proceed after the specified timeout, making it less deterministic and dependent on the operating system for timing.

## Daemon Threads

**_Daemon Threads_ are the low-priority threads** that will execute in the background to provide support for the non-daemon threads (a thread that executes the main logic of the project is called a non-daemon or user thread). **_Daemon Threads_ in Java are also known as Service Provider Threads.**

> **daemon threads are threads in a program that won't stop the program from ending, even if they haven't completed their work. They're kind of like background tasks that are not crucial for the program to keep running.**

**Some examples of _Daemon Threads_ are _Garbage Collector,_ _Signal Dispatcher_, _Attach Listener_, _Finalizer_, etc.**

- **The life cycle of daemon threads depends on user threads.** It provides services to user threads for background supporting tasks.
- They cannot prevent the JVM from exiting when all the user threads finish their execution.
- When all the user threads terminate, **JVM terminates _Daemon threads_ automatically.**
- It is a thread with the lowest priority possible.
- JVM won’t be concerned about whether the _Daemon thread_ is active or not.

###  Methods for _Daemon Thread_

- ***``void setDaemon(boolean status)``***: To **make a thread a daemon thread**. We can change the nature of a thread by using this method.
- **_``boolean isDaemon()``_**: Used to determine whether or not the current thread is a daemon. **If the thread is Daemon, it returns true; otherwise false.**

```java
public class Task extends Thread
{
	String threadName;
	public Task(String name){
		threadName = name;
	}
	public void run() {
		if(Thread.currentThread().isDaemon())
		{
			System.out.println(threadName + " is Daemon Thread");
		} else{
			System.out.println(threadName + " is User Thread");
		}
	}
	public static void main(String[] args)
	{
		Task thread1 = new Task("thread1");
		Task thread2 = new Task("thread2");
		// Making thread1 as Daemon
		thread1.setDaemon(true);
		thread1.start();
		thread2.start();
	}
}
```

```shell
thread1 is Daemon Thread 
thread2 is User Thread
```

We can change the daemon nature of a thread using `setDaemon()`, but changing the daemon nature is possible before starting a thread only. **After starting a thread, if we are trying to change the daemon nature, we will get [_IllegalThreadStateException_](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalThreadStateException.html)_._**

```java
Task thread = new Task("user-thread");
thread.start();
thread.setDaemon(true);           // java.lang.IllegalThreadStateException
```

**CSD EXAMPLE**

```JAVA
class Application {  
    private static void threadCallback()  
    {  
        var random = new Random();  
        var self = Thread.currentThread();  
  
        Console.writeLine("%s Thread is %s", self.getName(), self.isDaemon() ? "daemon" : "non-daemon");  
  
        for (var i = 0; i < 10; ++i)  
            Console.write("%d ", i * 10);  
  
        Console.writeLine();  
        var t = new Thread(Application::threadCallback);  
  
        t.setDaemon(random.nextBoolean());  
        t.start();  
    }  
  
    public static void run(String[] args)  
    {  
        var random = new Random();  
        var self = Thread.currentThread();  
  
        Console.writeLine("%s Thread is %s", self.getName(), self.isDaemon() ? "daemon" : "non-daemon");  
        var t = new Thread(Application::threadCallback);  
  
        t.setDaemon(random.nextBoolean());  
        t.start();  
        Console.writeLine("main ends");  
    }  
}
```


### The Main Thread

**By default, the _main_ thread is always non-daemon**, and for all the remaining threads, **daemon nature inherits from parent to child** i.e. if the parent thread is daemon then automatically child thread is also daemon and vice-versa.

![[Pasted image 20240227142333.png]]

Since the main thread is a non-daemon thread, any other thread created from it will remain non-daemon until explicitly made daemon by calling `setDaemon(true)` method.

**It is not possible to change the daemon nature of the _main_ thread because the main thread is already been started by JVM** at the beginning. If we try to change the daemon nature of the main thread by using `setDaemon()` method, then it will raise _``IllegalThreadStateException``_.

```java
class ThreadDemo {
	public static void main(String[] args){
		System.out.println(Thread.currentThread().isDaemon()); // false
		Thread.currentThread().setDaemon(true); // java.lang.IllegalThreadStateException
	}
}
```

### _Daemon Thread_ Termination

**JVM terminates all the daemon threads irrespective of whether daemon threads are running or not whenever the last user thread terminates.** The main purpose of a daemon thread is to provide services to the user thread for background-supporting tasks. If there is no user thread, why should JVM keep running this daemon thread? That is why JVM terminates the daemon thread if there is no user thread.

```java
class Task extends Thread {
	public void run(){
		for(int i=0;i<10;i++){
			System.out.println("Child Thread is executing");
			try {
				Thread.sleep(2000);
			} catch(InterruptedException e){
				//...
			}
		}
	}
}
class ThreadDemo{
	public static void main(String[] args){
		Task thread = new Task();
		thread.setDaemon(true);
		thread.start();
		System.out.println("Main thread is terminating");
	}
}
```

When the main/user thread terminates, immediately the daemon thread i.e. child thread terminates as well, and it won’t complete. It’s for-loop 10 times and JVM terminates it in the middle itself.

```shell
Child Thread is executing
main thread is terminating
```

### When to Use Daemon Threads?

**_Daemon threads_ are useful for background-supporting** tasks such as garbage collection, releasing the memory of unused objects and removing unwanted entries from the cache.

We can use _Daemon Threads_ in usecases like:

- **Collecting statistics and performing the status monitoring tasks –** Sending and receiving network heartbeats, supplying the services to monitoring tools, and so on.
- **Performing asynchronous I/O tasks –** We can create a queue of I/O requests, and set up a group of daemon threads servicing these requests asynchronously.
- **Listening for incoming connections –** daemon threads are very convenient in situations like this because they let us program a simple “forever” loop rather than creating a setup that pays attention to exit requests from the main thread.

### Difference between Daemon Thread and User Thread

- **Creation:** JVM creates _Daemon threads,_ whereas an application creates its own user threads.
-  **Usage:** _Daemon threads_ provide service to the user threads and always run in the background, whereas user threads are used for foreground and I/O tasks of an application.
- **Priority:** _Daemon threads_ are low-priority threads, whereas user threads are of high priority.
- **JVM Behavior:** JVM does not wait for daemon threads execution to complete, whereas JVM waits till the execution of the user thread is finished.
- **Life Cycle:** The daemon threads’ lifecycle depends on user threads, whereas user threads have an independent lifecycle.
- **Termination:** All the daemon threads are terminated once the last user thread has been terminated, irrespective of the daemon thread’s position at that time, whereas user threads are terminated after completing their corresponding jobs.

## Atomic

In Java, **atomic variables** and **operations** used in concurrency. The **multi-threading** environment leads to a problem when **concurrency** is unified. The shared entity such as objects and variables may be changed during the execution of the program. Hence, they may lead to inconsistency of the program. So, it is important to take care of the shared entity while accessing concurrently. In such cases, the **atomic variable** can be a solution to it.

Java provides a ``**java.util.concurrent.atomic**`` package in which atomic classes are defined. The atomic classes provide a **lock-free** and **thread-safe** environment or programming on a single variable. It also supports atomic operations. All the atomic classes have the get() and set() methods that work on the volatile variable. The method works the same as read and writes on volatile variables.

###  **Atomic Operations**

**Three** key concepts are associated with atomic actions in Java are as follows:

1. Atomicity deals with which actions and sets o actions have **invisible**
2. Visibility determines when the effect of one thread can be **seen** by another.
3. Ordering determines when actions in one thread occur out of order with respect to another thread.

When multiple threads attempt to update the same value through CAS, one of them wins and updates the value. **However, unlike in the case of locks, no other thread gets suspended**; instead, they’re simply informed that they did not manage to update the value. The threads can then proceed to do further work and context switches are completely avoided.

###  **Atomic Variables**

The most commonly used atomic variable classes in Java are [AtomicInteger](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/atomic/AtomicInteger.html), [AtomicLong](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/atomic/AtomicLong.html), [AtomicBoolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/atomic/AtomicBoolean.html), and [AtomicReference](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/atomic/AtomicReference.html). These classes represent an _int_, _long_, _boolean,_ and object reference respectively which can be atomically updated. The main methods exposed by these classes are:

- _**``get()``**_ – gets the value from the memory, so that changes made by other threads are visible; equivalent to reading a _volatile_ variable
- _**``incrementAndGet()``** –_ Atomically increments by one the current value
- _**``set()``**_ – writes the value to memory, so that the change is visible to other threads; equivalent to writing a _volatile_ variable
- _**``lazySet()``**_ – eventually writes the value to memory, maybe reordered with subsequent relevant memory operations. One use case is nullifying references, for the sake of garbage collection, which is never going to be accessed again. In this case, better performance is achieved by delaying the null _volatile_ write
- _**``compareAndSet()``**_ –  returns true when it succeeds, else false
- _**``weakCompareAndSet()``**_ –  it does not create happens-before orderings. This means that it may not necessarily see updates made to other variables.

**CSD EXAMPLE**

```java
public class IntIncrementor {  
    private final AtomicInteger m_value;  
    private final int m_count;  
  
    private void incrementerCallback(int idx)  
    {  
  
        for (var i = 0; i < m_count; ++i)  
            m_value.getAndIncrement();  
  
        /*  
            ++m_value;  
            mov reg, m_value            add reg, 1            mov m_value, 1         */    }  
  
    public IntIncrementor(int count)  
    {  
        m_count = count;  
        m_value = new AtomicInteger();  
    }  
  
    public int getValue()  
    {  
        return m_value.get();  
    }  
  
    public int getCount()  
    {  
        return m_count;  
    }  
  
    public void run(int nThreads)  
    {  
        Thread [] threads = new Thread[nThreads];  
  
        for (var i = 0; i < nThreads; ++i) {  
            var idx = i;  
  
            threads[i] = new Thread(() -> incrementerCallback(idx), "Thread-");  
            threads[i].start();  
        }  
  
        for (var t : threads)  
            try {  
                t.join();  
            }  
            catch (InterruptedException ignore) {  
  
            }  
    }  
}
```

##  Synchronization

Java Synchronization is used to make sure by some synchronization method that only one thread can access the resource at a given point in time.

### Java Synchronized Blocks

A synchronized block in Java is synchronized on some object. All synchronized blocks synchronize on the same object and can only have one thread executed inside them at a time. All other threads attempting to enter the synchronized block are blocked until the thread inside the synchronized block exits the block.

>  ***``Synchronized``* blocks in Java are marked with the synchronized keyword.**

```java
// Only one thread can execute at a time. 
// sync_object is a reference to an object
// whose lock associates with the [monitor](https://www.geeksforgeeks.org/monitors-in-process-synchronization/). 
// The code is said to be synchronized on
// the monitor object
synchronized(sync_object)
{
   // Access shared variables and other
   // shared resources
}
```

This synchronization is implemented in Java with a concept called monitors or locks. Only one thread can own a monitor at a given time. When a thread acquires a lock, it is said to have entered the monitor. All other threads attempting to enter the locked monitor will be suspended until the first thread exits the monitor.

### Types of Synchronization

There are two synchronizations in Java mentioned below:

1. Process Synchronization
2. Thread Synchronization

#### 1. Process Synchronization in Java

Process Synchronization is a technique used to coordinate the execution of multiple processes. It ensures that the shared resources are safe and in order.

#### 2. Thread Synchronization in Java

Thread Synchronization is used to coordinate and ordering of the execution of the threads in a multi-threaded program. There are two types of thread synchronization are mentioned below:

- Mutual Exclusive
- Cooperation (Inter-thread communication in Java)

### Mutual Exclusive

Mutual Exclusive helps keep threads from interfering with one another while sharing data. There are three types of Mutual Exclusive mentioned below:

- Synchronized method.
- Synchronized block.
- Static synchronization.

```java
// A Java program to demonstrate working of
// synchronized.

import java.io.*;
import java.util.*;

// A Class used to send a message
class Sender {
	public void send(String msg)
	{
		System.out.println("Sending\t" + msg);
		try {
			Thread.sleep(1000);
		}
		catch (Exception e) {
			System.out.println("Thread interrupted.");
		}
		System.out.println("\n" + msg + "Sent");
	}
}

// Class for send a message using Threads
class ThreadedSend extends Thread {
	private String msg;
	Sender sender;

	// Receives a message object and a string
	// message to be sent
	ThreadedSend(String m, Sender obj)
	{
		msg = m;
		sender = obj;
	}

	public void run()
	{
		// Only one thread can send a message
		// at a time.
		synchronized (sender)
		{
			// synchronizing the send object
			sender.send(msg);
		}
	}
}

// Driver class
class SyncDemo {
	public static void main(String args[])
	{
		Sender send = new Sender();
		ThreadedSend S1 = new ThreadedSend(" Hi ", send);
		ThreadedSend S2 = new ThreadedSend(" Bye ", send);

		// Start two threads of ThreadedSend type
		S1.start();
		S2.start();

		// wait for threads to end
		try {
			S1.join();
			S2.join();
		}
		catch (Exception e) {
			System.out.println("Interrupted");
		}
	}
}
```

```shell
Sending     Hi 

 Hi Sent
Sending     Bye 

 Bye Sent
```

**CSD SYNCHRONIZED STATEMENT EXAMPLE**

```java
public class IntIncrementor {  
    private int m_value1;  
    private long m_value2;  
    private final int m_count;  
  
    private void incrementerCallback(int idx)  
    {  
        for (var i = 0; i < m_count; ++i)  
            synchronized (this) {  
                ++m_value1;  
                m_value2 += m_value1;  
            }  
    }  
  
    public IntIncrementor(int count)  
    {  
        m_count = count;  
    }  
  
    public int getValue1()  
    {  
        return m_value1;  
    }  
  
    public long getValue2()  
    {  
        return m_value2;  
    }  
  
    public int getCount()  
    {  
        return m_count;  
    }  
  
    public void run(int nThreads)  
    {  
        Thread [] threads = new Thread[nThreads];  
  
        for (var i = 0; i < nThreads; ++i) {  
            var idx = i;  
  
            threads[i] = new Thread(() -> incrementerCallback(idx), "Thread-");  
            threads[i].start();  
        }  
  
        for (var t : threads)  
            try {  
                t.join();  
            }  
            catch (InterruptedException ignore) {  
  
            }  
    }  
}
```

**CSD SYNCHRONIZED METHOD EXAMPLE**

```JAVA
public class IntIncrementor {  
    private int m_value1;  
    private long m_value2;  
    private final int m_count;  
  
    private synchronized void doForValues()  
    {  
        ++m_value1;  
        m_value2 += m_value1;  
    }  
  
    private void incrementerCallback(int idx)  
    {  
        for (var i = 0; i < m_count; ++i)  
            doForValues();  
    }  
  
    public IntIncrementor(int count)  
    {  
        m_count = count;  
    }  
  
    public int getValue1()  
    {  
        return m_value1;  
    }  
  
    public long getValue2()  
    {  
        return m_value2;  
    }  
  
    public int getCount()  
    {  
        return m_count;  
    }  
  
    public void run(int nThreads)  
    {  
        Thread [] threads = new Thread[nThreads];  
  
        for (var i = 0; i < nThreads; ++i) {  
            var idx = i;  
  
            threads[i] = new Thread(() -> incrementerCallback(idx), "Thread-");  
            threads[i].start();  
        }  
  
        for (var t : threads)  
            try {  
                t.join();  
            }  
            catch (InterruptedException ignore) {  
  
            }  
    }  
}
```

**CSD SYNCHRONIZED STATEMENT EXAMPLE**

```java
public class IntIncrementor {  
    private static int ms_value1;  
    private static long ms_value2;  
    private static final Object SYNC_OBJECT = new Object();  
  
    private static void incrementerCallback(int count, int idx)  
    {  
        for (var i = 0; i < count; ++i)  
            synchronized (SYNC_OBJECT) {  
                ++ms_value1;  
                ms_value2 += ms_value1;  
            }  
    }  
  
    public static int getValue1()  
    {  
        return ms_value1;  
    }  
  
    public static long getValue2()  
    {  
        return ms_value2;  
    }  
  
    public static void run(int count, int nThreads)  
    {  
        Thread [] threads = new Thread[nThreads];  
  
        for (var i = 0; i < nThreads; ++i) {  
            var idx = i;  
  
            threads[i] = new Thread(() -> incrementerCallback(count, idx), "Thread-");  
            threads[i].start();  
        }  
  
        for (var t : threads)  
            try {  
                t.join();  
            }  
            catch (InterruptedException ignore) {  
  
            }  
    }  
}
```

**CSD SYNCHRONIZED STATIC METHOD EXAMPLE**

```java
public class IntIncrementor {  
    private static int ms_value1;  
    private static long ms_value2;  
  
    private static synchronized void doWorkForValues()  
    {  
        ++ms_value1;  
        ms_value2 += ms_value1;  
    }  
  
    private static void incrementerCallback(int count, int idx)  
    {  
        for (var i = 0; i < count; ++i)  
            doWorkForValues();  
    }  
  
    public static int getValue1()  
    {  
        return ms_value1;  
    }  
  
    public static long getValue2()  
    {  
        return ms_value2;  
    }  
  
    public static void run(int count, int nThreads)  
    {  
        Thread [] threads = new Thread[nThreads];  
  
        for (var i = 0; i < nThreads; ++i) {  
            var idx = i;  
  
            threads[i] = new Thread(() -> incrementerCallback(count, idx), "Thread-");  
            threads[i].start();  
        }  
  
        for (var t : threads)  
            try {  
                t.join();  
            }  
            catch (InterruptedException ignore) {  
  
            }  
    }  
}
```

**Important points:**

- When a thread enters into synchronized method or block, it acquires lock and once it completes its task and exits from the synchronized method, it releases the lock.
- When thread enters into synchronized instance method or block, it acquires Object level lock and when it enters into synchronized static method or block it acquires class level lock.
- Java synchronization will throw null pointer exception if Object used in synchronized block is null. For example, If in **synchronized(instance)** , **instance** is null then it will throw null pointer exception.
- In Java, **wait(), notify() and notifyAll()** are the important methods that are used in synchronization.
- You can not apply java **synchronized** keyword with the variables.
- Don’t synchronize on the non-final field on synchronized block because the reference to the non-final field may change anytime and then different threads might synchronize on different objects i.e. no synchronization at all.

**Advantages**

- **Multithreading:** Since java is multithreaded language, synchronization is a good way to achieve mutual exclusion on shared resource(s).
- **Instance and Static Methods:** Both synchronized instance methods and synchronized static methods can be executed concurrently because they are used to lock different Objects.

**Limitations**

- **Concurrency Limitations:** Java synchronization does not allow concurrent reads.
- **Decreases Efficiency:** Java synchronized method run very slowly and can degrade the performance, so you should synchronize the method when it is absolutely necessary otherwise not and to synchronize block only for critical section of the code.
##  Volatile

The `volatile` keyword in Java is used to indicate that a variable’s value can be modified by different threads. Used with the syntax, `volatile dataType variableName = x;` It ensures that changes made to a volatile variable by one thread are immediately visible to other threads.

```java
class SharedObj
{
   // volatile keyword here makes sure that
   // the changes made in one thread are 
   // immediately reflect in other thread
   static **volatile** int sharedVar = 6;
}
```

The `volatile` keyword in Java is a type of variable modifier that tells the JVM (Java Virtual Machine) that a variable can be accessed and modified by multiple threads. The `volatile` keyword is used in multithreaded environments to ensure that changes made to a variable by one thread are immediately visible to other threads.

```java
public class VolatileExample {
    private volatile int count = 0;

    public void incrementCount() {
        count++;
    }

    public void displayCount() {
        System.out.println("Count: " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        VolatileExample example = new VolatileExample();
        example.incrementCount();
        example.displayCount();
    }
}

# Output:
# Count: 1
```

The `volatile` keyword ensures that the updated value of `count` is immediately visible to all threads. If `count` was not declared as `volatile`, there could be a delay in visibility of the updated value to other threads, leading to inconsistent results.

### Advantages and Pitfalls of Volatile Keyword

- The primary advantage of the `volatile` keyword is its guarantee of visibility of changes across threads. It ensures that a change in a `volatile` variable in one thread is immediately reflected in all other threads.

- However, the `volatile` keyword does not guarantee atomicity.  the increment operation (`count++`) in the above code is not atomic. It involves multiple steps – reading the current value of `count`, incrementing it, and then writing the updated value back to `count`. These steps are not performed as a single, indivisible operation. Therefore, in a multithreaded environment, it’s possible for another thread to modify `count` between these steps, leading to unexpected results.

### Volatile and Memory Visibility

 In Java, each thread has its own stack, and it can also access the heap. The heap contains objects and instance variables, but local variables are stored in the thread’s stack and are not visible to other threads.

When a variable is declared `volatile`, it ensures that the value of the `volatile` variable is always read from and written to the main memory, and not from the thread’s local cache. This ensures that the most recent value of the `volatile` variable is always visible to all threads, which is crucial for maintaining data consistency in multithreading.

## Difference Between Atomic, Volatile and Synchronized

| Modifier      | Synchronized                                       | Volatile                                              | Atomic                                              |
|---------------|---------------------------------------------------|-------------------------------------------------------|------------------------------------------------------|
| 1. Applicable | Only blocks or methods                            | Variables only                                        | Variables only                                       |
| 2. Purpose     | Lock-based concurrent algorithm                   | Non-blocking algorithm, more scalable                  | Non-blocking algorithm                               |
| 3. Performance | Relatively low (due to lock acquisition/release) | Relatively high compared to synchronized              | Relatively high compared to both volatile and synchronized |
| 4. Hazards     | Not immune to concurrency hazards (deadlock, livelock) | Immune to concurrency hazards (deadlock, livelock)     | Immune to concurrency hazards (deadlock, livelock)    |

| Method         | Advantages                                                | Disadvantages                                             |
| -------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `volatile`     | Ensures visibility of changes across threads              | Does not guarantee atomicity for compound operations      |
| `synchronized` | Ensures atomicity for compound operations                 | Can lead to thread blocking and decreased performance     |
| Atomic classes | Ensures atomicity for specific operations without locking | Limited to specific operations provided by atomic classes |
## Compare and Swap Example – CAS Algorithm

### Optimistic and Pessimistic Locking

Traditional locking mechanisms, e.g. **using _synchronized_ keyword in java, is said to be pessimistic technique** of locking or multi-threading. It asks you to first guarantee that no other thread will interfere in between certain operation (i.e. lock the object), and then only allow you access to any instance/method.

> **It’s much like saying “please close the door first; otherwise some other crook will come in and rearrange your stuff”.**

Though above approach is safe and it does work, but it **put a significant penalty on your application in terms of performance**. Reason is simple that waiting threads can not do anything unless they also get a chance and perform the guarded operation.

There exist one more approach which is more efficient in performance, and it **optimistic** in nature. In this approach, you proceed with an update, **being hopeful that you can complete it without interference**. This approach relies on collision detection to determine if there has been interference from other parties during the update, in which case the operation fails and can be retried (or not).

> **The optimistic approach is like the old saying, “It is easier to obtain forgiveness than permission”, where “easier” here means “more efficient”.**


**Compare and Swap** is a good example of such optimistic approach

### Compare and Swap Algorithm

This algorithm compares the contents of a memory location to a given value and, only if they are the same, modifies the contents of that memory location to a given new value. This is done as a single atomic operation. The atomicity guarantees that the new value is calculated based on up-to-date information; if the value had been updated by another thread in the meantime, the write would fail. The result of the operation must indicate whether it performed the substitution; this can be done either with a simple Boolean response (this variant is often called compare-and-set), or by returning the value read from the memory location (not the value written to it).

There are 3 parameters for a CAS operation:

1. A memory location V where value has to be replaced
2. Old value A which was read by thread last time
3. New value B which should be written over V

> **CAS says “I think V should have the value A; if it does, put B there, otherwise don’t change it but tell me I was wrong.” CAS is an optimistic technique—it proceeds with the update in the hope of success, and can detect failure if another thread has updated the variable since it was last examined.**

**EXAMPLE**

Assume V is a memory location where value “10” is stored. There are multiple threads who want to increment this value and use the incremented value for other operations, a very practical scenario. Let’s break the whole CAS operation in steps:

**1) Thread 1 and 2 want to increment it, they both read the value and increment it to 11.**

_V = 10, A = 0, B = 0_

**2) Now thread 1 comes first and compare V with it’s last read value:**

_V = 10, A = 10, B = 11_

```java
if     A = V
   V = B
 else
   operation failed
   return V
```

Clearly the value of V will be overwritten as 11, i.e. operation was successful.

**3) Thread 2 comes and try the same operation as thread 1**

_V = 11, A = 10, B = 11_

```java
if     A = V
   V = B
 else
   operation failed
   return V
```

**4) In this case, V is not equal to A, so value is not replaced and current value of V i.e. 11 is returned. Now thread 2, again retry this operation with values:**

_V = 11, A = 11, B = 12_

And this time, condition is met and incremented value 12 is returned to thread 2.

In summary, when multiple threads attempt to update the same variable simultaneously using CAS, one wins and updates the variable’s value, and the rest lose. But the losers are not punished by suspension of thread. They are free to retry the operation or simply do nothing.
##  ``wait()``, ``notify()`` and ``notifyAll()``

The `Object` class in Java has three final methods that allow threads to communicate about the locked status of a resource.

###  ``wait()``

It tells the calling thread to give up the lock and go to sleep until some other thread enters the same monitor and calls `notify()`. The `wait()` method releases the lock prior to waiting and reacquires the lock prior to returning from the `wait()` method. The `wait()` method is actually tightly integrated with the synchronization lock, using a feature not available directly from the synchronization mechanism.

In other words, it is not possible for us to implement the `wait()` method purely in Java. It is a **native method**.

```java
synchronized( lockObject )
{ 
	while( ! condition )
	{ 
		lockObject.wait();
	}
	
	//take the action here;
}
```

### ``notify()``

It wakes up one single thread that called `wait()` on the same object. It should be noted that calling `notify()` does not actually give up a lock on a resource. It tells a waiting thread that that thread can wake up. However, the lock is not actually given up until the notifier’s synchronized block has completed.

So, if a notifier calls `notify()` on a resource but the notifier still needs to perform 10 seconds of actions on the resource within its synchronized block, the thread that had been waiting will need to wait at least another additional 10 seconds for the notifier to release the lock on the object, even though `notify()` had been called.

```java
synchronized(lockObject) 
{
	//establish_the_condition;

	lockObject.notify();
	
	//any additional code if needed
}
```

### ``notifyAll()``

It wakes up all the threads that called `wait()` on the same object. The highest priority thread will run first in most of the situation, though not guaranteed.

```java
synchronized(lockObject) 
{
	establish_the_condition;

	lockObject.notifyAll();
}
```

> **In general, a thread that uses the `wait()` method confirms that a condition does not exist (typically by checking a variable) and then calls the `wait()` method. When another thread establishes the condition (typically by setting the same variable), it calls the `notify()` method. The wait-and-notify mechanism does not specify what the specific condition/ variable value is. It is on developer’s hand to specify the condition to be checked before calling `wait()` or `notify()`**.


**EXAMPLE**

- Producer thread produce a new resource in every 1 second and put it in ‘taskQueue’.
- Consumer thread takes 1 seconds to process consumed resource from ‘taskQueue’.
- Max capacity of taskQueue is 5 i.e. maximum 5 resources can exist inside ‘taskQueue’ at any given time.
- Both threads run infinitely.

**Producer Thread**

```java
class Producer implements Runnable
{
   private final List<Integer> taskQueue;
   private final int           MAX_CAPACITY;

   public Producer(List<Integer> sharedQueue, int size)
   {
      this.taskQueue = sharedQueue;
      this.MAX_CAPACITY = size;
   }

   @Override
   public void run()
   {
      int counter = 0;
      while (true)
      {
         try
         {
            produce(counter++);
         } 
		 catch (InterruptedException ex)
         {
            ex.printStackTrace();
         }
      }
   }

   private void produce(int i) throws InterruptedException
   {
      synchronized (taskQueue)
      {
         while (taskQueue.size() == MAX_CAPACITY)
         {
            System.out.println("Queue is full " + Thread.currentThread().getName() + " is waiting , size: " + taskQueue.size());
            taskQueue.wait();
         }
		  
         Thread.sleep(1000);
         taskQueue.add(i);
         System.out.println("Produced: " + i);
         taskQueue.notifyAll();
      }
   }
}
```

- Here “`produce(counter++)`” code has been written inside infinite loop so that producer keeps producing elements at regular interval.
- We have written the `produce()` method code following the general guideline to write `wait()` method as mentioned in first section.
- Once the `wait()` is over, producer add an element in taskQueue and called `notifyAll()` method. Because the last-time `wait()` method was called by consumer thread (that’s why producer is out of waiting state), consumer gets the notification.
- Consumer thread after getting notification, if ready to consume the element as per written logic.
- Note that both threads use `sleep()` methods as well for simulating time delays in creating and consuming elements.

**Consumer Thread**

```java
class Consumer implements Runnable
{
   private final List<Integer> taskQueue;

   public Consumer(List<Integer> sharedQueue)
   {
      this.taskQueue = sharedQueue;
   }

   @Override
   public void run()
   {
      while (true)
      {
         try
         {
            consume();
         } catch (InterruptedException ex)
         {
            ex.printStackTrace();
         }
      }
   }

   private void consume() throws InterruptedException
   {
      synchronized (taskQueue)
      {
         while (taskQueue.isEmpty())
         {
            System.out.println("Queue is empty " + Thread.currentThread().getName() + " is waiting , size: " + taskQueue.size());
            taskQueue.wait();
         }
         Thread.sleep(1000);
         int i = (Integer) taskQueue.remove(0);
         System.out.println("Consumed: " + i);
         taskQueue.notifyAll();
      }
   }
}
```


- Here “`consume()`” code has been written inside infinite loop so that consumer keeps consuming elements whenever it finds something in taskQueue.
- Once the `wait()` is over, consumer removes an element in taskQueue and called `notifyAll()` method. Because the last-time wait() method was called by producer thread (that’s why producer is in waiting state), producer gets the notification.
- Producer thread after getting notification, if ready to produce the element as per written logic.

**Test**

```java
public class ProducerConsumerExampleWithWaitAndNotify
{
   public static void main(String[] args)
   {
      List<Integer> taskQueue = new ArrayList<Integer>();
      int MAX_CAPACITY = 5;
      Thread tProducer = new Thread(new Producer(taskQueue, MAX_CAPACITY), "Producer");
      Thread tConsumer = new Thread(new Consumer(taskQueue), "Consumer");
      tProducer.start();
      tConsumer.start();
   }
}
```

```shell
Produced: 0
Consumed: 0
Queue is empty Consumer is waiting , size: 0
Produced: 1
Produced: 2
Consumed: 1
Consumed: 2
Queue is empty Consumer is waiting , size: 0
Produced: 3
Produced: 4
Consumed: 3
Produced: 5
Consumed: 4
Produced: 6
Consumed: 5
Consumed: 6
Queue is empty Consumer is waiting , size: 0
Produced: 7
Consumed: 7
Queue is empty Consumer is waiting , size: 0
```

###  Difference between ``sleep()`` and ``wait()``

#### Method called on

- `wait()` – Call on an object; current thread must synchronize on the lock object.
- `sleep()` – Call on a Thread; always currently executing thread.

####  Synchronized

- `wait()` – when synchronized multiple threads access same Object one by one.
- `sleep()` – when synchronized multiple threads wait for sleep over of sleeping thread.

####  Lock Duration

- `wait()` – release the lock for other objects to have chance to execute.
- `sleep()` – keep lock for at least t times if timeout specified or somebody interrupt.

#### Wake up condition

- `wait()` – until call notify(), notifyAll() from object
- `sleep()` – until at least time expire or call interrupt().

#### Usage

- `sleep()` – for time-synchronization
- `wait()` – for multi-thread-synchronization.

## ThreadLocal Variables

one of the most critical aspects of a concurrent application is shared data. When you create thread that implements the `Runnable` interface and then start various `Thread` objects using the same `Runnable` object, all the threads share the same attributes that are defined inside the runnable object. This essentially means that if you change any attribute in a thread, all the threads will be affected by this change and will see the modified value by first thread. Sometimes it is desired behavior e.g. multiple threads increasing / decreasing the same counter variable; but sometimes you want to ensure that every thread MUST work on it’s own copy of thread instance and does not affect others data.

###  When to use ThreadLocal?

1. **Thread Isolation is Required**: If you have data that needs to be isolated on a per-thread basis and you don't want different threads to interfere with each other's data.
    
2. **Avoid Passing Context Explicitly**: Instead of passing context data explicitly through method parameters or through other means, `ThreadLocal` allows you to access the data directly within the thread's execution context.
    
3. **Concurrency without Shared State**: When you want to achieve concurrency without the need for shared state management or synchronization mechanisms between threads.

### ThreadLocal Class

```java
public class ThreadLocal<T> extends Object {...}
```

`ThreadLocal` instances are typically **_private static_** fields in classes that wish to associate state with a thread (e.g., a user ID or Transaction ID).

This class has following methods:

1. **``get()``** : Returns the value in the current thread’s copy of this thread-local variable.
2. **``initialValue()``** : Returns the current thread’s “initial value” for this thread-local variable.
3. **``remove()``** : Removes the current thread’s value for this thread-local variable.
4. **``set(T value)``** : Sets the current thread’s copy of this thread-local variable to the specified value.

**EXAMPLE**

```java
class DemoTask implements Runnable
{
   // Atomic integer containing the next thread ID to be assigned
   private static final AtomicInteger        nextId   = new AtomicInteger(0);
    
   // Thread local variable containing each thread's ID
   private static final ThreadLocal<Integer> threadId = new ThreadLocal<Integer>()
                                                         {
                                                            @Override
                                                            protected Integer initialValue()
                                                            {
                                                               return nextId.getAndIncrement();
                                                            }
                                                         };
 
   // Returns the current thread's unique ID, assigning it if necessary
   public int getThreadId()
   {
      return threadId.get();
   }
   // Returns the current thread's starting timestamp
   private static final ThreadLocal<Date> startDate = new ThreadLocal<Date>()
                                                 {
                                                    protected Date initialValue()
                                                    {
                                                       return new Date();
                                                    }
                                                 };
 
   
 
   @Override
   public void run()
   {
      System.out.printf("Starting Thread: %s : %s\n", getThreadId(), startDate.get());
      try
      {
         TimeUnit.SECONDS.sleep((int) Math.rint(Math.random() * 10));
      } catch (InterruptedException e)
      {
         e.printStackTrace();
      }
      System.out.printf("Thread Finished: %s : %s\n", getThreadId(), startDate.get());
   }
}
```

```shell
Starting Thread: 0 : Wed Dec 24 15:04:40 IST 2014
Thread Finished: 0 : Wed Dec 24 15:04:40 IST 2014
 
Starting Thread: 1 : Wed Dec 24 15:04:42 IST 2014
Thread Finished: 1 : Wed Dec 24 15:04:42 IST 2014
 
Starting Thread: 2 : Wed Dec 24 15:04:44 IST 2014
Thread Finished: 2 : Wed Dec 24 15:04:44 IST 2014
```

> **Most common use of thread local is when you have some object that is not thread-safe, but you want to avoid synchronizing access to that object using synchronized keyword/block. Instead, give each thread its own instance of the object to work with.**  
>**A good alternative to synchronization or threadlocal is to make the variable a local variable. Local variables are always thread safe. The only thing which may prevent you to do this is your application design constraints.**

##  Executor Framework

The Executor Framework is a powerful and flexible tool for managing and executing tasks in Java applications. **_It provides a way to separate the task execution logic from the application code, allowing developers to focus on business logic rather than thread management._**

![[Pasted image 20240229132328.png]]

The framework includes several key components, including the `Executor`, `ExecutorService`, `ScheduledExecutorService`, and `ThreadPoolExecutor`.

==**_The Executor Framework is particularly useful for managing concurrent tasks in applications with a large number of threads or high levels of concurrency._**== It is widely used in applications such as web servers, where multiple requests must be processed simultaneously.

==**_By providing a simple and efficient way to manage task execution,_**== ==**_the Executor Framework can help developers improve the_**== ==**performance** and  **_scalability_** of their applications while minimizing the risk of threading errors and other concurrency issues._**==

### Benefits of Executor Framework

- The framework mainly separates task creation and execution. Task creation is mainly boilerplate code and is easily replaceable.
- With an executor, we have to create tasks that implement either Runnable or Callable interface and send them to the executor.
- Executor internally maintains a (configurable) thread pool to improve application performance by avoiding the continuous spawning of threads.
- Executor is responsible for executing the tasks, and running them with the necessary threads from the pool.

### `Executor`:

This interface provides a way to execute submitted `Runnable` tasks.

> ==An Executor is normally used instead of explicitly creating threads.==

rather than invoking `new Thread(new RunnableTask()).start()` for each task of a set of tasks

```java
Executor executor = new ThreadPoolExecutor(1, 10,  0L, TimeUnit.MILLISECONDS, new LinkedBlockingQueue<Runnable>());  
executor.execute(runnableTask);
```

`execute()`: This execute() method executes the given `Runnable` task at some time in the future. The command(task) may execute in a new thread, from the pooled thread, or in the calling thread, at the discretion of the `Executor` implementation (e.g. `ThreadPoolExecutor`).

#### Types of executor

- **Single thread Executor**

	The ``SingleThreadExecutor`` is a special type of executor that has only a single thread. It is used when we need to execute tasks in sequential order.

	`ExecutorService executor = Executors.newSingleThreadExecutor()`

- **Fixed thread pool**

	FixedThreadPool is another special type of executor that is a thread pool having a fixed number of threads. By this executor, the submitted task is executed by the n thread.  
	The tasks are then stored in **LinkedBlockingQueue** until previous tasks are not completed.
	
	`ExecutorService executor = Executors.newFixedThreadPool(4);`

**CSD EXAMPLE**

```java
public class StringGenerator {  
    private final List<String> m_list;  
    private final int m_count;  
    private final int m_nThreads;  
    private final RandomGenerator m_randomGenerator;  
    private final ExecutorService m_threadPool;  
  
    private void generateCallback()  
    {  
        var self = Thread.currentThread();  
  
        for (var i = 0; i < m_count; ++i)  
            synchronized (this) {  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(5, 15))));  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(1, 15))));  
            }  
    }  
  
    public StringGenerator(List<String> list, int count, int nThreads, RandomGenerator randomGenerator)  
    {  
        m_list = list;  
        m_count = count;  
        m_randomGenerator = randomGenerator;  
        m_nThreads = nThreads;  
        m_threadPool = Executors.newFixedThreadPool(m_nThreads);  
    }  
  
    public int size()  
    {  
        return m_list.size();  
    }  
  
    public void run()  
    {  
        Future<?> [] futures = new Future[m_nThreads];  
  
        for (var i = 0; i < m_nThreads; ++i)  
            futures[i] = m_threadPool.submit(this::generateCallback);  
  
        for (var future : futures)  
            try {  
                future.get();  
            }  
            catch (ExecutionException | InterruptedException ignore) {  
  
            }  
  
        for (var str : m_list)  
            Console.writeLine(str);  
  
        m_threadPool.shutdown();  
    }  
}
```

- **Cached thread pool**

	The ``CachedThreadPool`` is a special type of thread pool that is used to execute short-lived parallel tasks. The cached thread pool doesn't have a fixed number of threads. When a new task comes at a time and all the threads are busy executing some other tasks, a new thread is created by the pool and added to the executor.
	
	`ExecutorService executor = Executors.newCachedThreadPool();`

**CSD EXAMPLE**

```java
public class StringGenerator {  
    private final List<String> m_list;  
  
    private final int m_min;  
    private final int m_bound;  
    private final int m_count;  
  
    private final RandomGenerator m_randomGenerator;  
    private final ExecutorService m_threadPool;  
  
    private void generateCallback()  
    {  
        var self = Thread.currentThread();  
  
        for (var i = 0; i < m_count; ++i)  
            synchronized (this) {  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(5, 15))));  
                m_list.add(String.format("%s:%s", self.getName(), StringUtil.getRandomTextEN(m_randomGenerator, m_randomGenerator.nextInt(1, 15))));  
            }  
    }  
  
    public StringGenerator(List<String> list, int min, int bound, int count, RandomGenerator randomGenerator)  
    {  
        m_list = list;  
        m_min = min;  
        m_bound = bound;  
        m_count = count;  
        m_randomGenerator = randomGenerator;  
        m_threadPool = Executors.newCachedThreadPool();  
    }  
  
    public int size()  
    {  
        return m_list.size();  
    }  
  
    public void run()  
    {  
        Future<?> [] futures = new Future[m_randomGenerator.nextInt(m_min, m_bound)];  
  
        Console.writeLine("Number of threads needed:%s", futures.length);  
  
        for (var i = 0; i < futures.length; ++i)  
            futures[i] = m_threadPool.submit(this::generateCallback);  
  
        m_threadPool.shutdown();  
  
        for (var future : futures)  
            try {  
                future.get();  
            }  
            catch (ExecutionException | InterruptedException ignore) {  
  
            }  
  
        for (var str : m_list)  
            Console.writeLine(str);  
    }  
}
```

- **Scheduled executor service**

	The ``ScheduledExecutorService`` interface runs tasks after some predefined delay and/or periodically.
	
	`ScheduledExecutorService scheduledExecService = Executors.newScheduledThreadPool(1);   `  
	The **``scheduleAtFixedRate``** and **``scheduleWithFixedDelay``** are the two methods that are used to schedule the task in ``ScheduledExecutor``.  
	The **``scheduleAtFixedRate``** method executes the task with a fixed interval when the previous task ended.  
	The **``scheduleWithFixedDelay``** method starts the delay count after the current task is complete.  
	The main difference between these two methods is their interpretation of the delay between successive executions of a scheduled job.
	
```java
	scheduledExecService.scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)   `
	
	scheduledExecService.scheduleWithFixedDelay(Runnable command, long initialDelay, long period, TimeUnit unit)
```

**CSD EXAMPLE**

```java
public class DigitalClock {  
    private final DateTimeFormatter m_formatter;  
    private final ScheduledExecutorService m_scheduledExecutorService;  
    private final int m_timeoutValue;  
    private final TimeUnit m_timeUnit;  
  
    public DigitalClock(int timeoutValue, TimeUnit timeUnit)  
    {  
        m_formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH.mm.ss");  
        m_scheduledExecutorService = Executors.newSingleThreadScheduledExecutor();  
        m_timeoutValue = timeoutValue;  
        m_timeUnit = timeUnit;  
    }  
  
    public void run()  
    {  
        Console.writeLine("%s", m_formatter.format(LocalDateTime.now()));  
        var future = m_scheduledExecutorService.schedule(() -> Console.writeLine("%s", m_formatter.format(LocalDateTime.now())), m_timeoutValue, m_timeUnit);  
  
        try {  
            future.get();  
        }  
        catch (ExecutionException | InterruptedException ignore){  
  
        }  
  
        m_scheduledExecutorService.shutdown();  
    }
```

### ``ExecutorService``:

An `ExecutorService` provides methods to manage termination and methods that can produce a `Future` for tracking the progress of one or more asynchronous tasks.  
An ``ExecutorService`` can be shut down, which will cause it to reject new tasks.

> ==**`ExecutorService`**== ==**_is an extended version of_**== ==**_Executor_**== ==**_with more methods and features._**==

1. _When an_ `ExecutorService` _is terminated then it has no tasks actively executing, no tasks waiting for execution, and no new tasks can be submitted._
2. _Hence an unused_ `ExecutorService` _should be shut down to allow the reclamation of its resources._

#### ``ExecutorService`` Methods

1. **``submit()``**: this method accepts a ==**runnable**== or ==**callable**== ==task== and returns a **`Future`**_that can be used to wait for completion and/or to cancel execution._

2. **``invokeAny()``**: this method accepts a collection of callable tasks and returns a result if any tasks are successful.

3. **``invokeAll()``**: this method accepts a collection of callable tasks and returns a List of Future, which will hold the result returned by each task when the asynchronous tasks are completed.

4. `shutdown()` and `shutdownNow()`:

	The `shutdown()` method of `ExecutorService` will allow previously submitted tasks to execute before terminating the ExecutorService and performing memory clean-up, whereas the `shutdownNow()` method prevents waiting for tasks from starting and attempts to stop currently executing tasks.
	
	This `shutdownNow()` returns a list of tasks that are waiting to be processed. It is up to the developer to decide what to do with these tasks.



```java
//Create executorService using ThreadPoolExecutor implementation of  
//ExecutorService.  
  
ExecutorService executorService = new ThreadPoolExecutor(1, 5, 0L,  
TimeUnit.MILLISECONDS,  
new LinkedBlockingQueue<Runnable>());  
//Create callable tasks using lambda implementation of call method of  
//Callable Interface  
  
Callable<String> callableTask = () -> {  
System.out.println("Call method called.");  
TimeUnit.MILLISECONDS.sleep(2000);  
return "Task execution in call method";  
};  
  
//submit single callable task to executorService, that is returning a Future  
Future<String> future = executorService.submit(callableTask);  
System.out.println(future.get());  
  
//Create list of callable tasks  
List<Callable<String>> callableTasks = new ArrayList<>();  
callableTasks.add(callableTask);  
callableTasks.add(callableTask);  
callableTasks.add(callableTask);  
  
//submit the list of callable tasks to invokeAny method that returns a result.  
String result = executorService.invokeAny(callableTasks);  
System.out.println(result);  
  
//submit the list of callable tasks to invokeAll method that returns a list  
// of futures representing results of asynchronous tasks.  
List<Future<String>> futures = executorService.invokeAll(callableTasks);  
  
//shutdown the executorService after completing all tasks to reclaim memory.  
executorService.shutdown();
```

##### What is ``ThreadPoolExecutor``?`

The **``ThreadPoolExecutor``** is an implementation of **``ExecutorService``** and provides a pool of threads that execute the **_runnable_** _or_ **_callable tasks_**.

```java
ExecutorService executorService = new ThreadPoolExecutor(1, 5, 0L,  
TimeUnit.MILLISECONDS,  
new LinkedBlockingQueue<Runnable>());
```
`corePoolSize` — the number of threads to keep in the pool, even if they are idle unless allowCoreThreadTimeOut is set.

`maximumPoolSize` — the maximum number of threads to allow in the pool.

`keepAliveTime` — when the number of threads is greater than the core, this is the maximum time that excess idle threads will wait for new tasks before terminating.

`unit` — the time unit for the keepAliveTime argument.

`workQueue` — the queue to use for holding tasks before they are executed. This queue will hold only the Runnable tasks submitted by the execute.

**the above code can be replaced by a factory method of the Executors class:**

```java
ExecutorService executorService = Executors.newFixedThreadPool(10);
```

The advantages of using Thread pools are that it addresses two different problems:

- They usually provide improved performance when executing large numbers of asynchronous tasks, due to reduced per-task invocation overhead.
- The `ThreadPoolExecutor` provides an efficient way of managing threads and resources associated with it while executing a huge number of async tasks.

## The Future Interface

The `Future` interface is an interface that represents a result that will eventually be returned in the future. We can check if a `Future` has been fed the result, if it's awaiting a result or if it has failed before we try to access it

```java
public interface Future<V> {
    V get() throws InterruptedException, ExecutionException;
    V get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException;
    boolean isCancelled();
    boolean isDone();
    boolean cancel(boolean mayInterruptIfRunning)
}
```

The `get()` method retrieves the result. If the result has not yet been returned into a `Future` instance, the `get()` method _will wait_ for the result to be returned. It's _crucial_ to note that `get()` will block your application if you call it before the result has been returned.

also specify a `timeout` after which the `get()` method will throw an exception if the result hasn't yet been returned, preventing huge bottlenecks.

The `cancel()` method attempts to cancel the execution of the current task. The attempt will fail if the task has already completed, has been canceled, or could not be canceled because of some other reasons.

The `isDone()` and `isCancelled()` methods are dedicated to finding out the current status of an associated `Callable` task.

**CSD EXAMPLE**

```java
class Application {  
    private static void doCalculate(int nThreads, int count, int min, int bound)  
    {  
            var threadPool = Executors.newFixedThreadPool(nThreads);  
            var futures = new ArrayList<Future<Long>>(nThreads);  
            var threadParams = new ThreadParam[nThreads];  
  
            for (var i = 0; i < nThreads; ++i) {  
                int idx = i;  
  
                threadParams[idx] = new ThreadParam(count, min, bound);  
                futures.add(threadPool.submit(() -> generateAndFindTotalThreadCallback(threadParams[idx])));  
            }  
  
            try {  
                for (var future : futures)  
                    Console.writeLine("Result:%d", future.get());  
            }  
            catch (ExecutionException ex) {  
                Console.Error.writeLine("Error Message:%s", ex.getMessage());  
            }  
            catch (InterruptedException ignore) {  
  
            }  
  
            threadPool.shutdown();  
    }  
  
    private static long generateAndFindTotalThreadCallback(ThreadParam param)  
    {  
        var random = new Random();  
        var count = param.getCount();  
        var min = param.getMin();  
        var bound = param.getBound();  
        var total = 0L;  
  
        for (var i = 0; i < count; ++i) {  
            var val = random.nextInt(min, bound);  
  
            //Console.writeLine("%s:%d", self.getName(), val);  
            total += val;  
        }  
  
        return total;  
    }  
  
    public static void run(String[] args)  
    {  
        if (args.length != 4) {  
            Console.Error.writeLine("Wrong number of arguments!...");  
            System.exit(1);  
        }  
  
        try {  
            doCalculate(parseInt(args[0]), parseInt(args[1]), parseInt(args[2]), parseInt(args[3]));  
        }  
        catch (NumberFormatException ignore) {  
            Console.writeLine("Invalid arguments!...");  
        }  
    }  
}
```

### Limitations of the Future

- `Future`s can not be explicitly completed (setting its value and status).
- It doesn't have a mechanism to create stages of processing that are chained together.
- There is no mechanism to run `Future`s in parallel and after to combine their results together.
- The `Future` does not have any exception handling constructs.

 Java provides concrete Future implementations that provide these features (`CompletableFuture`, `CountedCompleter`, `ForkJoinTask, FutureTask`).



# NETWORK PROGRAMMING

## Interprocess Communication #CSD_NOTES

In modern systems, direct communication between processes is not inherently possible. In this sense, processes operate in an isolated manner from each other. One process cannot directly access the memory area of another process. However, in certain situations, communication between processes may be necessary. This type of communication between processes is referred to as ***Inter-Process Communication (IPC)*** in operating system terminology.

IPC generally can be divided into two main categories:

- Communication Between Processes of the Same Machine
- Communication Between Processes of Different Machines

### Communication Between Processes of the Same Machine

The communication techniques between processes on the same machine vary in operating systems. For example, in Unix/Linux and MacOS X systems, pipes (pipe and fifo), message queues, and shared memory areas (shared memory) are typical communication techniques. In addition to these, there are other communication techniques.

Although Android systems are developed on the embedded Linux kernel, applications developed with the Android SDK (Software Development Kit) cannot directly use these techniques. To utilize these techniques in Android applications, development must be done using the NDK (Native Development Kit). So, how will two Android applications (processes) communicate with each other? For this purpose, there are some techniques provided by the Android SDK. For example, Messenger and AIDL (Android Interface Definition Language) services are used in this context. These are briefly referred to as ***Binder*** and ***Remote Services.*** In addition to these, there are also some methods that can be indirectly used for communication.

### Communication Between Processes of Different Machines

Different machines may be connected to each other within a network. We may want a program running on one machine to send and receive information to and from a process on another machine connected to the network. In such communication, various actors beyond the operating system would come into play. For instance, hardware components up to the hub used in the cabling system would be involved. Moreover, in such communications, even the operating systems can be different from each other. In heterogeneous environments like these, predefined rules are necessary for the healthy execution of communication.

For example, what are the cable standards and connectors? What will be the characteristics of the network card? How will information be segmented into packets and transmitted? How will machines distinguish themselves from each other, and so on? All of these specifications are referred to as ***protocol***.

Just like functions become capable of performing higher-level tasks by calling each other, protocols are also constructed by stacking layers on top of each other. Each upper protocol defines only its own requirements with the assumption that the lower layers are already in place. There are many benefits to such a layered design. For example, higher-level protocols do not contain details, and they are less affected by changes in lower-level protocols. This is how many protocol families are created for communication between different machines. Examples include AppleTalk, NETBIOS, and so on.

The IEEE has published a document named ***OSI (Open System Interconnection)*** outlining how protocol layers should be created for computer communication under the network category. This document is known as the OSI model. The OSI model is not a protocol family but serves as a guide for creating protocol families. OSI consists of a total of 7 layers:

![[Pasted image 20240229143026.png]]

At the lowest layer of OSI is the ***Physical Layer***, where the communication medium is defined. This includes specifications for cables, connectors, voltage levels, etc. Above this is the **Data Link Layer**, which includes determinations related to network cards, physical addressing, and so on. For example, the Ethernet Protocol, which is a protocol for Ethernet cards, is a Data Link Layer Protocol. The '***Network Layer***' is one of the most important layers where logical addressing is defined, and the segmentation and transmission of information into packets are defined. For example, the IP Protocol of the IP protocol family is associated with the Network layer according to OSI. In the Network layer, there are also routing determinations for internetworking. Above the Network layer is the ***Transport Layer***, where specifications include packet numbering, defining logical port addresses, and provisions for compensating for errors. For instance, the TCP and UDP protocols in the IP protocol family are protocols associated with the Transport Layer. The ***Session Layer*** is not present in many families. Here, there are determinations for establishing the necessary sessions for communication, such as permissions and authentication. Above this is the ***Presentation Layer***, where specifications for compressing, decompressing, encrypting, etc., the information sent and received are found. The IP protocol family does not have a Presentation Layer. Finally, at the top is the ***Application Layer***, which contains specifications that software created to achieve a specific purpose will use. For example, POP3 used for email and FTP used for file transfer are Application Layer Protocols.


The name ***Internet*** is derived from the word ***internetworking***. Internetworking is formed by connecting local networks to each other through devices called routers. Internetworking is a fundamental term, and the name of the IP protocol family comes from this concept. Today, when we say ***Internet***, the massive network that has evolved from ARPANET comes to mind. (When writing '***Internet***' with an uppercase 'I' or ***The Internet***, this network is understood.) Undoubtedly, with the existing protocols, anyone can establish their own internet. For example, we can create a separate Internet world with a few friends. In fact, some countries have their own unique internets in this way.

## IP Protocol Family

IP is an open protocol family. Here, 'open' means it is managed by an independent consortium where no company owns it. Additionally, documents are shared openly, and anyone interested can make suggestions.

The IP protocol was designed by Vint Cerf and Bob Kahn in 1974, initially as TCP and later in the form of IP. Subsequently, other members joined the family. The first significant implementation was done on ***BSD*** systems. Its popularity greatly increased in 1983 when ARPANET transitioned to the IP family.

The fundamental protocols of the IP protocol family consist of four layers.

![[Pasted image 20240305073900.png]]

The most crucial base protocol of the family is the ***IP (Internetworking Protocol)***. In fact, it is this protocol that gives the family its name. The IP protocol is a ***packet-switching protocol***, meaning information is segmented into packets for transmission and reception. In the IP protocol, addressing is logical rather than physical. In the IP protocol family, each unit connected to the network is called a 'host.' In the IP protocol, each host has a logical address called an '***IP address***' associated with its name.

A logical address implies that it is assigned not in terms of hardware but through software, meaning it is not determined by hardware but by the software. However, for example, the ***MAC*** address used by the Ethernet protocol is a physical address. A physical address is one that is hardware-based, either physically embedded on the card or detected and processed by the hardware itself. Therefore, logical addresses are dynamic, while physical addresses are static. Logical addresses are assigned to us when we join a network. Of course, we can also insist on being assigned a specific address.

The IP protocol also has versions. Currently, the predominantly used version is IPV4. However, IPV6 has slowly become more widespread. In IPV4, IP addresses are 4 bytes long. In contrast, in IPV6, IP addresses are 16 bytes long. The 4-byte IP addresses are now inadequate for current needs.

Today, in our computers, ***Ethernet and Wireless Protocols*** are used as the physical and data link layers. The Ethernet protocol requires an Ethernet card. This card is used to physically send and receive information from our computer. The Ethernet protocol is also a packet-switching protocol, meaning information is sent and received in packets. Packet switching enables efficient use of the communication line. We can create a local area network (LAN) by connecting Ethernet cards with a hub. The networks in our homes today are local networks. Devices called '***routers***' are used to connect local networks to each other. An Ethernet card (i.e., network card) is used for packet communication between computers on the same network. However, a router is used for packet communication between different networks. Today, modems like ADSL in our homes also serve as routers. 

![[Pasted image 20240305080611.png]]


In our home, the local network connects to the massive network called the Internet through a router, acting like a single host. Therefore, we have only one IP address that will be used externally for the Internet (assuming we have a single router and connection). Our local network in our home is a separate IP network, essentially a separate world. If we wish, we can run all Internet applications (i.e., IP protocol applications) on our local network without accessing the Internet at all. This is commonly referred to as an '***Intranet***.' In this case, a computer in our home has a local IP address, and our router has a public IP address seen from the Internet. The router distributes incoming packets from the outside world to the appropriate computer in the local network. It also sends local network packets to the outside world if they are destined for external addresses. When we send information from one host to another in our local network, the router is not involved.

In the IP protocol, a sent packet has an 'IP header' at the beginning, which contains metadata information about the packet. For example, details such as which IP address the packet is sent to, checksum information, which IP version is used, etc. In practice (although not mandatory), since the information is ultimately sent and received with an Ethernet card, the IP packet is encoded in the data section of the Ethernet protocol's ethernet packet. The Ethernet protocol also has a separate header section.

![[Pasted image 20240305081458.png]]

Can information consisting of multiple packets be sent with the IP protocol? Yes, but for this, we need to create a sort of separate protocol by assigning numbers to the packets. In fact, the TCP protocol is a similar protocol to achieve this

- ***TCP (Transmission Control Protocol)*** is a reliable protocol, meaning it compensates for the breakdown of communication on the way and ensures the proper transfer of packets. This is because TCP includes ***flow control***, allowing the sender and receiver to mutually address and compensate for any misbehaving packets. TCP is a ***stream-oriented*** protocol, meaning it can resume reading byte by byte from where it left off. With TCP, larger pieces of information can be sent and received. In this case, TCP divides the information into IP packets, assigns numbers to them, and ensures their secure delivery to the other side. The receiving end can then retrieve the information byte by byte, as if reading from a pipe.

- ***UDP (User Datagram Protocol)*** provides unreliable ***packet-based communication***. In UDP, information is sent and received in independent packets, similar to IP. In UDP, a packet is either received or not, and reading byte by byte is not possible. There is no feedback regarding whether the packet has been received. Of course, due to this feature, UDP is faster. UDP is especially preferred for periodic data transmissions, television broadcasting, and similar processes.

- TCP is a ***connection-oriented protocol***, while UDP is ***connectionless***. A connection-oriented protocol means that the two parties must establish a connection before communicating and get to know each other for mutual conversation. TCP typically implies a ***client-server*** style of operation. In client-server communication, one side becomes the client, and the other side becomes the server. The client side connects to the server side, and communication takes place afterward.

| Protocol | Connection Type | Data Type         | Reliability  | Speed     |
|----------|------------------|-------------------|--------------|-----------|
| TCP      | Connection-oriented | Stream-based    | Reliable     | Slow      |
| UDP      | Connectionless     | Datagram-based  | Unreliable   | Fast      |

In TCP and UDP, the concept of a **port number** is also involved. Port numbers are designed to differentiate applications on the same host, analogous to internal phone numbers within a company. In TCP and UDP protocols, knowing only the IP address of the host is not sufficient to send information. It is also necessary to know which port the application on that host is associated with. Typically, the representation includes the IP address and port number separated by a ':' character, like "ip:port".

In IPV4, there are a total of 65536 port numbers (meaning two bytes are allocated for the port number). In IPV6, port numbers are 4 bytes long. The first 1024 port numbers in IPV4 are reserved for Internet's own application protocols, known as **"well-known"** ports. For example, FTP uses port 21, SSH uses port 22, Telnet uses port 23, and HTTP uses port 80. If you are assigning a port number for your own applications, it is recommended not to use the first 1024 ports.

## **Client-Server Model**

As mentioned above, the TCP type operates as a client-server model. In the Client-Server model, there are two separate programs called client and server. The main task is performed by the server program. The client only makes requests. The server does the work and sends the results to the client. Depending on how it is written, a server can serve multiple clients 'simultaneously.

>**Key Notes**: If a server, while serving one client, cannot serve another client simultaneously, such servers are called "***single-client***" or "***iterative***" servers. On the contrary, if a client can receive services while another client's service is ongoing, such servers are called "**multi-client**" or "**concurrent**" servers.

![[Pasted image 20240305084207.png]]

In the Client-Server model, the client initially connects to the server. This concept is generally referred to as "handshaking." Communication begins afterward. Although Client-Server applications often evoke TCP, it is essentially a communication architecture. In other words, the use of the IP family is not necessary for client-server operation. This interaction, for example, can be achieved between processes on the same machine using pipes or message queues.

**Advantages of the Client-Server model include:**

1. The machine on which the server program runs can be powerful. We may want to leverage its capabilities. For example, performing a time-consuming task on a mobile device might be more convenient by using the mobile device as a client and having the server perform the main task.
    
2. The server program can facilitate resource sharing. For instance, a printer is connected to a single computer. Print programs on other computers act as clients, sending requests to the server machine where the printer is connected. The server performs the print operation for the client. Similarly, a server might be connected to a database, and clients can request data from it. For example, in bank ATMs, the database is not inside the ATM machine. The ATM program inside behaves like a client program.
    
3. The server program can facilitate collaboration among clients. It can mediate communication between them. For instance, in a chat program, clients don't need to know each other. Each client connects to the server, and the server facilitates communication between clients.
    
4. Client-Server operation can be encountered in distributed applications. This means we might want to perform specific parts of a task on different computers and then combine the results.

### Socket Concept

The communication between processes on different machines requires the support of protocols by the operating system. Nowadays, operating systems commonly support various protocols. Operating systems like Windows, Mac OS X, and Linux have long been supporting the IP protocol family. To enable the development of application programs using a specific protocol family on operating systems, there needs to be a library. This library is referred to as the '***socket library***.'

Systems such as Windows, Mac OS X, and Linux support the socket library in a very similar manner. Originally designed for use with the C programming language, the socket library has served as the basis for creating similar libraries in many environments. In higher-level environments like Java, there are classes that facilitate writing code for socket operations independently of the underlying operating system.

The socket library is not designed exclusively for the IP protocol family. Socket functions are common interfaces for many protocol families. It serves as a general interface that encompasses various protocols. Therefore, the parametric structures of functions tend to be a bit more complex

The socket library was first implemented in 1983 on BSD systems. It was later applied to other systems. Microsoft's socket interface is derived from BSD sockets, and it is called the ***Winsock*** library. In Windows, there are two groups of socket APIs. The first one is entirely BSD-compatible APIs (where function names are the same as in BSD). The second group is Windows-specific socket APIs that start with WSA. If we use BSD-compatible socket functions on Windows, we can ensure compatibility with UNIX/Linux as well.

---

## Java Networking

All the Java program communications over the network are done at the application layer. The **java.net** package of the J2SE APIs comprises various classes and interfaces that execute the low-level communication features, enabling the user to formulate programs that focus on resolving the problem.

### Common Network Protocols

The **java.net** package of the Java programming language includes various classes and interfaces that provide an easy-to-use means to access network resources. Other than classes and interfaces, the **java.net** package also provides support for the two well-known network protocols.

1. **Transmission Control Protocol (TCP) –** TCP or Transmission Control Protocol allows secure communication between different applications. TCP is a connection-oriented protocol which means that once a connection is established, data can be transmitted in two directions. This protocol is typically used over the Internet Protocol. Therefore, TCP is also referred to as TCP/IP. 



2. **User Datagram Protocol (UDP) –** UDP or User Datagram Protocol is a connection-less protocol that allows data packets to be transmitted between different applications. UDP is a simpler Internet protocol in which error-checking and recovery services are not required. In UDP, there is no overhead for opening a connection, maintaining a connection, or terminating a connection. In UDP, the data is continuously sent to the recipient, whether they receive it or not.


#### ***TCP (Transmission Control Protocol)***

Transmission Control Protocol is a connection-oriented protocol for communications that helps in the exchange of messages between different devices over a network. The Internet Protocol (IP), which establishes the technique for sending data packets between computers, works with TCP.

The position of TCP is at the transport layer of the OSI model. TCP also helps in ensuring that information is transmitted accurately by establishing a virtual connection between the sender and receiver.

##### Internet Protocol (IP)?

Internet Protocol is a method that is useful for sending data from one device to another from all over the internet. Every device contains a unique IP Address that helps it communicate and exchange data across other devices present on the internet.
#####  Working of Transmission Control Protocol (TCP)

To make sure that each message reaches its target location intact, the TCP/IP model breaks down the data into small bundles and afterward reassembles the bundles into the original message on the opposite end. Sending the information in little bundles of information makes it simpler to maintain efficiency as opposed to sending everything in one go.

After a particular message is broken down into bundles, these bundles may travel along multiple routes if one route is jammed but the destination remains the same.

![[Pasted image 20240305111127.png]]

 the TCP breaks the data into small packets and forwards it toward the Internet Protocol (IP) layer. The packets are then sent to the destination through different routes.

The TCP layer in the user’s system waits for the transmission to get finished and acknowledges once all packets have been received.

##### Features of TCP

- TCP keeps track of the segments being transmitted or received by assigning numbers to every single one of them.
- Flow control limits the rate at which a sender transfers data. This is done to ensure reliable delivery.
- TCP implements an error control mechanism for reliable data transfer.
- TCP takes into account the level of congestion in the network.

##### Advantages of TCP

- It is reliable for maintaining a connection between Sender and Receiver.
- It is responsible for sending data in a particular sequence.
- Its operations are not dependent on OS.
- It allows and supports many routing protocols.
- It can reduce the speed of data based on the speed of the receiver.

##### Disadvantages of TCP

- It is slower than UDP and it takes more bandwidth.
- Slower upon starting of transfer of a file.
- Not suitable for LAN and PAN Networks.
- It does not have a multicast or broadcast category.
- It does not load the whole page if a single data of the page is missing.

#### User Datagram Protocol (UDP)

 it is an ***unreliable and connectionless protocol.*** So, there is no need to establish a connection before data transfer. The UDP helps to establish low-latency and loss-tolerating connections over the network. The UDP enables process-to-process communication.

 For real-time services like computer gaming, voice or video communication, and live conferences; we need UDP. Since high performance is needed, UDP permits packets to be dropped instead of processing delayed packets. There is no error checking in UDP, so it also saves bandwidth.

![[Pasted image 20240305112544.png]]

##### ***UDP Header***

UDP header is an ***8-byte*** fixed and simple header, while for TCP it may vary from 20 bytes to 60 bytes. The first 8 Bytes contain all necessary header information and the remaining part consists of data. UDP port number fields are each 16 bits long, therefore the range for port numbers is defined from 0 to 65535; port number 0 is reserved. Port numbers help to distinguish different user requests or processes.

![[Pasted image 20240305113049.png]]

1. ***Source Port:*** Source Port is a 2 Byte long field used to identify the port number of the source.
2. ***Destination Port:*** It is a 2 Byte long field, used to identify the port of the destined packet.
3. ***Length:*** Length is the length of UDP including the header and the data. It is a 16-bits field.
4. ***Checksum:*** Checksum is 2 Bytes long field. It is the 16-bit one’s complement of the one’s complement sum of the UDP header, the pseudo-header of information from the IP header, and the data, padded with zero octets at the end (if necessary) to make a multiple of two octets.

#### Features of UDP

- Used for simple request-response communication when the size of data is less and hence there is lesser concern about flow and error control.
- It is a suitable protocol for multicasting as UDP supports packet switching.
- UDP is used for some routing update protocols like [RIP(Routing Information Protocol)](https://www.geeksforgeeks.org/routing-information-protocol-rip/).
- Normally used for real-time applications which can not tolerate uneven delays between sections of a received message.

#### Advantages of UDP

- It does not require any connection for sending or receiving data.
- Broadcast and Multicast are available in UDP.
- UDP can operate on a large range of networks.
- UDP has live and real-time data.
- UDP can deliver data if all the components of the data are not complete.

#### Disadvantages of UDP

- We can not have any way to acknowledge the successful transfer of data.
- UDP cannot have the mechanism to track the sequence of data.
- UDP is connectionless, and due to this, it is unreliable to transfer data.
- In case of a Collision, UDP packets are dropped by Routers in comparison to TCP.
- UDP can drop packets in case of detection of errors.

#### ***User Interface***

A user interface should allow the creation of new receive ports, receive operations on the receive ports that returns the data octets and an indication of source port and source address, and an operation that allows a datagram to be sent, specifying the data, source and destination ports and address to be sent.

#### ***IP Interface***

- The UDP module must be able to determine the source and destination internet address and the protocol field from internet header 
- One possible UDP/IP interface would return the whole internet datagram including the entire internet header in response to a receive operation
- Such an interface would also allow the UDP to pass a full internet datagram complete with header to the IP to send. the IP would verify certain fields for consistency and compute the internet header checksum.
- The IP interface allows the UDP module to interact with the network layer of the protocol stack, which is responsible for routing and delivering data across the network.
- The IP interface provides a mechanism for the UDP module to communicate with other hosts on the network by providing access to the underlying IP protocol.
- The IP interface can be used by the UDP module to send and receive data packets over the network, with the help of IP routing and addressing mechanisms.
- The IP interface provides a level of abstraction that allows the UDP module to interact with the network layer without having to deal with the complexities of IP routing and addressing directly.
- The IP interface also handles fragmentation and reassembly of IP packets, which is important for large data transmissions that may exceed the maximum packet size allowed by the network.
- The IP interface may also provide additional services, such as support for Quality of Service (QoS) parameters and security mechanisms such as IPsec.
- The IP interface is a critical component of the Internet Protocol Suite, as it enables communication between hosts on the internet and allows for the seamless transmission of data packets across the network.

#### Differences between TCP and UDP

|Where TCP is Used|Where UDP is Used|
|---|---|
|Sending Emails|Gaming|
|Transferring Files|Video Streaming|
|Web Browsing|Online Video Chats|

|Basis|Transmission Control Protocol (TCP)|User Datagram Protocol (UDP)|
|---|---|---|
|Type of Service|[TCP](https://www.geeksforgeeks.org/what-is-transmission-control-protocol-tcp/) is a connection-oriented protocol. Connection <br><br>orientation means that the communicating devices should establish a connection before transmitting data and should close the connection after transmitting the data.|[UDP](https://www.geeksforgeeks.org/user-datagram-protocol-udp/) is the Datagram-oriented protocol. This is because <br><br>there is no overhead for opening a connection, maintaining a connection, or terminating a connection. UDP is efficient for broadcast and multicast types of network transmission.|
|Reliability|TCP is reliable as it guarantees the delivery of data to the destination router.|The delivery of data to the destination cannot be guaranteed in UDP.|
|Error checking mechanism|TCP provides extensive error-checking mechanisms. <br><br>It is because it provides flow control and acknowledgment of data.|UDP has only the basic error-checking mechanism using checksums.|
|Acknowledgment|An acknowledgment segment is present.|No acknowledgment segment.|
|Sequence|Sequencing of data is a feature of Transmission Control <br><br>Protocol (TCP). this means that packets arrive in order at the receiver.|There is no sequencing of data in UDP. If the order is required, it has to be managed by the application layer.|
|Speed|TCP is comparatively slower than UDP.|UDP is faster, simpler, and more efficient than TCP.|
|Retransmission|Retransmission of lost packets is possible in TCP, but not in UDP.|There is no retransmission of lost packets in the User Datagram Protocol (UDP).|
|Header Length|TCP has a (20-60) bytes variable length header.|UDP has an 8 bytes fixed-length header.|
|Weight|TCP is heavy-weight.|UDP is lightweight.|
|Handshaking Techniques|Uses handshakes such as SYN, ACK, SYN-ACK|It’s a connectionless protocol i.e. No handshake|
|Broadcasting|TCP doesn’t support Broadcasting.|UDP supports Broadcasting.|
|Protocols|TCP is used by [HTTP, HTTPs](https://www.geeksforgeeks.org/difference-between-http-and-https-2/), [FTP](https://www.geeksforgeeks.org/file-transfer-protocol-ftp/), [SMTP](https://www.geeksforgeeks.org/simple-mail-transfer-protocol-smtp/) and [Telnet](https://www.geeksforgeeks.org/introduction-to-telnet/).|UDP is used by [DNS](https://www.geeksforgeeks.org/details-on-dns/), [DHCP](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/), TFTP, [SNMP](https://www.geeksforgeeks.org/simple-network-management-protocol-snmp/), [RIP](https://www.geeksforgeeks.org/routing-information-protocol-rip/), and [VoIP](https://www.geeksforgeeks.org/voice-over-internet-protocol-voip/).|
|Stream Type|The TCP connection is a byte stream.|UDP connection is a message stream.|
|Overhead|Low but higher than UDP.|Very low.|
|Applications|This protocol is primarily utilized in situations when a safe and trustworthy communication procedure is necessary, such as in email, on the web surfing, and in military services.|This protocol is used in situations where quick communication is necessary but where dependability is not a concern, such as VoIP, game streaming, video, and music streaming, etc.|

###  Java Networking Terminology

- **IP Address –** An IP address is a unique address that distinguishes a device on the internet or a local network. IP stands for “Internet Protocol.” It comprises a set of rules governing the format of data sent via the internet or local network. IP Address is referred to as a logical address that can be modified. It is composed of octets. The range of each octet varies from 0 to 255.

	- Range of the IP Address – 0.0.0.0  to  255.255.255.255
	- For Example – 192.168.0.1

- **Port Number –** A port number is a method to recognize a particular process connecting internet or other network information when it reaches a server. The port number is used to identify different applications uniquely. The port number behaves as a communication endpoint among applications. The port number is correlated with the IP address for transmission and communication among two applications. There are 65,535 port numbers, but not all are used every day.

- **Protocol –** A network protocol is an organized set of commands that define how data is transmitted between different devices in the same network. Network protocols are the reason through which a user can easily communicate with people all over the world and thus play a critical role in modern digital communications. For Example – TCP, FTP, POP, etc.

- **MAC Address –** MAC address stands for Media Access Control address. It is a bizarre identifier that is allocated to a NIC (Network Interface Controller/ Card). It contains a 48 bit or 64-bit address, which is combined with the network adapter. MAC address can be in hexadecimal composition. In simple words, a MAC address is a unique number that is used to track a device in a network.

- **Socket –** A socket is one endpoint of a two-way communication connection between the two applications running on the network. The socket mechanism presents a method of inter-process communication (IPC) by setting named contact points between which the communication occurs. A socket is tied to a port number so that the TCP layer can recognize the application to which the data is intended to be sent.

 - **Connection-oriented and connection-less protocol –** In a connection-oriented service, the user must establish a connection before starting the communication. When the connection is established, the user can send the message or the information, and after this, they can release the connection. However, In connectionless protocol, the data is transported in one route from source to destination without verifying that the destination is still there or not or if it is ready to receive the message. Authentication is not needed in the connectionless protocol.
	- Example of Connection-oriented Protocol – Transmission Control Protocol (TCP)
	- Example of Connectionless Protocol – User Datagram Protocol (UDP)

### Java Networking classes

The **java.net** package of the Java programming language includes various classes that provide an easy-to-use means to access network resources. The classes covered in the **java.net** package

[**CacheRequest –**](https://www.geeksforgeeks.org/java-net-cacherequest-class-in-java/) The ``CacheRequest`` class is used in java whenever there is a need to store resources in ``ResponseCache``. The objects of this class provide an edge for the ``OutputStream`` object to store resource data into the cache.

 > **Represents channels for storing resources in the ``ResponseCache``. Instances of such a class provide an ``OutputStream`` object which is called by protocol handlers to store the resource data into the cache, and also an ``abort()`` method which allows a cache store operation to be interrupted and abandoned.**
 
[**CookieHandler**](https://www.geeksforgeeks.org/java-net-cookiehandler-class-in-java/) **–** The ``CookieHandler`` class is used in Java to implement a callback mechanism for securing up an HTTP state management policy implementation inside the HTTP protocol handler. The HTTP state management mechanism specifies the mechanism of how to make HTTP requests and responses.

> **A CookieHandler object provides a callback mechanism to hook up a HTTP state management policy implementation into the HTTP protocol handler. The HTTP state management mechanism specifies a way to create a stateful session with HTTP requests and responses.**

[**CookieManager**](https://www.geeksforgeeks.org/java-net-cookiemanager-class-in-java/) **–**  The ``CookieManager`` class is used to provide a precise implementation of ``CookieHandler``. This class separates the storage of cookies from the policy surrounding accepting and rejecting cookies. A ``CookieManager`` comprises a ``CookieStore`` and a ``CookiePolicy``.

```
CookieHandler <------- HttpURLConnection
       ^
       | impl
       |         use
 CookieManager -------> CookiePolicy
             |   use
             |--------> HttpCookie
             |              ^
             |              | use
             |   use        |
             |--------> CookieStore
                            ^
                            | impl
                            |
                  Internal in-memory implementation
```

- ``CookieHandler`` is at the core of cookie management. User can call ``CookieHandler.setDefault`` to set a concrete ``CookieHandler`` implementation to be used.
- ``CookiePolicy.shouldAccept`` will be called by ``CookieManager.put`` to see whether or not one cookie should be accepted and put into cookie store. User can use any of three pre-defined ``CookiePolicy``, namely ``ACCEPT_ALL``, ``ACCEPT_NONE`` and ``ACCEPT_ORIGINAL_SERVER``, or user can define his own ``CookiePolicy`` implementation and tell ``CookieManager`` to use it.
- ``CookieStore`` is the place where any accepted HTTP cookie is stored in. If not specified when created, a ``CookieManager`` instance will use an internal in-memory implementation. Or user can implements one and tell ``CookieManager`` to use it.
- Currently, only`` CookieStore.add(URI, HttpCookie)`` and ``CookieStore.get(URI)`` are used by ``CookieManager``. Others are for completeness and might be needed by a more sophisticated ``CookieStore`` implementation, e.g. a ``NetscapeCookieSotre``.

[**DatagramPacket**](https://www.geeksforgeeks.org/java-net-datagrampacket-class-java/) **–** The ``DatagramPacket`` class is used to provide a facility for the connectionless transfer of messages from one system to another. This class provides tools for the production of datagram packets for connectionless transmission by applying the datagram socket class.

[**InetAddress**](https://www.geeksforgeeks.org/java-net-inetaddress-class-in-java/) **–** The ``InetAddress`` class is used to provide methods to get the IP address of any hostname. An IP address is expressed by a 32-bit or 128-bit unsigned number. ``InetAddress`` can handle both IPv4 and IPv6 addresses.

[**Server Socket**](https://www.geeksforgeeks.org/java-net-serversocket-class-in-java/) **–** The ``ServerSocket`` class is used for implementing system-independent implementation of the server-side of a client/server Socket Connection. The constructor for ``ServerSocket`` class throws an exception if it can’t listen on the specified port.

[**Socket**](https://www.geeksforgeeks.org/java-net-socket-class-in-java/) **–** The Socket class is used to create socket objects that help the users in implementing all fundamental socket operations. The users can implement various networking actions such as sending, reading data, and closing connections. Each Socket object built using **``java.net.Socket``** class has been connected exactly with 1 remote host; for connecting to another host, a user must create a new socket object.

[**DatagramSocket**](https://www.geeksforgeeks.org/java-net-datagramsocket-class-java/) **–** The ``DatagramSocket`` class is a network socket that provides a connection-less point for sending and receiving packets. Every packet sent from a datagram socket is individually routed and delivered. It can further be practiced for transmitting and accepting broadcast information. Datagram Sockets is Java’s mechanism for providing network communication via UDP instead of TCP

[**Proxy**](https://www.geeksforgeeks.org/java-net-proxy-class-in-java/) **–** A proxy is a changeless object and a kind of tool or method or program or system, which serves to preserve the data of its users and computers. It behaves like a wall between computers and internet users. A Proxy Object represents the Proxy settings to be applied with a connection.

[**URL**](https://www.geeksforgeeks.org/url-class-java-examples/) **–** The URL class in Java is the entry point to any available sources on the internet. A Class URL describes a Uniform Resource Locator, which is a signal to a “resource” on the World Wide Web. A source can denote a simple file or directory, or it can indicate a more difficult object, such as a query to a database or a search engine.

[**URLConnection**](https://www.geeksforgeeks.org/java-net-urlconnection-class-in-java/) **–** The ``URLConnection`` class in Java is an abstract class describing a connection of a resource as defined by a similar URL. The ``URLConnection`` class is used for assisting two distinct yet interrelated purposes. Firstly it provides control on interaction with a server(especially an HTTP server) than a URL class. Furthermore, with a ``URLConnection``, a user can verify the header transferred by the server and can react consequently.

### Java Networking Interfaces

1. **CookiePolicy –** The ``CookiePolicy`` interface in the **java.net** package provides the classes for implementing various networking applications. It decides which cookies should be accepted and which should be rejected. In ``CookiePolicy``, there are three pre-defined policy implementations, namely ``ACCEPT_ALL``, ``ACCEPT_NONE``, and ``ACCEPT_ORIGINAL_SERVER``.  
     
2. **CookieStore –** A ``CookieStore`` is an interface that describes a storage space for cookies. ``CookieManager`` combines the cookies to the ``CookieStore`` for each HTTP response and recovers cookies from the ``CookieStore`` for each HTTP request.  
     
3. **FileNameMap –** The ``FileNameMap`` interface is an uncomplicated interface that implements a tool to outline a file name and a MIME type string. ``FileNameMap`` charges a filename map ( known as a mimetable) from a data file.  
     
4. **SocketOption –** The ``SocketOption`` interface helps the users to control the behavior of sockets. Often, it is essential to develop necessary features in Sockets. ``SocketOptions`` allows the user to set various standard options.  
     
5. **SocketImplFactory –** The ``SocketImplFactory`` interface defines a factory for ``SocketImpl`` instances. It is used by the socket class to create socket implementations that implement various policies.  
     
6. **ProtocolFamily –** This interface represents a family of communication protocols. The ``ProtocolFamily`` interface contains a method known as ``name()``, which returns the name of the protocol family.

###  Socket Programming

Java Socket programming is practiced for communication between the applications working on different JRE. Sockets implement the communication tool between two computers using TCP. Java Socket programming can either be connection-oriented or connection-less. In Socket Programming, Socket and ``ServerSocket`` classes are managed for connection-oriented socket programming. However, ``DatagramSocket`` and ``DatagramPacket`` classes are utilized for connection-less socket programming.

A client application generates a socket on its end of the communication and strives to combine that socket with a server. When the connection is established, the server generates an object of socket class on its communication end. The client and the server can now communicate by writing to and reading from the socket.

The **``java.net.Socket``** class describes a socket, and the **``java.net.ServerSocket``** class implements a tool for the server program to host clients and build connections with them.

**Steps to establishing a TCP connection between two computing devices using Socket Programming**

**Step 1 –** The server instantiates a ``ServerSocket`` object, indicating at which port number communication will occur.

**Step 2 –** After instantiating the ``ServerSocket`` object, the server requests the ``accept()`` method of the ``ServerSocket`` class. This program pauses until a client connects to the server on the given port.

**Step 3 –** After the server is idling, a client instantiates an object of Socket class, defining the server name and the port number to connect to.

**Step 4 –** After the above step, the constructor of the Socket class strives to connect the client to the designated server and the port number. If communication is authenticated, the client forthwith has a Socket object proficient in interacting with the server.

**Step 5 –** On the server-side, the ``accept()`` method returns a reference to a new socket on the server connected to the client’s socket.

After the connections are stabilized, communication can happen using I/O streams. Each object of a socket class has both an ``OutputStream`` and an ``InputStream``. The client’s ``OutputStream`` is correlated to the server’s ``InputStream``, and the client’s ``InputStream`` is combined with the server’s ``OutputStream``. Transmission Control Protocol (TCP) is a two-way communication protocol. Hence information can be transmitted over both streams at the corresponding time.

**Client-Side Java Implementation:**

```java
// A Java program for a ClientSide

import java.io.*;
import java.net.*;

public class clientSide {

	// initialize socket and input output streams
	private Socket socket = null;
	private DataInputStream input = null;
	private DataOutputStream out = null;

	// constructor to put ip address and port
	public clientSide(String address, int port)
	{

		// establish a connection
		try {

			socket = new Socket(address, port);

			System.out.println("Connected");

			// takes input from terminal
			input = new DataInputStream(System.in);

			// sends output to the socket
			out = new DataOutputStream(
				socket.getOutputStream());
		}

		catch (UnknownHostException u) {

			System.out.println(u);
		}

		catch (IOException i) {

			System.out.println(i);
		}

		// string to read message from input
		String line = "";

		// keep reading until "End" is input
		while (!line.equals("End")) {

			try {

				line = input.readLine();

				out.writeUTF(line);
			}

			catch (IOException i) {

				System.out.println(i);
			}
		}

		// close the connection
		try {

			input.close();

			out.close();

			socket.close();
		}

		catch (IOException i) {

			System.out.println(i);
		}
	}

	public static void main(String[] args)
	{

		clientSide client
			= new clientSide("127.0.0.1", 5000);
	}
}
```

**Server Side Java Implementation:**

```java
// A Java program for a serverSide
import java.io.*;
import java.net.*;

public class serverSide {

	// initialize socket and input stream
	private Socket socket = null;
	private ServerSocket server = null;
	private DataInputStream in = null;

	// constructor with port
	public serverSide(int port)
	{

		// starts server and waits for a connection
		try {
			server = new ServerSocket(port);

			System.out.println("Server started");

			System.out.println("Waiting for a client ...");

			socket = server.accept();

			System.out.println("Client accepted");

			// takes input from the client socket
			in = new DataInputStream(
				new BufferedInputStream(
					socket.getInputStream()));

			String line = "";

			// reads message from client until "End" is sent
			while (!line.equals("End")) {

				try {

					line = in.readUTF();

					System.out.println(line);
				}

				catch (IOException i) {

					System.out.println(i);
				}
			}

			System.out.println("Closing connection");

			// close connection
			socket.close();

			in.close();
		}

		catch (IOException i) {

			System.out.println(i);
		}
	}

	public static void main(String[] args)
	{

		serverSide server = new serverSide(5000);
	}
}
```

**CSD TCP EXAMPLE**

**TcpUtil**
```java
public final class TcpUtil {  
    private static int receive(DataInputStream dis, byte [] data, int offset, int length) throws IOException  
    {  
        int result;  
        int left = length, index = 0;  
  
        while (left > 0) {  
            if ((result = dis.read(data, offset, left)) == -1)  
                return -1;  
              
            if (result == 0)  
                break;  
              
            index += result;  
            left -= result;  
        }  
  
        return index;  
    }  
  
    private static int receive(DataInputStream dis, byte [] data) throws IOException  
    {  
        return receive(dis, data, 0, data.length);  
    }  
  
    private static int send(DataOutputStream dos, byte [] data, int offset, int length) throws IOException  
    {                   
       int curOffset = offset;         
       int left = length;  
       int total = 0;  
       int written;  
       int initWritten = dos.size();  
         
       while (curOffset < length) {  
          dos.write(data, curOffset, left);  
          dos.flush();  
          written = dos.size() - initWritten;  
          total += written;          
          left -= written;  
          curOffset += written;  
       }    
         
       return total;  
    }  
      
    private static int send(DataOutputStream dos, byte [] data) throws IOException  
    {  
        return send(dos, data, 0, data.length);  
    }  
  
    private TcpUtil() {}  
  
    public static Optional<ServerSocket> getFirstAvailableSocket(int backlog, int minPort, int maxPort)  
    {  
       Optional<ServerSocket> result = Optional.empty();  
  
       for (int port = minPort; port <= maxPort; ++port)  
          try {  
             result = Optional.of(new ServerSocket(backlog, port));  
          }  
          catch (IOException ignore) {  
          }  
  
       return result;  
    }  
  
    public static Optional<ServerSocket> getFirstAvailablePort(int minPort, int maxPort)  
    {  
       Optional<ServerSocket> result = Optional.empty();  
  
       for (int port = minPort; port <= maxPort; ++port)  
          try {  
             result = Optional.of(new ServerSocket(port));  
          }  
          catch (IOException ignore) {  
          }  
  
       return result;  
    }  
  
    public static Optional<ServerSocket> getFirstAvailableSocket(int backlog, int...ports)  
    {  
       Optional<ServerSocket> result = Optional.empty();  
  
       for (var port : ports)  
          try {  
             result = Optional.of(new ServerSocket(backlog, port));  
          }  
          catch (IOException ignore) {  
          }  
  
       return result;  
    }  
  
    public static Optional<ServerSocket> getFirstAvailableSocket(int...ports)  
    {  
       Optional<ServerSocket> result = Optional.empty();  
  
       for (var port : ports)  
          try {  
             result = Optional.of(new ServerSocket(port));  
          }  
          catch (IOException ignore) {  
          }  
  
       return result;  
    }  
  
  
    public static int receive(Socket socket, byte [] data, int offset, int length)  
    {  
       try {  
          return receive(new DataInputStream(socket.getInputStream()), data, offset, length);  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receive", ex);  
       }  
    }  
  
    public static int receive(Socket socket, byte [] data)  
    {  
       try {  
          return receive(socket, data, 0, data.length);  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receive", ex.getCause());  
       }  
    }  
  
    public static int send(Socket socket, byte [] data, int offset, int length)  
    {  
       try {  
          return send(new DataOutputStream(socket.getOutputStream()), data, offset, length);  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.send", ex);  
       }  
    }  
  
    public static int send(Socket socket, byte [] data)  
    {  
       try {  
          return send(socket, data, 0, data.length);  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.send", ex.getCause());  
       }  
    }  
  
    public static byte receiveByte(Socket socket)  
    {  
       try {  
          byte [] data = new byte[1];  
  
          receive(socket, data);  
  
          return data[0];  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveByte", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveByte", ex);  
       }  
    }  
  
    public static short receiveShort(Socket socket)  
    {  
       try {  
          byte[] data = new byte[2];  
  
          receive(socket, data);  
  
          return BitConverter.toShort(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveShort", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveShort", ex);  
       }  
    }  
  
    public static int receiveInt(Socket socket)  
    {  
       try {  
          byte[] data = new byte[4];  
  
          receive(socket, data);  
  
          return BitConverter.toInt(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveInt", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveInt", ex);  
       }  
    }  
  
    public static long receiveLong(Socket socket)  
    {  
       try {  
          byte[] data = new byte[8];  
  
          receive(socket, data);  
  
          return BitConverter.toLong(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveLong", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveLong", ex);  
       }  
    }  
  
    public static float receiveFloat(Socket socket)  
    {  
       try {  
          byte[] data = new byte[4];  
  
          receive(socket, data);  
  
          return BitConverter.toFloat(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveFloat", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveFloat", ex);  
       }  
    }  
  
    public static double receiveDouble(Socket socket)  
    {  
       try {  
          byte[] data = new byte[8];  
  
          receive(socket, data);  
  
          return BitConverter.toDouble(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveDouble", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveDouble", ex);  
       }  
    }  
  
    public static char receiveChar(Socket socket)  
    {  
       try {  
          byte[] data = new byte[2];  
  
          receive(socket, data);  
  
          return BitConverter.toChar(data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveChar", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveChar", ex);  
       }  
    }  
  
    public static boolean receiveBoolean(Socket socket)  
    {  
       try {  
          return new DataInputStream(socket.getInputStream()).readByte() != 0;  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveBoolean", ex);  
       }  
    }  
  
    public static String receiveStringViaLength(Socket socket)  
    {  
       return receiveStringViaLength(socket, StandardCharsets.UTF_8);  
    }  
  
    public static String receiveStringViaLength(Socket socket, Charset charset)  
    {  
       try {  
          byte[] dataLen = new byte[4];  
          receive(socket, dataLen);  
  
          byte[] data = new byte[BitConverter.toInt(dataLen)];  
  
          receive(socket, data);  
  
          return BitConverter.toString(data, charset);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveStringViaLength", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveStringViaLength", ex);  
       }  
    }  
  
    public static String receiveString(Socket socket, int length)  
    {  
       return receiveString(socket, length, StandardCharsets.UTF_8);  
    }  
  
    public static String receiveString(Socket socket, int length, Charset charset)  
    {  
       try {  
          byte[] data = new byte[length];  
  
          receive(socket, data);  
  
          return BitConverter.toString(data, charset);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveString", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveString", ex);  
       }  
    }  
  
    public static void receiveFile(Socket socket, File file)  
    {  
       receiveFile(socket, file.getAbsolutePath());  
    }  
  
    public static void receiveFile(Socket socket, String path)  
    {  
       try (FileOutputStream fos = new FileOutputStream(path)) {  
          int result;  
  
          for (;;) {  
             var size = receiveInt(socket);  
  
             if (size <= 0)  
                break;  
  
             var data = new byte[size];  
  
             result = receive(socket, data);  
             fos.write(data, 0, result);  
          }  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.receiveFile", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.receiveFile", ex);  
       }  
    }  
  
    public static void sendByte(Socket socket, byte val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendByte", ex);  
       }  
    }  
  
    public static void sendShort(Socket socket, short val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendShort", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendShort", ex);  
       }  
    }  
  
    public static void sendInt(Socket socket, int val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendInt", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendInt", ex);  
       }  
    }  
  
    public static void sendLong(Socket socket, long val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendLong", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendLong", ex);  
       }  
    }  
  
    public static void sendFloat(Socket socket, float val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendFloat", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendFloat", ex);  
       }  
    }  
  
    public static void sendDouble(Socket socket, double val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendDouble", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendDouble", ex);  
       }  
    }  
  
    public static void sendChar(Socket socket, char val)  
    {  
       try {  
          send(socket, BitConverter.getBytes(val));  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendChar", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendChar", ex);  
       }  
    }  
  
    public static void sendBoolean(Socket socket, boolean val)  
    {  
       try {  
          DataOutputStream dos = new DataOutputStream(socket.getOutputStream());  
  
          dos.writeByte(val ? 1 : 0);  
          dos.flush();  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendBoolean", ex);  
       }  
    }  
  
    public static void sendStringViaLength(Socket socket, String str)  
    {  
       sendStringViaLength(socket, str, StandardCharsets.UTF_8);  
    }  
  
    public static void sendStringViaLength(Socket socket, String str, Charset charset)  
    {  
       try {  
          byte[] data = BitConverter.getBytes(str, charset);  
          byte[] dataLen = BitConverter.getBytes(data.length);  
  
          send(socket, dataLen);  
          send(socket, data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendStringViaLength", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendStringViaLength", ex);  
       }  
    }  
  
    public static void sendString(Socket socket, String str)  
    {  
       sendString(socket, str, StandardCharsets.UTF_8);  
    }  
  
    public static void sendString(Socket socket, String str, Charset charset)  
    {  
       try {  
          byte[] data = BitConverter.getBytes(str, charset);  
  
          send(socket, data);  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendString", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendString", ex);  
       }  
    }  
  
    public static void sendFile(Socket socket, File file, int blockSize)  
    {  
       sendFile(socket, file.getAbsolutePath(), blockSize);  
    }  
  
    public static void sendFile(Socket socket, String path, int blockSize)  
    {  
       byte [] data = new byte[blockSize];  
  
       try (FileInputStream fis = new FileInputStream(path)) {  
          int result;  
  
          for (;;) {  
             result = fis.read(data);  
             sendInt(socket, result);  
             if (result <= 0)  
                break;  
             send(socket, data, 0, result);  
          }  
       }  
       catch (NetworkException ex) {  
          throw new NetworkException("TcpUtil.sendFile", ex.getCause());  
       }  
       catch (Throwable ex) {  
          throw new NetworkException("TcpUtil.sendFile", ex);  
       }  
    }  
}
```

**CImage**

```java
public enum CImageFormat {  
    BMP, GIF, JPEG, PNG, TIFF, WBMP  
}

public class CImage {  
    private final File m_path;  
    private BufferedImage  m_bufferedImage;  
  
    public CImage(String path) throws IOException  
    {  
        this(new File(path));  
    }  
  
    public CImage(File path) throws IOException  
    {  
        if (!path.exists())  
            throw new IOException("image not found");  
  
        m_path = path;  
        m_bufferedImage = ImageIO.read(m_path);  
    }  
  
    public int getWidth()  
    {  
        return m_bufferedImage.getWidth();  
    }  
  
    public int getHeight()  
    {  
        return m_bufferedImage.getHeight();  
    }  
  
    public BufferedImage getBufferedImage()  
    {  
        return m_bufferedImage;  
    }  
  
    public void grayScale()  
    {  
        int width = m_bufferedImage.getWidth();  
        int height = m_bufferedImage.getHeight();  
  
        for (int i = 0; i < width; ++i)  
            for (int k = 0; k < height; ++k) {  
                Color c = new Color(m_bufferedImage.getRGB(i, k));  
                int avg = (int)Math.floor((c.getRed() + c.getGreen() + c.getBlue()) / 3.);  
  
                m_bufferedImage.setRGB(i, k, new Color(avg, avg, avg).getRGB());  
            }  
    }  
  
    public void binary(int threshold)  
    {  
        int width = m_bufferedImage.getWidth();  
        int height = m_bufferedImage.getHeight();  
  
        for (int i = 0; i < width; ++i)  
            for (int k = 0; k < height; ++k) {  
                Color c = new Color(m_bufferedImage.getRGB(i, k));  
  
                int value = c.getRed() > threshold ? 255 : 0;  
  
                m_bufferedImage.setRGB(i, k, new Color(value, value, value).getRGB());  
            }  
    }  
  
    public void save(String output, CImageFormat format) throws IOException  
    {  
        save(new File(output), format);  
    }  
  
    public void save(File output, CImageFormat format) throws IOException  
    {  
        ImageIO.write(m_bufferedImage, format.toString().toLowerCase(), output);  
    }  
  
    public void reset() throws IOException  
    {  
        m_bufferedImage = ImageIO.read(m_path);  
    }  
  
    //...  
}
```

**BinaryImageServer**
```java
public class BinaryImageServer {  
    private static final int SOCKET_TIMEOUT = 10000;  
    private static final DateTimeFormatter FORMATTER = DateTimeFormatter.ofPattern("dd-MM-yyy_HH-mm-ss-n");  
    private static final File IMAGE_PATH = new File("binary_images");  
  
    private final ConcurrentServer m_server;  
  
    private void saveFile(Socket socket, String path) throws IOException  
    {  
        try {  
            var file = new File(IMAGE_PATH, String.format("%s.png", new File(path).getName()));  
  
            TcpUtil.receiveFile(socket, file);  
            var threshold = TcpUtil.receiveInt(socket);  
            file = doBinaryImage(file, threshold);  
  
            TcpUtil.sendInt(socket, 1);  
            TcpUtil.sendFile(socket, file, 1024);  
        }  
        catch (NetworkException ex) {  
            Console.Error.writeLine("Network problem:%s", ex.getMessage());  
        }  
  
        TcpUtil.sendInt(socket, 0);  
    }  
  
    private File doBinaryImage(File file, int threshold) throws IOException  
    {  
        var image = new CImage(file);  
  
        var path = file.getAbsolutePath();  
        file = new File(path.substring(0, path.lastIndexOf('.') + 1) +  "-bin.png");  
  
        image.binary(threshold);  
        image.save(file, CImageFormat.PNG);  
  
        return file;  
    }  
  
    private void handleClient(Socket socket)  
    {  
        try (socket) {  
            socket.setSoTimeout(SOCKET_TIMEOUT);  
            var hostAddress = socket.getInetAddress().getHostAddress();  
            var port = socket.getPort();  
            Console.writeLine("Client connected to Binary image server via %s:%d", hostAddress, port);  
            var path = String.format("%s_%d_%s", hostAddress, port, FORMATTER.format(LocalDateTime.now()));  
  
            saveFile(socket, path);  
        }  
        catch (IOException ex) {  
            Console.Error.writeLine("BinaryImageServer:IO Exception Occurred:%s", ex.getMessage());  
        }  
        catch (Throwable ex) {  
            Console.Error.writeLine("BinaryImageServer:Exception Occurred:%s", ex.getMessage());  
        }  
    }  
  
    public BinaryImageServer(int port, int backlog) throws IOException  
    {  
        m_server = ConcurrentServer.builder()  
                .setPort(port)  
                .setBacklog(backlog)  
                .setInitRunnable(IMAGE_PATH::mkdirs)  
                .setBeforeAcceptRunnable(() -> Console.writeLine("Binary image server is waiting for a client on port:%d", port))  
                .setClientSocketConsumer(this::handleClient)  
                .setServerExceptionConsumer(ex -> Console.Error.writeLine("Exception Occurred:%s", ex.getMessage()))  
                .build();  
    }  
  
    public void run()  
    {  
        m_server.start();  
    }  
  
    public void close()  
    {  
        m_server.stop();  
    }  
  
}
```

**GrayscaleImageServer**

```java
public class GrayscaleImageServer implements Closeable {  
    private static final int SOCKET_TIMEOUT = 10000;  
    private static final DateTimeFormatter FORMATTER = DateTimeFormatter.ofPattern("dd-MM-yyy_HH-mm-ss-n");  
    private static final File IMAGE_PATH = new File("grayscale_images");  
  
    private final ConcurrentServer m_server;  
  
    private void saveFile(Socket socket, String path) throws IOException  
    {  
        try {  
            var file = new File(IMAGE_PATH, String.format("%s.png", new File(path).getName()));  
  
            TcpUtil.receiveFile(socket, file);  
            file = doGrayscale(file);  
            TcpUtil.sendInt(socket, 1);  
            TcpUtil.sendFile(socket, file, 1024);  
        }  
        catch (NetworkException ex) {  
            Console.Error.writeLine("Network problem:%s", ex.getMessage());  
        }  
  
        TcpUtil.sendInt(socket, 0);  
    }  
  
    private File doGrayscale(File file) throws IOException  
    {  
        var image = new CImage(file);  
  
        var path = file.getAbsolutePath();  
        file = new File(path.substring(0, path.lastIndexOf('.') + 1) +  "-gs.png");  
  
        image.grayScale();  
        image.save(file, CImageFormat.PNG);  
  
        return file;  
    }  
  
    private void handleClient(Socket socket)  
    {  
        try (socket) {  
            socket.setSoTimeout(SOCKET_TIMEOUT);  
            var hostAddress = socket.getInetAddress().getHostAddress();  
            var port = socket.getPort();  
            Console.writeLine("Client connected to grayscale image server via %s:%d", hostAddress, port);  
            var path = String.format("%s_%d_%s", hostAddress, port, FORMATTER.format(LocalDateTime.now()));  
  
            saveFile(socket, path);  
        }  
        catch (IOException ex) {  
            Console.Error.writeLine("GrayScaleImageServer:IO Exception Occurred:%s", ex.getMessage());  
        }  
        catch (Throwable ex) {  
            Console.Error.writeLine("GrayScaleImageServer:Exception Occurred:%s", ex.getMessage());  
        }  
    }  
  
  
    public GrayscaleImageServer(int port, int backlog) throws IOException  
    {  
        m_server = ConcurrentServer.builder()  
                .setPort(port)  
                .setBacklog(backlog)  
                .setInitRunnable(IMAGE_PATH::mkdirs)  
                .setBeforeAcceptRunnable(() -> Console.writeLine("Grayscale image server is waiting for a client on port:%d", port))  
                .setClientSocketConsumer(this::handleClient)  
                .setServerExceptionConsumer(ex -> Console.Error.writeLine("Exception Occurred:%s", ex.getMessage()))  
                .build();  
    }  
  
    public void run()  
    {  
        m_server.start();  
    }  
  
    public void close()  
    {  
        m_server.stop();  
    }  
}
```

**Application**

```java
class Application {  
    public static void run(String[] args)  
    {  
        try {  
            checkLengthEquals(args.length, 2, "wrong number of arguments!..");  
  
            var port = Integer.parseInt(args[0]);  
            var backlog = Integer.parseInt(args[1]);  
            var grayscaleServer = new GrayscaleImageServer(port, backlog);  
            var binaryServer = new BinaryImageServer(port + 1, backlog);  
  
            new CommandPrompt.Builder()  
                    .setPrompt("server")  
                    .register(new ManageServerCommands(grayscaleServer, binaryServer, Executors.newCachedThreadPool()))  
                    .build().run();  
  
        }  
        catch (NumberFormatException ignore) {  
            Console.Error.writeLine("Invalid arguments");  
        }  
        catch (IOException ex) {  
            Console.Error.writeLine("IO Exception occurred:%s", ex.getMessage());  
        }  
    }  
}
```


### Internet Protocol version 4 (IPv4)

**IP** stands for **Internet Protocol** and **v4** stands for **Version Four** (IPv4). IPv4 was the primary version brought into action for production within the ARPANET in 1983.   
IP version four addresses are 32-bit integers which will be expressed in decimal notation.   
Example- 192.0.2.126 could be an IPv4 address. 

![[Pasted image 20240308123012.png]]
#### Parts of IPv4

- **Network part:**   
    The network part indicates the distinctive variety that’s appointed to the network. The network part conjointly identifies the category of the network that’s assigned.
- **Host Part:**   
    The host part uniquely identifies the machine on your network. This part of the IPv4 address is assigned to every host.   
    For each host on the network, the network part is the same, however, the host half must vary.
- **Subnet number:**   
    This is the nonobligatory part of IPv4. Local networks that have massive numbers of hosts are divided into subnets and subnet numbers are appointed to that.

#### Characteristics of IPv4

- IPv4 could be a 32-Bit IP Address.
- IPv4 could be a numeric address, and its bits are separated by a dot.
- The number of header fields is twelve and the length of the header field is twenty.
- It has Unicast, broadcast, and multicast style of addresses.
- IPv4 supports VLSM (Virtual Length Subnet Mask).
- IPv4 uses the Post Address Resolution Protocol to map to the MAC address.
- RIP may be a routing protocol supported by the routed daemon.
- Networks ought to be designed either manually or with DHCP.
- Packet fragmentation permits from routers and causing host.

#### Advantages of IPv4

- IPv4 security permits encryption to keep up privacy and security.
- IPV4 network allocation is significant and presently has quite 85000 practical routers.
- It becomes easy to attach multiple devices across an outsized network while not NAT.
- This is a model of communication so provides quality service also as economical knowledge transfer.
- IPV4 addresses are redefined and permit flawless encoding.
- Routing is a lot of scalable and economical as a result of addressing is collective more effectively.
- Data communication across the network becomes a lot of specific in multicast organizations.
    - Limits net growth for existing users and hinders the use of the net for brand new users.
    - Internet Routing is inefficient in IPv4.
    - IPv4 has high System Management prices and it’s labor-intensive, complex, slow & frequent to errors.
    - Security features are nonobligatory.
    - Difficult to feature support for future desires as a result of adding it on is extremely high overhead since it hinders the flexibility to attach everything over IP.

#### **Limitations of IPv4**

- IP relies on network layer addresses to identify end-points on network, and each network has a unique IP address.
- The world’s supply of unique IP addresses is dwindling, and they might eventually run out theoretically.
- If there are multiple host, we need IP addresses of next class.
- Complex host and routing configuration, non-hierarchical addressing, difficult to re-numbering addresses, large routing tables, non-trivial implementations in providing security, QoS (Quality of Service), mobility and multi-homing, multicasting etc. are the big limitation of IPv4 so that’s why IPv6 came into the picture.

### Internet Protocol version 6 (IPv6)

IPv6 was developed by Internet Engineering Task Force (IETF) to deal with the problem of IPv4 exhaustion. IPv6 is a 128-bits address having an address space of 2128, which is way bigger than IPv4. IPv6 use Hexa-Decimal format separated by colon (:) .
#### Components in Address format :   

1. There are 8 groups and each group represents 2 Bytes (16-bits). 
2. Each Hex-Digit is of 4 bits (1 nibble)
3. Delimiter used – colon (:)

![[Pasted image 20240308123408.png]]

#### Benefits of IPv6

The recent Version of IP IPv6 has a greater advantage over IPv4. Here are some of the mentioned benefits:

- ***Larger Address Space:*** IPv6 has a greater address space than IPv4, which is required for expanding the IP Connected Devices. IPv6 has 128 bit IP Address rather and IPv4 has a 32-bit Address.
- ***Improved Security:*** IPv6 has some improved security which is built in with it. IPv6 offers security like Data Authentication, Data Encryption, etc. Here, an Internet Connection is more Secure.
- ***Simplified Header Format:*** As compared to IPv4, IPv6 has a simpler and more effective header Structure, which is more cost-effective and also increases the speed of Internet Connection.
- ***Prioritize:*** IPv6 contains stronger and more reliable support for QoS features, which helps in increasing traffic over websites and increases audio and video quality on pages.
- ***Improved Support for Mobile Devices:*** IPv6 has increased and better support for Mobile Devices. It helps in making quick connections over other Mobile Devices and in a safer way than IPv4.

#### ***Difference Between IPv4 and IPv6***

|****IPv4****|****IPv6****|
|---|---|
|IPv4 has a 32-bit address length|IPv6 has a 128-bit address length|
|It Supports Manual and DHCP address configuration|It supports Auto and renumbering address configuration|
|In IPv4 end to end, connection integrity is Unachievable|In IPv6 end-to-end, connection integrity is Achievable|
|It can generate 4.29×109 address space|The address space of IPv6 is quite large it can produce 3.4×1038 address space|
|The Security feature is dependent on the application|IPSEC is an inbuilt security feature in the IPv6 protocol|
|Address representation of IPv4 is in decimal|Address Representation of IPv6 is in hexadecimal|
|Fragmentation performed by Sender and forwarding routers|In IPv6 fragmentation is performed only by the sender|
|In IPv4 Packet flow identification is not available|In IPv6 packet flow identification are Available and uses the flow label field in the header|
|In IPv4 checksum field is available|In IPv6 checksum field is not available|
|It has a broadcast Message Transmission Scheme|In IPv6 multicast and anycast message transmission scheme is available|
|In IPv4 Encryption and Authentication facility not provided|In IPv6 Encryption and Authentication are provided|
|IPv4 has a header of 20-60 bytes.|IPv6 has a header of 40 bytes fixed|
|IPv4 can be converted to IPv6|Not all IPv6 can be converted to IPv4|
|IPv4 consists of 4 fields which are separated by addresses dot (.)|IPv6 consists of 8 fields, which are separated by a colon (:)|
|IPv4’s  IP addresses are divided into five different classes. Class A , Class B, Class C, Class D , Class E.|IPv6 does not have any classes of the IP address.|
|IPv4 supports VLSM(Variable Length subnet mask).|IPv6 does not support VLSM.|
|Example of IPv4:  66.94.29.13|Example of IPv6: 2001:0000:3238:DFE1:0063:0000:0000:FEFB|

###  Difference between Connection-oriented and Connection-less Services

**Connection-oriented service** is related to the telephone system. It includes connection establishment and connection termination. In a connection-oriented service, the Handshake method is used to establish the connection between sender and receiver.

**Connection-less service** is related to the postal system. It does not include any connection establishment and connection termination. Connection-less Service does not give a guarantee of reliability. In this, Packets do not follow the same path to reach their destination.

|S.NO|Connection-oriented Service|Connection-less Service|
|---|---|---|
|1.|[Connection-oriented](https://www.geeksforgeeks.org/connection-oriented-service/) service is related to the telephone system.|[Connection-less](https://www.geeksforgeeks.org/connection-less-service/) service is related to the postal system.|
|2.|Connection-oriented service is preferred by long and steady communication.|Connection-less Service is preferred by bursty communication.|
|3.|Connection-oriented Service is necessary.|Connection-less Service is not compulsory.|
|4.|Connection-oriented Service is feasible.|Connection-less Service is not feasible.|
|5.|In connection-oriented Service, Congestion is not possible.|In connection-less Service, Congestion is possible.|
|6.|Connection-oriented Service gives the guarantee of reliability.|Connection-less Service does not give a guarantee of reliability.|
|7.|In connection-oriented Service, Packets follow the same route.|In connection-less Service, Packets do not follow the same route.|
|8.|Connection-oriented services require a bandwidth of a high range.|Connection-less Service requires a bandwidth of low range.|
|9.|Ex: [TCP (Transmission Control Protocol)](https://www.geeksforgeeks.org/what-is-transmission-control-protocol-tcp/)|Ex: [UDP (User Datagram Protocol)](https://www.geeksforgeeks.org/user-datagram-protocol-udp/)|
|10.|Connection-oriented requires authentication.|Connection-less Service does not require authentication.|
