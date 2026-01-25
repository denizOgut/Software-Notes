
# Binary Search

 Searching is the process of locating a specific item within a collection. It could be finding a contact in your phone, locating a book on a shelf, or identifying a file on your computer. In every case, you begin with a target, something you want to find, and you examine the available data to locate it.

## Limitations of linear search

With linear search, as the number of items grows, the time required grows equally. The search is guaranteed to succeed, but may take far too long when the data becomes large. Linear search does not use any helpful structure or shortcuts, making it slow and inefficient at large scale.

![[Pasted image 20260101155455.png]]

## Binary search

Binary search is one of computer science's most widely used search algorithms and is used to find the position of a target value in a sorted array by leveraging the array's sorted order. Instead of a linear search, it uses an intelligent strategy by partitioning the search space into two halves and discarding the half where the target cannot be present. 

Looking at the problem of finding a student who scored `85` marks in a sorted list of results containing thousands of students. Instead of checking each student's score individually, you begin by examining the score of the student at the middle of the list.

![[Pasted image 20260101155620.png]]

If the **middle** score is **less than** `85`, the target **must be in the second half**, so you discard everything in the first half, including the middle score.

![[Pasted image 20260101155642.png]]

Similarly, if the **middle** student scored **more than** `85`, then the student you’re looking for **must be in the first half**, so you can discard the entire second half.

![[Pasted image 20260101155658.png]]

You repeat this process, halving the remaining list each time, until the score `85` appears as the midpoint of the narrowed range.

![[Pasted image 20260101155729.png]]

- **Step 1**: Start with the full list of student scores included in the search.
- **Step 2**: Check the score at the midpoint of the list.
    - **Step 2.1**: If the middle score is `85`, you’ve found the student, stop the search.
    - **Step 2.2**: If the middle score is less than `85`, for example, `78`, eliminate the middle position and all scores below it, then repeat Step 2 with the second half.
    - **Step 2.3**: If the middle score is greater than `85`, for example, `92`, eliminate the middle position and all scores above it, then repeat Step 2 with the first half.
- **Step 3**: If the search space reduces to zero and `85` is never found, no student on the list has that score.

## Advantages

- **Efficiency:** Binary search has a time complexity of **O(logN)**, which makes it significantly faster than linear search for large arrays.
- **Versatility:** Binary search can be used to find a target value in a sorted array and to find approximations, closest elements, peaks and valleys, intersection points of curves, and more.
- **Simplicity:** Binary search is a relatively simple algorithm to implement, making it accessible to programmers of all skill levels.

## Limitations

- **Requires sorted array:** Binary search's biggest limitation is that it only works on sorted arrays. If the array is not sorted, the algorithm will not work.
- **Limited to arrays:** Binary search is limited to searching arrays. It cannot be used to search linked lists or other data structures.

## Algorithm

### 1. arr[mid] == target

The search is complete if the middle element equals the target, because this means you have narrowed the list down to the exact position where the value appears.

![[Pasted image 20260101155943.png]]

### 2. arr[mid] < target

If the middle element is smaller than the target, the algorithm eliminates the first half of the array, including the middle element and continues the search in the second half.

![[Pasted image 20260101155956.png]]

### 3. arr[mid] > target

If the middle element is larger than the target, the algorithm eliminates the second half of the array, including the middle element and continues the search in the first half.

![[Pasted image 20260101160009.png]]

**Algorithm**

- **Step 1:** Set two indices, `low` and `high`, to the first and last indices of the array, respectively.
- **Step 2:** While `low` is less than or equal to `high`, do the following:
    - **Step 2.1:** Calculate the middle index as `mid = (low + high) / 2`.
    - **Step 2.2:** If the middle element **equals** the `target` value, return the middle index.
    - **Step 2.3:** If the middle element is **less than** the `target` value, set `low` to `mid + 1`.
    - **Step 2.4:** If the middle element **exceeds** the `target` value, set `high` to `mid - 1`.
- **Step 3:** If the loop exits without finding the target value, return `-1` to indicate that the `target` value is not in the array.

## Implementation

```java
class Solution {
    public int binarySearch(int[] arr,int target){

        // Starting index of the search range
        int low=0;

        // Ending index of the search range
        int high=arr.length-1;

        while(low<=high){

            // Calculate the middle index
            int mid=(low+high)/2;

            // Found the target, return the index
            if(arr[mid]==target){
                return mid;
            }

            // If the target is greater than the element at mid
            // Adjust the search range to the right half
            else if(arr[mid]<target){
                low=mid+1;
            }

            // Else if the target is smaller than the element at mid
            // Adjust the search range to the left half
            else{
                high=mid-1;
            }
        }

        // Target not found in the array
        return -1;
    }
}

```

# Lower Bound

 there are situations where simply finding a target value is not enough. Sometimes, we need to locate a specific position, for example, the first occurrence of a value in a sorted list, which binary search alone does not directly provide. To see why this can be a problem, let’s look at an example.

Imagine you are a school teacher with a sorted list of thousands of students. Several students scored `85` marks, and you want to identify the student who appears **first in the list** with that score.

