
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


# Two Pointer Pattern

Some problems require traversing an array from both ends simultaneously, and while this is often done with nested loops (inefficient), it can be solved more effectively using two-pointer techniques. It allows us to solve problems in linear time and single-pass, which would otherwise require inefficient nested loops.

![[Pasted image 20250910133956.png]]

## Two pointer technique

The two-pointer technique uses two variables, `left` and `right` initialized with 0 and end of the array, respectively, to traverse the array from both directions simultaneously until they meet in the middle. As we traverse the array, we perform the operations on the data items at these indices to solve the problem. At the end of each iteration, we increase and/or decrease `left` and `right` by some steps dictated by the problem to close the gap between them.

## Algorithm

- **Step 1:** Initialize two variables `left` and `right` to values dictated by the problem such that `left` < `right`
- **Step 2:** Loop while `left` < `right` and do the following
    - **Step 2.1:** Do some operations using `arr[left]` and `arr[right]` as dictated by the problem
    - **Step 2.2:** Decide if `left` should be increased
    - **Step 2.3:** Decide if `right` should be decreased

## Implementation

```java
import java.util.List;

public static void twoPointer(List<Integer> arr) {

        // Initialize left and right pointers to the start and end of the list

        int left = 0;

        int right = arr.size() - 1;

        // Loop until the pointers meet

        while (left < right) {
            /*

            Perform the operation on arr.get(left) and arr.get(right)

            */

            // Adjust pointers based on conditions

            if (shouldIncreaseLeft()) {

                left += increment;

            }

            if (shouldDecreaseRight()) {

                right -= decrement;

            }

        }

    }
```


## Identifying direct application

The two-pointer technique can only be directly applied to specific problems that fall under the two-pointer pattern.

> **Template:**  
   Given an array `arr` perform some operations on `arr[i]` and `arr[j]` where `i = x` and `j = y` such that `x < y` and with each iteration, `i` and `j` come closer to each other by some steps.


### Example  Flip characters

**Problem statement:** We are given an array `arr` and we have to reverse it in-place. **==An in-place reversal means we must modify the original array and not create and return a new one==**.

 **Brute force solution**

The brute-force solution to this problem is to traverse the array in the reverse direction (from end to start) and copy the items to `temp` array. Next, we traverse the `temp` array in the forward direction (from start to end) and copy the items to the original array.

```java
public void reverse(char[] arr) {

    // Create temp array to store reverse

    char[] temp = new char[arr.length];

    int lastIndex = arr.length - 1;

    // Traverse arr in revrese direction

    // and copy data to tmep

    for(int i=lastIndex; i >= 0; i--)

        temp[lastIndex-i] = arr[i];

    // Traverse temp in forward direction and

    // and copy data to arr

    for(int i=0; i <= lastIndex; i++)

        arr[i] = temp[i];

}
```


 **Two pointer solution**

> Given an array `arr` swap `arr[i]` and `arr[j]` where `i = 0` and `j = arr.length - 1` and with each iteration, `i` and `j` come closer to each other by 2 steps (1 each).

```java
class Solution {

    public void reverse(int[] arr) {

        // Initialize two pointers, one pointing to the beginning of the

        // array and the other pointing to the end of the array

        int left = 0;

        int right = arr.length - 1;

        // Use a while loop to traverse the array using the two pointers

        while (left < right) {

            // Swap the values pointed by the left and right pointers

            char temp = arr[left];

            arr[left] = arr[right];

            arr[right] = temp;

            // Move the pointers towards the center of the array

            left++;

            right--;

        }

    }

}
// --------------------------------------------------------------------------------------

class Solution {
    public void reverse(int[] arr) {
        int left = 0, right = arr.length - 1;
        while (left < right) {
            int temp = arr[left];
            arr[left++] = arr[right];
            arr[right--] = temp;
        }
    }
}

// --------------------------------------------------------------------------------------

class Solution {
    public void reverse(int[] arr) {
        for (int left = 0, right = arr.length - 1; left < right; left++, right--) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
        }
    }
}


```


### Example   Palindrome checker

Given a string **s**, write a function that returns `true` if it is a palindrome or `false` otherwise.

A palindrome is a string that reads the same forward and backward after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters.

```java
class Solution {

    public boolean solution(String s) {

         if (s == null)

            return false;

        StringBuilder sb = new StringBuilder();

        for (char c : s.toCharArray()) {

            if (Character.isLetterOrDigit(c)) {

                sb.append(Character.toLowerCase(c));

            }

        }

        char[] chars = sb.toString().toCharArray();

        int left = 0, right = chars.length - 1;

        while(left < right) {

            if(chars[left++] != chars[right--])

                return false;
        }

        return true;

    }

}
```

```java
class Solution {
    public boolean solution(String s) {
        if (s == null) return false;

        
        StringBuilder sb = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (Character.isLetterOrDigit(c)) {
                sb.append(Character.toLowerCase(c));
            }
        }

        char[] chars = sb.toString().toCharArray();

        
        for (int left = 0, right = chars.length - 1; left < right; left++, right--) {
            if (chars[left] != chars[right]) {
                return false;
            }
        }

        return true;
    }
}
```


### Example  Vowel exchange

Given a string **s**, write a function to reverse the vowels in the string and return the updated string.

For this problem, consider only the vowels in the English alphabet: `a`, `e`, `i`, `o`, `u`, including both uppercase and lowercase forms.

```java
static boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' 
               || c == 'o' || c == 'u';
    }

    static String reverseVowels(String s) {
        char[] str = s.toCharArray();
        int left = 0, right = str.length - 1;
        
        // Two-pointer approach to swap vowels
        while (left < right) {
            
            // Move left pointer until a vowel is found
            while (left < right && !isVowel(str[left])) {
                left++;
            }

            // Move right pointer until a vowel is found
            while (left < right && !isVowel(str[right])) {
                right--;
            }

            // Swap the vowels
            if (left < right) {
                char temp = str[left];
                str[left] = str[right];
                str[right] = temp;
                left++;
                right--;
            }
        }
        
        return new String(str);
    }
```

```java
class Solution {
    public String solution(String s) {
    
        char[] chars = s.toCharArray();
        int left = 0, right = s.length() - 1;
        String vowels = "aeiou";
        
        while(left < right) {
            if(vowels.indexOf(chars[left]) == -1) {
                left++;
            } else if(vowels.indexOf(chars[right]) == -1) {
                right--;
            } else {
                // Swap vowels
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right] = temp;
                left++;
                right--;
            }
        }
        
        return new String(chars);
    }
}
```

### Example Reverse words

Given a string **s**, write a function that reverses the words in the given string while preserving the original word order. The string may contain leading or trailing white spaces, and the words in the input string might be separated by more than a single space character.

```java
class Solution {

    public String solution(String s) {

        if (s == null || s.isEmpty()) {

            return s;

        }

        String[] words = s.trim().split("\\s+");

        for (int i = 0; i < words.length; i++) {

            words[i] = reverseWord(words[i]);

        }

        return String.join(" ", words);

    }

    private String reverseWord(String word) {

        char[] chars = word.toCharArray();

        int left = 0, right = chars.length - 1;

        while (left < right) {

            char temp = chars[left];

            chars[left] = chars[right];

            chars[right] = temp;

            left++;

            right--;

        }

        return new String(chars);

    }

}
```

```java
class Solution {

    public int findWordEnd(char[] arr, int start) {

        // Assign the start index to the end index

        int end = start;

        // Iterate through the string until a space is encountered

        while (end < arr.length && arr[end] != ' ') {

            end++;

        }

        // Return the index of the last character of the word

        return end - 1;

    }


    public void reverseWord(char[] arr, int left, int right) {

        // Use a while loop to traverse the string using the two pointers

        while (left < right) {

            // Swap the characters pointed by the left and right pointers

            char temp = arr[left];

            arr[left] = arr[right];

            arr[right] = temp;

            // Move the pointers towards the center of the string

            left++;

            right--;

        }
    }

  

    public String reverseWords(String s) {

        char[] arr = s.toCharArray();

        int start = 0;

  

        // Iterate through the string

        while (start < s.length()) {

            // Skip any leading spaces

            if (arr[start] == ' ') {

                start++;

                continue;

            }


            // Find the end of the current word

            int end = findWordEnd(arr, start);

            // Reverse the characters in the current word using two

            // pointer method

            reverseWord(arr, start, end);

            // Move the start pointer to the next word

            start = end + 1;

        }

        return new String(arr);

    }

}
```

### Example Reverse segments

Given a string **s** and an integer **k**, write a function that reverses **k** characters of the string for every **2k** characters from the start of the string and returns the new string.

> You must abide by the following constraints:
> 
> - If there are fewer than **k** characters left, reverse them all.
> - If there are at least **k** but fewer than **2k** characters left, reverse only the first k characters and leave the rest untouched.

```java
class Solution {
    public String solution(String s, int k) {
        char[] chars = s.toCharArray();
        
        for (int i = 0; i < chars.length; i += 2 * k) {
            int left = i;
            int right = Math.min(i + k - 1, chars.length - 1);
            
            while (left < right) {
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right] = temp;
                left++;
                right--;
            }
        }
        
        return new String(chars);
    }
}
```

