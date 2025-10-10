

> Sorting is arranging items in a specific order, typically ascending or descending, based on some criteria.

Sorting is mostly used for two reasons.

> - **Ordering:** Arranging items in a sequence ordered by some criteria.
> - **Categorizing**: Grouping items with similar properties.

#  Classification of sorting algorithms

## Comparison sorting

Comparison-based sorting algorithms rely on comparing elements in the list to determine their order. These algorithms compare elements using a comparison operator (e.g., less than, greater than) and rearrange the elements based on the results of these comparisons.

![[Pasted image 20251009121554.png]]

## Stable sorting

A stable sort is a sorting algorithm that preserves the relative order of equal elements in the input list. **==In other words, if two elements in the input list have the same value and one comes before the other, they will also be in the same order in the sorted list.==** Stability is important in sorting algorithms, especially when sorting by multiple keys or when the original order of equal elements is significant

![[Pasted image 20251009121643.png]]

## Unstable sorting

An unstable sorting algorithm does not guarantee preserving the relative order of equal elements in the input list. **==In other words, if two elements in the input list have the same value and one comes before the other, they may not necessarily be in the same order in the sorted list.==**

![[Pasted image 20251009121725.png]]


## In-place sorting

In-place sorting is a sorting algorithm that sorts the elements of an array or list without requiring additional space proportional to the number of sorted elements. **==In other words, the algorithm sorts the elements in the original array or list without using any extra memory==**

![[Pasted image 20251009121928.png]]

## Out-of-place sorting

Out-of-place sorting is a sorting algorithm that requires additional space proportional to the number of sorted elements. **==In other words, the algorithm sorts the elements of an array or list by creating a new array or list to store the sorted elements rather than sorting the elements in the original array or list.==**

![[Pasted image 20251009122028.png]]

## Adaptive sorting

Adaptive sorting is a property of sorting algorithms that refers to their ability to take advantage of existing order in the input data to improve performance. **==In other words, an adaptive sorting algorithm can perform better when the input data is already partially sorted or nearly sorted.==**

![[Pasted image 20251009122210.png]]

## Non-adaptive sorting

Non-adaptive sorting is a property of sorting algorithms that refers to their inability to take advantage of existing order in the input data to improve performance. **==In other words, a non-adaptive sorting algorithm performs the same regardless of the input order.==**

![[Pasted image 20251009122239.png]]


# Bubble Sort

## Introduction

Bubble sort, also known as sinking sort, is one of the simplest sorting algorithms that **==works by moving an item to its correct position by comparing it against the element that comes after it. If the element after it is smaller, it is swapped with the current element.==** This process is repeated until no more swaps are needed to be performed in a pass, resulting in a final sorted list.

> **Why is this sort called bubble sort?**
	This process is similar to how bubbles rise to the surface of water, where the lighter bubbles move upwards while the heavier ones sink. In Bubble sort, the smaller (or lighter) elements "bubble" to the front of the list, while the larger (or heavier) elements "sink" to the end.

## Real life example

A real-life example of this sorting process in action would be if you were a teacher tasked with organizing a line of students by their heights. To do this, you would start by comparing the height of the first student with the second student. If the first student is taller, you would swap their positions and continue this process until you reach the end of the line. By following this method, the student at the end of the line will be the tallest. You would then repeat this process from the beginning of the line until all the students are sorted according to their height.

- **Step 1.1:** Compare the heights of the first and second students in the line and swap them if necessary.
- **Step 1.2:** Compare the heights of the second and third students in the line and swap them if necessary.
- ...
- ...
- **Step 1.N-1:** Compare the heights of the (N - 1)th and Nth students in the line and swap them if necessary.
- **Step 2:** Reduce the search space by excluding the last student from the line, as he is now standing in the correct position.
- **Step 3:** Repeat the above process until all students have reached their correct positions.

## Advantages

Even though it's not the most efficient sorting algorithm, bubble sort presents several advantages.

