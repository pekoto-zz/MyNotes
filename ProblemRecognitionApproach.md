# Problem Recognition Patterns (in progress)

## General Techniques

### 1. Brute force first
Go for a brute force solution first, identify the bottleneck (largest big O), then think about how you could get rid of it (see __Optimization Techniques__ below).

If you are dealing with a recursive or backtracking problem, solve the problem first, and then think about memoization or dynamic programming.

### 2. Algorithm first, then code.
Think about the algorithm first, and then think about what this would look like in code. Think about the general algorithm you, a human being, would use to solve the problem, and then think about what this would look like in code. Trying to do both at once can tangle you in knots for complex problems. If you at least demonstrate you understand the algorithm, you demonstrate you can solve problems.

### 3. Data structure brainstorm
Run through common data structures to see if they would help: maps, heaps, tries, trees, lists.

### 4. Dealing with connected data
Do you need to count connected data in some way? (E.g., count 1s in a matrix). Use a breadth-first search or depth-first search. Rememeber that DFS is recursive, so could run out of stack memory.

### 5. Dealing with related but unconnected data
Do you need to count related data in some way, but the data is not fully connected? (E.g., count name frequency given a list of pairs of different name spellings). Try connecting the data as a graph and then doing a depth-first search to count the connected components.

### 6. Find permutations/paths
If you have to find some permutations, the problem is likely recursive. Remember the general algorithm:
* Identify the base case (nowhere left to go/nothing left to process/target value found)
* Pick a thing from your collection
* Recurse with that thing removed from the collection
* Put the thing back in your collection