Using a standard binary search, you can quickly locate a student with `85` marks, but there is no guarantee it will be the first. Binary search stops when it finds the target value. You could land somewhere in the middle of all the `85s`, missing the student at the beginning of that range.

The lower-bound algorithm is a popular variant of binary search. **==It aims to find the index of the first element in a sorted array greater than or equal to the target.==**

> - If multiple values equal the target, it returns the index of the first occurrence
> - If the target is not present, it returns the index of the smallest element greater than the target
> - If no such element exists, it returns the size of the array.

You begin by examining the middle score in the list.

If the middle score is **less than** `85`, the first `85` must be in the second half, so you discard the first half, including the middle score.

If the middle score is **greater than or equal** to `85`, this position could be the first occurrence, but there may still be an earlier `85` in the list. To ensure we find the earliest position, we continue searching in the first half, keeping the middle position included in the search space, since it could be the first occurrence.

This process is repeated, halving the remaining search range each time, until the search space cannot be divided further. At that point, the left boundary of the search range points to the first occurrence of `85` in the list.

By systematically narrowing the search while considering the possibility of earlier occurrences, this method finds the first `85` efficiently, even in a list of thousands of scores. It combines the speed of binary search with the precision needed to locate the lower bound of the target value.

> - **Step 1**: Start with the full list of student scores included in the search.
> - **Step 2**: Check the score at the midpoint of the list.
>     - **Step 2.1**: If the middle score is less than `85`, for example, `78`, eliminate the middle position and all scores below it, then repeat Step 2 with the second half.
>     - **Step 2.2**: If the middle score is greater than or equal to `85`, for example, `85` or `92`, keep the middle position in the search space and continue searching in the first half, since the first occurrence could be earlier in the list.
> - **Step 3**: Repeat Step 2 until the search space cannot be divided further. The left boundary at this point points to the first element greater than or equal to `85`, which is the lower bound.

## Advantages

The lower bound algorithm builds on binary search to efficiently locate the first occurrence of a target value in a sorted array. Its advantages include:

> - **Efficiency:** By halving the search space at each step, lower bound finds the first occurrence in O(log N) time, making it far faster than linear search for large datasets.
> - **Precision:** Unlike standard binary search, lower bound guarantees the earliest position of the target, which is useful when multiple elements have the same value.
> - **Versatility:** Lower bound can be used to identify insertion points, ranges of repeated elements, or boundaries in sorted arrays.

## Limitations

While powerful, the lower bound algorithm has some constraints:

> - **Requires sorted array:** Lower bound only works correctly on arrays that are sorted in ascending order.
> - **Limited to arrays:** It is designed for random-access structures like arrays and cannot be directly applied to linked lists or other non-contiguous data structures.
> - **Single purpose:** Lower bound specifically finds the first occurrence or insertion point, so it does not directly identify the last occurrence or elements strictly greater than the target (for that, upper bound is needed).

## Algorithm

The lower-bound algorithm compares the target value with the middle element of the input array and takes one of two actions based on the result.

### 1. arr[mid] < target

If the middle element is less than the target, the algorithm reduces the search space by eliminating the first half of the array, including the middle element, and continues the search in the second half. This ensures that all elements smaller than the target are skipped efficiently.

![[Pasted image 20260101164715.png]]

### 2. arr[mid] >= target

If the middle element is greater than or equal to the target, the algorithm narrows the search space by eliminating the second half of the array while keeping the middle element, since it could be the first occurrence of the target. This approach ensures that no potential candidate for the lower bound is skipped.

![[Pasted image 20260101164737.png]]

### Possible results of lower bound

The lower bound search returns the first position in a sorted array where the target could be inserted without violating the order. Depending on the array and the target, there are three main types of outcomes:

#### 1. First occurrence of target

If the target is present in the array, the lower bound points to the first occurrence of that element. This ensures that even if multiple elements in the array have the same value, the algorithm identifies the earliest position where the target appears

#### 2. First element larger than target

If the target is not present in the array but is smaller than some of the existing elements, the lower bound will point to the first element that is greater than the target. This provides the position where the target could be inserted while maintaining the array’s sorted order.

#### 3. End of the array

If the target is larger than all existing elements in the array, the lower bound will point to the end of the array, which corresponds to an index equal to the array’s size. This indicates that the target would be inserted at the very end to maintain the sorted order.

**Algorithm**

- **Step 1:** Set two indices, `low` and `high`, to the first index and the size of the array, respectively.
- **Step 2:** While `low` is less than `high`, do the following:
    - **Step 2.1:** Calculate the middle index as `mid = low + (high - low) / 2`.
    - **Step 2.2:** If the middle element is **less than** the `target` value, set `low` to `mid + 1`.
    - **Step 2.3:** If the middle element is **greater than or equal** to the `target` value, set `high` to `mid`.
- **Step 3:** At the end of the loop, the `low` index would either be the index of the first occurrence of the target, the index of the smallest element greater than the `target`, or the end of the list.

## Implementation