> - **Simplicity:** Bubble sort is quite simple to understand and implement, making it an ideal choice for learning about sorting.
> - **Adaptive:** Smart implementations of bubble sort can ensure that if the input list is partially sorted, the time complexity can be reduced to close to **O(N)**.
> - **Stable:** Bubble sort is stable, i.e., it does not change the list's relative order of equal values.
> - **In-place:** Bubble sort can sort the input list itself without allocating new memory for the algorithm.

## Limitations

> - **Inefficient:** Compared to other sorting algorithms bubble sort is not ideal for sorting large data sets as it presents an average time complexity of **O(N^2)**.


## Algorithm

The algorithm works by dividing the given array into two subarrays. The first subarray contains the unsorted elements, while the second subarray holds the sorted elements. During each iteration, the algorithm compares the first two elements of the unsorted subarray and swaps them if the first element is larger than the second. This process continues until it reaches the start of the sorted subarray. As a result, the unsorted subarray shrinks by one element while the sorted subarray expands by one element. The algorithm repeats this process until the size of the unsorted subarray becomes zero.

**Algorithm**

- **Step 1.1:** Compare the first element with the second element of the unsorted part of the list and swap them if necessary.
- **Step 1.2:** Compare the second element with the third element of the unsorted part of the list and swap them if necessary.
- ...
- ...
- **Step 1.N:** Compare the (N-1)th element with the Nth element of the unsorted part of the list and swap them if necessary.
- **Step 2:** Reduce the size of the unsorted sublist by moving the rightmost index one to the left.
- **Step 3:** Repeat the above steps until the size of the unsorted sublist becomes zero.

## Implementation

```java
class Solution {

    public void bubbleSort(int[] arr) {

        int n = arr.length;

        // Iterate through each element in the array
        for (int i = 0; i < n - 1; i++) {

            // Compare adjacent elements and swap them if they are in the  wrong order

            for (int j = 0; j < n - i - 1; j++) {

                if (arr[j] > arr[j + 1]) {

                    // Swap arr[j] and arr[j + 1]

                    int temp = arr[j];

                    arr[j] = arr[j + 1];

                    arr[j + 1] = temp;
                }
            }
        }
    }
}
```


# Selection Sort

builds the final sorted list by dividing the input list into two sublists, one sorted and the other unsorted. At each iteration, it picks the smallest element from the unsorted list and moves it to the end of the sorted list.

>**Is selection sort faster than bubble sort?**  
  Selection sort almost consistently outperforms bubble sort in real-world applications as it uses a single swap instead of multiple swaps used by bubble sort to place an item in its sorted position.

## Real life example

Let's consider the bubble sort example. Imagine you are a teacher and need to sort a line of students based on their height. The most intuitive approach would be to select the shortest student from the line and swap their position with the first student. Then, find the second shortest student from the remaining students and swap their position with the second student in the line.  You would then repeat this process until you have swapped the last student in the line.

- **Step 1:** Find the shortest student from the unsorted part of the line.
- **Step 2:** Swap this student with the student standing at the start of the unsorted part of the line.
- **Step 3:** Reduce the search space by excluding the first student from the unsorted part of the line as they are now stating at the correct position.
- **Step 3:** Repeat the above process until no more students are in the unsorted part of the line.

## Advantages

Even though it's not the most efficient sorting algorithm, selection sort presents several advantages.

> - **Simplicity:** Selection sort is quite simple to understand and implement, making it an ideal choice for learning about sorting.
> - **In-place:** Selection sort can sort the input list without allocating new memory for the algorithm.

## Limitations

> - **Inefficient:** Compared to other sorting algorithms selection sort is not ideal for sorting large data sets as it presents an average time complexity of **O(N^2)**.
> - **Unstable:** Selection sort is not stable i.e. it can change the relative order of equal values in the list


## Algorithm

The algorithm divides the given array into two subarrays. The first part is the sorted subarray, while the second contains unsorted elements. It identifies the smallest element from the unsorted subarray during each iteration and swaps it with the first element. This allows the sorted subarray to grow while the unsorted subarray shrinks. The algorithm repeats this process until the size of the unsorted subarray becomes zero.

- **Step 1:** Find the smallest element from the unsorted sublist of the list.
- **Step 2:** Swap it with the first element of the unsorted sublist.
- **Step 3:** Reduce the size of the unsorted sublist by moving the leftmost index by one to the right.
- **Step 4:** Repeat the above steps until the size of the unsorted sublist becomes zero.

