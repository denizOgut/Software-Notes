
# Introduction to Backtracking

Simply put, backtracking is an algorithmic technique for solving problems by building a solution incrementally, one piece at a time. It identifies potential solutions by validating every result against a fixed set of constraints. ==Backtracking is a **brute-force** approach to finding the desired solution by trying all possible options.==

Backtracking suggests that if the current result is unsuitable, **backtrack** and try other solutions using the same technique. backtracking very heavily relies on recursion. When exploring the solutions, a bounding function is applied so that the algorithm can check if the solution built so far satisfies the constraints. If it does, it continues searching. If it doesn’t, the branch will be eliminated, and the algorithm will return to the previous level.

### Phone unlocking problem

 Imagine that you just got a new phone for yourself and set a 4-digit numeric password for its lock screen before going for a nap. You wake up and forget the password that you set. How will you unlock your phone now?

> To keep the problem simple, lets limit the digits to only 0 and 1

There are two observations to make here -

> - It is just a 4-digit number; every digit can only be 0 or 1. This means there is only a **finite** number of possible passwords.
> - You can validate if the password is correct by entering it into the phone and seeing if it unlocks.

The two observations above are the necessary and complete conditions for a backtracking solution. It is easy to imagine how we can find the password now. We just need to list all possible 4-digit numbers made up of only 0s and 1s and try them out.

We start by building the first potential solution to our problem. Starting with the first digit, we incrementally move ahead to build the 4-digit number by **appending** either a `0` or `1`.

Once we create our first 4-digit number, we **validate** it by entering it as the phone password. If the phone unlocks, this is the correct password, and we have our solution. Otherwise, it means some other number is the password.

If the first result we calculated is not the solution to our problem, we take a **step back** and make a **different choice** this time to get a new result. Once we have the brand new result, we validate it again.

We keep **repeating** this process of going **one step back** and updating our choice to generate all possible 4-digit numbers made up of only `0s` and `1s` and enter them into the phone. It is guaranteed that one of them will be the correct password.

## Key Components of Backtracking

### Finite set of outcomes

Backtracking is a brute-force technique that validates each outcome as a potential solution. A problem with a ==backtracking solution should be deterministic and have a **finite set** of potential outcomes.==

![[Pasted image 20251227114224.png]]

### Solution validation

Backtracking is almost always a brute-force solution. We generate all the possible outcomes for a problem and validate each to decide on a solution subset. A problem with a backtracking solution should have a validation algorithm/function to determine if an outcome is a solution

![[Pasted image 20251227114301.png]]

### Recursive structure

A backtracking solution incrementally builds results by starting from a problem and making choices at every step to lead to a solution. If the choices lead to a wrong result, one needs to take one step back at a time and make different choices that lead to a different outcome.

To accomplish this, the implementation should always be **aware** of all the choices made, starting from the initial problem state to the current state, and be able to take a step back and try a different path if the choices do not lead to a solution. A recursive implementation can easily accomplish this.

> - Every function call can be considered as **making** a choice
> - The function call stack **remembers** all the choices
> - At the end of a function call, control goes **one step back** to the calling function, where we can make a different choice by calling the function again with different inputs.

![[Pasted image 20251227114604.png]]

### State space tree

Processing a backtracking solution generates a state-space **tree**. Every backtracking solution starts from a problem state and tries to reach one or more solution states by making choices. If the choices do not lead to a solution state, we backtrack and make different choices.

A space state tree is a tree that represents all the possible states (solution or non-solution), starting from the root as the initial state (problem state) to the leaf as a terminal state (potential solution state). The intermediate states can be either fulfilling or defying. A fulfilling state can lead to a solution, while a defying state cannot. We decide if a state is fulfilling or defying using an algorithm/function specific to the problem. Not all backtracking problems have to define states in their state space tree.

A backtracking solution explores the tree starting from the root, moving through fulfilling states, and backtracking whenever a defying state or dead end is encountered. Upon reaching a terminal state, the solution is validated, and the algorithm backtracks to explore alternative paths until all possible solutions are found.

![[Pasted image 20251227114813.png]]

## Implementing Backtracking Algorithms

Backtracking solutions are implemented using recursive function calls. We use these recursive function calls to move from one state to another, starting from the initial problem state. Each function call from a state signifies a choice that leads to another state. This process continues until we reach a terminal state where we decide if our decisions make up a proper solution using some validation function/algorithm.

In case we reach a state that is not a solution, the function call ends and returns the control to the caller, which is also the state from where we moved to the next state. At this point, we can move to a new state, continue the process, or backtrack even further.

```java
public class CrackPassword {

    private static final String PASSWORD = "0101";

    public static void crackPassword(String state) {
        if (state.length() == 4 && state.equals(PASSWORD)) {
            System.out.println("Password cracked");
        }

        if (state.length() == 4) {
            return;
        }

        for (int i = 0; i <= 1; i++) {
            String newState = state + (char) ('0' + i);
            crackPassword(newState);
        }
    }

    public static void main(String[] args) {
        crackPassword("");
    }
}
```

# Pattern: Unconditional Enumeration

Backtracking is the ultimate brute-force technique to solve any problem that starts from an initial state, explores the entire problem space, and builds a solution incrementally. Unconditional enumeration is the most fundamental backtracking technique, which starts from an initial problem state, explores the entire problem space by making a independent set of choices from every state and collects the solution states and backtracks to make different choices.

>**==It is important to note that any choice we make at a step is independent of any earlier choices; hence, we call this process unconditional enumeration.==**

The unconditional enumeration pattern is the classification of problems that can be solved using the unconditional enumeration backtracking technique.

![[Pasted image 20251227121909.png]]

## Unconditional enumeration

In unconditional enumeration, we begin with an initial problem state defined by some state variables. At every step, we can make one of many **independent** choices to reduce the size of the problem and move to another state. This process of making choices at every step is repeated recursively until we reach a solution state. As we make these choices and move from one state to another, we incrementally build the solution in some state variable.

We maintain a shared container as we explore the problem space, and add a solution state to it when we reach it. This way, when the entire problem space is explored, the container contains an enumeration of all solution states.

Instead of the state space tree, unconditional enumeration can more easily be visualised as a linear list of nodes where the length of the list represents the depth of the problem space (`n`). We start from the first node, and we can move from one node to the next by making **one** of many (`k`) **independent** choices.

![[Pasted image 20251227122025.png]]

We create a state variable `state` to incrementally build the solution based on the choices we make using some function `f`. As we move closer to the end of the list by making a series of choices, the problem space is reduced, and the variable `state` aggregates the outcomes of all the previous choices.

The problem space is ultimately reduced to a solution state (base case in this case) when we reach the last node, and the variable `state` holds the contribution of all choices made from the initial problem state to the solution state. It counts as one solution to the problem, and so we usually save the value of `state` in some container when we reach a solution state.

The goal of unconditional enumeration is to enumerate **all** possible outcomes that can be reached by making **all** possible choices from start to end.

### The unconditional enumeration problem

Consider an example where the depth of the problem space is represented by an integer `n` and we start from the initial problem state with some default value of a `state` variable. We can make multiple choices, denoted by an integer `choice` at every step, to reduce the problem space, and we update the `state` variable with those choices as we make them. We have the following functions that we can use.

- `getChoices` - Takes as an input the current size of the problem space `n` and returns a list of choices we can make.
- `makeChoice` - Takes as input the state variable `state` and a `choice` from the list of available choices and adds the contribution of `choice` to `state`.
- `revertLastChoice` - Takes as in-out the state variable `state` and reverts the contribution of the last choice that was made.
- `getReducedInput` - Takes the current size of problem space `n` as input and returns a value denoting the size of the reduced problem space.
- `isSolutionState` - Takes the current size of problem space `n` as input and returns true if it is a solution state.

### The unconditional enumeration technique