```java
class Solution{
    public int lowerBound(int[] arr,int target){

        // Initialise starting index to 0
        int low=0;

        // Initialise ending index to arr.length instead of arr.length-1
        int high=arr.length;

        // Find first index where element >= target
        while(low<high){

            // Find the middle index
            int mid=low+(high-low)/2;

            // Search right subarray
            if(arr[mid]<target){
                low=mid+1;
            }

            // Search left subarray including mid
            else{
                high=mid;
            }
        }

        // Return the lower bound index
        return low;
    }
}

```

# Upper Bound

there are situations where locating the first occurrence of a value is not enough. Sometimes we need to find the last occurrence of a value in a sorted list, which neither standard binary search nor lower-bound directly provides.

## Limitations of lower bound

Lower bound is good at finding the first occurrence of the target, which is useful when multiple students have the same score. However, lower bound does not provide the position of the first element strictly greater than the target. In other words, it only guarantees the start of the target’s range, leaving the upper boundary unknown.

## Upper bound

Similar to the lower-bound algorithm, the upper-bound algorithm is another popular variation of binary search. It aims to find the index of the first element in a sorted array that is **strictly greater** than the **target**. 

> - If no value greater than the target is present, it returns the size of the array

If the middle score is **less than or equal** to `85`, the first score strictly greater than `85` must be in the second half, so you discard the first half, including the middle score.

If the middle score is **greater** than `85`, this position could be the first element strictly greater than `85`, but there may still be an earlier one in the list. To ensure we find the earliest such score, we continue searching in the first half, keeping the middle position included in the search space, since it could be the correct upper bound.

This process is repeated, halving the remaining search range each time, until the search space cannot be divided further. At that point, the left boundary of the search range points to the first element strictly greater than `85` in the list.

By systematically narrowing the search while accounting for the possibility that earlier elements exceed the target, this method efficiently identifies the first score strictly greater than `85`, even in a list of thousands of scores. It combines the speed of binary search with the precision needed to locate the upper bound of the target value.

> - **Step 1:** Start with the full list of student scores included in the search.
> - **Step 2:** Check the score at the midpoint of the current search range.
>     - **Step 2.1:** If the middle score is less than or equal to `85`, for example, `78` or `85`, eliminate the middle position and all scores below it, then continue searching in the second half, since the first element strictly greater than 85 must be higher up.
>     - **Step 2.2:** If the middle score is greater than `85`, for example, `92`, keep the middle position in the search space and continue searching in the first half, because this could be the first element strictly greater than `85`.
> - **Step 3:** Repeat Step 2 until the search space cannot be divided further. The left boundary at this point points to the first element strictly greater than `85`, which is the upper bound.

## Advantages

The upper bound extends binary search to efficiently find the first element in a sorted array that is strictly greater than a target. Its main advantages include:

> - **Efficiency:** By halving the search space at each step, upper bound can locate the first element greater than the target in **O(log N)** time, which is much faster than linear search for large datasets.
> - **Precision:** Unlike standard binary search, upper bound guarantees the earliest position of an element greater than the target, which is useful when multiple elements exceed the target.
> - **Versatility:** Upper bound can identify insertion points, boundaries of ranges, or the next higher value in sorted arrays, making it useful in ranking, grade thresholds, or interval computations.

## Limitations

While powerful, the upper bound algorithm has some constraints:

> - **Requires sorted array:** Upper bound only works correctly on arrays sorted in ascending order.
> - **Limited to arrays:** It is designed for random-access structures like arrays and cannot be directly applied to linked lists or other non-contiguous data structures.
> - **Single purpose:** Upper bound specifically finds the first element strictly greater than the target, so it does not directly find the first occurrence of the target itself (for that, lower bound is needed).

## Algorithm

The upper-bound algorithm is used to find the first position in a sorted array where a given target value can be exceeded. In other words, it returns the index of the first element that is strictly greater than the target value. This is useful for insertion, range queries, and counting elements greater than a value. The algorithm begins by initializing two indices that define the current search range in which the upper-bound may exist.

> - `low` is set to the first index of the array i.e `0`.
> - `high` is set to the last index of the array i.e `arr.size()` (one position past the last valid index).

These indices define a **half-open** search range `[low, high)`, where `low` is inclusive and `high` is exclusive.

**Why is `high` initialized to the array size?**

Using `high = arr.size()` allows the algorithm to handle cases where the target value is greater than all elements in the array. In such cases, the upper bound is the end of the array, which represents the position immediately after the last occurrence of the target and is a valid insertion point to maintain the sorted order.

The algorithm enters a loop that continues as long as `low < high`. This condition ensures that there is still at least one possible position where the lower bound could exist.

**Why** **do we continue while `low < high` and not** `low <= high` **?**

In upper bound, we also use `low < high` because the search range is treated as a **half-open** interval `[low, high)`. The loop continues narrowing the range until `low == high`, which gives the correct position immediately after the last occurrence of the target. Using `low <= high` could overrun the array since high is initially set to `arr.size()`. Unlike standard binary search, upper bound does not need to examine every element, only the position where the target could be inserted to maintain the sorted order.

Inside the loop, the middle index is calculated as:

> - `mid = low + (high - low ) / 2`

**Why is the middle index calculated as** `mid = low + (high - low) / 2` **instead of** mid = (low + high) / 2 ?