```java
class Solution {

    public void selectionSort(int[] arr) {

        int n = arr.length;

        // Iterate over each element except the last one
        for (int i = 0; i < n - 1; i++) {

            // Assume the current element is the smallest
            int minIndex = i;

            // Find the index of the smallest element in the remaining unsorted portion

            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {

                    // Update the index of the smallest element
                    minIndex = j;
                }
            }
            
            // Swap the current element with the smallest element found
            int temp = arr[i];

            arr[i] = arr[minIndex];

            arr[minIndex] = temp;
        }
    }
}
```


# Insertion Sort

Insertion sort is a sorting algorithm that builds the final sorted list by simply moving the items to their correct positions one at a time. It's not the most efficient algorithm and follows a brute-force approach, but it's simple to understand and implement.

## Real life example

An example of this sorting in action is when you have a hand of cards and want to arrange them in ascending order. When holding a set of cards, you would typically scan through them and reposition the cards that are not in order to the front or back. You might begin by selecting cards and placing them in their proper positions. While doing so, you would shift all the cards after it to the right. You will continue this process until all the cards are in order

- **Step 1:** Find the card that is out of order relative to the cards around it.
- **Step 2:** Remove the card from the deck.
- **Step 3:** Find where this card belongs.
- **Step 4:** Shift all the cards from that spot to one place to the right.
- **Step 5:** Insert the removed card on the new spot.
- **Step 6:** Repeat the above until all the cards are in their correct positions.

## Advantages

Even though it's not the most efficient sorting algorithm, insertion sort presents several advantages.

> - **Simplicity:** Insertion sort is quite simple to understand and implement, making it an ideal choice for learning about sorting.
> - **Efficiency:** In practice, insertion sort is more efficient than other quadratic sorting algorithms, such as selection sort and bubble sort, when the data set is small.
> - **Adaptive:** The efficiency of insertion sort increases if the input list is partially sorted. The time complexity of the sort reduces to **O(k*N)** from **O(N^2)** when each element in the list is no more than k places away from its sorted position.
> - **Stable:** Insertion sort is stable i.e. it does not change the relative order of equal values in the list
> - **In-place:** Insertion sort can sort the input list without allocating new memory for the algorithm.

## Limitations

> - **Inefficient:** Compared to other sorting algorithms insertion sort is not ideal for sorting large data sets as it presents an average time complexity of **O(N^2)**.


## Algorithm

Like bubble and selection sorts, insertion sort divides the input array into two subarrays. The first subarray contains the sorted items, while the second contains all the unsorted items. The first item in the array is considered sorted during the first pass and is part of the "sorted subarray". During each iteration, the algorithm picks the first element from the unsorted subarray and tries to insert it into the sorted subarray. The algorithm compares the first element of the unsorted subarray with the last element of the sorted subarray (i.e., the element just before the unsorted subarray). If the first element of the unsorted subarray is less than the last element of the sorted subarray, they are swapped. This process continues until the unsorted element reaches its correct position in the sorted subarray.

- **Step 1:** Pick the first element from the unsorted sublist.
- **Step 2:** Compare the element with the element on its left and swap them if the element on the left is larger (or smaller, depending on the sorting order).
- **Step 3:** Keep repeating step 2 until no more swaps are needed.
- **Step 4:** Reduce the size of the unsorted sublist by moving the leftmost index by one to the right.
- **Step 5:** Repeat the above steps until the size of the unsorted sublist becomes zero.

## Implementation