### Example Reverse segments

Given a string **s**, write a function that returns a string of words in reverse order concatenated by a single space. The words of the input string are separated by **at least** a single space. The string may contain leading or trailing white spaces or multiple spaces between two words. The returned string must only have one space between the words. Do not include any leading or trailing whitespaces.

```java
public class Solution {
    public String reverseWords(String s) {
        // Step 1: Trim the string to remove leading/trailing spaces
        s = s.trim();
        
        // Step 2: Use StringBuilder to build result
        StringBuilder result = new StringBuilder();
        
        // Step 3: Two pointers approach - scan from right to left
        int right = s.length() - 1;
        
        while (right >= 0) {
            // Skip spaces
            while (right >= 0 && s.charAt(right) == ' ') {
                right--;
            }
            
            // If we've reached the beginning, break
            if (right < 0) break;
            
            // Find the start of current word
            int left = right;
            while (left >= 0 && s.charAt(left) != ' ') {
                left--;
            }
            
            // Add the word to result
            if (result.length() > 0) {
                result.append(' '); // Add space before word (except first word)
            }
            result.append(s.substring(left + 1, right + 1));
            
            // Move right pointer to continue
            right = left;
        }
        
        return result.toString();
    }
}
```

--- 

# Two Pointer Reduction

Some problems may not fit the template for the direct application of the two-pointer pattern, but we may be able to reduce them to problems that fit the template and can be solved by directly applying the two-pointer technique.

We need to make some critical observations to determine whether the reduction is possible; asking yourself the following questions will help you determine whether a problem can be reduced to another problem solvable by directly applying a two-pointer pattern.

**Ask yourself questions:**

- **==Q1. Does the order of items in the array matter?**==  
- ==**Q2. Do we need to work simultaneously with two items in the array?**==  
- ==**Q3. Does traversing from both ends have some special characteristics?**==  
- ==**Q4. Can we reduce the problem to another problem? If yes, ask yourself the above questions for the reduced problem==**

## Example

> **Problem statement:** We are given an array `arr` of integers and an integer value `target`. We must return true if two values exist in the array whose sum equals `target`.

![[Pasted image 20250911090735.png]]

 **Brute force solution**

The brute-force solution to this problem is to use nested loops to pick every item in the array and check its sum with all the other items. If the sum of any two items equals the target, we return true. Otherwise, we return false.

```java
public static boolean twoSum(int[] arr, int target) {
    // Use nested loop to find sum of all pairs
    for (int i = 0; i < arr.length; i++) {
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[i] + arr.get[j] == target) {
                return true;
            }

        }

    }
    return false;
}
```

 **Two pointer reduction solution**

The critical observation here is that the order of items in the array does not matter, and sorting the array establishes some special relationship between items when traversed from both ends.

The sorted order of the array allows us to discard values whose sum with other values in the array will always be either greater or less than the `target`. This reduces the problem to a problem solvable by direct application of the two-pointer pattern. We traverse from both ends, operate on the data items, and close the gap between `left` and `right` in each iteration

```java
import java.util.*;

class Solution {

    public int[] twoSum(int[] arr, int target) {

        // Sort the array in non-decreasing order

        Arrays.sort(arr);

        int left = 0;

        int right = arr.length - 1;

        // Use a while loop to traverse the array using the two pointers

        while (left < right) {

            int sum = arr[left] + arr[right];

            // Found a pair that sums up to the target

            if (sum == target) {

                return new int[] { arr[left], arr[right] };

            }
            // Move the left pointer to increase the sum

            else if (sum < target) {

                left++;

            }
            // Move the right pointer to decrease the sum
            else {
                right--;
            }

        }
        // No pair found, return an empty array

        return new int[0];
    }

}
```

 **Proof of correctness**

The two pointer solution works by discarding one item in each iteration that can never be paired with any other item in the array to make the sum equal to `target`.

Consider that the `sum = arr[left] + arr[right]` is less than `target` in the first iteration. Since `arr[right]` is the maximum item in the array, we can be sure that no other item can be added to `arr[left]` to get a greater sum. This means all pairs in the array containing `arr[left]` are smaller than `target`. Another way to look at it is that we paired all items in the array with `arr[left]` and found the sum to be less than `target`.

![[Pasted image 20250911091545.png]]

consider the `sum = arr[left] + arr[right]` is greater than `target` the remaining array. This would mean all pairs in the **remaining** array with `arr[right]` in it have a sum greater than `target` as `arr[left]` is the minimum of all **remaining** items.

![[Pasted image 20250911091722.png]]

However, in this iteration, we only considered the pairs of `arr[right]` with the **remaining** items in the array and not the discarded item `arr[0]`. This is sufficient because we already considered **all** pairs of the previously discarded items, including the ones with `arr[right]`, before discarding them.

## Example Two sum

Given an integer array **arr** and an integer **target**, write a function to check if two numbers exist in the array that sum up to the target. If such a pair exists, return them in an array, if not return an empty array. You can return the answer in **any order**.

```java
import java.util.Arrays;  
  
public class Solution {  
  
    public int[] twoSum(int[] arr, int target)  
    {  
        if (arr == null || arr.length < 2) {  
            return new int[0];  
        }  
        Arrays.sort(arr);  
  
        int left = 0;  
  
        int right = arr.length - 1;  
  
        while (left < right) {  
  
            if (arr[left] + arr[right] == target) {  
                return new int[]{arr[left], arr[right]};  
            }  
  
            if (arr[left] + arr[right] < target) {  
                left++;  
            } else {  
                right--;  
            }  
        }  
  
        return new int[0];  
    }  
}
```

## Example  Target limited two sum

Given an array **arr** consisting of non negative integers and an integer **target**, write a function to find the maximum possible sum such that there exist two distinct indices `i` and `j`, satisfying the condition `A[i] + A[j] = sum` and the sum is **less than** the **target**. If there are no such indices `i` and `j` that satisfy the equation, return `-1`.

```java
import java.util.Arrays;  
  
public class Solution {  
  
    public int targetLimitedTwoSum(int[] arr, int target) {  
        Arrays.sort(arr);  
  
        int left = 0;  
        int right = arr.length - 1;  
  
        int maxSum = Integer.MIN_VALUE;  
  
        while (left < right) {  
            int sum = arr[left] + arr[right];  
            if (sum <= target) {  
                maxSum = Math.max(maxSum, sum);  
                left++;  
            } else {  
                right--;  
            }  
        }  
       return maxSum;  
    }  
}
```


## Example  Duplicate aware two sum

Given an integer array **arr** and an integer **target**, write a function to check if two numbers exist in the array that sum up to the target. If such pairs exist, return all of them, if not return an empty array. You can return the answer in **any order**.

You must not return the same pair more than once i.e. all pairs should be unique.

```java
public List<List<Integer>> duplicateAwareTwoSum(int[] arr, int target) {  
    Arrays.sort(arr);  
    int left = 0, right = arr.length - 1;  
    List<List<Integer>> result = new ArrayList<>();  
  
    while (left < right) {  
        int sum = arr[left] + arr[right];  
        if (sum == target) {  
            result.add(Arrays.asList(arr[left], arr[right]));  
            left++;  
            right--;  
            while (left < right && arr[left] == arr[left - 1]) left++;  
            while (left < right && arr[right] == arr[right + 1]) right--;  
        } else if (sum < target) {  
            left++;  
        } else {  
            right--;  
        }  
    }  
    return result;  
}
```


## Example   Largest container

You are given an integer array **heights**, where `height[i]` represents the height of a wall at position `i`. Write a function to find two walls that, together with the x-axis, form a container holding the maximum water and return the area of this container.

``**Area = min(heights[i], heights[j]) × (j − i)**

Where `i` and `j` are the indices of the two walls, and `i` < `j`.``

![[Pasted image 20250911100039.png]]

```java
public class Solution {  
    public int largestContainer(int[] heights)  
    {  
        int left = 0, right = heights.length - 1, maxArea = 0;  
        while (left < right) {  
            int area = Math.min(heights[left], heights[right]) * (right - left);  
            maxArea = Math.max(maxArea, area);  
            if (heights[left] < heights[right]) {  
                left++;  
            } else {  
                right--;  
            }  
        }  
        return maxArea;  
    }  
}
```

---

# Two Pointer Subproblem

Some problems may consist of smaller subproblems that can be solved using the two-pointer technique. Solving these subproblems may either partially or fully solve the original problem. These are usually **medium** or **hard** problems

> **==Ask yourself questions:==**  
   **==Q1. Can the problem or solution be broken down into smaller subproblems?==**  
   **==Q2. Can any subproblem be solved using the two-pointer technique?**==

## Example K Rotations

**Problem statement:** We are given an array `arr` of integers and an integer value `k`. We must rotate the array `k` times to the left.

![[Pasted image 20250912092251.png]]


**Brute force solution**

The brute-force solution is to create another array and copy items from the original array to the new one at k shifted indices. Then, we can copy the items from the new array to the original one.