When calculating the middle of a range, `mid = low + (high - low) / 2` is preferred over `mid = (low + high) / 2` because directly adding `low` and `high` can overflow the integer range when they are large, while computing the difference first keeps the value safe and then adds it back to low without overflow

Based on the value of `arr[mid]`, the algorithm makes one of three possible decisions.

### 1. arr[mid] <= target

If the middle element is **less than or equal** to the target, all elements up to and including `mid` are less than or equal to the target and can be skipped. The algorithm therefore narrows the search to the right half of the array by updating `low = mid + 1`, efficiently eliminating positions that cannot be the upper bound.

### 2. arr[mid] > target

If the middle element is **greater** than the target, `mid` could be a valid upper bound, but there may be an earlier position that also satisfies this condition. To ensure no potential candidate is skipped, the algorithm narrows the search to the left half by updating `high = mid`, keeping mid in the search range.

The algorithm repeatedly narrows the search space until it identifies the upper bound. The loop terminates when `low == high`, at which point the search range has been reduced to a single position, representing the upper bound. 

### Possible results of upper bound

The upper-bound search returns the index of the first element in a sorted array that is strictly greater than the target. Depending on the array and the target, there are two main types of outcomes:

#### 1. First greater element

If an element strictly greater than the target exists in the array, the upper bound points to the first occurrence of that element. This ensures that even if multiple elements are greater than the target, the algorithm identifies the earliest position where a value exceeds the target.

#### 2. End of the array

If the target is larger than all existing elements in the array, the upper bound will point to the end of the array, which corresponds to an index equal to the array’s size. This indicates that there is no element strictly greater than the target, and the target would effectively be positioned at the very end if inserted while maintaining the sorted order.

**Algorithm**

- **Step 1:** Initialize search boundaries, set `low = 0`, `high = arr.size() `
- **Step 2:** Iterate while `low < high`
    - **Step 2.1:** Calculate middle index `mid = low + (high - low) / 2`
    - **Step 2.2:** If `arr[mid] <= target`:
        - **Step 2.2.1:** Set `low = mid + 1`
    - **Step 2.3:** Else:
        - **Step 2.3.1:** Set `high = mid`
- **Step 3:** Return `low`

## Implementation

```java
class Solution{
    public int upperBound(int[] arr,int target){

        // Initialise starting index to 0
        int low=0;

        // Initialise ending index to arr.length
        int high=arr.length;

        // Find first index where element > target
        while(low<high){

            // Find the middle index
            int mid=low+(high-low)/2;

            // Search right subarray
            if(arr[mid]<=target){
                low=mid+1;
            }

            // Search left subarray including mid
            else{
                high=mid;
            }
        }

        // Return the upper bound index
        return low;
    }
}
```

#  2D Binary Search

Imagine a school teacher who maintains a sorted table of student marks, where:

> - Each row is sorted in ascending order
> - The first element of each row is greater than the last element of the previous row.

![[Pasted image 20260103225921.png]]

Now, suppose you want to quickly find out whether a specific score, say `85`, exists anywhere in this table. A simple approach is to scan the grid row by row, examining each element sequentially until the target is found. This method follows a natural, left-to-right, top-to-bottom pattern, making it easy to understand and implement.

This works for small datasets, but it quickly becomes impractical when the table contains thousands, or even millions of cells.

As the dataset grows, manually checking each cell becomes time-consuming, underscoring the need for a more efficient strategy.

## Limitations of binary search

You could also attempt binary search on each row individually, but that would still require checking every row unless you get lucky. You lose the true power of binary search, which is the ability to discard large portions of the search space.

![[Pasted image 20260103230017.png]]

**==Each row is sorted from left to right, and every row starts with a score that is greater than the last score of the previous row. This means the entire table behaves like a single, continuous, increasing sequence, just laid out in two dimensions.==**

2D binary search is an extension of the classic binary search algorithm for two-dimensional grids. Similar to standard binary search, it leverages the sorted order to efficiently locate a target value. Instead of examining each cell individually, 2D binary search repeatedly partitions the search space, eliminating regions where the target cannot possibly exist. By doing so, it reduces the number of comparisons dramatically, just like binary search halves the search space in a one-dimensional space.

If the **middle** score is **less** than `85`, the target **must be located after this point** in the table, so you discard all cells above and to the left of the middle element, as none of them can contain the target.

Similarly, if the **middle** score is **greater** than `85`, the target must be located **before this point** in the table, so you can discard all cells below and to the right of the middle element, as none of them can contain the target.

You repeat this process, halving the remaining region of the table at each step, until the score `85` is found at the midpoint of the narrowed section.

By leveraging the sorted structure of the rows and columns, this method eliminates large sections of the table at every step, requiring far fewer comparisons and making the search significantly faster than checking each cell individually.

> - **Step 1**: Start with the full 2D table of student scores included in the search.
> - **Step 2**: Check the score at the midpoint of the current region of the table (middle row, middle column).
>     - **Step 2.1**: If the middle score is `85`, you’ve found the student, stop the search.
>     - **Step 2.2**: If the middle score is less than `85`, for example, `78`, eliminate all cells above and to the left of the middle element, then repeat Step 2 with the remaining lower-right region.
>     - **Step 2.3**: If the middle score is greater than `85`, for example, `92`, eliminate all cells below and to the right of the middle element, then repeat Step 2 with the remaining upper-left region.
> - **Step 3**: If the search space reduces to zero and `85` is never found, no student in the table has that score.