To solve this problem, we create a recursive function `unconditionalEnumeration` that takes as input the integer `n` denoting the problem space, a reference to the state variable `state` ,and a reference to a list `enumerations` to store all the solution states.

We initialize `state` to a default value and `enumerations` to an empty list in the calling function and pass them as reference arguments to the function `unconditionalEnumeration` along with the input `n`.

As we enter the function, we check if the current state is a solution state case using `isSolutionState`. If the current state is a solution state, we add the current value of  `state` to the list `enumerations` and return to the caller.

If the current state is not a solution state, we use the function `getReducedInput` to get the next input for the reduced problem space in a variable `reducedInput`. Next, we use the function `getChoices` to get a list of all the choices we can make to reduce the problem space. We then iterate through the list of all choices and in each iteration, simulate making that choice by adding its contribution to `state` using `makeChoice`. We then recursively call the same function with `reducedInput` and the updated `state`. The same process is repeated recursively after the function call until it reaches a solution state.

When the recursive call ends, we revert the last choice made using `revertLastChoice` on `state` and continue the iteration to make the next choice.

Since we call `revertLastChoice` after returning from **every** recursive call, it is guaranteed that the choice made before making the same recursive call is the one that is reverted.

This way, we simulate making a choice at every step until we reach a solution state, aggregate the consequences of all those choices in `state`, and add the final value of `state` (outcome) to the `enumerations`. We also undo the choices in the same order as they are made, as we backtrack to make different choices the next time in the same way.

When all the recursive calls end, control is passed back to the caller of `unconditionalEnumeration`, the `enumerations` list has the list of all outcomes from all choices, and the variable `state` is reverted to the default value with which it was initialized.

Consider the example below, where we start from a problem state where `n = 3` and the function `getReducedInput` reduces the input value by 1 until we reach the solution state `n = 1`. At every step, we make **independent** choices returned by the `getChoices` function and enumerate all the choices that lead to a solution state starting from the problem state.

## Algorithm

he algorithm given below outlines the generic unconditional-enumeration technique, making use of the functions `getReducedInput`, `getChoices`, `makeChoice`, `revertLastChoice`, and `isSolutionState`. All these functions and their implementations are problem-dependent.

We also create a calling function that initializes the state variables `state` and `enumerations` and passes them by reference to the top-level recursive call.

> **unconditionalEnumeration(n, [ref] state, [ref] enumerations)**
> 
> - **Step 1:** Check if the current state is a solution state using `isSolutionState`. If it is a solution state, do the following:
>     - **Step 1.1:** Add `state` to the `enumerations` list
>     - **Step 1.2:** Return to the caller
> - **Step 2:** `choices` = Call `getChoices(n)`
> - **Step 3:** `reducedInput` = Call `getReducedInput(n)`
> - **Step 4:** Iterate in `choices` using a variable `choice` and do the following:
>     - **Step 4.1:** Call `makeChoice(state, choice)` to add the contribution of `choice` to `state`
>     - **Step 4.2:** Call `unconditionalEnumeration(reducedInput, state, enumerations)`
>     - **Step 4.3:** Call `revertLasChoice(state)` to remove the contribution of `choice` from `state`
> - **Step 4:** Return to the caller
> 
> **callingFunction(n)**
> 
> - **Step 1:** Create a variable `state` and set it to some `default` value
> - **Step 2:** Create a list `enumerations`
> - **Step 3:** Call `unconditionalEnumeration(n, state, enumerations)`
> - **Step 4:** Return `enumerations`

## Implementation

```java
import java.util.ArrayList;
import java.util.List;

class Solution {

    public void unconditionalEnumeration(
        int n,
        List<Integer> state,
        List<List<Integer>> enumerations
    ) {
        // Check if the current state is a solution state
        if (isSolutionState(n, state)) {
            // Add the current state to the list of enumerations
            // as it is the aggregation of all choices from the start
            // and hence forms a complete solution
            enumerations.add(new ArrayList<>(state));
            return;
        }

        // Get all possible choices for the current state
        List<Integer> choices = getChoices(n);

        // Iterate through each choice
        for (int choice : choices) {
            // Simulate making that choice by update the state with it
            makeChoice(state, choice);

            // Get the input for the next state
            int reducedInput = getReducedInput(n);

            // Recursively call the function with the reduced input
            unconditionalEnumeration(reducedInput, state, enumerations);

            // Simulate reverting the previous choice (backtracking)
            revertLastChoice(state);
        }
    }

    // Checks if the current state is a solution state
    private boolean isSolutionState(int n, List<Integer> state) {
        // Implement your solution state conditions here
        return n == 0;
    }

    // Returns the list of possible choices for the current state
    private List<Integer> getChoices(int n) {
        // Implement your logic to generate choices here
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        return list;
    }

    // Applies a choice to the current state
    private void makeChoice(List<Integer> state, int choice) {
        // Implement your logic to update the state here
        state.add(choice);
    }

    // Reverts the most recent choice (backtracking step)
    private void revertLastChoice(List<Integer> state) {
        // Implement your logic to update the state here
        if (!state.isEmpty()) {
            state.remove(state.size() - 1);
        }
    }

    // Reduces the problem input for the next recursive call
    private int getReducedInput(int n) {
        // Implement your logic to reduce the input here
        return n - 1;
    }
}
```

## Identifying the Unconditional Enumeration Pattern

By systematically exploring these states, unconditional enumeration ensures that all valid solutions are considered. Most problems where we can make a fixed set of choices that are independent of any previously made choice can be solved using the unconditional enumeration technique.

If the problem statement or its solution follows the generic template below, it can be solved using unconditional enumeration.

**Template:**  
  
Given an initial problem state, enumerate all the solution states that can be reached from it by making a fixed set of independent choices at each step.

> **Problem statement:** Given an integer array `arr` containing unique elements, write a function that returns all possible subsets (the power set) of the elements in arr. The solution set must not contain duplicate subsets. You can return the subsets in any order.


### The Unconditional Enumeration Solution

By closely observing the problem, we can identify a brute-force approach to building all subsets. We start with an empty set (the initial problem state) and iterate over the array. In each iteration, we have two choices: either select the number at that index and add it to our set, or ignore it and proceed to the next index.

It is clear from the above what the initial problem state (empty set) is, and the choices we have to reduce the problem space incrementally build the solution. The solution to the problem fits the template description for the unconditional enumeration pattern we learned earlier.

**Template:**  
  
Given an initial problem state (empty set), enumerate all the solution states (all subsets) that can be reached from it by making a fixed set of independent choices (add a number to the set or ignore it) at each step.

We create a recursive function `findSubsets` that takes as input the array `arr`, the current index we are at in the array `index`, reference to a list `currentSet` that holds current set that is made from our choices, and reference to a 2D list `subsets` that will hold all the subsets (solution states). The recursive function `findSubsets` recursively explores the entire problem space, starting from the given `index` in the array `arr`, and adds all the subsets to the `subsets` list.

It is important to note that the variables `index` and `currentSet` collectively define the state in the state space tree that we explore.

We initialize the `currentSet` and `subsets` lists in the calling function as empty lists and pass them by reference to the `findSubsets` function along with the input array `arr` and starting with `index` 0 that makes up the initial problem state.

As we enter the findSubsets function, we check if we have finished making choices for all the items in the array by checking if `index` == size of `arr`. If yes, it means no more choices can be made, and we are at a solution state where `currentSet` is the subset built based on our choices. We add `currentSet` to `subsets` and return to the caller.

If we are not at a solution state, we have two choices to make. We can either ignore the item and `arr[index]` or add it to `currentSet`. We make the first choice by recursively calling findSubsets on `index+1` without modifying `currentSet`. When this recursive call ends, we make the second choice by adding `arr[index]` to `currentSet` and again calling `findSubsets` recursively. When this recursive call ends, we revert our choice by popping the last item from the `currentSet` list and returning to the caller.