```java
class Solution {
    public void insertionSort(int[] arr) {
        // Get the length of the array
        int n = arr.length;
        
        // Select each element from the unsorted portion one by one
        // Start from 1 because element at index 0 is already considered "sorted"
        for (int unsortedIndex = 1; unsortedIndex < n; unsortedIndex++) {
            
            // Take and save the current element that we're going to sort
            // This element will be inserted into its correct position in the sorted left portion
            int elementToInsert = arr[unsortedIndex];
            
            // Start from the end of the sorted portion (the last element to the left of selected element)
            // We'll move backwards to make space for this element
            int sortedIndex = unsortedIndex - 1;
            
            // Check two conditions:
            // 1) sortedIndex >= 0: Haven't reached the beginning of array? (boundary check)
            // 2) arr[sortedIndex] > elementToInsert: Is the left element greater than the element we're inserting?
            // If both are true: shift elements to the right, create empty space
            while (sortedIndex >= 0 && arr[sortedIndex] > elementToInsert) {
                
                // Shift the larger element one position to the right (create space)
                // Example: [2, 5, _] → [2, _, 5]
                arr[sortedIndex + 1] = arr[sortedIndex];
                
                // Move one step to the left, continue checking
                sortedIndex--;
            }
            
            // While loop ended, which means:
            // - Either we reached the beginning of array (sortedIndex = -1)
            // - Or we found a smaller/equal element
            // Now insert our element into the empty space (sortedIndex + 1)
            arr[sortedIndex + 1] = elementToInsert;
        }
    }
}
```

# Counting Sort

Counting sort is a non-comparison-based sorting algorithm that operates by counting the number of occurrences of each unique element in the input list and using this information to place each element in the correct position in the output list. It is particularly useful when the range of input elements is known and relatively small compared to the number of elements to be sorted.

## Real life example

Let's again become a teacher to understand the real-world application of this algorithm. Let's say you were a teacher assigned the task of sorting answer sheets of students who scored out of 10. However, the catch is that there is a large number of students. For this example, let's say there are 200 students. You could use some of the sorts we studied earlier, but they would be quite time-consuming as you would need to do a lot of comparisons. Since the range of scores is relatively small, you could use a different strategy. You could count the times each score appears and stack the sheets with the same score on top of each other. To do so, you would only need one pass over all the answer sheets and no comparison.

Once you have all the different stacks, you can arrange the individual answer sheets by incrementally unwinding the stacks, starting with the stack with the lowest (or highest, depending on the sorting order) score. You keep doing this until the sheets from all the stacks are lined up.  

> - **Step 1:** Stack the answer sheets with the same score on top of each other.
> - **Step 2:** Unwind the stack with the lowest (or highest, depending on the sorting order) score and start lining the sheets.
> - **Step 3:** Pick the next stack that fulfills the sorting order and repeat step 2 until all the stacks are unwinded.

## Advantages

> - **Simplicity:** Counting sort is quite simple to understand and implement.
> - **Efficiency:** With its linear time complexity, counting sort is very efficient when the range of input values is small compared to the number of elements in the input list. It outperforms comparison-based sorting algorithms like quicksort or merge sort in such cases.
> - **Stable:** Counting sort is stable i.e. it does not change the relative order of equal values in the list.

## Limitations

> - **Space complexity:** Counting Sort requires additional space to store the count array and the output list, both of which have a size proportional to the range of input values. This can be a limitation when the range of input values is large or when memory is limited.
> - **Not In-place:** Counting sort is not an in-place algorithm; it needs to write the output to a different list, which could be problematic if memory is limited.

## Algorithm

This algorithm can be divided into three major steps

> - **Step 1:** Calculate the frequency of each element.
> - **Step 2:** Calculate the cumulative sum of frequencies.
> - **Step 3:** Build the sorted list.

### Step 1: Calculate the frequency of each element

The first step is to calculate the frequency of each unique element in the input array and store it in an auxiliary array called **count**. The size of this auxiliary array is equal to the maximum value in the input array + 1. The algorithm uses this count array as a key value mapping where each array index is a key, and the index's value is that key's frequency

### Step 2: Calculate the cumulative sum of frequencies

The second step is to iterate over the count array and convert it to a cumulative sum array.

### Step 3: Build the sorted list

The final phase of the algorithm is to iterate over the input array in **reverse order** and place each element in the output array using the count array. Once an element is placed in the input array, its count is decreased from the count array. At the end of the iteration, all the elements on the input array will be placed in the output array in a sorted manner.

**Algorithm**