## Advantages

2D binary search is highly efficient for finding items in large, sorted grids. By systematically eliminating large sections of the table at each step, it drastically reduces the number of comparisons compared to scanning each cell individually. The key advantages of 2D binary search are outlined below:

> - **Efficiency:** 2D binary search reduces the search space exponentially at each step, making it far faster than linear scanning of all rows and columns, especially for large grids.
> - **Leverages structure:** The algorithm takes advantage of the sorted rows and columns to make safe eliminations of entire regions of the grid.
> - **Predictable performance:** Like binary search, its time complexity is **O(log(M) + log(N))** for an **M x N** grid when applied optimally, giving consistent and scalable performance.

## Limitations

Despite its efficiency, 2D binary search has certain constraints. It relies heavily on the table's sorted structure and cannot be applied to grids that do not meet these ordering conditions. The main limitations are summarized below:

> - **Requires a sorted grid:** The algorithm only works if each row and column is sorted and the relative ordering of rows is preserved. Unsorted or partially sorted grids break the logic.
> - **Complex implementation:** Compared to linear scanning, 2D binary search involves more sophisticated calculations to map indices and manage regions, making it slightly harder to implement.
> - **Limited flexibility:** Changes to the dataset (e.g., inserting or removing rows/columns) may require recomputing the search logic or re-sorting the grid.

## Algorithm

 To explain this algorithm, we will use a 2D matrix sorted in ascending order both row-wise and column-wise, and search for a target value. For the algorithm to work, the input array should meet the two conditions below.

> - The 2D matrix should be **sorted in rows and columns**, meaning each row and each column is sorted in ascending order.
> - The last number in each row should be **less than or equal to** the first number in the next row.

For such input, we can tweak the existing binary search algorithm to search the 2D matrix rather than using the poorly performing linear search.

![[Pasted image 20260103230631.png]]

### Flatten the 2D matrix

We already know how to execute a binary search in a sorted array. If we flatten this 2D matrix into a 1D sorted array, we can use binary search to find the target. There are two ways to do it

#### 1. Create a new 1D array

Creating a new 1D array and copying values from the 2D matrix presents two issues. First, allocating an additional **O(N*M)** memory for the new array is required. Second, iterating over the 2D matrix to copy all values adds an **O(N*M)** time complexity to the algorithm. Even if the binary search algorithm is applied to the new 1D array, the time complexity will always be **O(N*M)** due to the sequential copy operation. This contradicts the idea that binary search is expected to maintain a logarithmic time complexity in all cases.

![[Pasted image 20260103230740.png]]

#### 2. Use a virtual 1D array

A better way to flatten the 2D matrix is to create a virtual 1D array within it, where each index of this virtual array maps to one cell in the 2D matrix.

![[Pasted image 20260103230756.png]]

If we have a 2D matrix with **N** rows and **M** columns. This would give us a total of **(N*M)** cells. Our virtual 1D array would also be the same size to accommodate all these cells. For a given cell `[row, col]` in the 2D matrix, the corresponding index `i` in the virtual array could be calculated using the following function

> - `i = row * N + col`

![[Pasted image 20260103230810.png]]

Similarly, for a given index `i` in the virtual array, the corresponding row and column numbers in the 2D matrix could be calculated using the following function

> - `row = i / M`
> - `col = i % M`

![[Pasted image 20260103230826.png]]

The 2D Binary Search algorithm searches for a target value in a sorted 2D matrix with **N** rows and **M** columns, where each row and column is sorted in ascending order. The algorithm treats the matrix as a flattened 1D array of size **N×M** to apply standard binary search efficiently. The algorithm begins by initializing two indices that define the current search range in which the target value may exist.

> - `low` is set to the first index of the virtual array i.e `0`.
> - `high` is set to the last index of the virtual array i.e `(N * M) - 1`.

The algorithm enters a loop that continues as long as `low <= high`. This condition ensures that there are still elements remaining in the search range that could potentially match the target value.

**Why do we continue while `low <= high`?**

In a 2D binary search mapped to a virtual 1D array, we continue while `low <= high` to ensure that all possible positions in the matrix are examined. When low becomes greater than high, it means the search range is empty and every element has been considered. At this point, the target cannot be present in the matrix.

Inside the loop, the algorithm calculates the middle index using:

> - `mid = low + (high - low ) / 2`

The middle index is mapped to 2D indices using the number of columns **M**:

> - `row = mid / M`
> - `col = mid % M`

Once the `row` and `col` indices are determined, the algorithm applies the standard binary search procedure by comparing the target value with `matrix[row][col]`, the middle element of the current search range. Based on this comparison, it then makes one of three possible decisions to continue the search.

### 1. matrix[row][col] == target

The search is complete when the middle element is **equal** to the target value, indicating that the matrix has been narrowed down to the exact position of the element. In this case, `true` is returned, indicating the target is found.

### 2. matrix[row][col] < target

