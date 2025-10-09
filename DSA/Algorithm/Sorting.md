

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