```java
public class KRotate {
    public static void kRotate(int[] arr, int k) {

        int n = arr.length;
        // Normalize k to avoid unnecessary rotations

        k = k % n;

        // Create a temporary array of the same size

        int[] temp = new int[n];

        // Copy items into the temp array starting from index k

        for (int i = 0; i < n; i++) {

            // Rotate if we go out of bounds

            temp[i] = arr[(i + k) % n];

        }
        // Copy items from the temp array back to the original array

        for (int i = 0; i < n; i++) {

            arr[i] = temp[i];
        }
    }
}
```

**Two pointer subproblem**

The critical observation here is that a rotation can be viewed as a sequence of three reversal operations. We reverse the entire array, then the last k items, and finally, the remaining N-k items

![[Pasted image 20250912092701.png]]

```java
class Solution {
    public void reverse(int[] arr, int start, int end) {

        while (start < end) {

            int temp = arr[start];

            arr[start] = arr[end];

            arr[end] = temp;

            start++;

            end--;

        }

    }

  
    public void kRotations(int[] arr, int k) {

        int n = arr.length;

        // Set k to be in the range of [0, n)

        k %= n;
        
        // Reverse the entire array using two pointer method

        reverse(arr, 0, n - 1);

        // Reverse the first k elements using two pointer method

        reverse(arr, 0, k - 1);

        // Reverse the remaining elements using two pointer method

        reverse(arr, k, n - 1);

    }

}
```

## Example Three sum

Given an integer array **arr**, write a function that returns all the triplets `[arr[i], arr[j], arr[k]]` such that `i != j`, `i != k`, and `j != k`, and `arr[i] + arr[j] + arr[k] == 0`. You can return the answer in **any order**.

Notice that the solution set must not contain duplicate triplets.

```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] arr) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(arr);
        
        for (int i = 0; i < arr.length - 2; i++) {
            // Skip duplicate "first" elements
            if (i > 0 && arr[i] == arr[i - 1]) continue;

            int left = i + 1;
            int right = arr.length - 1;

            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];

                if (sum == 0) {
                    result.add(Arrays.asList(arr[i], arr[left], arr[right]));

                    
                    while (left < right && arr[left] == arr[left + 1]) left++;
                    while (left < right && arr[right] == arr[right - 1]) right--;

                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;  
                } else {
                    right--; 
                }
            }
        }

        return result;
    }
}
```

## Example  Approximate three sum 

Given an integer array **arr** and an integer **target**, write a function to find three integers in arr such that the sum is closest to the target. You must return the sum of the three integers

```java
import java.util.*;

class Solution {
    public int approximateThreeSum(int[] arr, int target) {
        // Step 1: Sort the array to enable two-pointer technique
        Arrays.sort(arr);
        
        int closestSum = arr[0] + arr[1] + arr[2]; // Initialize with first triplet
        
        // Step 2: Iterate through array, fixing first element
        for (int i = 0; i < arr.length - 2; i++) {
            // Step 3: Use two pointers for remaining elements
            int left = i + 1;
            int right = arr.length - 1;
            
            while (left < right) {
                int currentSum = arr[i] + arr[left] + arr[right];
                
                // Update closest sum if current is closer to target
                if (Math.abs(currentSum - target) < Math.abs(closestSum - target)) {
                    closestSum = currentSum;
                }
                
                if (currentSum == target) {
                    // Found exact match, can't get closer
                    return currentSum;
                } else if (currentSum < target) {
                    // Sum is too small, need larger numbers
                    left++;
                } else {
                    // Sum is too large, need smaller numbers
                    right--;
                }
            }
        }
        
        return closestSum;
    }
}

```

## Example  Approximate three sum 

Given an array **arr** and an integer **target**, write a function to find and return an array of all the unique quadruplets `[arr[a], arr[b], arr[c], arr[d]]` such that the following conditions are met:

1. `0 <= a, b, c, d < n`

2. `a`, `b` , `c` and `d` are distinct

3. `arr[a] + arr[b] + arr[c] + arr[d] = target`

```java
import java.util.*;

class Solution {
    public List<List<Integer>> fourSum(int[] arr, int target) {
        List<List<Integer>> result = new ArrayList<>();
        
        // Handle edge case
        if (arr == null || arr.length < 4) {
            return result;
        }
        
        // Step 1: Sort the array
        Arrays.sort(arr);
        
        // Step 2: Fix first element
        for (int i = 0; i < arr.length - 3; i++) {
            // Skip duplicates for first element
            if (i > 0 && arr[i] == arr[i - 1]) {
                continue;
            }
            
            // Step 3: Fix second element
            for (int j = i + 1; j < arr.length - 2; j++) {
                // Skip duplicates for second element
                if (j > i + 1 && arr[j] == arr[j - 1]) {
                    continue;
                }
                
                // Step 4: Use two pointers for remaining two elements
                int left = j + 1;
                int right = arr.length - 1;
                
                // Calculate the target for the two remaining elements
                long twoSum = (long) target - arr[i] - arr[j];
                
                while (left < right) {
                    int currentSum = arr[left] + arr[right];
                    
                    if (currentSum == twoSum) {
                        // Found a quadruplet
                        result.add(Arrays.asList(arr[i], arr[j], arr[left], arr[right]));
                        
                        // Skip duplicates for left pointer
                        while (left < right && arr[left] == arr[left + 1]) {
                            left++;
                        }
                        // Skip duplicates for right pointer
                        while (left < right && arr[right] == arr[right - 1]) {
                            right--;
                        }
                        
                        left++;
                        right--;
                    } else if (currentSum < twoSum) {
                        // Sum is too small, move left pointer right
                        left++;
                    } else {
                        // Sum is too large, move right pointer left
                        right--;
                    }
                }
            }
        }
        
        return result;
    }
}

```

---

#  The Simultaneous Traversal Pattern
 
 there are cases where we may need to operate on data items from two arrays of different sizes at once. This requires traversing both arrays at the same time, and the decision to move to the next item in any of those may depend on the outcome of some function. We may move ahead only in one array or in both of them. The simultaneous traversal technique can be used to iterate in both arrays simultaneously in a single pass.

![[Pasted image 20250916090940.png]]

The simultaneous traversal technique is just an extension of traversing in a single array. Consider we have two arrays `arr1` and `arr2`, we maintain two variables, `index1` and `index2` holding the current index of the first and second array, respectively. In each iteration, based on some condition, we move ahead in either one or both arrays. This process is repeated until any array is traversed completely, which is the terminating condition in most cases. After the simultaneous traversal terminates, we may want to check if any array has still not been completely traversed and process its items.

This technique can be applied to two arrays in multiple ways, depending on the direction of traversal and the number of hops in iteration. We could either traverse from start to end in both arrays, the other way around, or a mix of both. Another variation would be if we hop multiple steps in each array in every iteration instead of just one.

## Algorithm

1. **Initialize variables**
   - Set `index1 = 0`
   - Set `index2 = 0`

2. **Traverse both arrays simultaneously**
   - While `index1 < arr1.size()` **and** `index2 < arr2.size()`:
     - **Step 2.1:** Decide if we should traverse in the first array  
       - If yes → process `arr1[index1]` and increment `index1`
     - **Step 2.2:** Decide if we should traverse in the second array  
       - If yes → process `arr2[index2]` and increment `index2`

3. **Process remaining elements of `arr1` (if any)**
   - While `index1 < arr1.size()` → process `arr1[index1]` and increment `index1`

4. **Process remaining elements of `arr2` (if any)**
   - While `index2 < arr2.size()` → process `arr2[index2]` and increment `index2`

## Implementation

```java
class SimultaneousTraversal {

    public void simultaneousTraversal(List<Integer> arr1, List<Integer> arr2) {

        // Initialize index variables for two arrays

        int index1 = 0, index2 = 0;

        // Traverse both arrays simultaneously until

        // the end of any one array is reached

        while (index1 < arr1.size() && index2 < arr2.size()) {

            if (shouldMoveFirst) { // Replace this with actual condition

  

                // Process arr1[index1]

                // ....

                index1++;

            }

            if (shouldMoveSecond) { // Replace this with actual condition

                // Process arr2[index2]

                // ....

                index2++;

            }

        }


        while (index1 < arr1.size()) {

            // Process arr1[index1]

            // .......

            index1++;

        }

        while (index2 < arr2.size()) {

            // Process arr2[index2]

            // .......

            index2++;

        }

    }

}
```


## Identifying the simultaneous traversal pattern

> **Template:** 
    Given two arrays, simultaneously traverse in both arrays based on the outcome of some function applied to items of both arrays.

**Problem statement:** Given two arrays `s` and `t`, check if `s` is a subsequence of `t`.

**Brute force solution**

  
The simplest brute-force solution to this problem is to pick the first item in `s` and traverse in the array `t` until we find the first occurrence of that item in `t`. We then pick the next item in `s` and traverse `t` from where we left off earlier until we find the first occurrence of the next item. We repeat this process and return `true` if we find all the items of `s` in `t` this way. Otherwise, if we reach the end of `t` while some items in `s` still remain, we return `false`.