- **Step 1:** Create a new array called "count" with its size equal to the (maximum element in the list + 1).
- **Step 2:** Count the occurrences of each unique element in the input list and store these counts in the "count" array.
- **Step 3:** Modify the count array to store the cumulative sum of counts. Each element in the count array represents the number of elements less than or equal to the index value.
- **Step 4:** Iterate through the original input list in reverse order and use the count array to determine the correct position of each element in the sorted output list.
- **Step 5:** Decrement the count of the element's value in the count array and use this value as the index in the output list.

## Implementation

```java
class Solution {
    public int[] countingSort(int[] arr, int k) {
        int n = arr.length;
        // Create a count array to store the frequency of each key
        int[] count = new int[k + 1];
        // Store the frequency of each key in the count array
        for (int i = 0; i < n; i++) {
            count[arr[i]]++;
        }
        // Modify the count array to store the actual position of each
        // key in the sorted array
        for (int i = 1; i <= k; i++) {
            count[i] += count[i - 1];
        }
        // Create a temporary array to store the sorted result
        int[] result = new int[n];
        // Build the sorted result array
        for (int i = n - 1; i >= 0; i--) {
            result[count[arr[i]] - 1] = arr[i];
            count[arr[i]]--;
        }
        return result;
    }
}
```

# Quick Sort

Quicksort is a widely used comparison-based sorting algorithm based on the divide and conquer algorithm paradigm. It is known to be slightly faster than Merge sort and Heap sort for randomized data, especially on more significant distributions. The algorithm selects a pivot in the input list and then partitions the list into two sublists: one containing all elements less than the pivot and the other containing all elements greater than the pivot. This process continues recursively on the sublists until the entire list is sorted.

## Real life example

A real-life example of this sorting in action would be if you were a librarian. You would have books scattered everywhere and be tasked with arranging them alphabetically by title. You could choose a random book, make it a pivot, and start placing all the books along this pivot. Place all the books where the title comes before the pivot on the left and books where their titles come after the pivot to the right. Doing so ensures that the book chosen as the pivot is in its correct spot. You then repeat the same process on the books on the left and right sides of the pivot. At the end, you will have all the books ordered correctly.

> - **Step 1:** Chose a random book from all the leftover books and make it a pivot
> - **Step 2:** Place the books with the titles before the pivot to the left and those with the titles after the pivot to the right.
> - **Step 3:** Repeat steps 1-2 for the left and right partitions produced in step 2.

The space complexity of quicksort is **O(logN)** due to the recursive calls on the sublists. Each recursive call requires a constant amount of space for the function call stack, and the depth of the call stack is **O(logN)** in the average and worst cases.

## Advantages

> - **Efficiency:** Quicksort is very efficient, especially for large datasets. The average case's time complexity is **O(N*logN)**, faster than many other sorting algorithms.
> - **Adaptive:** Quicksort is adaptive, meaning its performance improves when the input list is partially or nearly sorted. The partitioning step becomes more efficient when the list is partially sorted.
> - **Parallelization:** Quicksort can be easily parallelized, allowing it to take advantage of multi-core processors and parallel computing environments
> - **In-place:** Quicksort can sort the input list itself without allocating new memory for the algorithm to run.

## Limitations

> - **Unstable:** Quicksort is unstable; it can change the list's relative order of equal values.
> - **Inefficient:** Quicksort is not as efficient for small datasets, as the partitioning step's overhead can outweigh the algorithm's efficiency benefits.

## Algorithm

The quicksort algorithm operates when at least two elements are in the input array. It follows a partitioning process, which divides the input array into two consecutive non-empty subarrays around a pivot. Elements smaller than the pivot are placed on its left side, while elements greater than the pivot are placed on its right side. After partitioning, the quicksort algorithm recursively repeats this process on the two subarrays. The pivot element is not included in the recursion as it is already in its correct position. The result is a sorted array once all the recursive steps are completed.

- **Step 1:** If the range has less than two elements, return as there is nothing to do
- **Step 2:** Randomly pick a "pivot". This could be any random element in the input list.
- **Step 3:** Partition the elements of the input list into two sublists such that all elements less than the pivot go to the the first sublist and all the elements greater than the pivot go to the second sublist. The elements equal to the pivot can go either way.
- **Step 4:** Recursively apply the above steps to the two sublists produced in Step 3.