This way, at every step, make two choices and update and revert the `currentSet` list accordingly and adding `currentSet` to the `subsets` list when we have made a series of choices for all items in the array (solution state). At the end of all recursive calls, the `subsets` list will have all power set (all subsets) of the array in the calling function.

```java
import java.util.ArrayList;
import java.util.List;

class Solution {

    void findSubsets(
        List<Integer> arr,
        int index,
        List<Integer> currentSet,
        List<List<Integer>> subsets
    ) {

        if (index == arr.size()) {
            // Add the current subset to the subsets
            subsets.add(new ArrayList<>(currentSet));
            return;
        }

        // Choice 1. Ignore the current element from the subset
        // Recur with the next element
        findSubsets(arr, index + 1, currentSet, subsets);

        // findSubsets for the next choice

        // Choice 2. Include the current element in the subset
        currentSet.add(arr.get(index));
        // Recur with the next element
        findSubsets(arr, index + 1, currentSet, subsets);

        // Undo the previous choice before moving to next element
        currentSet.remove(currentSet.size() - 1);
    }

    List<List<Integer>> uniqueSubsets(List<Integer> arr) {

        // Vector to store the subsets
        List<List<Integer>> subsets = new ArrayList<>();

        // Temporary vector to store the current subset
        List<Integer> currentSet = new ArrayList<>();

        // Start the recursive search from index 0
        findSubsets(arr, 0, currentSet, subsets);

        // Return the vector containing all subsets
        return subsets;
    }
}

```

## Example  Unique Subsets

Given an integer array **arr** containing unique elements, write a function that returns all possible subsets (the power set) of the elements in arr. The solution set must not contain duplicate subsets. You can return the subsets in **any order**.

```java
import java.util.*;

class Solution {

    private void generateSubsets(
        int[] arr,
        int index,
        List<Integer> state,
        List<List<Integer>> result
    ) {

        // Every state is a valid subset -> add directly
        result.add(new ArrayList<>(state));

        // Loop through all possible indices starting from the current
        // index
        for (int i = index; i < arr.length; i++) {

            // Include the current element in the subset (make a choice)
            state.add(arr[i]);

            // Recur with the next element (reduced input -> i+1)
            generateSubsets(arr, i + 1, state, result);

            // Backtrack by removing the last element (revert the choice)
            state.remove(state.size() - 1);
        }
    }

    public List<List<Integer>> uniqueSubsets(int[] arr) {

        // List to store the subsets
        List<List<Integer>> result = new ArrayList<>();

        // Temporary list to store the current subset
        List<Integer> state = new ArrayList<>();

        // Start backtracking from index 0
        generateSubsets(arr, 0, state, result);

        // Return the list containing all subsets
        return result;
    }
}

```

## Example Number Sequence

Given two non-negative integers **n** and **k**, write a function that returns all possible sequences of length n, where each element is an integer in the range `[1, k]`. You can return the sequences in **any order**.

```java
import java.util.*;

class Solution {

    private void generateSequence(
        int n,
        int k,
        int index,
        List<Integer> state,
        List<List<Integer>> result
    ) {

        // If the current sequence has reached length n (solution state)
        if (index == n) {

            // Add the complete sequence to the result
            result.add(new ArrayList<>(state));

            // Return to continue exploring other possibilities
            return;
        }

        // Get all possible choices for the current position
        // (numbers 1..k)
        for (int choice = 1; choice <= k; choice++) {

            // Add current number to the state (make choice)
            state.add(choice);

            // Recurse to fill the next position in the sequence
            generateSequence(n, k, index + 1, state, result);

            // Backtrack by removing the last added number (revert
            // choice)
            state.remove(state.size() - 1);
        }
    }

    public List<List<Integer>> numberSequence(int n, int k) {

        // Stores all generated sequences (solution states)
        List<List<Integer>> result = new ArrayList<>();

        // Stores the current sequence being built (state)
        List<Integer> state = new ArrayList<>();

        // Generate all sequences using backtracking
        generateSequence(n, k, 0, state, result);

        // Return the list containing all sequences
        return result;
    }
}

```

## Example Phone combinations

Given a string **digits** consisting of numbers from `2` to `9`, write a function to generate and return a list of all possible letter combinations that the numbers could represent. The mapping of each number to its corresponding letters (just like on the telephone buttons) is provided below. You can return the answer in **any order**.

**Note** - the digit `1` does not map to any letter

```java
import java.util.*;

class Solution {

    // Mapping of digits to their corresponding letters (telephone button
    // mapping)
    private final String[] phoneMapping = {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
    };

    private void generateCombinations(
        String digits,
        int index,
        StringBuilder state,
        List<String> result
    ) {

        // If the current combination has reached the length of digits,
        // add it to result (solution state)
        if (index == digits.length()) {
            result.add(state.toString());
            return;
        }

        // Get the current digit
        char digit = digits.charAt(index);

        // Get the corresponding string of letters for the current digit
        String letters = phoneMapping[digit - '0'];

        // Try every letter corresponding to the current digit
        for (char letter : letters.toCharArray()) {

            // Add the letter to the current combination (make choice)
            state.append(letter);

            // Recur with the next digit (reduced input -> index + 1)
            generateCombinations(digits, index + 1, state, result);

            // Remove the last letter to backtrack (revert choice)
            state.deleteCharAt(state.length() - 1);
        }
    }

    public List<String> phoneCombinations(String digits) {

        // If the input digits are empty, return an empty result
        if (digits.isEmpty()) {
            return new ArrayList<>();
        }

        // List to store the combinations
        List<String> result = new ArrayList<>();

        // Temporary string to store the current combination (state)
        StringBuilder state = new StringBuilder();

        // Start the unconditional enumeration process from index 0
        generateCombinations(digits, 0, state, result);

        // Return the list containing all combinations
        return result;
    }
}
```

## Example Case Transformations

Given a string **s**, write a function that returns a list of all possible strings that can be created by transforming each letter in s individually to be either lowercase or uppercase. The output may be returned in **any order**.

```java
import java.util.*;

class Solution {

    private char toggleCase(char c) {

        // If the character is in lowercase, return the uppercase version
        if (Character.isLowerCase(c)) {
            return Character.toUpperCase(c);
        }

        // Otherwise, if the character is in uppercase, return the
        // lowercase version
        else {
            return Character.toLowerCase(c);
        }
    }

    private void generateTransformations(
        StringBuilder state,
        int index,
        List<String> result
    ) {

        // If index reaches the end of the string, store the current
        // transformation (solution state)
        if (index == state.length()) {
            result.add(state.toString());
            return;
        }

        // Recur without changing the current character (no choice)
        generateTransformations(state, index + 1, result);

        // If the current character is a letter, toggle its case and
        // recurse
        char currentChar = state.charAt(index);
        if (Character.isLetter(currentChar)) {

            // Toggle the case of the current character and recurse (make
            // choice)
            state.setCharAt(index, toggleCase(currentChar));

            // Recur with the next character (reduced input -> index + 1)
            generateTransformations(state, index + 1, result);

            // Revert the case back to the original character (revert
            // choice)
            state.setCharAt(index, currentChar);
        }
    }

    public List<String> caseTransformations(String s) {

        // List to store the transformations
        List<String> result = new ArrayList<>();

        // Temporary state as StringBuilder
        StringBuilder state = new StringBuilder(s);

        // Start the unconditional enumeration process from index 0
        generateTransformations(state, 0, result);

        // Return the list containing all transformations
        return result;
    }
}
```

# Pattern: Conditional Enumeration

unlike unconditional enumeration, in which choices at each step are independent of previous choices, in conditional enumeration, the set of choices at each step depends on the choices made in previous steps. To enumerate all solutions, we start from an initial state and, at each step, choose from a set of available choices to move to another state, eventually exploring the entire problem space.