[Best resource: Marty Stepp's videos](https://www.youtube.com/user/martystepp/videos)

After you have come up with the general recursive algorithm, think about how you can cache some values in a map or array (memoization).

### 7. Returning the next something...
If you need to return the next something (.e.g, daily temperatures problem), consider using a stack since this will return the most recent thing you visited. What happens if you iterate backwards and put on the stack? -- you get the next.

If you have to keep track of the lowest/highest something, and keep the data ordered (e.g., buy/sell stocks, 3-digit increasing substring), consider setting the element as the min/max, and then comparing to the next element. If you need three elements, you can set element 1 to the min, check if the next one is greater than min and less than current second highest, etc.

### 8. Think small
Usually a small example will be enough to prove an algorithm wrong. Also, picking small, simple examples that you can solve by hand will help you spot patterns to crack the algorithm. Likewise, if you're having trouble with a given example, try a simpler example: an array with 1 or 2 elements, etc.

### 9. Think exhaustively
What possible cases do you have? For example, if looking at overlapping intervals, there are only 3 ways 2 intervals can be:

* Disjoint (one after another)
* Overlapping (one starts before another ends, but after it start)
* Nested (one starts after another starts, and ends before it ends)

### 10. Model on existing
Can you model your problem on some existing algorithm? What does it look like?

### 11. Identify the pain point
If you are doing some work repeatedly -- choosing the max or min, say -- can you find a data structure to make that more efficient?

### 12. Relax some constraints
For example, if it's hard to find the closest sum, could you instead try to find the exact sum?

## Optimization Techniques
1. Do you need an O(n) runtime? Forget about sorting. Can you store data in a map instead?
2. Do you need to use O(1) space? Does sorting the data help?
3. Do you need an O(n) runtime and O(1) space? Then you probably need to mark the data in the original data structure somehow. For example, by setting it to negative. Remember, you can run through a data structure multiple times.
4. Does traversing the data backwards make things easier?
5. If it's a linked list problem, what would happen if you used a two pointer approach?
6. If you're dealing with trees, think recursion.
7. Do you need to keep a running track of a minimum or maximum value? Think heaps. In Java, `PriorityQueue` doesn't support remove in log n time. Instead you can use a `TreeMap` (Red-black tree implementation), which will keep track of the min or max in log n time, and also allow for log n removals.
8. If you have to reimplement a mathematical operation without using operators, you will probably have to use bit manipulation. Break down the basics of the operation to work out what is going on with the numbers, and then think about how you would replicate that using bitwise operators.
9. Are you dealing with a limited range of ints -- temperatures, numbers, etc.?
Then you might be able to stick them in a fixed size array or map with counts or indexes. Then when you iterate that for each element you will still get a fixed-time runtime.

## String processing

# __TODO__:
Trie notes
Suffix trie notes
Suffix array notes

### Common edge cases
1. Null
2. Empty.
3. Length 1
4. Uppercase/lowercase/mixed?
5. Special characters (e.g., accented a)
6. All characters same
7. Whitespace
8. If parsing, what if the token is contained as part of the element we wanted to parse out (e.g., string split by spaces, but name has a space in it)
9. Last part not processed (e.g., imagine calculator app -- it ends in a number and no operator, do you still process this last number?)
10. Creating a new string every time instead of using `StringBuffer`

## Dynamic Programming
Dynamic programming is useful when we satisfy the __principle of optimality__. That is, partial solutions can be optimally extended without worrying about the specifics of that partial solution.

For example, when working out edit distance, we care about what the previous min edit distance was, and we don't have some constraint relating to the that previous partial solution, like, you can only make 2 deletes, etc.

## Tree problems

```
// Sample tree:

         6
        / \
       4   7
      / \   \
     3   5   8
```

### Preorder traversal
```java
doSomething(node);
visit(node.left);
visit(node.right);

// Output: 6, 4, 3, 5, 7, 8
```

__Note:__ Useful for serializing and deserializing a binary tree. Go through the tree adding each node to a queue, and X for null.
Then go through the queue recursively to rebuild the tree.

### Inorder traversal
```java
visit(node.left);
doSomething(node);
visit(node.right);

// Output: 3, 4, 5, 6, 7, 8
```

__Note:__ In a BST, inorder traversal will give you the nodes in sorted order.

### Postorder traversal
```java
visit(node.left);
visit(node.right);
doSomething(node);

// Output: 3, 5, 4, 8, 7, 6
```

### Level-order traversal
Essentially this boils down a BFS.
1. Put the root on a queue
2. Get the size of the queue
3. Set up a loop to iterate _size_ times
4. On each iteration of the loop, get a node from the tree and add its children to the queue
5. Go to 1
6. Break when the queue is empty

This can be used for various things: printing level-order, check if each level is symmetrical, "inverting" the children at each level, etc.

### Bottom-up recursion
Use an inorder traversal.
Go down to the bottom of the tree first, and then count on the way back up.

For example, to get the height:

```java
public int getHeight(Node node) {
    if(node == null) {
        return 0;
    }

    int leftHeight = getHeight(node.left);
    int rightHeight = getHeight(node.right);
    
    return 1 + Math.max(leftHeight, rightHeight);
}
```

### Top-down recursion
Use a preorder traversal.
Check the value of this node, and then recurse for left and right.

For example, to get the longest increasing sequence:

```java

int max = Integer.MIN_VALUE;

public void getLongest(Node node, int lastValue, int length) {

   if(node == null) {
       return;
   }
   
   if(lastValue+1 == node.value) {
      length++;
      max = Math.max(max, length+1);
   } else {
      length = 1;
   }
    
   getLongest(node.left, node.value, length);
   getLongest(node.right, node.value, length);
}

```

### Getting distance from the root
This is useful when trying to find the distance between nodes, all nodes k nodes away, etc.

```java
public int getDistance(Node node, Node target) {
   if(node == null) {
       return -1;
   }
   
   if(node == target) {
       return 0;
   }
   
   int leftDist = getDistance(node.left, target);
   
   if(leftDist >= 0) {
      return leftDist+1;
   }
   
   int rightDist = getDistance(node.right, target);
   
   if(rightDist >= 0) {
      return rightDist+1;
   }
   
   return -1;
}
```

### Total nodes
The total nodes in a complete tree is (2^k)-1, where k is the height of the tree. E.g., a tree with height 3 will have 2^3  = 8-1 = 7 nodes.

### Tree Tips
* We often recurse when doing tree problems -- e.g., when getting the height. Can we also do something else while in the recursive method? For example, if finding the max diameter, we are finding the height of the left and right subtrees anyway, so we could also check to see if we have a new max diameter (left + right height) at the same time.

* It can often become confusing trying to pass some value (like ```java int max```) around. To make this easier for interview purposes, you can declare this value outside of the function.

* Don't forget inorder, preorder, and postorder traversals. These can often be used to find brute force solutions. E.g., find the highest, get in order, compare if trees are equal, check if contains subtree, etc. (these are rarely optimum solutions though).

## Permutation, Combination, and Subset Formulas

### Permutations with repeats
How many ways can you choose k elements from n elements.
Example: How many 4 digit pin numbers are there?

``` n^k. ```

Example:
How many ways can we choose a 4 digit PIN using 0-9?
10^4 = 10,000

### Permutations without repeats
How many permutations of k elements are there from a string containing n elements?

``` n!/(n-k)! ```

For example:
From ABC, how many length 2 permutations are there?
```
3!/(3-2)! = 6
AB
AC
BA
BC
CA
CB
```

__Note:__ This means for any string, where we choose all elements, there are ``` n! ``` permutations of that string.
3!/(3-3)! = 3!/0! = 6

```
ABC! = 3! = 6

ABC
ACB
BAC
BCA
CAB
CBA
```
### Unique permutations from a string with repeats
Given a string with repeated elements, how many unique permutations are there?

```  n!/(repeat element 1 count)!*(repeat element 2 count)!... ```
```
Example:
For {1, 1, 2, 3}, we have 4 elements, and 1 is repeated twice, so:
4!/2! = 24/2 = 12 unique permutations

1,1,2,3
1,1,3,2
1,2,1,3
1,2,3,1
1,3,2,1,
1,3,1,2
2,1,1,3
2,1,3,1
2,3,1,1
3,1,2,1
3,1,1,2
3,2,1,1
```
### Combinations without repeats
How many ways can you choose k elements from n, if order doesn't matter?
For example, how many ways can you choose 6 lottery numbers from 49.

``` n!/(n-k)!k! ```

49!/(49-6)!6! = 13,983,816

### Subsets
The number of subsets given some superset.
``` 2^n. ```

This is because for each element it can either be in the set or not.

For example, {1, 2, 3} = 2^3 = 8.
{}, {1}, {2}, {3}, {1, 2}, {1,3}, {2,3}, {1,2,3}

## Generating Permutations
This follows the basic recursive pattern:
1. Pick a thing, add it one set and remove it from the other
2. Recurse
3. Unpick the thing

But the "picking" stage is just swapping elements. You can see why this works when you logically generate all permutations:

```java
{1, 2, 3} // Swap each element with itself
{1, 3, 2} // Swap 3 with 2
{2, 1, 3} // Swap 1 with 2
{2, 3, 1} // Swap 3 with 1
...
```

```java
public void generatePermutations(int[] arr, int index, List<int[]> permutations) {
    
    if(index == arr.length) {
        permutations.add(arr.clone());
        return;
    }

    for(int i = index; i < arr.length; i++) {
       swap(arr, i, index);
       generationPermutations(arr, index+1, permutations);
       swap(arr, i, index);
    }
}
```

If we want to generate unique permutations in an array with duplicate elements, we can just check that ``` i != index && arr[i] != arr[index] ```.

What is the running time of this? Well, we have n! permutations. The inner loop takes n time, giving us n * n!. But recall that ``` arr.clone() ``` takes n time. So in total we have: n * (n * n!).

### String permutations
String permutations (and recursive String functions generally) have a slight tweak. Since creating a new String creates a new object in memory, you don't have to unchoose.

```java
// Initially called with generationPermutations("", "abc", results);

public void generatePermutations(String prefix, String suffix, List<String> permutations) {
    if(suffix.length() == 0) {
        permutations.add(prefix);
        return;
    }
    
    for(int i = 0; i < suffix.length(); i++) {
       generatePermutations(prefix + suffix.charAt(i),
                            suffix.substring(0, i) + suffix.substring(i+1, suffix.length()),
                            premutations);
    }
}
```

__Tip:__ If you are given the data in some other format, such as 2 arrays -- one containing a count of chars, and the other containing the chars, there are two options:

1. Just modify these 2 lists to be one list. E.g., turn {a, b, c}, {2, 1, 3} into the list {a, a, b, c, c, c} or String aabccc.
2. Alternatively, just use the same strategy -- to decide what to pick net you scan through the count array until you hit the first non-zero element starting from the current index.

## Generating subsets
Although inefficient, generating subsets can often be used to find a brute force solution (e.g., find min/max/closest set of things).

Essentially we use a recursive base case and build approach. When generating subsets, we take the empty set, add an element to it, and then add elements to those subsets, etc.

```java
{1, 2, 3} // Set

{} // Empty set
{1} // Empty set + 1
{2} // Empty set + 2
{1, 2} // Empty set + 1 + 2
{3} // Empty set + 3
{1, 3} // Empty set + 1 + 3
{2, 3} // Empty set + 2 + 3
{1, 2, 3} // Empty set + 1 + 2 + 3
```

```java

public List<List<Integer>> generateSubsets(int[] arr, int index) {

    if(index == arr.length) {
        List<Integer> emptySet = new ArrayList<>();
        List<List<Integer>> setOfSets = new ArrayList<List<Integer>>();
        setOfSets.add(emptySet);
        return setOfSets;
    }

    List<List<Integer>> subsets = generateSubsets(arr, index+1);
    
    int item = arr[index];
    
    List<List<Integer>> allSubsetsForThisItem = new ArrayList<List<Integer>>();
    
    for(List<Integer> subset : subsets) {
         List<Integer> subsetForThisItem = new ArrayList<Integer>();
         subsetForThisItem.addAll(subset);
         subsetForThisItem.add(item);
         allSubsetsForThisItem.add(subsetForThisItem);
    }
    
    // Add on the previous subsets
    allSubsetsForThisItem.addAll(subsets);

    return allSubsetsForThisItem;
}

```

Complexity: O(n*2^n)

## Sorting Summary

| Sort          | Time                           | Space         | Stable?       | Notes                                                  |
| ------------- | ------------------------------ | ------------- | ------------- | ------------------------------------------------------ |
| Quicksort     | n log n average, worst: n^2    | log n         | No            | Worst-case can be made very unlikely by shuffling data |
| Mergesort     | n log n                        |     n         | Yes           |                                                        |
| Heapsort      | n log n                        |     1         | Yes           | constant extra space if you use existing array, practically usually slower than QS due to operations                                                       |

## __TODO__: 
_General problem solving tips from other docs_

_Recursion & backtracking reminders_

_Sorting tips, summary table_

_Sliding window_

_Powers of 2s_

_estimating, important (max, min, GB, TB, etc.), sum of_

(Go through all docs to see what would be useful to summarise)