```java
class SubsequenceChecker {

    boolean isSubsequence(List<Integer> s, List<Integer> t) {

        int j = 0;

        // Traverse each element of array `s`
        for (int i = 0; i < s.size(); i++) {
            if (j == t.size()) {
                return false;
            }

            // Store current element of `s`

            int item = s.get(i);

            // Traverse `t` and look for `item` in `t`

            while (j < t.size()) {

                if (item.equals(t.get(j))) {

                    j++;

                    break;

                }

                j++;

            }

        }

        return true;

    }

}
```

**Simultaneous traversal solution**

> **Template:**
    Given two arrays, simultaneously traverse both arrays and compare items in both arrays. If they are equal, iterate in both arrays; otherwise, iterate in only one.

```java
class Solution {

    public boolean subsequenceChecker(String s, String t) {

        // pointer for s

        int index1 = 0;

        // pointer for t

        int index2 = 0;

  

        while (index1 < s.length() && index2 < t.length()) {

            if (s.charAt(index1) == t.charAt(index2)) {

                // If the current character matches, move the pointer for

                // s

                index1++;

            }

            // Move the pointer for t in every iteration

            index2++;

        }

        // If index1 reaches the end of s, it means all characters in s

        // are found in t in the same order

        return index1 == s.length();
    }

}
```

## Example Subsequence checker

Given two strings, **s** and **t**. Write a function that returns `true` if s is a subsequence of t, or `false` otherwise.

```java
class Solution {

    public boolean subsequenceChecker(String s, String t) {

 // pointer for s

        int index1 = 0;

        // pointer for t

        int index2 = 0;

        while (index1 < s.length() && index2 < t.length()) {

            if (s.charAt(index1) == t.charAt(index2)) {

                // If the current character matches, move the pointer for

                // s

                index1++;

            }

            // Move the pointer for t in every iteration

            index2++;

        }

        // If index1 reaches the end of s, it means all characters in s

        // are found in t in the same order

        return index1 == s.length();

    }

}
```

## Example  Merge sorted arrays

Given two integer arrays, **arr1** and **arr2**, sorted in non-decreasing order, and two integers, **m** and **n**, representing the number of elements in arr1 and arr2, respectively. Write a function to modify array arr1 in place to merge array arr2 into the back of array arr1.

>You may assume that arr1 has enough space (size that is greater or equal to m + n) to hold additional elements from arr2.

```java
class Solution {

    public void mergeSortedArrays(int[] arr1, int m, int[] arr2, int n) {

        // last index of non-zero elements in arr1

        int index1 = m - 1;

        // last index of elements in arr2

        int index2 = n - 1;

        // last index of arr1

        int index3 = m + n - 1;

        // merging arr1 and arr2 from the rightmost end of the arrays

        while (index1 >= 0 && index2 >= 0) {

            // if the element in arr1 is greater than the element in arr2

            // then place the element from arr1 to the last index of arr1

            // and decrement the index of arr1

            if (arr1[index1] > arr2[index2]) {

                arr1[index3--] = arr1[index1--];

            }

            // if the element in arr2 is greater than the element in arr1

            // then place the element from arr2 to the last index of arr1

            // and decrement the index of arr2

            else {

                arr1[index3--] = arr2[index2--];

            }

        }

  

        // if there are still remaining elements in arr2

        while (index2 >= 0) {

            arr1[index3--] = arr2[index2--];

        }

    }

}
```

## Example  Unique intersections

Given two integer arrays **arr1** and **arr2**, write a function to find and return an array of their intersection. You can return the result in **any order**.

Each element in the result **must be unique**.

```java
class Solution {  
    public List<Integer> uniqueIntersections(int[] arr1, int[] arr2) {  
        List<Integer> result = new ArrayList<>();  
        int  index1 = 0, index2 = 0;  
        Arrays.sort(arr1);  
        Arrays.sort(arr2);  
        while(index1 < arr1.length && index2 < arr2.length){  
            if(arr1[index1] == arr2[index2] && !result.contains(arr1[index1])){  
                result.add(arr1[index1]);  
                index1++;  
                index2++;  
            }else if(arr1[index1] < arr2[index2]){  
                index1++;  
            }else{  
                index2++;  
            }  
        }  
  
        return result;  
    }  
}
```

## Example Repeated intersections

Given two integer arrays, **arr1**, and **arr2**, write a function to find and return an array of their intersection. You can return the result in **any order**.

Each element in the result must appear **as many times as it appears in both arrays.**

```java
class Solution {  
    public List<Integer> uniqueIntersections(int[] arr1, int[] arr2) {  
        List<Integer> result = new ArrayList<>();  
        int  index1 = 0, index2 = 0;  
        Arrays.sort(arr1);  
        Arrays.sort(arr2);  
        while(index1 < arr1.length && index2 < arr2.length){  
            if(arr1[index1] == arr2[index2]){  
                result.add(arr1[index1]);  
                index1++;  
                index2++;  
            }else if(arr1[index1] < arr2[index2]){  
                index1++;  
            }else{  
                index2++;  
            }  
        }  
        return result;  
    }  
}
```

---

#  Fixed sized Sliding Window

The fixed sized sliding window pattern is a classification of problems that can be solved using the fixed sized sliding window technique.

![[Pasted image 20250918113157.png]]

## Fixed sized sliding window technique

Consider a function `f` such that `f(i, j)` denotes the aggregated value of `f` over the subarray from index `i` to index `j` (including both).

![[Pasted image 20250918113244.png]]

Now consider we need to apply this function to all subarrays of size `k` in the given array, i.e. `f(0, k-1), f(1, k), .... f(n-k, n-1)`.

![[Pasted image 20250918113311.png]]

The fixed-sized sliding window technique uses two variables `start` and `end`, to maintain a fixed-sized **window** (subarray). Another variable `aggregate` holds the output of `f` when applied over the data items of the current window. We slide the window 1 step to the right in each iteration and update `aggregate` accordingly

![[Pasted image 20250918113341.png]]

 For a fixed-sized widow of size `k`, we initialize `start = 0` and `end = 0` and iterate until `end` reaches the end of the array. In each iteration, we add the contribution of `arr[end]` to the aggregate and then check if the window size `end - start + 1` is greater than `k`. If the window size is greater than `k`, we remove the contribution of the item at `arr[start]` from `aggregate` by using the removal operation for the function `f  and then contract the current window from the start by incrementing `start` by 1.

==**The fixed-sized sliding window technique avoids the inner loop by removing the contribution of the removed item using the removal operation for the function and adding the contribution of the newly added item as the window slides**==

## Algorithm

- **Step 1: Initialize two variables, `start` and `end` to 0.**
- **Step 2: Create a variable `aggregate` to store the aggregated value of a window and initialize it to some default value**
- **Step 3: Loop while `end` < `arr.size()` and do the following**
    - **Step 3.1: Add contribution of `arr[end]` to `aggregate`**
    - **Step 3.2: If the size of the current window (`end` - `start` + 1) is greater than `k` remove the contribution of `arr[start]` from `aggregate` and increment `start` by 1**
    - **Step 3.2: If the size of the current window (`end` - `start` + 1) is equals `k`, process `aggregate`**
    - **Step 3.3: Increment `end` by 1**


```java
public class FixedSizeSlidingWindow {

    public void fixedSizeSlidingWindow(int[] arr, int k) {

        // Initialize start and end to 0

        int start = 0, end = 0;

        // Initialize aggregate to a default value

        int aggregate = 0;

        // Move the window one step to the right until

        // it reaches the end of the array

        while (end < arr.length) {

            // Add contribution of arr[end]

            aggregate = fAdd(aggregate, arr[end]);

            // Check if window size is greater than k

            if (end - start + 1 > k) {

                // Remove contribution of arr[start]

                aggregate = fRemove(aggregate, arr[start]);

                // Increment start to contract the window from the start

                start++;
            }

            // Check if window size equals k

            if (end - start + 1 == k) {

                // Process aggregate

            }
            // Increment end to expand the window from the end

            end++;
        }
    }
}
```

## Identifying the fixed sized sliding window pattern

Given an array, compute the value of an aggregate function `f` for all subarrays of size `k`.  We should be able to add/remove the contribution of an item from the aggregate computed by **`f`.**

> **Problem statement:** Given an array `arr` and an integer `k`, we need to find the maximum average of all subarrays of size `k`.


**Brute force solution**

The brute-force solution to this problem is to use a loop to traverse the array from start to N-k (where N is the size of the array) using a variable `start`. In each iteration, use another loop to iterate from `start` to `start + k-  1`. to compute the average of `k` sized subarray starting at `start`. We update the maximum if we find the average of any subarray greater than any averages seen earlier

```java
class KSubarrayAverage {

  public double kSubarrayAverage(int[] arr, int k) {

      int n = arr.length;

      // Initialize maximumAverage to -infinite

      double maxAverage = -1e9;

      for (int i = 0; i <= n - k; i++) {

          int sum = 0;

          for (int j = 0; j < k; j++) {

              sum += arr[i + j];

          }

          maxAverage = Math.max(maxAverage, (double) sum / k);

      }

      return maxAverage;

  }

}
```

**Fixed sized sliding window solution**

Given an array `arr`, compute the average (function `f` ) for all subarrays of size `k`.  We can add/remove the contribution of an item from the aggregate computed by the average (function **`f`**)

We keep the sum of all items in the window instead of the average, as the average can be easily computed from the sum and size of the window. We initialize two variables `sum` and `maxAverage` with 0 and `-infinite` denoting the sum of the current window and the maximum average seen so far.

We then create a window by initalizing `start` and `end` to 0 and iterate until `end` reaches the end of the array. In each iteration, we add the contribution of the item at `end` and compute the average if needed. If the average of the current window is greater than `maxAverage`, we update `maxAverage`. At the end of all iterations, `maxAverage` will have the maximum average of all subarrays of size `k`.

```java
class Solution {