>It is essential to note that any choice we make at a step is **dependent** on the choices we made earlier, and hence we call this process **conditional** enumeration.

>The conditional enumeration pattern is the classification of problems that can be solved using the conditional enumeration backtracking technique.

![[Pasted image 20251227215813.png]]

In conditional enumeration, we begin with an initial problem state defined by some state variables. At every step, we can make one of many **dependent** choices to reduce the size of the problem and move to another state. This process of making choices at every step is repeated recursively until we reach a solution state. As we make these choices and move from one state to another, we incrementally build the solution in some state variable.

Consider the state space tree below, where we have an initial problem state and `k` dependent choices that we can make at each step. The depth of the problem space is denoted by `n`, which is the maximum number of choices we must make to reach a solution state. At every step, making a different choice may lead to completely different solution states in the end. We recursively make a series of choices until we reach a solution state, then backtrack to update our choices. In this way, we visit every solution state exactly once.

We maintain a shared container as we explore the problem space, and add a solution state to it when we reach it. This way, when the entire problem space is explored, the container contains an enumeration of all solution states.

Instead of the state space tree, conditional enumeration can more easily be visualised as a linear list of nodes where the length of the list represents the depth of the problem space (`n`). We start from the first node, and we can move from one node to the next by making **one** of many (`k`) **dependent** choices.

We create a state variable `state` to incrementally build the solution based on the choices we make, using some function `f`. As we move closer to the end of the list by making a series of choices, the problem space is reduced, and the variable `state` aggregates the outcomes of all the previous choices. We also create another variable `control` that captures the effect of the previously made choices on subsequent choices using some function `g`. It is used at every step to determine the available choices to move to the next step. This way, each step accounts for the choices made in previous steps when computing the set of choices it can make to proceed.

The problem space is ultimately reduced to a solution state (base case in this case) when we reach the last node, and the variable `state` denotes the aggregated outcome of the series of choices made from the beginning to the end. It counts as one solution to the problem, and so we usually save the value of `state` in some container.

The goal of conditional enumeration is to enumerate all possible outcomes that can be reached by making all possible choices from start to end. As we will see later, we also usually have functions `fInverse` and `gInverse` to remove the contribution of the **last** choice made from `state` and `control` respectively. We use them undo previous choices and repeat the process, altering a choice in the sequence of choices until we collect all possible solutions.

### The conditional enumeration problem

Consider an example where the size of the problem space is represented by an integer `n` and we start from the initial problem state with some default values of the `state` and `control` variables. We can make multiple choices, denoted by an integer `choice` at every step, to reduce the problem space, and we update the `state` variable with those choices as we make them. We have the following functions that we can use.

- `getChoices` - Takes as an input the `control` variable and `n` and returns a list of choices we can make for the current input `n`.
- `makeChoice` - Takes as input the state variable `state` and a `choice` from the list of available choices and adds the contribution of `choice` to `state`.
- `updateControl` - Takes as input `n`, reference to `control` variable and the `choice` we make and adds the contribution of `choice` to `control`.
- `revertLastChoiceFromState` - Takes as input the state variable `state` and reverts the contribution of the last choice that was made.
- `revertLastChoiceFromControl` - Takes as input the control variable `control` and reverts the contribution of the last choice that was made.
- `getReducedInput` - Takes the current size of problem space `n` and the `control` variable as input and returns a value denoting the size of the reduced problem space.
- `isSolutionState` - Takes the current size of problem space `n` as input and returns true if it is a solution state.

Note how for conditional enumeration the `getReducedInput` and `getChoices` functions depend not only on the current size of the problem space, but also on the `control` variable that accounts for the previously made choices.

The goal is to find the exhaustive list of all possible outcomes that can be achieved by making all possible choices starting from the initial problem state.

Note that this is the generic conditional enumeration problem. Most of these functions and their definitions are very problem-specific. For example, in some problems, the `control` variable may be a primitive type and need not be shared across recursive calls; we can use local copies. In that case, the `updateControl` function would return a new copy of the updated control variable instead of updating the shared copy, and there would be no `revertLastChoiceFromControl` function.

### The conditional enumeration technique

To solve this problem, we create a recursive function `conditionalEnumeration` that takes as input the integer `n` denoting the problem space, a reference to the state variable `state`, a `control` variable accounting for the previously made choices, and a reference to a list `enumerations` to store all the solution states.

We initialize `state` and `control` to default values and `enumerations` to an empty list in the calling function and pass them as reference arguments to the function `conditionalEnumeration` along with the input `n`.

As we enter the function, we check if the current step is a solution state using `isSolutionState`. If the current step is a solution state, we add the current value of  `state` to the list `enumerations` and return to the caller.

If the current state is not a solution state, we use the function `getReducedInput` to get the next input for the reduced problem space in a variable `reducedInput`. Next, we use the function `getChoices` passing it the variables `n` and `control` to get a list of all the choices we can make to reduce the problem space. We then iterate through the list of all choices, and in each iteration, simulate making that choice by adding its contribution to `state` using `makeChoice` and updating the `control` variable using the `updateControl` function that accounts for this choice.

We then recursively call the same function with `reducedInput`, the updated `state` and the updated `control`. The same process is repeated recursively until it reaches a solution state, where we add the current value of `state` to the `enumerations` list. When a recursive call ends and control goes back to the caller, we revert the last choice made using `revertLastChoiceFromState` and `revertLastChoiceFromControl` on `state` and `control` variables respectively, and continue the iteration to make the next choice in exactly the same way.

Since we call `revertLastChoiceFromState` and `revertLstChoiceFromControl` after returning from **every** recursive call, it is guaranteed that the choice made before making a recursive call is the one that is reverted after returning from it.

This way, we simulate making a choice at every step until we reach a solution state, aggregate the consequences of all those choices in `state`, and add the final value of `state` (outcome) to the `enumerations` list. We also undo the choices in the same order they were made, so that backtracking to make different choices next time works the same way.

When all the recursive calls end, control is passed back to the caller of `conditionalEnumeration`, the `enumerations` list has the list of all outcomes from all choices, and the variables `state` and `control` are reverted to the default value with which they were initialized.

Consider the example below, where we start from a problem state where `n = 3` and the function `getReducedInput` reduces the input value by 1 until we reach the solution state `n = 1`. At every step the `getChoices` function returns two choices starting from the previously made choice itself. We enumerate all the choices that lead to a solution state starting from the problem state.

## Algorithm

The algorithm given below outlines the generic conditional-enumeration technique, making use of the functions `reduceInput`, `getChoices`, `makeChoice`, `updateControl`, `revertLastChoiceFromState`, `revertLastChoiceFromControl` and `isSolutionState`. All these functions and their implementations are problem-dependent.

All these functions and their implementations are highly problem-dependent, but the overall structure of the algorithm remains the same.

We also create a calling function that initializes the state variables `state`, `control` and `enumerations` with default values. It then passes them as a reference to the top-level recursive call. 

> **conditionalEnumeration(n, [ref] control, [ref] state, [ref] enumerations)**
> 
> - **Step 1:** Call `isSolutionState(n, state)` to check if it is a solution state. If yes, do the following:
>     - **Step 1.1:** Add `state` to the `enumerations` list
>     - **Step 1.2:** Return to the caller
> - **Step 2:** Set `choices` = Call `getChoices(n, control)` to get all choices available at this step.
> - **Step 3:** Iterate over `choices` using a variable `choice` and do the following:
>     - **Step 3.1:** Call `makeChoice(state, choice)` to add the contribution of `choice` to the `state` variable
>     - **Step 3.2:** Call `updateControl(n, control, choice)` to update the control variable based on the current choice and input `n`
>     - **Step 3.3:** Set `reducedInput` = Call `getReducedInput(n, control)` to obtain the reduced size of the problem space for the next recursive call
>     - **Step 3.4:** Call `conditionalEnumeration(reducedInput, control, state, enumerations)`
>     - **Step 3.5:** Call `revertLastChoiceFromControl(control)` to revert the contribution of the last choice from the control variable
>     - **Step 3.6:** Call `revertLastChoiceFromState(state)` to revert the contribution of the last choice from the state variable
> - **Step 4:** Return to the caller