```java
import java.util.*;

class Solution {
    // Helper method to swap elements in the array
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    private int partition(int[] arr, int left, int right) {
        // Randomly select a pivot index between left and right
        Random rand = new Random();
        int pivot = left + rand.nextInt(right - left + 1);
        // Get the pivot value
        int pivotVal = arr[pivot];
        // Move the pivot to the end
        swap(arr, pivot, right);
        // Index of smaller element
        int cursor = left;
        for (int i = left; i < right; i++) {
            if (arr[i] < pivotVal) {
                // Swap elements
                swap(arr, cursor, i);
                cursor++;
            }
        }
        // Swap pivot to its correct position
        swap(arr, cursor, right);
        // Return the pivot index
        return cursor;
    }

    private void quicksort(int[] arr, int left, int right) {
        if (left < right) {
            // Partition the array
            int pivot = partition(arr, left, right);
            // Recursively sort the left subarray
            quicksort(arr, left, pivot - 1);
            // Recursively sort the right subarray
            quicksort(arr, pivot + 1, right);
        }
    }

    public void quickSort(int[] arr) {
        int n = arr.length;
        // Call Quicksort function
        quicksort(arr, 0, n - 1);
    }
}
```

# Merge Sort

Merge sort is one of the most efficient and widely used sorting algorithms. It is a general-purpose comparison-based sort that uses a divide-and-conquer approach under the hood. It works by recursively dividing the input list into smaller sublists, sorting each, and merging them to produce a single list.

## Real life example

Continuing on the quicksort example. Imagine you're a librarian tasked with organizing a large number of books in alphabetical order by title. Instead of using quicksort, you could use the merge sort approach. You can divide the books into smaller, manageable groups and sort them independently. Then, you can merge the sorted groups to create a larger, fully sorted group. Repeat this process until all the groups are merged into the final ordered list of books.  

> - **Step 1:** Divide the books into smaller groups of manageable size.
> - **Step 2:** Sort each group of books alphabetically by title.
> - **Step 3:** Merge the groups to create larger sorted groups.
> - **Step 4:** Repeat steps 1-3 until all books are sorted into one large group.

## Advantages

> - **Efficiency:** Merge sort is one of the most efficient, especially for large datasets. Its time complexity for all cases is **O(N*logN)**, faster than many other sorting algorithms.
> - **Stable:** Merge sort is stable, i.e., it does not change the list's relative order of equal values.
> - **Parallelization:** Merge sort can be easily parallelized, allowing it to use multi-core processors and parallel computing environments.

## Limitations

> - **Space complexity:** Merge sort requires additional space to store the sorted subarrays during the merge phase. This can be a limitation when memory is limited.
> - **Not In-place:** Merge sort is not an in-place algorithm; it needs to write the output to a different list, which could be problematic if memory is limited.

## Algorithm

The algorithm starts by dividing the input array into two subarrays of equal size. It then recursively calls the left and right subarrays and keeps on doing so until the left and right subarrays have only a single element left. Thereafter, the algorithm starts merging the subarrays in a sorted manner and returning them to the caller. This process keeps on repeating until the entire array is sorted.


- **Step 1:** If the size of the input list is <= 1 return the array. (Base case)
- **Step 2:** Divide the unsorted list into two halves (left and right).
- **Step 3:** Call Step 1 with each of these halves and store their results in two output lists.
- **Step 4:** Merge the two output lists obtained from the above step in a sorted manner.
- **Step 5:** Return the merged list back to the caller.