    public double kSubarrayAverage(int[] arr, int k) {

        int n = arr.length;
        // to store the starting index of the subarray

        int start = 0;

        // to store the ending index of the subarray

        int end = 0;

        // to store the current subarray sum

        int sum = 0;

        // to store the maximum average

        double maxAverage = Double.NEGATIVE_INFINITY;

        // loop through the array

        while (end < n) {

            // add the current element to the current subarray sum

            sum += arr[end];

            // if the current subarray has more than k elements

            // then remove elements from the start of the subarray till

            // the subarray has exactly k elements

            if (end - start + 1 > k) {

                // remove the first element from the subarray

                sum -= arr[start];

                // move the start pointer forward

                start++;

            }

            // if the current subarray has exactly k elements

            // then calculate the average and update the maximum average

            if (end - start + 1 == k) {

                // calculate the average and update the maximum average

                maxAverage = Math.max(maxAverage, (double) sum / k);

            }

            // move the end pointer forward

            end++;

        }

        return maxAverage;

    }

}
```


## Example Subarray size equals K

Given an integer array **arr** and a positive integer **k**, write a function to find and return the minimum sum among all subarrays of size k. If no such subarray exists, return `-1` instead.


```java
class Solution {

    public int subarraySizeEqualsK(int[] arr, int k) {

        // Edge case: If k is greater than the array size, return -1.

        if (k > arr.length) {

            return -1;

        }

        // To store the starting index of the subarray

        int start = 0;
        
        // To store the ending index of the subarray

        int end = 0;

        // To store the current subarray sum

        int sum = 0;

        // We want to find the minimum sum.

        int minSum = Integer.MAX_VALUE;

        // Sliding window to process all subarrays of size k

        while (end < arr.length) {

            // Add contribution of arr[end] to the current window sum

            sum += arr[end];

            // If the current subarray has more than k elements

            // then remove elements from the start of the subarray till

            // the subarray has exactly k elements

            if (end - start + 1 > k) {

                // Remove contribution of arr[start] as the window is now

                // too large

                sum -= arr[start];

                // Contract the window from the left

                start++;

            }

            // Check if the window size is exactly k

            if (end - start + 1 == k) {

                // Update the minimum sum

                minSum = Math.min(minSum, sum);

            }

            // Expand the window from the right

            end++;

        }
        return minSum;
    }

}
```

## Example  Consecutive ones

Given a binary array **arr** and a positive integer **k**, write a function to find and return the maximum number of consecutive `1's` from among all subarrays of size k.

```java
class Solution {

    public int consecutiveOnes(int[] arr, int k) {

        // To store the starting index of the subarray

        int start = 0;

        // To store the ending index of the subarray

        int end = 0;

        // To store the current count of 1s in the window

        int countOnes = 0;

        // To store the maximum number of 1s in any subarray of size k

        int maxOnes = 0;

        // Loop through the array

        while (end < arr.length) {

            // Add the current element to the count if it's 1

            if (arr[end] == 1) {

                countOnes++;

            }

            // If the current subarray has more than k elements

            // then shrink it from the start

            if (end - start + 1 > k) {

                // Remove the contribution of arr[start] if it was 1

                if (arr[start] == 1) {

                    countOnes--;

                }

                // Move the start pointer forward

                start++;

            }

            // If the current subarray has exactly k elements

            // then update the maximum number of 1s

            if (end - start + 1 == k) {

                maxOnes = Math.max(maxOnes, countOnes);

            }

            // Move the end pointer forward

            end++;

        }

        return maxOnes;

    }

}
```


## Example  Negative window

Given an integer array **arr** and a positive integer **k**, write a function to find and return the count of negative numbers in every subarray of size k

```java
import java.util.*;

  

class Solution {

    public List<Integer> negativeWindow(int[] arr, int k) {

        // To store the starting index of the subarray

        int start = 0;

        // To store the ending index of the subarray

        int end = 0;

        // To store the current count of negative numbers in the window

        int negativeCount = 0;

        // To store the count of negative numbers in subarrays of size k

        List<Integer> result = new ArrayList<>();

        // Loop through the array

        while (end < arr.length) {

            // Add the current element if it is negative

            if (arr[end] < 0) {

                negativeCount++;

            }

            // If the current subarray has more than k elements

            // then shrink it from the start

            if (end - start + 1 > k) {

                // Remove the contribution of arr[start]

                if (arr[start] < 0) {

                    negativeCount--;

                }

                // Move the start pointer forward

                start++;

            }

            // If the current subarray has exactly k elements

            // then add the count to the result

            if (end - start + 1 == k) {

                result.add(negativeCount);

            }

            // Move the end pointer forward

            end++;

        }
        return result;

    }
}
```

## Example  Even odd count

Given an integer array **arr** and a positive integer **k**, write a function to find and return the count of even and odd numbers, respectively, in every subarray of size k.

```java
import java.util.*;

class Solution {

    public List<List<Integer>> evenOddCount(int[] arr, int k) {

        // To store the starting index of the subarray

        int start = 0;

        // To store the ending index of the subarray

        int end = 0;

        // To store the current count of even numbers in the window

        int evenCount = 0;

        // To store the current count of odd numbers in the window

        int oddCount = 0;

        // To store the result as lists {evenCount, oddCount}

        List<List<Integer>> result = new ArrayList<>();

        // Loop through the array

        while (end < arr.length) {

            // Add the current element to the respective count

            if (arr[end] % 2 == 0) {

                evenCount++;

            } else {

                oddCount++;

            }
            // If the current subarray has more than k elements

            // then shrink it from the start

            if (end - start + 1 > k) {

                // Remove the contribution of arr[start]

                if (arr[start] % 2 == 0) {

                    evenCount--;

                } else {

                    oddCount--;

                }
                // Move the start pointer forward

                start++;

            }

            // If the current subarray has exactly k elements

            // then add the counts to the result

            if (end - start + 1 == k) {

                result.add(List.of(evenCount, oddCount));

            }
            // Move the end pointer forward

            end++;

        }
        return result;

    }

}
```

---

# Variable Sized Sliding Window Pattern 

Some problems may require us to find the output of an aggregate function over **all** subarrays of an array and then further aggregate the results from all subarrays into a single value. To solve these problems, we would need to run fixed-sized sliding windows of all sizes from 1 to N(size of the array) through the array to aggregate results for all subarrays, which is inefficient.

However, for some problems, we may only need to find results for **some** subarrays and skip the remaining. These problems can be solved by the variable-sized sliding window technique, which contracts or expands the window in each iteration as it slides through the array

![[Pasted image 20250918140451.png]]

## Variable sized sliding technique

The variable-sized sliding window technique uses two variables `start` and `end` to maintain a window in the array and a variable `aggregate` that always holds the aggregated value of `f` over the current window.

We initialize `aggregate` with some default value dictated by the problem and start with `start = 0` and `end = 0` that denotes a zero-sized window. We iterate until `end` reaches the end of the array and, in each interaction, do some or all of the operations given below.

### 1. Update aggregate with item at end

![[Pasted image 20250918140731.png]]

### 2. Process the aggregate

The value stored in `aggregate` is the aggregated value of the function `f` over the subarray from `start` to `end`. We process it as dictated by the problem.

![[Pasted image 20250918140758.png]]

### 3. Contract the window by incrementing start

If we can skip all remaining subarrays starting at `start` (the ones ending beyond `end`)  we can increment `start` by 1, which also contracts the window. We also update `aggregate` to remove the contributions of the item removed from the window.

![[Pasted image 20250918140838.png]]

### 4. Expand the window by incrementing end

If we want to consider the next subarray starting at `start` (from `start` to `end+1`)  in the next iteration, we can increment `end` by one, which also expands the window. We don't add the contribution of the newly added item to `aggregate` yet, as that will be done in the next iteration

![[Pasted image 20250918141319.png]]

## Algorithm

- **Step 1: Initialize two variables, `start` and `end` to 0.**
- **Step 2: Initialize `aggregate` to some initial value dictated by the problem.**
- **Step 3: Loop until `end` < `arr.size()` and do the following**
    - **Step 3.1: Check if we should compute aggregate**
        - **Step 3.1.1: Add contribution of `arr[end]` to `aggregate`**
    - **Step 3.2: Process `aggregate`**
    - **Step 3.3: Check if we should contract the window**
        - **Step 3.3.1: Remove the contribution of `arr[start]` from `aggregate`**
        - **Step 3.3.2: Increment `start`**
    - **Step 3.3: Check if we should expand the window**
        - **Step 3.3.2: Increment `end`**


## Implementation