> **callingFunction(n)**
> 
> - **Step 1:** Create a variable `state` and initialize it to some default value
> - **Step 2:** Create a variable `control` and initialize it to some default value
> - **Step 3:** Create an empty list `enumerations`
> - **Step 4:** Call `conditionalEnumeration(n, control, state, enumerations)`
> - **Step 5:** Return `enumerations`

## Implementation

```java
import java.util.ArrayList;
import java.util.List;

class Solution {

    public void conditionalEnumeration(
        int n,
        List<Integer> control,
        List<Integer> state,
        List<List<Integer>> enumerations
    ) {

        // Check if the current size of the problem space along with the state variable
        // represents a solution state
        if (isSolutionState(n, state)) {

            // The state contains the aggregation of all choices made so far
            // and therefore represents a complete solution
            enumerations.add(new ArrayList<>(state));
            return;
        }

        // Get all possible choices that can be made for the current input n
        // using the control variable
        List<Integer> choices = getChoices(n, control);

        // Iterate through each available choice
        for (int choice : choices) {

            // Update the state variable by applying the current choice
            makeChoice(state, choice);

            // Update the control variable based on the current choice and n
            updateControl(n, control, choice);

            // Reduce the size of the problem space based on the current control
            int reducedInput = getReducedInput(n, control);

            // Recur on the reduced problem space
            conditionalEnumeration(reducedInput, control, state, enumerations);

            // Revert the contribution of the last choice from control (backtracking)
            revertLastChoiceFromControl(control);

            // Revert the contribution of the last choice from state (backtracking)
            revertLastChoiceFromState(state);
        }
    }

    // Returns true if the current size of the problem space corresponds
    // to a solution state
    private boolean isSolutionState(int n, List<Integer> state) {
        return n == 0 || state.size() >= 3;
    }

    // Generates all possible choices that can be made for the current input n
    // using the control variable
    private List<Integer> getChoices(int n, List<Integer> control) {
        List<Integer> choices = new ArrayList<>();
        choices.add(control.size());
        choices.add(control.size() + 1);
        return choices;
    }

    // Updates the state variable by adding the contribution of the given choice
    private void makeChoice(List<Integer> state, int choice) {
        state.add(choice);
    }

    // Reverts the contribution of the most recent choice from the state variable
    private void revertLastChoiceFromState(List<Integer> state) {
        if (!state.isEmpty()) {
            state.remove(state.size() - 1);
        }
    }

    // Updates the control variable based on the given choice and input n
    private void updateControl(int n, List<Integer> control, int choice) {
        if (n % 2 == 0) {
            control.add(choice + n);
        } else {
            control.add(choice - n);
        }
    }

    // Reverts the contribution of the most recent choice from the control variable
    private void revertLastChoiceFromControl(List<Integer> control) {
        if (!control.isEmpty()) {
            control.remove(control.size() - 1);
        }
    }

    // Returns the reduced size of the problem space for the next recursive call
    // based on the current input n and the control variable
    private int getReducedInput(int n, List<Integer> control) {
        return n - 1;
    }
}
```

## Example String permutations

```java
import java.util.*;

class Solution {

    private void swap(StringBuilder str, int left, int right) {

        // Storing the left and right character of string
        char leftChar = str.charAt(left), rightChar = str.charAt(right);
        str.setCharAt(left, rightChar);
        str.setCharAt(right, leftChar);
    }

    private void generatePermutations(
        StringBuilder state,
        int index,
        List<String> result
    ) {

        // If index reaches the end of the string, we have found a
        // permutation (solution state)
        if (index == state.length()) {

            // Add the current permutation (string) to the result list
            result.add(state.toString());

            // Return to continue exploring other possibilities
            return;
        }

        // Loop through the characters starting from the current index
        // to generate permutations (dynamic choices)
        for (int i = index; i < state.length(); i++) {

            // Swap the characters at the current index and i to create a
            // new permutation (make choice)
            swap(state, index, i);

            // Recursively call generate for the remaining characters
            // (reduced input -> index + 1)
            generatePermutations(state, index + 1, result);

            // Swap back the characters to revert to the original string
            // (revert choice)
            swap(state, index, i);
        }
    }

    public List<String> stringPermutations(String s) {

        // List to store the permutations
        List<String> result = new ArrayList<>();

        // Convert string to StringBuilder for easy swapping
        StringBuilder state = new StringBuilder(s);

        // Start the conditional enumeration process from index 0
        generatePermutations(state, 0, result);

        // Return the list containing all permutations
        return result;
    }
}
```

## Example  Target Sum Combinations

Given an array **arr** that contains distinct integers and an integer **target**, write a function to return a list of all unique combinations of the numbers in arr that add up to the target. You can return the list of combinations in **any order**.

```java
import java.util.*;

class Solution {

    private void generateCombinations(
        int[] arr,
        int target,
        int start,
        List<Integer> state,
        List<List<Integer>> result
    ) {

        // If the current combination adds up to the target, store it
        // (solution state)
        if (target == 0) {

            // Store the current combination
            result.add(new ArrayList<>(state));

            // Return to continue exploring other possibilities
            return;
        }

        // Loop through all possible choices starting from 'start' index
        for (int i = start; i < arr.length; i++) {

            // Skip numbers greater than the remaining target
            if (arr[i] > target) {
                continue;
            }

            // Include the current number in the combination (make
            // choice)
            state.add(arr[i]);

            // Recurse with updated target
            // Note: 'i' is passed to allow reuse of the same number
            generateCombinations(arr, target - arr[i], i, state, result);

            // Backtrack by removing the last added number (revert
            // choice)
            state.remove(state.size() - 1);
        }
    }

    public List<List<Integer>> targetSumCombinations(
        int[] arr,
        int target
    ) {

        // Sort the array to ensure combinations are generated in
        // ascending order
        Arrays.sort(arr);

        // List to store all valid combinations (solution states)
        List<List<Integer>> result = new ArrayList<>();

        // Temporary list to store the current combination (state)
        List<Integer> state = new ArrayList<>();

        // Start the conditional enumeration (backtracking) process from
        // index 0 control: the starting index for choices at each step
        int start = 0;

        // Begin generating combinations
        generateCombinations(arr, target, start, state, result);

        // Return the list of all valid target sum combinations
        return result;
    }
}

```

## Example Generate parentheses

Given a positive integer **n**, write a function to generate and return a list of all possible combinations of well-formed parentheses with n pairs. You can return the output in **any order**.

```java
import java.util.*;

class Solution {

    private void generateCombinations(
        int n,
        int open,
        int close,
        StringBuilder state,
        List<String> result
    ) {

        // If the current combination has used all n pairs of parentheses
        // (solution state)
        if (state.length() == 2 * n) {

            // Store the valid combination
            result.add(state.toString());

            // Return to continue exploring other possibilities
            return;
        }

        // If we can add an open parenthesis, do so and recurse
        if (open < n) {

            // Add an open parenthesis (make choice)
            state.append('(');

            // Recurse with updated open count (reduced input -> open +
            // 1)
            generateCombinations(n, open + 1, close, state, result);

            // Backtrack (remove the last added parenthesis / revert
            // choice)
            state.deleteCharAt(state.length() - 1);
        }

        // If we can add a close parenthesis, do so and recurse
        if (close < open) {

            // Add a close parenthesis (make choice)
            state.append(')');

            // Recurse with updated close count (reduced input -> close +
            // 1)
            generateCombinations(n, open, close + 1, state, result);

            // Backtrack (remove the last added parenthesis / revert
            // choice)
            state.deleteCharAt(state.length() - 1);
        }
    }

    public List<String> generateParentheses(int n) {

        // List to store all valid combinations
        List<String> result = new ArrayList<>();

        // StringBuilder to build the current combination of parentheses
        // (state)
        StringBuilder state = new StringBuilder();

        // Start the conditional enumeration process with 0 open and 0
        // close parentheses control: number of open parentheses used
        int open = 0;

        // control: number of close parentheses used
        int close = 0;

        // Begin generating parentheses combinations
        generateCombinations(n, open, close, state, result);

        // Return the list of all valid parentheses combinations
        return result;
    }
}

```

