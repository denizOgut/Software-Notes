
#  Introduction to arrays
## Understanding the problem

When writing a program, we often need a collection of data items that can be accessed sequentially.

![[Pasted image 20250909090539.png]]

but what if there are hundreds of students in the class? In this case, we need to create hundreds of variables to store this data.

![[Pasted image 20250909090617.png]]

### Limitations of using variables

- A variable can store only one value at a time.
- Different variables that store the same type of information must have different names.
- Using separate variables to store data is not scalable.
- Too many variables complicate the source code and the programming logic, making it error-prone.


## Exploring a possible solution

An array is a contiguous segment of memory that can store multiple data items simultaneously. **==In its simplest form, an array has a fixed size and can store only a fixed number of data items. All items in an array must be of the same type.==**

![[Pasted image 20250909090753.png]]

## Overview of supported operations

### Creating an array

The syntax and rules for creating an array depend on the programming language. An array with a fixed size cannot be modified after creation, and all data items in an array must be the same type.

```java
public static void main() {

    // Declaring an array of size 5

    int[] numbers = new int[5];

    // Initializing an array

    int[] numbers2 = {1, 2, 3, 4, 5};


    // Creating an array of size N

    int[] arr = new int[N];

}
```


### Accessing elements in an array

>**Why do array indices start from 0 instead of 1?**
  Array indices start from **0** because it directly corresponds to the memory offset from the first element, making calculations simpler and faster.

![[Pasted image 20250909091239.png]]

```java
public static void main() {

    // Initializing an array

    int[] numbers = {1, 2, 3, 4, 5};

    // Array elements are accessed using

    // square brackets []

    System.out.println("1st value: " + numbers[0]);

    System.out.println("5th value: " + numbers[4]);

}
```

### Modifying elements in an array

Elements in an array are modified in place just like values held by variables. Just like modifying a value held in a variable, to modify a value in an array, we write the accessor `array[index]` on the left side of the assignment operator and the value to be assigned on the right side.

```java
public static void main() {
    // Initializing an array

    int[] numbers = {1, 2, 3, 4, 5};

    // Modifying the first and second element of an array

    numbers[0] = 6;

    numbers[2] = 7;

}
```

### Traversing an array

Traversal is one of the most common operations performed on an array. It is the only way to search for a value in an array and is implemented by using a loop control variable as an index (starting from 0). **==To safely traverse an array, the size of the array should be known.==**

Higher-level programming languages have inbuilt functions within the array to get its length however, the programmer needs to keep track of the array's size.

```java
public static void main() {

    // Initializing an array

    int[] numbers = {1, 2, 3, 4, 5};

    // Traversal using indices

    for(int i=0; i<5; i++) {

        System.out.println("Value at index: " + i + " is: " numbers[i]);

    }

    // Traversal without indices

    for(int number: numbers) {

        System.out.println(number);

    }

}
```

## Internal mechanics of arrays

### Memory addresses

We can only access array elements using indices because an array is stored in continuous memory.

![[Pasted image 20250909091718.png]]

Memory is logically organized in RAM as a sequence of blocks, each 1 byte (8 bits) long. Every block has a unique identifier that can be used to locate it in memory, called its address. The address is nothing but a number that is the relative position of the block from the start (starting from 0).

### Layout in memory

An array is just a **continuous** segment of memory that stores data of a single type. Each data item in the array has a fixed size equal to the size of its data type, so **==the total size of an array is the sum of the size of all data items.==**

> The address of the block in memory where the array starts is also called the base address of an array. The base address, along with the index, is used to access data items in an array.

![[Pasted image 20250909091853.png]]

### Accessing data items

it is easy to figure out a mathematical formula to calculate the address of a data item at a given `index` if we know the **base address** (where the array starts in memory) and the **size** of each data item.

> Since the array index passed is added to the array's base address, we must add 0 to access the first element. This is why indices in an array start with 0 and not 1.

![[Pasted image 20250909092002.png]]