```java
public class SlidingWindow {
    public  void slidingWindow(int[] arr) {

        // Initialize start and end to 0

        int start = 0, end = 0;

        // Initialize aggregate to a default value

        int aggregate = 0;

        // Move the window one step to the right until

        // it reaches the end of the array

        while (end < arr.length) {

            if (shouldComputeAggregate) {

            // Add contribution of arr[end]

            aggregate = f(aggregate, arr[end]);

            }

            // Process aggregate

            // ......

            // (Add your processing code here)

            if (shouldContractWindow) {

                // Remove contribution of arr[start] using the inverse function

                aggregate = fInverse(aggregate, arr[start]);

                // Contract window

                start++;

            }

            if (shouldExpandWindow) {

                end++;

            }
        }
    }
}
```

## Identifying variable sized sliding window pattern

**Template:**

Given an array, compute the value of an aggregate function `f` for **all** subarrays. Apply another aggregate function `g` on the results and return the output. We should be able to add/remove the contribution of an item from the aggregate computed by `f`.

## Example

> **Problem statement:** Given an integer array `arr` find the subarray with the largest sum and return the sum.

**Brute force solution**

The brute-force solution to this problem is to use nested loops to find the sum of all possible subarrays. If the sum of any subarray is greater than the maximum seen so far, we update the maximum sum value. Below is an execution of the brute force solution on an array.

```java
  

class MaxSubarraySum {

    public int maxSubarraySum(int[] arr) {
        // Initialize maxSum to a very small number
        int maxSum = Integer.MIN_VALUE;
        // Use nested loops to calculate the sum of all subarrays
        for (int i = 0; i < arr.length; i++) {
            int sum = 0;
            for (int j = i; j < arr.length; j++) {
                sum += arr[j];
                // Update maxSum if the current sum is greater
                maxSum = Math.max(sum, maxSum);
            }
        }
        return maxSum;
    }
}
```


**Variable sized sliding window solution**

Given an array `arr`, compute the sum (function `f` ) for **all** subarrays. Find the maximum (function `g` ) of all results. We can add/remove the contribution of an item from the aggregate computed by sum (function `f`).

By closely observing the problem, we can see that we don't need to calculate the sum of all subarrays to find the subarray with the maximum sum. Let's look at the algorithm in more detail, and we will look at the proof of correctness later in the lesson.

We initialize `start` and `end` to 0 to create a sliding window and iterate using `end` until we reach the end of the array. We create variables `sum` and `maxSum` to aggregate the sum of all items in the current window and keep track of the maximum sum seen so far. In each iteration, we add the item at `end` to the `sum` and update `maxSum` if `sum` is greater than the maximum seen so far. If the `sum` turns negative at any point, we set `start = end + 1` to effectively contract the window size back to 0 when the window expands at the end of the iteration. We also set `sum = 0` to reset the sum as the window size is now 0.

```java
class Solution {

    public int maxSubarraySum(int[] arr) {

        int n = arr.length;

        if (n == 0) {

            return 0;

        }

        // Initialize start and end to 0

        int start = 0;

        int end = 0;

        // Initialize sum to a default value (current sum)

        int sum = arr[end];

        // To store the maximum subarray sum found so far

        int maxSum = arr[end];

        // Increment to start from index 1 as index 0 has already been

        // taken into account

        end++;

        // Sliding window

        while (end < n) {

            // If the current sum becomes negative, reset the window

            if (sum < 0) {

                sum = arr[end];

                start = end + 1;

            }

            // Otherwise, add contribution of arr[end]

            else {

                sum += arr[end];

            }

            // Update the maximum subarray sum found so far

            maxSum = Math.max(maxSum, sum);

            // Expand the window from the right

            end++;

        }

        return maxSum;
    }
}
```

## Example Consecutive ones II

Given a binary array **arr**, write a function to find and return the maximum number of consecutive `1's` in the array.

```java
class Solution {

    public int consecutiveOnesII(int[] arr) {

        // To store the starting index of the subarray
        int start = 0;

        // To store the ending index of the subarray
        int end = 0;

        // To store the current count of 1s in the window
        int countOnes = 0;

        // To store the maximum number of 1s in any subarray
        int maxOnes = 0;

        // Move the window one step to the right until it reaches the end

        // of the array
        while (end < arr.length) {
            // Add the current element to the count if it's 1
            if (arr[end] == 1) {
                countOnes++;
            }
            // Otherwise, process the aggregate and reset count
            else {
                // Process aggregate when we encounter a 0

                maxOnes = Math.max(maxOnes, countOnes);
                
                // Reset count for consecutive ones
                countOnes = 0;
            }
            // Expand the window
            end++;
        }

        // Final check for the last segment of ones
        maxOnes = Math.max(maxOnes, countOnes);
        return maxOnes;
    }
}
```

## Example Product conundrum

Given an array of positive integers **arr** and an integer **k**, write a function to find and return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than k.

```java
  public int productConundrum(int[] arr, int k) {
        // To store the starting index of the subarray
        int start = 0;
        // To store the ending index of the subarray

        int end = 0;
        // Initialize product to 1

        int product = 1;

  
        // Initialize answer to 0
        int answer = 0;

  
        // Move the window one step to the right until it reaches the end
        // of the array
        while (end < arr.length) {
            // Add contribution of arr[end]
            product *= arr[end];

            // Process aggregate

            while (start <= end && product >= k) {
                // Remove contribution of arr[start] using the inverse
                // function
                product /= arr[start];
  
                // Contract window
                start++;

            }

            // Count valid subarrays

            answer += end - start + 1;

            // Expand the window
            end++;

        }

        return answer;
    }
}
```


## Example Largest product subarray

Given an integer array **arr**, write a function to find the subarray with the largest product and return this product.

```java
public int largestProductSubarray(int[] arr) {
        // To store the starting index of the subarray

        int start = 0;
        // To store the ending index of the subarray

        int end = 0;
        // Initialize aggregate to track maximum and minimum products

        int maxSoFar = arr[end];

        int minSoFar = arr[end];

        int maxProduct = arr[end];

        // Increment to start from index 1 as index 0 has already been

        // taken into account

        end++;

        // Move the window one step to the right until

        // it reaches the end of the array

        while (end < arr.length) {
            // When we enter the window with arr[end]

            if (arr[end] < 0) {
                // If the current element is negative, swap the max and

                // min

                int temp = maxSoFar;

                maxSoFar = minSoFar;

                minSoFar = temp;

            }


            // Update maxSoFar and minSoFar with the current element

            maxSoFar = Math.max(arr[end], maxSoFar * arr[end]);

            minSoFar = Math.min(arr[end], minSoFar * arr[end]);

            // Update the maximum product seen so far

            maxProduct = Math.max(maxProduct, maxSoFar)

            // Check if we should contract the window (if needed)

            // In this case, we might want to start a new subarray

            // when we encounter a zero. This handles zero in the array.

            if (arr[end] == 0) {

                // Reset the products if we hit a zero

                maxSoFar = 1;

                minSoFar = 1;
                // Move start to the next element after zero

                start = end + 1;
            }
            // Expand the window
            end++;

        }
        // Return the maximum product seen so far
        return maxProduct;
    }
```

---

# Interval Merging

In some array problems, the data items stored in the array may represent an interval. An interval can be thought of as two points on the x-axis of a cartesian plane, where the x-axis represents any scalar metrics like time, distance, etc. An interval is denoted by a start and end coordinate that is often stored as a pair at each index in the array.

![[Pasted image 20250920131611.png]]

## Line sweep technique

The line sweep technique, also known as the sweep line algorithm, is a powerful approach to efficiently solve geometric problems involving events (such as intervals) on an axis of the cartesian plane. It works by "sweeping" a line across the set of events while maintaining a data structure that keeps track of active events as the line progresses

### 1. Sort the events

The first step is to sort the intervals, as the line sweep algorithm requires the events to be sorted in some order in the array holding them. Intervals are generally sorted by their start or end values. If sorted by their start values, intervals with the same start values are further sorted by their end values. Similarly, if the intervals are sorted by their end values, intervals with the same end values are further sorted by their start values.

![[Pasted image 20250920132720.png]]

This way, the array can be viewed as the x-axis of the cartesian plane with events marked on it from left to right. This allows us to traverse the array as if we were swiping a line through it on the x-axis of the cartesian plane.

![[Pasted image 20250920132739.png]]

### 2. Sweep the line

Once we have sorted the array of intervals, traversing it from start to end becomes the same as moving on the x-axis from left to right. We keep some data structure like an event counter, set, or list to keep state information as we traverse the array from start to end. This can be visualized as a vertical line moving from left to right on the x-axis and hence is called a line sweep. As the sweep line moves, it dynamically updates the state variables to correctly process overlaps, merges, or other conditions dictated by the problem.

## Understanding interval merging pattern

Some interval problems require merging all the overlapping intervals in a given array into a single interval that covers all the merged intervals. There are a few brute-force solutions to this problem using nested loops, but all of them are complicated and inefficient

### Interval merging technique

Consider we are given an array of intervals `arr` where each item in the array is a pair of an interval's start and end coordinates. The first step in merging the intervals is to sort the array in a non-decreasing order of the start coordinates of intervals. In case two intervals have the same start coordinate, we sort them by their end coordinates.