## Example Generate IP addresses

Given a string **s** which consists only of digits, write a function to find and return a list of all possible valid IP addresses that can be formed by adding dots into the string. You can return the answer in **any order**.

Each IP address must have exactly four integers separated by single dots and each integer must be between `0` and `255` (inclusive). The IP address must not contain any leading zeros. This means that, for example, `0.1.2.201` is valid, but `00.1.2.201` is not.

```java
import java.util.*;

class Solution {

    private String join(List<String> parts) {
        return (
            parts.get(0) +
            "." +
            parts.get(1) +
            "." +
            parts.get(2) +
            "." +
            parts.get(3)
        );
    }

    private boolean isValidPart(String part) {

        // Leading zeros are invalid unless the part is exactly "0"
        if (part.length() > 1 && part.charAt(0) == '0') {
            return false;
        }

        // Convert part to integer and check range
        int value = Integer.parseInt(part);

        // Valid if in the range 0-255
        return value >= 0 && value <= 255;
    }

    private void generateCombinations(
        String s,
        int start,
        List<String> state,
        List<String> result
    ) {

        // If the current state has 4 segments, check for solution
        if (state.size() == 4) {

            // If all characters in the string are used, store the
            // solution
            if (start == s.length()) {
                result.add(join(state));
            }

            // Return to continue exploring other possibilities
            return;
        }

        // Loop through possible substring lengths (1 to 3)
        for (int len = 1; len <= 3; ++len) {

            // Ensure we do not exceed the bounds of the string
            if (start + len > s.length()) {
                break;
            }

            // Extract the substring for the current segment
            String part = s.substring(start, start + len);

            // Only proceed if the current part is valid
            if (isValidPart(part)) {

                // Include the current part in the state (make choice)
                state.add(part);

                // Recurse with updated control (next starting index)
                generateCombinations(s, start + len, state, result);

                // Backtrack by removing the last added part (revert
                // choice)
                state.remove(state.size() - 1);
            }
        }
    }

    public List<String> generateIPAddresses(String s) {

        // List to store all valid IP addresses (solution states)
        List<String> result = new ArrayList<>();

        // Temporary list to store the current IP segments (state)
        List<String> state = new ArrayList<>();

        // Start the conditional enumeration (backtracking) process from
        // index 0 control: starting index for substring choices
        int start = 0;

        // Begin generating IP addresses
        generateCombinations(s, start, state, result);

        // Return the list of all valid IP addresses
        return result;
    }
}
```
# Backtracking Search

In some cases, there may be many solution states, but we only need to find one. We start from an initial problem state and, at each step, choose from a set of available choices to move to another state, eventually exploring the entire problem space. Every time we move to a new state, we determine its validity and if it is a solution state by validating it against some constraints. As soon as we reach a solution state, we halt further exploration and return it as the solution to the problem.

It is essential to note that any choice we make at a step may be either independent or dependent on the choices we made earlier.

The search pattern is the classification of problems that can be solved using backtracking to search for solution states in a problem space.

## Searching using backtracking

Consider the state space tree below, where we have an initial problem state and `k` dependent choices that we can make at each step. The depth of the problem space is denoted by `n`, which is the maximum number of choices we must make to reach a solution state.

At every step, making a different choice may lead to completely different solution states in the end. We recursively make a series of choices until we reach a solution state. Once we reach a solution state, we terminate the search and return it as the solution, and so, we don't need to explore the entire problem space.

Note that each step may have a different number of choices, and those choices may be independent or dependent on previously made choices. We only show `k` choices in the state space tree below to make it simpler and easier to understand.

We create a state variable `state` to record the outcome of choices we make to reach a solution state, starting from the initial state, using some function `f`. At each step, we check if the current step is a solution state. If it is a solution state, we store the `state` variable in a `solution` container and terminate further search.

We also create another variable `control` that captures the effect of the previously made choices on subsequent choices using some function `g`. It is used at every step to determine the available choices to move to the next step. This way, each step accounts for the choices made in previous steps when computing the set of choices it can make to proceed.

The goal of the search problem is to find **any** solution state that can be reached by making any valid set of choices from the initial state. In the above example, we did not have to backtrack as we reached the solution state 

As we will see later, we also usually have functions `fInverse` and `gInverse` to remove the contribution of the **last** choice made from `state` and `control` respectively. We use them to undo previous choices and make new, different choices when we have no further choices left to move on from a step.

It is important to note that some series of choices may reach a solution state earlier than others, and so the order of making the choices matters in most cases. The goal of the search problem is to find any solution state, and so we terminate further exploration when we find a solution state.

### The search problem

Consider an example where the problem space is represented by an integer `n` , and we start from the initial problem state with some default values of the `state` and `control` variables. We can make multiple choices, denoted by an integer `choice` at every step, to reduce the problem space, and we update the `state` variable with those choices as we make them. The goal is to find **any** solution state and the sequence of choices that lead to it, starting from the initial problem state.

We have the following functions that we can use.

- `getChoices ( control, n )` - Takes as an input the `control` variable and the current problem space `n` and returns a list of choices we can make.
- `makeChoice (state, choice)` - Takes as input the state variable `state` and a `choice` from the list of available choices and adds the contribution of `choice` to `state`.
- `updateControl (control, choice)` - Takes as input the current problem space `n`, reference to the variable `control` and the `choice` we decide to make and adds the contribution of `choice` to `control`.
- `revertLastChoiceFromState (state)` - Takes as input the variable `state` and reverts the contribution of the last choice that was made from it.
- `revertLastChoiceFromControl (control)` - Takes as input the variable `control` and reverts the contribution of the last choice that was made from it.
- `getReducedProblemSpace (n, choice)` - Takes as input the current problem space `n` and the `choice` we decide to make, and returns a value denoting the reduced problem space.
- `isSolutionState (n)` - Takes as input the current problem space `n` and returns true if it is a solution.

### The search technique

To solve this problem, we create a recursive function `search` that takes as input the integer `n` denoting the problem space, a reference to the state variable `state`, a `control` variable accounting for the previously made choices, and a reference to a variable `solution` to the solution state. We initialize `state` and `control` to default values and `solution` to a sentinel value in the calling function and pass them as reference arguments to the function `search` along with the input `n`.

As we enter the function, we check if the current step is a solution state using `isSolutionState`. If the current step is a solution state, we set the value of `solution` to `state` and return to the caller.

If the current state is not a solution state, we use the function `getChoices` passing it the variables `n` and `control` to get a list of all the choices we can make to reduce the problem space. We then iterate through the list of all choices, using a variable `choice`, and in each iteration, simulate making that choice by adding its contribution to `state` using `makeChoice` and updating the `control` variable using the `updateControl` function that accounts for this choice. We then use the function `getReducedProblemSpace` passing it `n` and the `choice` to get the reduced problem space in a variable `reducedProblemSpace`. 

We then recursively call the `search` function with `reducedProblemSpace`, the updated `state` and the updated `control`. The same process is repeated recursively until it reaches a solution state, where we set the current value of `state` to `solution`. When a recursive call ends and control goes back to the caller, we revert the last choice made using `revertLastChoiceFromState` and `revertLastChoiceFromControl` on `state` and `control` variables respectively. We then check if `solution` still has the sentinel value it was initialized with.