## Array Capacity VS Length

- **Capacity**: Fixed size set at creation, e.g. `new DVD[6]` → capacity 6, valid indices 0–5, checked with `.length`. Accessing outside this range causes `ArrayIndexOutOfBoundsException`.
    
- **Length**: Actual number of items stored (you track this). An array can have capacity 6 but length 3 if only 3 slots are filled. In problems like ``LeetCode``, assume `length == capacity`, and the last index is `.length - 1`.

```java
// Create a new array with a capacity of 6.
int[] array = new int[6];

// Current length is 0, because it has 0 elements.
int length = 0;

// Add 3 items into it.
for (int i = 0; i < 3; i++) {
    array[i] = i * i;
    // Each time we add an element, the length goes up by one.
    length++;
}

System.out.println("The Array has a capacity of " + array.length);
System.out.println("The Array has a length of " + length);
```

# Multidimensional arrays

Consider a situation where we need to store the age of students in a class for all the classes in a school. The school has classes starting from the 1st standard to the 4th standard, and every class has 60 students.

![[Pasted image 20250909093139.png]]

This is an easy way to solve this problem, but what if there were 12 classes (from class 1 to class 12) instead of just four? In that case, we would have to create 12 arrays, which will solve the problem. However, storing and managing arrays in multiple variables will be difficult.

## Limitations single dimension arrays

- Different arrays holding the same type of information have to be named differently
- Using different arrays to store data is not scalable
- Too many variables make the source code and programming logic very complex and error-prone

## Defining dimensions for arrays

 the dimension of an object is the minimum number of coordinates needed to specify any point in it. When talking about arrays, it is easy to visualize up to three-dimensional arrays and see what these coordinates mean (row, column, depth).

![[Pasted image 20250909093404.png]]

> In almost all modern programming languages, the dimensions are written from **higher to lower,** like  `Dn x Dn-1 x Dn-2  ... D1`  where the `Di` is the size of the ith dimension.

![[Pasted image 20250909093508.png]]

To access a data item and index `I1, I2, I3 ... In` , we use the same **higher-to-lower** notation in almost all programming languages.

## Multidimensional arrays

An array can store data of any datatypes. **==A multidimensional array is an array of arrays.==** It is just a regular array, but instead of storing any primitive or user-defined datatype, **==it stores an array (single or multidimensional) as its data item.==** The depth to which this goes (array of arrays) is called the **dimension** of the array.

- **Single dimension array** - An array of non-array datatype
- **Two dimension array** - An array of arrays of non-array datatype
- **Three dimension array** - An array of arrays of arrays of non-array datatype
And this can go on

## Overview of supported operations

### Construction

Almost all the major programming languages support adding more dimensions to a regular array in one form or another. **==Since a multidimensional array is just an array, it has a fixed size that cannot be modified after creation. All data items in the array must be of the same data type.==**

![[Pasted image 20250909094157.png]]

```java
public static void main() {

    // Declaring a 2D array

    int[][] numbers2d;

    // Declaring a 3D array

    int[][][] numbers3d;

    // Initializing a 2D array of size 2x3

    int[][] numbers2d = {   {1, 2, 3},

                            {4, 5, 6}

                        };

    // Initializing a 3D array of size 2x3x2

    int[][][] numbers3d = {

                            { {1, 2}, {4, 5}, {7, 8} },

                            { {9, 10}, {11, 12}, {13, 14} },

                           };

}
```

### Accessing elements

can access data items in a multidimensional array like a regular array using the subscript operator `[]` and an index. Since every data item in a multidimensional array is also an array, we chain the subscript operator to access the data item in the internal array.

![[Pasted image 20250909094403.png]]

```java
public static void main() {

    // Initializing a 2d array

    int[][] numbers2d = {   {1, 2, 3},

                            {4, 5, 6}
                        };


    // Array elements are accessed using

    // square brackets [] twice

    System.out.println("(0,2) value: " + numbers2d[0][2]);

    System.out.println("(1,2) value: " + numbers2d[1][2]);

}
```