If the value at the middle index is **less** than the target, the target cannot be in the left portion of the matrix or at the middle position (i.e the first half of the virtual array). As a result, the algorithm discards this section and continues the search in the right half by updating `low = mid + 1`.

### 3. matrix[row][col] > target

If the value at the middle index is **greater** than the target, the target cannot be in the right portion of the matrix or at the middle position (i.e the first half of the virtual array). The algorithm therefore discards this section and continues the search in the left half by updating `high = mid - 1`.

The algorithm repeatedly compares the target with the element at `matrix[row][col]` (mapped from the virtual 1D array) and narrows the search space accordingly. If the loop terminates without finding the target, it indicates that the element does not exist in the matrix, and the algorithm returns `false` to signal an unsuccessful search.

**Algorithm**

- **Step 1:** Initialize matrix dimensions, set `rows = matrix.size()`, `cols = matrix[0].size() `
- **Step 2:** Initialize search boundaries, set `low = 0`, `high = rows * cols - 1 `
- **Step 3:** Iterate while `low <= high`
    - **Step 3.1:** Calculate middle index `mid = low + (high - low) / 2`
    - **Step 3.2:** Map middle index to 2D coordinates, set `row = mid / cols`, `col = mid % cols`
    - **Step 3.3:** If `matrix[row][col] == target`:
        - **Step 3.3.1:** Return `true`
    - **Step 3.4:** Else If `matrix[row][col] < target`:
        - **Step 3.4.1:** Set `low = mid + 1`
    - **Step 3.5:** Else if `matrix[row][col] > target`:
        - **Step 3.5.1:** Set `high = mid - 1`
- **Step 4:** If the loop ends without returning, the target is not in the matrix, return `false`

## Implementation

```java
class Solution{
    public boolean binarySearch2D(int[][] matrix,int target){

        int rows=matrix.length;
        int cols=matrix[0].length;

        int low=0;
        int high=rows*cols-1;

        while(low<=high){

            int mid=low+(high-low)/2;

            int row=mid/cols;
            int col=mid%cols;

            if(matrix[row][col]==target){
                return true;
            }
            else if(matrix[row][col]<target){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }

        return false;
    }
}

```

#  Staircase Search

2D binary search is probably the best algorithm for searching a sorted matrix. However, it only works when the conditions mentioned below are fulfilled for the input.

> **==- Each row is sorted in ascending order==**
> **==- The first element of each row is greater than the last element of the previous row.**==

However, in practice, data is often only partially sorted.

Imagine a teacher maintaining a table of student scores in which each row and each column is sorted in ascending order, but **the last score in one row** may be **greater than** the **first score in the next row**.

In other words, the second condition required for applying 2D binary search is not satisfied, making the standard algorithm inapplicable.

![[Pasted image 20260104125647.png]]

Now, suppose you want to find out whether a score of `85` exists. A standard 2D binary search relies on a strict global ordering across rows and columns, so it cannot be applied here. The algorithm would assume that all elements after a certain midpoint are larger, which is clearly not true for this table.

![[Pasted image 20260104125701.png]]

In this scenario, the natural approach is still a sequential scan, moving row by row and column by column. While simple, this method is inefficient for large tables. The challenge is understanding the constraints imposed by partial sorting: the data is somewhat structured, but not enough for traditional 2D binary search.

This works for small datasets, but it quickly becomes impractical when the table contains thousands, or even millions of cells.

As the dataset grows, manually checking each cell becomes time-consuming, underscoring the need for a more efficient strategy.

## Limitations of 2D binary search

Since the conditions for 2D binary search are not met, the algorithm cannot be applied to such datasets, even if the table is partially sorted.

You could also attempt binary search on each row individually, but that would still require checking every row unless you get lucky. You lose the true power of binary search, which is the ability to discard large portions of the search space.

The key to improving performance lies in leveraging the table’s partial sorting. It only needs to 

> - The table should be sorted in rows and columns, meaning each row and each column is sorted in ascending order.

## Staircase search

Staircase search is an efficient technique for searching partially sorted two-dimensional grids, where each row and each column is sorted in ascending order. Still, the matrix does not meet the stricter conditions required for 2D binary search. Instead of relying on global ordering, staircase search leverages local ordering within rows and columns to systematically narrow the search region.

Looking at the problem of finding a student who scored `85` marks in a large table sorted by rows and columns, you might start at the top-right corner.

![[Pasted image 20260104130118.png]]

If the **current score** is **less** than `85`, the target **must be in a region with larger values**, so you move in the direction of increasing scores. From the top-right corner, this means moving downward, which eliminates the entire row above. Every value in that row is smaller than the target and therefore cannot contain it.

![[Pasted image 20260104130238.png]]

Similarly, if the **current score** is **greater** than `85`, the target **must be in a region with smaller values**, so you move toward decreasing scores. From the top-right corner, this means moving left, which eliminates the entire column to the right. Every value in that column is larger than the target and can safely be discarded.

![[Pasted image 20260104130251.png]]

By repeating this process, stepping down or left depending on the comparison, you progressively **“walk”** through the matrix in a staircase-shaped path, discarding one row or one column at every step until the score `85` is found, or the search space is exhausted.