If yes, it means we have not found the solution, and so, we continue the iteration to make the next choice in exactly the same way. On the other hand, if `solution` does not have the sentinel value, it means a solution state was found, and we should terminate further search. In this case, we return to the caller.

Since we call `revertLastChoiceFromState` and `revertLstChoiceFromControl` after returning from **every** recursive call, it is guaranteed that the choice made before making a recursive call is the one that is reverted after returning from it.

This way, we simulate making a choice at every step until we reach a solution state, aggregate the consequences of all those choices in `state`, and add the final value of `state` (outcome) to `solution`. We also undo the choices in the same order they were made, so that backtracking to make different choices next time works the same way.

When all the recursive calls end, control is passed back to the caller of `search`, the solution variable holds the solution to the problem if it exists; otherwise, it holds the sentinel value it was initialized with.

## Algorithm

The algorithm given below outlines the generic search technique, making use of the functions `reduceInput`, `getChoices`, `makeChoice`, `updateControl`, `revertLastChoiceFromState`, `revertLastChoiceFromControl` and `isSolutionState`. All these functions and their implementations are problem-dependent.

All these functions and their implementations are highly problem-dependent, but the overall structure of the algorithm remains the same.

We also create a calling function that initializes the variables `state`, `control`, `choices`, and `solution` with default and sentinel values, and makes the top-level recursive call.

> **search(n, [ref] control, [ref] state, [ref] solution)**
> 
> - **Step 1:** Call `isSolutionState(n, state)` to check if it is a solution state.
>     - **Step 1.1:** If true, set `solution` = `state`
>     - **Step 1.2:** Return to the caller
> - **Step 2:** Set `choices` = Call `getChoices(n, control)` to get all choices available at this step.
> - **Step 3:** Iterate over `choices` using a variable `choice` and do the following:
>     - **Step 3.1:** Call `makeChoice(state, choice)` to add the contribution of `choice` to the `state` variable
>     - **Step 3.2:** Call `updateControl(n, control, choice)` to update the control variable based on the current choice and input `n`
>     - **Step 3.3:** Set `reducedProblemSpace` = Call `getReducedProblemSpace(n, choice)` to obtain the reduced problem space for the next recursive call
>     - **Step 3.4:** Call `search(reducedProblemSpace, control, state, solution)`
>     - **Step 3.5:** Call `revertLastChoiceFromControl(control)` to revert the contribution of the last choice from the control variable
>     - **Step 3.6:** Call `revertLastChoiceFromState(state)` to revert the contribution of the last choice from the state variable
>     - **Step 3.7:** If `solution` does not have the sentinel value, return to the caller, otherwise go to the next steps
> - **Step 4:** Return to the caller
> 
> **callingFunction(n)**
> 
> - **Step 1:** Create a variable `state` and initialize it to a default value
> - **Step 2:** Create a variable `control` and initialize it to a default value
> - **Step 3:** Create a variable `solution` and initialize it with some sentinel value
> - **Step 4:** Call `search(n, control, state, solution)`
> - **Step 5:** Return `solution`

## Implementation

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {

    public void search(
        int n,
        List<Integer> control,
        List<Integer> state,
        List<List<Integer>> solution
    ) {

        // Check if the current size of the problem space along with the state variable
        // represents a solution state
        if (isSolutionState(n, state)) {

            // The state contains the aggregation of all choices made so far
            // and therefore represents a complete solution
            solution.add(new ArrayList<>(state));
            return;
        }

        // Get all possible choices that can be made for the current input n
        // using the control variable
        List<Integer> choices = getChoices(n, control);

        // Iterate through each available choice
        for (int choice : choices) {

            // Update the state variable by applying the current choice
            makeChoice(state, choice);

            // Update the control variable based on the current choice and n
            updateControl(n, control, choice);

            // Reduce the problem space based on the current choice
            int reducedProblemSpace = getReducedProblemSpace(n, choice);

            // Recur on the reduced problem space
            search(reducedProblemSpace, control, state, solution);

            // Revert the contribution of the last choice from control (backtracking)
            revertLastChoiceFromControl(control);

            // Revert the contribution of the last choice from state (backtracking)
            revertLastChoiceFromState(state);

            if (!solution.isEmpty()) {
                // Terminate further search as a solution has been found
                return;
            }
        }
    }

    // Returns true if the current size of the problem space corresponds
    // to a solution state
    private boolean isSolutionState(int n, List<Integer> state) {
        return n == 0 || state.size() >= 3;
    }

    // Generates all possible choices that can be made for the current input n
    // using the control variable
    private List<Integer> getChoices(int n, List<Integer> control) {
        return Arrays.asList(control.size(), control.size() + 1);
    }

    // Updates the state variable by adding the contribution of the given choice
    private void makeChoice(List<Integer> state, int choice) {
        state.add(choice);
    }

    // Reverts the contribution of the most recent choice from the state variable
    private void revertLastChoiceFromState(List<Integer> state) {
        if (!state.isEmpty()) {
            state.remove(state.size() - 1);
        }
    }

    // Updates the control variable based on the given choice and input n
    private void updateControl(int n, List<Integer> control, int choice) {
        if (n % 2 == 0) {
            control.add(choice + n);
        } else {
            control.add(choice - n);
        }
    }

    // Reverts the contribution of the most recent choice from the control variable
    private void revertLastChoiceFromControl(List<Integer> control) {
        if (!control.isEmpty()) {
            control.remove(control.size() - 1);
        }
    }

    // Returns the reduced problem space for the next recursive call
    // based on the current input n and the choice
    private int getReducedProblemSpace(int n, int choice) {
        return n - choice;
    }
}

```

## Example Rat in a Maze

Given a 2D integer **maze** of size **N** * **M** with walkable space denoted by `0` and obstacles denoted by `1`. A rat is placed at index `(0, 0)`, and a function is written to find and return a string containing the path the rat can take to reach the destination at coordinates `(N - 1, M - 1)`. As multiple correct answers can exist, the judge will output `true` if your function returns one of the correct paths. Otherwise, it will output `false`.

```java
class Solution {

    // Stores the final path found (any one valid path)
    private String answer = "";

    private void searchPath(
        int[][] maze,
        int row,
        int col,
        StringBuilder state,
        int rows,
        int cols
    ) {

        // If a solution is already found, stop further exploration
        // (early return)
        if (!answer.isEmpty()) {
            return;
        }

        // Invalid move check: boundaries or blocked cell
        if (
            row < 0 ||
            col < 0 ||
            row >= rows ||
            col >= cols ||
            maze[row][col] != 0
        ) {
            return;
        }

        // Solution found: reached bottom-right corner
        if (row == rows - 1 && col == cols - 1) {

            // Store the found state as the answer
            answer = state.toString();

            // Stop further exploration
            return;
        }

        // Make choice: mark current cell as visited
        // Store original value to revert later
        int cellValue = maze[row][col];

        // Mark as visited
        maze[row][col] = -1;

        // Explore all four directions (choices)

        // Move Up (make choice)
        state.append('U');
        searchPath(maze, row - 1, col, state, rows, cols);
        state.deleteCharAt(state.length() - 1);

        // Move Down (make choice)
        state.append('D');
        searchPath(maze, row + 1, col, state, rows, cols);
        state.deleteCharAt(state.length() - 1);

        // Move Left (make choice)
        state.append('L');
        searchPath(maze, row, col - 1, state, rows, cols);
        state.deleteCharAt(state.length() - 1);

        // Move Right (make choice)
        state.append('R');
        searchPath(maze, row, col + 1, state, rows, cols);
        state.deleteCharAt(state.length() - 1);

        // Revert choice: unmark current cell to allow other paths
        maze[row][col] = cellValue;
    }