We then create another array `merged` to store all the merged intervals and initialize it with the first interval in the now-sorted `arr`. These arrays can be viewed geometrically as intervals on the x-axis of a cartesian plane, and we can now apply the line sweep technique to merge the overlapping intervals in a single pass. As we will see later, we expand the **last** interval of the `merged` when we see an overlapping interval in `arr` to merge it.

![[Pasted image 20250920133152.png]]

We then iterate in the `arr` starting from the second interval and check if it intersects with the **last** interval in the `merged` array. If the start coordinate of the interval in `arr` lies between the start and end coordinates of the **last** interval in `merged`, it means they intersect and should be merged. We merge them by updating the end coordinate of the last interval in `merged` to the end coordinate of the interval in `arr` if it is greater. We repeat this process until we find a non-intersecting interval.

If, at any point, we reach an interval that does not intersect with the last interval in `merged`, we append that interval to `merged` to make it the new last interval in `merged` which will expand to merge further intervals from `arr`. This process is repeated until we reach the end of `arr` at which point we will have the merged intervals in `merged`.

### Algorithm

- ==**Step 1: Sort the input array `arr` by the start coordinate of intervals**==
- ==**Step 2: Create a list `merged` to store the merged intervals and initialize it with the first interval from sorted `arr`.**==
- ==**Step 3: Iterate in `arr` starting from the second item:**==
    - ==**Step 3.1: If the start coordinate of the interval in `arr` lies between the start and end coordinates of the last interval in `merged`, set the end coordinate of `merged` to the end coordinate of the interval in `arr` it it is greater:**==
    - ==**Step 3.2: If the interval in `arr` does not intersect with the last interval in `merged`, append the interval in `arr` to `merged==**


```java
class Solution {

    public int[][] mergeOverlapping(int[][] arr) {

        // Sort arr by start time

        Arrays.sort(arr, (a, b) -> Integer.compare(a[0], b[0]));

        // Initialize output list and push the first interval

        List<int[]> merged = new ArrayList<>();

        merged.add(arr[0]);

        // Loop through arr and merge if overlapping or adjacent

        for (int i = 1; i < arr.length; i++) {

            // If the current interval overlaps with the last interval in

            // the merged list, merge them

            if (arr[i][0] <= merged.get(merged.size() - 1)[1]) {
                merged.get(merged.size() - 1)[1] =
                    Math.max(
                        merged.get(merged.size() - 1)[1],
                        arr[i][1]
                    );

            }

            // If the current interval is non-overlapping, add it to the
            // merged list
            else {
                merged.add(arr[i]);
            }
        }
        // Convert output list to 2D array and return

        return merged.toArray(new int[merged.size()][]);
    }
}
```

###  Identifying the interval merging pattern

>**Template:**
Given an array of intervals, merge all overlapping intervals.

**Problem statement:** Given an array of start and end times of expected deliveries for a day. Find the **minimum** number of non-overlapping intervals in the day when at least one delivery is expected at any time in each interval.

![[Pasted image 20250920133618.png]]

### Interval merging technique

The overlapping intervals in the given array can be merged to find all non-overlapping intervals in the day. At least one delivery is expected at any time in each merged interval, and the number of merged intervals is also the minimum number of intervals satisfying the given condition. The problem description fits the template for the interval merging pattern.

>**Template:**  
  Given an array of intervals (delivery intervals), merge all overlapping intervals.

```java
class Solution {
    public int[][] overlapReduction(int[][] times) {
        // Sort times by start time
        Arrays.sort(times, (a, b) -> Integer.compare(a[0], b[0]));
        // Initialize output list and push the first time

        List<int[]> merged = new ArrayList<>();
        merged.add(times[0]);
        // Loop through times and merge if overlapping or adjacent
        for (int i = 1; i < times.length; i++) {
            // If the current time overlaps with the last time in
            // the merged list, merge them
            if (times[i][0] <= merged.get(merged.size() - 1)[1]) {
                merged.get(merged.size() - 1)[1] =
                    Math.max(
                       merged.get(merged.size() - 1)[1],
                        times[i][1]
                    );
            }
            // If the current time is non-overlapping, add it to the
            // merged list
            else {
                merged.add(times[i]);
            }
        }
        // Convert output list to 2D array and return
        return merged.toArray(new int[merged.size()][]);

    }
}
```

## Example  Verify schedule

Given an array of **meetings** consisting of the start and end times `[[s1, e1], [s2, e2], ...] (si < ei)` of meetings, write a function that returns `true` if a person could attend all meetings. Return `false` otherwise.

Two intervals `[s1, e1]` and `[s2, e2]` are considered overlapping if `e1 > s2`. If `e1 == s2`, the intervals are not considered overlapping.

```java
class Solution {
    public boolean verifySchedule(int[][] meetings) {

        // sort the meetings on their start time
        Arrays.sort(meetings, Comparator.comparingInt(a -> a[0]));

        // check if any two meetings overlap
        for (int i = 1; i < meetings.length; i++) {
            if (meetings[i][0] < meetings[i - 1][1]) {
                return false;
            }
        }
        return true;
    }
}
```

## Example  Employee free time

Given an array of **meetings** consisting of the start and end times `[[s1, e1], [s2, e2], ...] (si < ei)` of all meetings of the employees of a company, write a function to find and return the time intervals where all the employees are free, i.e., none of them are in a meeting.

Two intervals `[s1, e1]` and `[s2, e2]` are considered overlapping if `e1 >= s2`.

```java
class Solution {
    public int[][] employeeFreeTime(int[][] meetings) {
        // Sort meetings by start time
        Arrays.sort(meetings, (a, b) -> Integer.compare(a[0], b[0]));
        // Initialize output list and push the first meeting

        List<int[]> merged = new ArrayList<>();
        merged.add(meetings[0]);

        // Loop through meetings and merge if overlapping or adjacent

        for (int i = 1; i < meetings.length; i++) {
            // If the current meeting overlaps with the last meeting in

            // the merged list, merge them

            if (meetings[i][0] <= merged.get(merged.size() - 1)[1]) {

                merged.get(merged.size() - 1)[1] = Math.max(
                
                    merged.get(merged.size() - 1)[1],
                    meetings[i][1]
                );
            }

            // If the current meeting is non-overlapping, add it to the
            // merged list
            else {
                merged.add(meetings[i]);
            }
        }
        // Find gaps between merged meetings to get free time

        List<int[]> freeTimes = new ArrayList<>();

        for (int i = 1; i < merged.size(); i++) {

            int start = merged.get(i - 1)[1];

            int end = merged.get(i)[0];

            if (start < end) {

                freeTimes.add(new int[] { start, end });
            }
        }
        // Convert the list to an array and return
        return freeTimes.toArray(new int[freeTimes.size()][]);
    }
}
```

---

# Maximum  Overlap

 For many interval problems, we use the start and end coordinates of an interval as individual points on an axis and use the line sweep algorithm of these points.
 
![[Pasted image 20250920134215.png]]

## Line sweep technique

The basic idea remains the same when using the line-swept technique on points instead of intervals. We first arrange the points in some order and  "sweep" a line across the set of points while maintaining a data structure that keeps track of the current state. Let's understand how the line sweep technique can be applied to points.

### 1. Convert intervals to points

If given an array of intervals instead of points, we split each interval into two points, start and end, and create a new array of points to operate on instead of the array of intervals.

![[Pasted image 20250920134251.png]]

### 2. Sort the points

The next step is to sort the points, as the line sweep algorithm requires the events to be sorted in some order in the array holding them. This way, the array can be viewed as the x-axis of the cartesian plane with points marked on it from left to right. This allows us to traverse the array as if we were swiping a line through it on the x-axis of the cartesian plane.

Points are generally sorted in a non-decreasing order of their values and clearly labeled as a start or end point. If a start and end point has the same value, we generally keep the end point before the start point, however the order may be different for different problems.

![[Pasted image 20250920134308.png]]

### 3. Sweep the line

Once we have sorted the array of intervals, traversing it from start to end becomes the same as moving on the x-axis from left to right. We keep some data structure like an event counter, set, or list to keep state information as we traverse the array from start to end. This can be visualized as a vertical line moving from left to right on the x-axis and hence is called a line sweep. As the sweep line moves, it dynamically updates the state variables to correctly process overlaps, merges, or other conditions dictated by the problem.

##  Understanding maximum overlap pattern

> The maximum overlapping intervals pattern is a classification of problems that can be solved using the line sweep technique to find the maximum number of overlapping intervals at any point from a list of intervals.

![[Pasted image 20250920134413.png]]

## Maximum overlapping intervals

Consider we are given an array of intervals `arr` where each item in the array is a pair of an interval's start and end coordinates.

To find intersecting intervals, we must separate the start and end coordinates and store them in a single array. We create an array `points` that will store all coordinates from `arr` along with their identification as start or end. We initialize `points` by traversing `arr` and appending each interval's start and end coordinates along with a flag denoting if it is an interval start or end.

![[Pasted image 20250920135014.png]]

Finally, we sort the `points`array in ascending order of values. If a start point and end point have the same value, we keep the end point **before** the start. This is because we will not count two intervals as overlapping if one interval starts at the same time as the other ends. As we will see later, when we sweep the line from left to right, keeping the end before the start, in this case, ensures we process the closing of an interval before opening the next.

![[Pasted image 20250920135033.png]]

Now, we create a counter variable `overlap` to count the overlapping intervals at any point and initialize it with 0. We also create another variable `maxOverlap` to keep track of the maximum intersecting intervals seen so far and initialize it with 0. We then traverse the `points` array, and every time we reach a start coordinate, it means some interval starts at this point, so we increment `overlap` by one. Similarly, every time we see an end coordinate, we decrement `overlap` by one. Throughout the traversal, we compare the current value of `overlap` with the `maxOverlap` and update it if needed.

This way, at the end of the traversal, `maxOverlap` will have the maximum overlapping intervals at any point. It takes at least two intervals for an overlap, and so, if the value of `maxOverlap` is less than 2, we set it to 0 as it means all intervals were non-overlapping.

## Algorithm

- **Step 1: Create a dynamic array `points` and store start and end points intervals in the array.**
- **Step 2: Sort the `points` array in non-decreasing order. If start and end points have the same value, end points should come before start.**
- **Step 3: Initialize two variables `overlap` and `maxOverlap` to 0 that will keep track of the current overlap and maximum overlap seen so far.**
- **Step 4: Iterate in `points` and do the following**
    - **Step 4.1: If the current point is a start point, increment `overlap` and update `maxOverlap` if needed.**
    - **Step 4.2: If the current point is an end point, decrement `overlaps`.**

```java
public int maximumOverlap(int[][] intervals) {
        // Create a dynamic array to store points
        List<int[]> points = new ArrayList<>();
        for (int[] interval : intervals) {
            // Add start and end points to the points array
            points.add(new int[]{interval[0], 's'});
            points.add(new int[]{interval[1], 'e'});
        }

        // Sort the points array, end points come before
        // start points as 'e' < 's'
        Collections.sort(points, (a, b) -> {
            if (a[0] != b[0]) {
                return Integer.compare(a[0], b[0]);
            }
            return Character.compare((char) a[1], (char) b[1]);
        });

        // Initialize 'overlap' and 'maxOverlap' to 0
        int overlap = 0, maxOverlap = 0;
        for (int[] point : points) {
            if (point[1] == 's') {
                // Increment overlap if we encounter a start point
                overlap++;
                maxOverlap = Math.max(overlap, maxOverlap);
            } else {
                // Decrement overlap if we encounter an end point
                overlap--;
            }
        }
        // For an overlap we need at least 2 intervals
        return maxOverlap > 1 ? maxOverlap : 0;
    }