![[Pasted image 20260104130306.png]]

> - **Step 1:** Start at the top-right corner of the 2D table of student scores.
> - **Step 2:** Compare the current cell’s score with `85`.
>     - **Step 2.1** If the current score is exactly `85`, you’ve found the student, stop the search.
>     - **Step 2.2:** If the current score is less than `85`, for example `78`, move down one row because all scores to the left are smaller and cannot contain `85`.
>     - **Step 2.3:** If the current score is greater than `85`, for example `92`, move left one column because all scores below are larger and cannot contain `85`.
> - **Step 3:** Repeat the comparisons as you move down or left. If you step outside the boundaries of the table without finding `85`, then no student in the table has that score.

## Advantages

Staircase search is a highly effective technique for finding a target value in a 2D grid where each row and each column is sorted in ascending order. By intelligently navigating from the top-right corner, the algorithm eliminates an entire row or column with every comparison. The key advantages of staircase search are outlined below:

> - **Efficiency:** Staircase search runs in **O(M + N)** time for an **M × N** grid, making it significantly faster than scanning all cells. Each step moves either left or down, ensuring steady progress toward the answer.
> - **Simple logic:** Compared to 2D binary search, staircase search is easier to visualize and implement. You only move in two directions: down or left, based on a simple comparison.
> - **Uses grid properties directly:** The algorithm leverages the sorted rows and columns without requiring index conversion or virtual flattening, making it intuitive and practical.
> - **No extra space:** Staircase search operates directly on the grid and requires no additional data structures or preprocessing.

## Limitations

While staircase search is efficient and easy to apply, it also has limitations. Its performance and correctness depend entirely on the grid structure, and it cannot adapt to unsorted or inconsistently sorted data. The primary limitations are:

> - **Requires row-wise and column-wise sorting:** The algorithm only works if both rows and columns are sorted. If either condition is violated, left/down elimination becomes unsafe, and the search may fail.
> - **Not optimal for large grids:** For large **N × N** matrices, the worst-case time is **O(2N)**, which is slower than 2D binary search’s logarithmic behavior. This makes staircase search less suitable for extremely large, fully dense grids.
> - **Directional constraints:** The algorithm always moves left or down. If the grid is sorted differently (e.g., descending, or only row-sorted), staircase search cannot be applied without modification.


## Algorithm

The Staircase Search algorithm searches for a target value in a 2D matrix with **N** rows and **M** columns where each row and each column is sorted in ascending order. It exploits the sorted property of the matrix by starting at the **top-right corner** and moving only in directions that eliminate impossible positions, achieving efficient linear-time search. The algorithm begins by initializing two indices that define the current search range in which the target value may exist.

> - `row = 0` - (first row)
> - `col = M - 1` - (last column)

The algorithm enters a loop that continues as long as `row < N` and `col >= 0`. This condition guarantees that there are still elements in the search range that could potentially match the target value. At each step, the algorithm compares the target value with `matrix[row][col]`, the current element in the search. It then makes one of three possible decisions to continue the search.

### 1. matrix[row][col] == target

The search is complete when the current element is **equal** to the target value. In this case, the algorithm returns `true`, indicating that the target has been found in the matrix.

### 2. matrix[row][col] < target

If the current cell’s value is **less** than the target, the algorithm moves **down one row** by performing `row = row + 1`. This operation effectively eliminates the entire current row from consideration, since each row is sorted in ascending order and all elements to the left of the current cell are guaranteed to be smaller than the target.

### 3. matrix[row][col] > target

If the current cell’s value is **greater** than the target, the algorithm moves **left one column** by performing `col = col - 1`. This operation effectively eliminates the entire current column from consideration, since each column is sorted in ascending order and all elements below the current cell are guaranteed to be larger than the target.

The algorithm continues moving **down** or **left** at each step, comparing the current cell’s value with the target. The loop terminates when the target is found or when the indices go out of bounds `(row >= N or col < 0)`. If the search ends without finding the target, the algorithm returns `false`, indicating that the element does not exist in the matrix.

- **Step 1:** Initialize matrix dimensions, set `rows = matrix.size()`, `cols = matrix[0].size() `
- **Step 2:** Initialize starting positions, set `row = 0`, `col = cols - 1 `
- **Step 3:** Iterate while `row < rows && col >= 0`
    - **Step 3.1:** If `matrix[row][col] == target`:
        - **Step 3.1.1:** Return `true`
    - **Step 3.2:** Else If `matrix[row][col] < target`:
        - **Step 3.2.1:** Set `row = row + 1`
    - **Step 3.3:** Else if `matrix[row][col] > target`:
        - **Step 3.3.1:** Set `col = col - 1`
- **Step 4:** If the loop ends without returning, the target is not in the matrix, return `false`

## Implementation