    public String ratInAMaze(int[][] maze) {
        int rows = maze.length;
        int cols = maze[0].length;

        // Current path (state) represented as a StringBuilder
        StringBuilder state = new StringBuilder();

        // Start the search from the top-left corner (0,0)
        searchPath(maze, 0, 0, state, rows, cols);

        // Return the found state as the answer
        return answer;
    }
}
```

## Example  Word Quest

Given a 2D array **board** containing alphabets of the English language and a string called **word**. Write a function to check whether the word exists on the board. Return `true` if the word exists, or else return `false`.

```java
import java.util.*;

class Solution {

    private boolean searchWord(
        char[][] board,
        String word,
        int index,
        int row,
        int col
    ) {

        // If index reaches word length, we have successfully
        // found the entire word (solution state)
        if (index == word.length()) {
            return true;
        }

        // Check if current position is out of bounds or does not match
        // the character we are looking for
        if (
            row < 0 ||
            col < 0 ||
            row >= board.length ||
            col >= board[0].length ||
            board[row][col] != word.charAt(index)
        ) {

            // Dead end, backtrack
            return false;
        }

        // Store the original value before marking as visited
        char originalChar = board[row][col];

        // Mark current cell as visited by replacing it with a special
        // character so that it is not reused in this path
        board[row][col] = '#';

        // Recursively explore all four possible directions (down, up,
        // right, left) for the next character in the word (make choice)
        if (

            // Move Down
            searchWord(board, word, index + 1, row + 1, col) ||

            // Move Up
            searchWord(board, word, index + 1, row - 1, col) ||

            // Move Right
            searchWord(board, word, index + 1, row, col + 1) ||

            // Move Left
            searchWord(board, word, index + 1, row, col - 1)
        ) {
            return true;
        }

        // Backtrack: restore the original value to allow other paths
        // to use this cell
        board[row][col] = originalChar;

        // Return whether the word has been found along this path
        return false;
    }

    public boolean wordQuest(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;

        // Start backtracking search from every cell on the board
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {

                // Begin searching from cell (row, col)
                if (searchWord(board, word, 0, row, col)) {

                    // If a solution is found, immediately return true
                    return true;
                }
            }
        }

        // If no path leads to the word, return false
        return false;
    }
}
```

## Example  Solve N queens

Given a positive integer **n**, Write a function to find and return all possible distinct solutions of the n queen puzzle. Each solution should show a unique configuration of the queens' placement on the chessboard, where the letter `Q` represents a queen and `.` represents an empty space. You can return the answer in **any order**.

The n-queens puzzle involves placing **n** queens on an **n x n** chessboard so that no two queens can attack each other.

```java
import java.util.*;

class Solution {

    // Helper function to check if a queen can be safely placed at (row,
    // col)
    private boolean canPlaceQueen(int[] state, int row, int col) {
        for (int i = 0; i < row; i++) {

            // Check for column conflict: no other queen should be in the
            // same column Check for diagonal conflict: no other queen
            // should be in the same diagonal
            if (
                state[i] == col ||
                row - i == Math.abs(col - state[i])
            ) {
                return false;
            }
        }
        return true;
    }

    // Helper function to convert the current state list into a board
    // representation
    private List<String> makeSolution(int[] state, int n) {

        // Create an n x n board initialized with '.'
        List<String> board = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            char[] row = new char[n];
            Arrays.fill(row, '.');

            // Place queen
            row[state[i]] = 'Q';
            board.add(new String(row));
        }

        // Return the board representation
        return board;
    }

    private void searchSolution(
        int[] state,
        int row,
        int n,
        List<List<String>> result
    ) {

        // Check if all queens have been successfully placed
        if (row == n) {

            // Current state represents a valid solution, convert it to
            // board format and store
            result.add(makeSolution(state, n));

            // Stop searching further as we found a valid solution
            return;
        }

        // Loop through each column in the current row to try placing a
        // queen
        for (int col = 0; col < n; col++) {

            // Check if placing a queen at (row, col) is safe
            if (canPlaceQueen(state, row, col)) {

                // Place the queen in the current row at column col (make
                // choice)
                state[row] = col;

                // Recursively try to place queens in the next row
                searchSolution(state, row + 1, n, result);

                // Remove the queen from the current row to backtrack and
                // try the next column (revert choice)
                state[row] = -1;
            }
        }
    }

    public List<List<String>> solveNQueens(int n) {

        // List to store all valid board configurations (solution states)
        List<List<String>> result = new ArrayList<>();

        // State list: state[i] stores the column index of the queen
        // placed in row i
        int[] state = new int[n];
        Arrays.fill(state, -1);

        // Start the search process from the first row (row 0)
        searchSolution(state, 0, n, result);

        // Return all valid solutions found
        return result;
    }
}

```

## Example  Solve sudoku

Given a `9X9` 2D array **board** representing a partially filled Sudoku puzzle, write a function to return the solution for the puzzle by filling the empty cells. A valid solution to the Sudoku puzzle must abide by the following rules:

> - Each digit from `1` to `9` must appear exactly once in each row.
> - Each digit from `1` to `9` must appear exactly once in each column.
> - Each digit from `1` to `9` must appear exactly once in each of the `9` `3x3` sub-boxes of the grid.

```java
class Solution {

    // Checks if placing 'num' in the specified row is valid
    private boolean isValidRow(String[][] board, int row, String num) {
        for (int col = 0; col < 9; col++) {
            if (board[row][col].equals(num)) {
                return false;
            }
        }
        return true;
    }

    // Checks if placing 'num' in the specified column is valid
    private boolean isValidCol(String[][] board, int col, String num) {
        for (int row = 0; row < 9; row++) {
            if (board[row][col].equals(num)) {
                return false;
            }
        }
        return true;
    }

    // Checks if placing 'num' in the 3x3 sub-grid containing (row, col)
    // is valid
    private boolean isValidSubGrid(
        String[][] board,
        int row,
        int col,
        String num
    ) {
        int startRow = (row / 3) * 3;
        int startCol = (col / 3) * 3;

        for (int r = startRow; r < startRow + 3; r++) {
            for (int c = startCol; c < startCol + 3; c++) {
                if (board[r][c].equals(num)) {
                    return false;
                }
            }
        }
        return true;
    }

    // Checks if placing 'num' at (row, col) is valid in all respects
    private boolean isValidPlacement(
        String[][] board,
        int row,
        int col,
        String num
    ) {

        // Check row, column, and sub-grid constraints
        return (
            isValidRow(board, row, num) &&
            isValidCol(board, col, num) &&
            isValidSubGrid(board, row, col, num)
        );
    }

    // Recursive search function to fill the Sudoku board
    private boolean searchSolution(String[][] board) {

        // Iterate through each cell of the board
        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {

                // Only attempt to fill empty cells
                if (board[row][col].equals("X")) {

                    // Try all digits from "1" to "9" in this cell
                    for (int num = 1; num <= 9; num++) {
                        String strNum = Integer.toString(num);

                        // Check if placing the number is valid (solution
                        // state possible)
                        if (isValidPlacement(board, row, col, strNum)) {

                            // Place the number in the cell (make choice)
                            board[row][col] = strNum;

                            // Recursively attempt to fill the rest of
                            // the board
                            if (searchSolution(board)) {

                                // If successful, propagate success back
                                return true;
                            }

                            // If it did not lead to a solution, remove
                            // the number (revert choice)
                            board[row][col] = "X";
                        }
                    }

                    // If no valid number can be placed in this cell,
                    // backtrack
                    return false;
                }
            }
        }

        // If all cells are filled successfully, the board is solved
        return true;
    }

    public void solveSudoku(String[][] board) {

        // Start the search process to fill the board
        searchSolution(board);
    }
}

```