```

## Identifying the maximum overlap pattern

Some specific problems can be solved using the technique to find maximum overlapping intervals. These are generally **easy** or **medium** problems where we are given an array of intervals, and finding the maximum overlap partially or entirely solves the problem. If the problem statement or its solution follows the generic template below, it can be solved by applying the fixed-sized sliding window technique.

> **Template:**
 Given an array of intervals, find the maximum overlap between them

##  Example

```java
class Solution {

    public int minimumMeetingRooms(int[][] meetings) {

        // Create a dynamic list to store start and end times

        List<int[]> times = new ArrayList<>();

        // Add start and end times to the times list

        for (int[] interval : meetings) {

            times.add(new int[] { interval[0], 's' });

            times.add(new int[] { interval[1], 'e' });

        }

        // Sort the times list, end times come before start times as 'e'

        // < 's'

        Collections.sort(
            times,
            (a, b) -> (a[0] == b[0]) ? a[1] - b[1] : a[0] - b[0]
        );

        // Initialize 'rooms' and 'minRooms' to 0

        int rooms = 0, minRooms = 0;

        for (int[] point : times) {

            // Increment rooms if we encounter a start point

            if (point[1] == 's') {

                rooms++;

                minRooms = Math.max(rooms, minRooms);

            }

            // Decrement rooms if we encounter a start point
            else {
                rooms--;
            }
        }

        // For an overlap, we need at least 2 intervals

        return minRooms;
    }

}
```

## Example  Minimum meeting rooms

Given an array of **meetings** consisting of start and end times `[[s1, e1], [s2, e2], ...] (si < ei)` of meetings, write a function to find and return the minimum number of meeting rooms required so that all meetings can take place.

Two intervals `[s1, e1]` and `[s2, e2]` are considered overlapping if `e1 > s2`. If `e1 == s2`, the intervals are not considered overlapping

```java
// Define a class to store the time and type ('s' or 'e')
class TimePoint {
    int time;

    char type;

    TimePoint(int time, char type) {

        this.time = time;

        this.type = type;
    }
}

// Comparator for TimePoint

class Compare implements Comparator<TimePoint> {

    public int compare(TimePoint a, TimePoint b) {
        // Sort the times array, end times come before start times

        // as 'e' < 's'

        if (a.time == b.time) {

            return Character.compare(a.type, b.type);

        }
        return Integer.compare(a.time, b.time);

    }
}

class Solution {

    public int minimumMeetingRooms(List<List<Integer>> meetings) {
        // Create a dynamic array to store start and end times

        List<TimePoint> times = new ArrayList<>();

        for (List<Integer> interval : meetings) {
            // Add start and end times to the times array

            times.add(new TimePoint(interval.get(0), 's'));

            times.add(new TimePoint(interval.get(1), 'e'));
        }

        // Sort the times array using the custom compare function

        times.sort(new Compare());
        // Initialize 'rooms' and 'minRooms' to 0

        int rooms = 0, minRooms = 0;

        for (TimePoint point : times) {
            // Increment rooms if we encounter a start point

            if (point.type == 's') {
                rooms++;
                minRooms = Math.max(rooms, minRooms);
            }

            // Decrement rooms if we encounter an end point

            else {
                rooms--;
            }
        }
        // For an overlap we need at least 2 intervals

        return minRooms;
    }
}
```

## Example Peak resource requirement

en an array of **jobs**, consisting of start time, end time, and required resources `[[s1, e1, r1], [s2, e2, r2], ...] (si < ei)` for the jobs, write a function to find and return the busiest interval formed by overlapping jobs. 

The busiest interval is the period during which the total resources required across all overlapping jobs are maximised.

Your function should return both this interval and the corresponding maximum resources needed during that time.

Two intervals `[s1, e1]` and `[s2, e2]` are considered overlapping if `e1 > s2`. If `e1 == s2`, the intervals are not considered overlapping.

> You must abide by the following constraints:
> 
> - If multiple intervals tie for the maximum resources, return the first such interval.
> - The output should be in the form [`intervalStart`, `intervalEnd`, `maxResources`].
> - If there are no overlapping intervals, return [`-1`, -`1`, `0`].

```java
// Define a struct to store the time, type ('s' or 'e') and resources
class TimePoint {

    int time;

    char type;

    int resources;

    TimePoint(int time, char type, int resources) {

        this.time = time;

        this.type = type;

        this.resources = resources;

    }
}

// Comparator for TimePoint

class Compare implements Comparator<TimePoint> {

    public int compare(TimePoint a, TimePoint b) {

        // Sort the times array, end times come before start times

        // as 'e' < 's'

        if (a.time == b.time) {
            return Character.compare(a.type, b.type);
        }

        return Integer.compare(a.time, b.time);

    }
}

class Solution {

    public int[] peakResourceRequirement(List<List<Integer>> jobs) {

        // Create a dynamic array to store start and end times

        List<TimePoint> times = new ArrayList<>();

        for (List<Integer> job : jobs) {
            // Add start and end times to the times array

            times.add(new TimePoint(job.get(0), 's', job.get(2)));

            times.add(new TimePoint(job.get(1), 'e', job.get(2)));
        }

        // Sort the times array using the custom compare function

        times.sort(new Compare());

        // Currently required resources

        int currentResources = 0;

        // Maximum resources required at any time

        int maxResources = 0;

        // Start of the interval with maximum resources

        int intervalStart = -1;

        // End of the interval with maximum resources

        int intervalEnd = -1;

        for (TimePoint point : times) {

            if (point.type == 's') {

                // Add the resources of the current job

                currentResources += point.resources;

                // If the current resources exceed the maximum resources

                // update the maximum resources and start of the interval

                // with maximum resources

                if (currentResources > maxResources) {

                    maxResources = currentResources;

                    intervalStart = point.time;

                    // Reset the end of the interval with maximum

                    // resources

                    intervalEnd = -1;

                }
            }

            // 'e' - end of interval
            else {

                // If we are at the end of an interval with maximum

                // overlap and the current overlap is equal to the

                // maximum resources then update the end of the interval

                // with maximum resources

                if (
                    currentResources == maxResources && intervalEnd == -1

                ) {
                    intervalEnd = point.time;
                }
                // Decrement the current resources count

                currentResources -= point.resources;
            }
        }

        // If maxResources <= 1, return {-1, -1} indicating no overlap

        if (maxResources <= 1) {
            return new int[] { -1, -1, 0 };
        }

        return new int[] { intervalStart, intervalEnd, maxResources };

    }

}
```