```java
import java.util.*;

class Solution {
    public int[] merge(int[] leftArr, int[] rightArr) {
        // Create an empty array to store the merged array
        int[] mergedArr = new int[leftArr.length + rightArr.length];
        // Initialize two pointers, i for leftArr and j for rightArr
        int i = 0, j = 0, k = 0;
        // Compare elements from both arrays and add the smaller one to
        // the mergedArr
        while (i < leftArr.length && j < rightArr.length) {
            // If the element in leftArr is smaller or equal to the
            // element in rightArr add the element from leftArr to
            // mergedArr
            if (leftArr[i] <= rightArr[j]) {
                // Add element from leftArr to mergedArr
                mergedArr[k] = leftArr[i];
                // Move the pointer for leftArr to the next element
                i++;
            }
            // Else if the element in rightArr is smaller than the
            // element in leftArr add the element from rightArr to
            // mergedArr
            else {
                // Add element from rightArr to mergedArr
                mergedArr[k] = rightArr[j];
                // Move the pointer for rightArr to the next element
                j++;
            }
            k++;
        }
        // Add any remaining elements from leftArr (if any) to the
        // mergedArr
        while (i < leftArr.length) {
            mergedArr[k] = leftArr[i];
            i++;
            k++;
        }
        // Add any remaining elements from rightArr (if any) to the
        // mergedArr
        while (j < rightArr.length) {
            mergedArr[k] = rightArr[j];
            j++;
            k++;
        }
        // Return the sorted and merged array
        return mergedArr;
    }

    public int[] mergeSort(int[] arr) {
        // Base case: if the array has 1 or fewer elements, it is
        // already sorted
        if (arr.length <= 1) {
            return arr;
        }
        // Find the middle index of the array
        int mid = arr.length / 2;
        // Split the array into two halves
        int[] leftArr = Arrays.copyOfRange(arr, 0, mid);
        int[] rightArr = Arrays.copyOfRange(arr, mid, arr.length);
        // Recursively sort the left half
        leftArr = mergeSort(leftArr);
        // Recursively sort the right half
        rightArr = mergeSort(rightArr);
        // Merge the sorted halves and return the result
        return merge(leftArr, rightArr);
    }
}
```

# Heap Sort

Heapsort is another efficient sort algorithm that uses the heap data structure under the hood to sort a list. It can be considered an efficient implementation of selection sort using the heap data structure.

## Real life example

There are no concrete real-life examples of heapsort, as a heap is a data structure in computer memory. However, a scenario that closely resembles heapsort is working in the customer support team of a telecom company, where you have to handle customer calls based on their priority. This priority queue is maintained using a heap. When a new call comes in, it is placed in the correct order in the existing queue using a heap.  

## Advantages

> - **Efficiency:** Heapsort is one of the most efficient sorting algorithms, especially for large datasets. Its time complexity for all cases is **O(N*logN)**, faster than many other sorting algorithms.
> - **In-place:** Heapsort can sort the input list without allocating new memory for the algorithm.

## Limitations

> - **Unstable:** Heapsort is not stable, i.e., it can change the relative order of equal values in the list.

## Algorithm

Heapsort can be divided into two major steps.

> - **Step 1:** Build the heap.
> - **Step 2**: Remove the top element and heapify again

### Step 1: Build the heap

The first step is to convert the input array into a binary max heap. This is achieved by repeatedly "heapifying" the array, starting from the last non-leaf node and moving up the tree. Once the input array has been transformed into a heap, its root element will contain the largest number in the input array.

### Step 2: Remove the top element and heapify again

Once we have a binary max heap, we know that the root element is the largest among all the other elements. The root element is then swapped with the last element of the heap to move the largest element to the last. After doing so, the size of the heap is reduced by one by removing this last element from the heap, and the heap is "heapified" again to find the next largest element. This process is repeated until the heap becomes empty.

**Why is the last element removed from the heap?**

The last element is removed to ensure it is no longer part of the next "heapify" operation, as it is already the largest among the heap elements. The aim of the next "heapify" operation is to find the second largest element. If the largest element is not removed from the heap, the "heapify" process will always move this element to the top instead of the second largest element.

Like selection sort, heapsort maintains an unsorted space of elements, the heap, and a sorted space consisting of all the elements removed from the heap. Each iteration picks an item from the unsorted space and moves it to the sorted space by swapping elements.



- **Step 1:** Convert the input array into a max (or min, depending on the sorting order) heap.
- **Step 2:** Extract the root element from the heap and swap it with the last element in the heap.
- **Step 3:** Reduce the size of the heap by removing the last element from the heap.
- **Step 4:** Apply the "heapifiy" process to the heap.
- **Step 5:** Repeat steps 2-4 until the heap is empty.