### Modifying elements

![[Pasted image 20250909094545.png]]

```java
public static void main() {

    // Initializing a 2d array

    int[][] numbers2d = {   {1, 2, 3},

                            {4, 5, 6}
                        };

    // Array elements are modified using

    // square brackets [] twice

    numbers2d[0][2] = 5;

    numbers2d[1][2] = 3;

}
```

### Traversal

We need **==nested loops==** to iterate over all the indices in every dimension to traverse a multidimensional array.

```java
public static void main() {


    // Initializing a 2d array

    int[][] numbers2d = {   {1, 2, 3},

                            {4, 5, 6}

                        };


    for(int i = 0; i < numbers2d.length; i++) {

        for(int j = 0; j < numbers2d[i].length; j++) {

            System.out.println("Value at" + i + "," + j + " : " + numbers2d[i][j]);

        }

    }

}
```

## Internal mechanics of multidimensional arrays

Memory is logically organized in RAM as a **linear/single-dimensional** sequence of blocks
### Storing multidimensional arrays

we cannot store multidimensional arrays directly in the memory. To store N-dimensional arrays in memory, we must somehow **map** them to single-dimensional arrays.

![[Pasted image 20250909095126.png]]

For the programmer, the data they are accessing is stored logically in an N-dimensional space. So, they will access it using N indices representing its coordinates in the N-dimensional space. However, since the data is physically stored in memory (which is single-dimensional), there have to be very fast and efficient ways to convert the N-dimensional indices to a single index where the data is stored in memory.

Different techniques can be used to map an N-dimensional array into a single-dimensional memory. The most common techniques are given below.

 - Row major ordering
 - Column major ordering

## Understanding row major order

The row-major order **==is the simplest and most intuitive order for storing multidimensional arrays.==** It is one way to serialize/deserialize a multidimensional array to and from a single-dimensional/linear sequence.

In this order, consecutive elements in a **row** (as seen in the logical representation) of an array are placed consecutively to each other in the memory

![[Pasted image 20250909095505.png]]

### Layout in memory

It is hard to visualize the logical representation of this array. Row-major ordering is a way to serialize this multidimensional array into a single-dimensional/linear sequence of elements to store it in memory, which is also single-dimensional/linear.

> ==We iterate through all values in the array, with the **lowest dimension moving fastest**, and store element s sequentially in memory.==

### Accessing elements

if we know the **base address** (where the multidimensional array starts in memory) and the **size** of each element.

![[Pasted image 20250909095736.png]]


```java
class Solution {
    public int[] solution(int[][] matrix) {
        // calculate total number of elements
        int rows = matrix.length;
        int cols = matrix[0].length;
        int[] result = new int[rows * cols];

        int index = 0; // index for result array
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[index++] = matrix[i][j];
            }
        }
        return result;
    }
}
```

## Understanding column major order

The column-major order can be considered the converse/transpose of the row-major order. It is also one of the ways by which we can serialize/deserialize a multidimensional array to and from a single-dimensional/linear sequence

In column-major order, consecutive elements in a **column** (as seen in the logical representation) of an array are placed consecutively to each other in the memory.

![[Pasted image 20250909101759.png]]

### Layout in memory

We iterate through all values in the array, with the **highest dimension moving fastest**, and store elements sequentially in memory.

### Accessing elements

if we know the **base address** (where the multidimensional array starts in memory) and the **size** of each element.

![[Pasted image 20250909101912.png]]

```java
class Solution {

    public int[] solution(int[][] matrix) {

        int rows = matrix.length;

        int cols = matrix[0].length;

        int[] result = new int[rows * cols];

        int index = 0;

        for (int j = 0; j < cols; j++) {        

            for (int i = 0; i < rows; i++) {    

                result[index++] = matrix[i][j];

            }

        }

        return result;

    }

}
```