```go
class Solution{
    public boolean sortedMatrixSearch(int[][] matrix,int target){

        // Get the number of rows in the matrix
        int rows=matrix.length;

        // Get the number of columns in the matrix
        int cols=matrix[0].length;

        // Start from the first row
        int row=0;

        // Start from the last column
        int col=cols-1;

        while(row<rows&&col>=0){

            // Continue until we reach the bottom-left or top-right
            // corner of the matrix

            // If the current element is equal to the target, return
            // true
            if(matrix[row][col]==target){
                return true;
            }

            // Else if the current element is less than the target, move
            // to the next row
            else if(matrix[row][col]<target){
                row++;
            }

            // Else if the current element is greater than the target,
            // move to the previous column
            else{
                col--;
            }
        }

        // Return false if the target is not found
        return false;
    }
}

```

# Sorted Rotated Array

Binary search exponentially speeds up the search for values in a sequence by exploiting the order of items in it. There are many problems that may not be solvable by direct application of binary search, but by algorithms that use the same principle to reduce the size of the problem space by half in each iteration. One such problem is to find the minimum in a sorted rotated array.

A sorted rotated array is one where a sorted array is rotated in either direction by a certain number of times. The minimum item in a sorted rotated array is called the pivot item. Finding the minimum (pivot) item in a sorted rotated array is a classical problem that can be solved by exploiting the semi-sorted nature of the sequence.

![[Pasted image 20260104200113.png]]

## Finding the minimum in a sorted rotated array

It is easy to see that a sorted rotated array is made up of two sorted sequences that come one after the other. The minimum value in a sorted rotated array is also called its pivot item, and it is the first item in the second sorted sequence.

![[Pasted image 20260104200134.png]]

Given below is how the sorted rotated array from the example looks when its values are plotted on a Cartesian plane.

![[Pasted image 20260104200148.png]]

Since all the sorted rotated arrays have two sorted sequences arranged in the same way, we can leverage this information to devise an algorithm to find the minimum. Consider the example of a generic sorted rotated array mapped on a Cartesian plane, given below. We will use this generic example to devise the minimum-finding algorithm.

![[Pasted image 20260104200201.png]]

We start by creating two variables `low` and `high` and initializing them with the two ends of the array, and maintaining the following invariant:

**Invariant:** The minimum value is always between `low` and `high` and `low <= high`

Note that the initial values of `low` and `high` satisfies the invariant.

![[Pasted image 20260104200408.png]]

We then iterate until `low < high`, and in each iteration, we find the midpoint of the search space in `mid` and use it to reduce the size of the search space in a way that the invariant is maintained. Every time we find `mid`, it can fall in either the first or the second sorted sequence of the array. And so, there are two cases that we need to consider in each iteration:

### 1. arr[mid] > arr[high]

This can only happen if `mid` is in the first sorted sequence and `high` is in the second sorted sequence, respectively. Because for all other cases, `arr[mid]` will be less than or equal to `arr[high]`.

![[Pasted image 20260104200434.png]]

Since we know the minimum is in between `mid` and `high` (second sorted sequence), we discard the left half of the search (between `low` and `mid`) by setting `low = mid + 1` and preserve the invariant for the next iteration.

### 2. arr[mid] <= arr[high]

This can only happen if both `mid` and `high` either fall in the first or the second sorted sequence.

![[Pasted image 20260104200453.png]]

However, since we maintain the invariant that the minimum will always be between `low` and `high`, and we know that the minimum is the first item in the **second** sorted sequence. This means `high` can never be in the first sorted sequence, as it will invalidate the invariant. And so, we can only hit this case, if `mid` is in the second sorted sequence.

![[Pasted image 20260104200503.png]]

In this case, the array between `mid` and `high` is guaranteed to be sorted, and so, the minimum is guaranteed **not** to be after `mid`. We discard the right half of the search space (between `mid` and `high`) by setting `high` to `mid`. We set `high` to `mid` as `mid` Itself could be the minimum. This way, we preserve the invariant for the next iteration.

At the end of all iterations, when `low` becomes equal to `high`, the item at low is the minimum in the sorted rotated array.

Since the invariant holds true at the beginning and is preserved through all iterations, we are guaranteed to find the minimum item at the end of all iterations.

## Algorithm

The steps below combine all the cases using conditional statements and outline the algorithm to find the minimum in a sorted rotated array.

> **minimumInRotatedSortedArray(arr, target)**
> 
> - **Step 1:** Set `low` = 0
> - **Step 2:** Set `high` = size of `arr` - 1
> - **Step 3:** Iterate while `low` < `high` and do the following:
>     - **Step 3.1:** Set `mid` = `low` + (`high` - `low`) / 2
>     - **Step 3.2:** If `arr[mid]` > `arr[high]`, set `low` = `mid` + 1
>     - **Step 3.3:** Otherwise, set `high` = `mid`
> - **Step 4:** Return `low`

## Implementation

```java
class Solution{
    public int rotatedArrayMinimum(int[] arr){
        int low=0;
        int high=arr.length-1;

        // Perform binary search until low becomes equal to high
        while(low<high){
            int mid=low+(high-low)/2;

            // If the middle element is greater than the element at high
            // index, it means the minimum element lies in the right part
            // of the array.
            if(arr[mid]>arr[high]){
                low=mid+1;
            }

            // Otherwise, the minimum element lies in the left part of
            // the array.
            else{
                high=mid;
            }
        }

        // Return the index of the minimum element
        return low;
    }
}
```

