# Problem Recognition Patterns (in progress)

- [Approaching Problems](#approaching-problems)
  * [Basic Steps](#basic-steps)
  * [Misc. Tips](#misc-tips)
  * [Optimization Techniques](#optimization-techniques)
- [Sorting](#sorting)
  * [Quicksort](#quicksort)
  * [Mergesort](#mergesort)
  * [Heapsort](#heapsort)
  * [Insertion sort](#insertion-sort)
  * [Counting sort](#counting-sort)
  * [Radix sort](#radix-sort)
- [String processing](#string-processing)
  * [Tries](#tries)
  * [KMP (Knuth-Morris-Pratt)](#kmp--knuth-morris-pratt-)
  * [Rabin-Karb](#rabin-karb)
  * [Suffix tree](#suffix-tree)
  * [Full-text indexing](#full-text-indexing)
  * [Iterating chars](#iterating-chars)
- [Tree problems](#tree-problems)
  * [Preorder traversal](#preorder-traversal)
  * [Inorder traversal](#inorder-traversal)
  * [Postorder traversal](#postorder-traversal)
  * [Level-order traversal](#level-order-traversal)
  * [Bottom-up recursion](#bottom-up-recursion)
  * [Top-down recursion](#top-down-recursion)
  * [Getting distance from the root](#getting-distance-from-the-root)
  * [Total nodes](#total-nodes)
  * [Tree Tips](#tree-tips)
- [Graph Algorithms](#graph-algorithms)
  * [Dijkstra](#dijkstra)
  * [Topological Sort](#topological-sort)
  * [Union-Find (Disjoint Set)](#union-find--disjoint-set-)
  * [Minimum Spanning Tree](#minimum-spanning-tree)
  * [Segment Tree](#segment-tree)
  * [Binary Indexed Tree](#binary-indexed-tree)
- [Algorithm Patterns](#algorithm-patterns)
  * [Finding a Missing Element](#finding-a-missing-element)
  * [Sliding Window](#sliding-window)
  * [Calculator/Stack parsing](#calculator-stack-parsing)
- [Java](#java)
  * [Custom Comparator](#custom-comparator)
  * [Implementing equals()](#implementing-equals--)
  * [Implementing Comparable](#implementing-comparable)
  * [Implementing iterator](#implementing-iterator)
  * [String/Int/Char Manipulation](#string-int-char-manipulation)
  * [Common functions](#common-functions)
  * [Tips](#tips)
- [Big O](#big-o)
  * [Recursive runtimes](#recursive-runtimes)
- [Maths](#maths)
  * [Permutation, Combination, and Subset Formulas](#permutation--combination--and-subset-formulas)
    + [Permutations with repeats](#permutations-with-repeats)
    + [Permutations without repeats](#permutations-without-repeats)
    + [Unique permutations from a string with repeats](#unique-permutations-from-a-string-with-repeats)
    + [Combinations without repeats](#combinations-without-repeats)
    + [Subsets](#subsets)
  * [Generating Permutations](#generating-permutations)
    + [String permutations](#string-permutations)
  * [Generating subsets](#generating-subsets)
  * [Powers of 2](#powers-of-2)
    + [Estimating](#estimating)
    + [Summing](#summing)
    + [Notable Powers](#notable-powers)
  * [Sum of 1...n](#sum-of-1n)
  * [Log](#log)
- [Bit Manipulation](#bit-manipulation)
  * [GetBit](#getbit)
  * [SetBitZero](#setbitzero)
  * [SetBitOne](#setbitone)
  * [Two's Complement](#two-s-complement)
  * [General tips](#general-tips)
- [Testing/Edge Cases](#testing-edge-cases)
  * [Strings](#strings)
  * [Numbers](#numbers)
  * [Arrays/Collections/Streams](#arrays-collections-streams)
  * [Objects](#objects)
  * [Testing Steps](#testing-steps)
    + [1. Get an understanding](#1-get-an-understanding)
    + [2. Check the API](#2-check-the-api)
    + [3. Start writing test cases](#3-start-writing-test-cases)
      - [3.1 Normal/most important cases](#31-normal-most-important-cases)
    + [3.2 Start & end](#32-start---end)
  * [3.3 Small extremes](#33-small-extremes)
    + [3.4 Large extremes](#34-large-extremes)
    + [3.5 “Illegal” input](#35--illegal--input)
    + [3.6 “Strange”/Uncommon input](#36--strange--uncommon-input)
    + [3.7 Scalability/concurrency](#37-scalability-concurrency)
    + [3.8 Security](#38-security)
  * [Decouple Objects](#decouple-objects)
  * [Testing Big Data](#testing-big-data)
- [SQL](#sql)
  * [Wildcards](#wildcards)
  * [Joins](#joins)
    + [Left join](#left-join)
    + [Inner join](#inner-join)
    + [Full outer join](#full-outer-join)
  * [Nested queries](#nested-queries)
- [Big Data](#big-data)

## Approaching Problems

### Basic Steps

<details>
<summary>
 </summary> 
 
__Pick out key details__
* Is data sorted
* Is algorithm going to be run many times (so could be precomputed or cached)
* Is there a memory limitation
* Etc.

__Draw an example__
* Physically draw what the structure/data looks like
* Make sure it’s big enough, and realistic enough (e.g., don’t draw a perfectly balanced tree if the data isn’t perfectly balanced, try to avoid special cases)
* Work through the example by hand, determining what it should output

__Think of cases__
* Think of the main possibilities. E.g., Checking for 1 edit distance part -- consider what happens for an edit, insertion, or deletion. For overlapping intervals, think of how they could overlap, etc.
* If the problem seems to complex to reason about for the typical case, start reasoning from small cases
* Can consider edge cases, but don't wase too much time on them -- want to get the main algorithm down

__Brute force algorithm__
* No matter how bad, it gives you a starting point and shows that you at least understand what needs to be done

__Optimize__
* Use key details -- is the data sorted, etc.

__Walk through__
* Before implementation, soldify understanding by walking through your algorithm.
* MAYBE write pseudocode

__Implementation__
* Make a TODO: Edge cases, bad input, etc. You'll fill this in later
* Put in template methods for things you'll fill in later. E.g., MaxComparator, parseLine, etc.
* Again, if you don’t have time to write error checks, add a TODO: Check for…. Confirm what you want to do in case of error (Exception, error code, null, etc.)
* Use classes where appropriate (you can pretend the class exists, e.g., Point)
* If you get confused (happens often), go back to your example and work through it again

__Test__
* It will likely be too slow to work through your large example. Instead…
* “Conceptual” test -- work through and explain what each of code is supposed to do
* Check weird looking code (for loops starting at 2, etc.)
* Hot spots: empty strings, null nodes, integer division, recursive base cases, etc.
* Use a SMALL test case (it will be faster)
* Test edge cases (null values, single element values, extreme values)
* Carefully analyze why bugs occur and ensure your fix doesn’t break anything else

__When stuck__
* Use a fresh example
* Solve “incorrectly”, and then think about why the incorrect method doesn’t work/can be fixed
* Make a time/space tradeoff
* Precompute information (e.g., sort data)
* Use a hash table
* Start by solving small examples and build up to larger ones -- can you spot a pattern?
* Draw pictures: Don't think in your head. Draw up some different test inputs and solve them by hand.
</details>

### Misc. Tips

__Brute force first__

Go for a brute force solution first, identify the bottleneck (largest big O), then think about how you could get rid of it.

If you are dealing with a recursive or backtracking problem, solve the problem first, and then think about memoization or dynamic programming.

__Algorithm first, then code.__

Think about the algorithm first, and then think about what this would look like in code. Think about the general algorithm you, a human being, would use to solve the problem, and then think about what this would look like in code. Trying to do both at once can tangle you in knots for complex problems. If you at least demonstrate you understand the algorithm, you demonstrate you can solve problems.

__Data structure brainstorm__

Run through common data structures to see if they would help: maps, heaps, tries, trees, lists.

__Dealing with connected data__

Do you need to count connected data in some way? (E.g., count 1s in a matrix). Use a breadth-first search or depth-first search. Rememeber that DFS is recursive, so could run out of stack memory.

__Dealing with related but unconnected data__

Do you need to count related data in some way, but the data is not fully connected? (E.g., count name frequency given a list of pairs of different name spellings). Try connecting the data as a graph and then doing a depth-first search to count the connected components.

__Find permutations/paths__

If you have to find some permutations, the problem is likely recursive. Remember the general algorithm:
* Identify the base case (nowhere left to go/nothing left to process/target value found)
* Pick a thing from your collection
* Recurse with that thing removed from the collection
* Put the thing back in your collection

[Best resource: Marty Stepp's videos](https://www.youtube.com/user/martystepp/videos)

After you have come up with the general recursive algorithm, think about how you can cache some values in a map or array (memoization).

__Returning the next something...__

If you need to return the next something (.e.g, daily temperatures problem), consider using a stack since this will return the most recent thing you visited. What happens if you iterate backwards and put on the stack? -- you get the next.

If you have to keep track of the lowest/highest something, and keep the data ordered (e.g., buy/sell stocks, 3-digit increasing substring), consider setting the element as the min/max, and then comparing to the next element. If you need three elements, you can set element 1 to the min, check if the next one is greater than min and less than current second highest, etc.

__Think small__

Usually a small example will be enough to prove an algorithm wrong. Also, picking small, simple examples that you can solve by hand will help you spot patterns to crack the algorithm. Likewise, if you're having trouble with a given example, try a simpler example: an array with 1 or 2 elements, etc.

__Think exhaustively__

What possible cases do you have? For example, if looking at overlapping intervals, there are only 3 ways 2 intervals can be:

* Disjoint (one after another)
* Overlapping (one starts before another ends, but after it start)
* Nested (one starts after another starts, and ends before it ends)

__Model on existing__

Can you model your problem on some existing algorithm? What does it look like?

__Identify the pain point__

If you are doing some work repeatedly -- choosing the max or min, say -- can you find a data structure to make that more efficient?

__Relax some constraints__

For example, if it's hard to find the closest sum, could you instead try to find the exact sum?

__Sorting HashMaps__

If you need to sort a HashMap, read the key/value to a custom object with a custom comparator, and then use Collections.sort().

__Rearrange variables__

Don't be afraid to rearrange variables to make things easier. For example, make sure var1 always starts to the left of var2, or is the smaller string, etc.

```java
if(arg2.x < arg1.x) {
    f(arg2, arg1);
}
```

__Don't forget empty checks__

Check data structures are not empty before peek/poll.

__Mistakes are overlooked if you  spot/fix them__

Again, being present is key because I’m coaching you the whole way. If nerves take hold—pause, deep breath and pay attention to where I’m directing you. Concentrate on solving only the problem posed but be prepared to mentally pivot and sanity check along the way.

__Try backwards__

Does traversing the data backwards make things easier?

__Linked list problems__

What would happen if you used a two pointer approach?

__When dealing with trees...__

...think recursion.

__Tracking min/max__

Do you need to keep a running track of a minimum or maximum value? Think heaps. In Java, `PriorityQueue` doesn't support remove in log n time. Instead you can use a `TreeMap` (Red-black tree implementation), which will keep track of the min or max in log n time, and also allow for log n removals.

__Implementing maths operations__

If you have to reimplement a mathematical operation without using operators, you will probably have to use bit manipulation. Break down the basics of the operation to work out what is going on with the numbers, and then think about how you would replicate that using bitwise operators.

__Consider pivot/merge__

Can you use the pivot selection algorithm from Quicksort of the merge algorithm from merge sort? For example, consider Quickselect and Squares of sorted array problems.

### Optimization Techniques
* Do you need an O(n) runtime? Forget about sorting. Can you store data in a map instead?
* Do you need to use O(1) space? Does sorting the data help?
* Do you need an O(n) runtime and O(1) space? Then you probably need to mark the data in the original data structure somehow. For example, by setting it to negative. Remember, you can run through a data structure multiple times.
* Are you dealing with a limited range of ints -- temperatures, numbers, etc.?
Then you might be able to stick them in a fixed size array or map with counts or indexes. Then when you iterate that for each element you will still get a fixed-time runtime.

## Sorting

<details>
 <summary>
  
* Quicksort
* Mergesort
* Heapsort
* Insertion sort
* Counting sort
* Radix sort

 </summary>

| Sort          | Time                           | Space         | Stable?       | Notes                                                  |
| ------------- | ------------------------------ | ------------- | ------------- | ------------------------------------------------------ |
| Quicksort     | avg: n log n, worst: n^2       |     log n     | No            | Worst-case can be made very unlikely by shuffling data |
| Mergesort     | n log n                        |     n         | Yes           |                                                        |
| Heapsort      | n log n                        |     1         | No            | constant extra space if you use existing array, practically usually slower than QS due to operations  |
| Insertion     | n^2                            |     1         | Yes           | Although typically bad, works well if elements are almost sorted, for example if k distance away, time becomes nk |
| Counting sort | n + k                          |     n + k     | Yes           | Good when k is similar to n, giving n total time (k = size of radix -- the range of values) |
| Radix sort    | nw                             |     n + w     | Yes           | w = size of words/keys being sorted                                                       |

</details>

### Quicksort

<details>
 <summary>
 </summary>
  
```java
1. If left < right...
1.1 Partition
1.2 Sort(left, partitionIndex-1)
1.3 Sort(partitionIndex+1, right)

2. Partition(arr, left, right)
2.1 Set pivot val = left (in practice there are better values)
2.2 Set i = left+1, j = right
2.3 While true...
2.3.1 Increment i while < pivotVal && != right
2.3.2 Decrement j while > pivotVal && != left
2.3.3 if j > i, swap them, else break
2.3.4 Swap left and j, then return j
```

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/QuickSort.java)
__Note__: The partition algorithm can algorithm can also be used for _QuickSelect_ (find the Kth smallest element). It gives n^2 worst case, but n time average case.

### Mergesort

<details>
 <summary>
 </summary>

```java
1. If left < right...
1.1  Get the mid
1.2 Sort(left, mid)
1.3 Sort(mid+1, right)
1.4 Merge(arr, left, mid, right)

2. Merge(arr, left, mid, right)
2.1 Copy left and right into arrays
2.2 Take the smaller elements
2.3 Tidy up by taking left over elements

```

</details>

Unlike QuickSort, this is stable, but takes more memory.
[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/MergeSort.java)

### Heapsort

<details>
 <summary>
 </summary>


```java

Treat parent as (parentIndex*2)+1

1. Create a max heap: Starting at the bottom of the heap, sink each node down
2. Sink: swap the parent element with largest child, as long as a child is larger
3. Now you have a max heap:
3.1 Swap the last element with the first (largest element) -- the largest is now in the correct position
3.2 Decrement the last element index
3.3 Sink the new first element into the correct position
3.4 Go to 3.1
```

</details>

Given an array, we can sort in-place. In practice, the operations often make this slower than QuickSort.
[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/HeapSort.java)

### Insertion sort

<details>
 <summary>
 </summary>

```java
Go through each element and swap it with preceding element, as long as it is smaller

```

</details>

Not usually useful, but can be helpful if data is usually sorted or k-sorted.
[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/InsertionSort.java)

### Counting sort

<details>
 <summary>
 </summary>

```java
1. Set up a count array the size of the radix + 1
2. Iterate around value array, and increment count[val+1]

[1, 3, 2, 2]
-->
 0  1  2  3  4
[0, 0, 1, 2, 1]

3. Get the cumulative counts:
[0, 0, 1, 3, 4]

4. Copy the values from the original array into an auxiliary array using these counts, incrementing count each time
[1, 2, 2, 3]

5. Copy the values back into the main array

```

</details>

Useful if the radix is the same size as the digits, giving an O(n) algorithm.
[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/KeyIndexCounting.java)

### Radix sort

```java

(Basically counting sort but go through each letter of the string and use that as the value to count)

```

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/
RadixSort.java)

## String processing

### Tries

<details>
 <summary>Build</summary>

Build: nw, where n is the number of words, and w is the length of the longest word
Space: nw

```java

class Trie {

    TrieNode root;
    
    public Tree(String [] words) {
        root = new TreeNode();
        build(words);
    }

    private void build(String [] words) {
        TrieNode node = root;
        
        for(String word : words) {
           for(char c : word.toCharArray()) {
               if(!node.children.containsKey(c)) {
                   node.children.put(c, new TreeNode());
               }
               
               node = node.children.get(c);
           }
           
           node.word = word;
        }
    }

    private class TrieNode() {
        String word;
        HashMap<Character, TreeNode> children = new HashMap<>();
    }

}

```

</details>

<details>
 
 <summary>
 Query
 </summary>

Query: w, where w is the length of the query word

```java

public boolean contains(String word) {
   
    TreeNode node = root;
    
    for(char c : word.toCharArray()) {
        if(!node.children.contains(c)) {
            return false;
        }
    
        // Could also do if node.word != null, results.add(node.word) -- return all substrings of this word
    
        node = node.children.get(c);
    }
    
    return true;
}

// If you need to keep track of how far you are through the trie, you could also pass back the root itself and access the nodes in the algorithm (e.g., in a DFS).

```

</details>

### KMP (Knuth-Morris-Pratt)

<details>
 <summary>
 </summary>

A string matching algorithm that works in O(n+m) time and O(m) space.
Point: it doesn't backtrack along the main string -- meaning it can run on an infinite stream of text.

Essentially we build a FSA from the substring, treating it like a pattern, working where we should jump back to if we hit a mismatch.

```
1. Build FSA:
1.1 Set index = 0, i = 1
1.2 If index == i, increment index, set arr[i] = index, i++
1.3 Else, if index == 0, increment i, else index = arr[index-1] (jump back -- we matched this far, so see if we can restart the pattern from the previous point).
```

The actual pattern matching is then largely the same.

```
2. Pattern match:
2.1 While strIndex < str && ptnIndex < ptn
2.2 If strIndex == ptnIndex, increment both
2.3 Else, if ptnIndex == 0, increment strIndex, else, ptnIndex = arr[ptnIndex-1] -- again, we matched this far, so see if we can restart the pattern from the previous point
```

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/KmpSubstringMatching.java)

### Rabin-Karb
<details>
 
 <summary>
 </summary>

This is a useful substring matching algorithm because it can be used for several other algorithm problems, such as finding the max subarray of length k, etc. It can also be extended to check for several patterns at once (e.g., plagiarism checking).

To check for multiple substrings/patterns, simply put all of the hashes in a set, and then check if the string hash is in that set.

The idea is:
1. Take the hash of the pattern you're looking for, say the pattern is length k
2. Take a length k window of the search string.
3. If the window has the same hash as the pattern, run through the strings to see if they match
4. If they don't, update the window by subtracting the first letter from the hashed window value, and adding the next value

Average time: n+k
Space: k
Worst time: nk (imagine you had a bad hashing function that caused collisions for every hash window)

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/RabinKarpSubstringMatching.java)

### Suffix tree

<details>
 <summary>
 </summary>

* Check if m is a substring of n in O(m) time
* Find first occurance in O(m) time
* Find z occurances of m in O(m+z) time
* Space: O(n^2) (but can be reduced to O(n) by turning it into a suffix array in O(n) time)

Note: Can construct in O(n) time and O(n) space using Ukkonen’s algorithm.

[Great video](https://www.youtube.com/watch?v=VA9m_l6LpwI)

![Suffix tree](https://raw.githubusercontent.com/pekoto/MyNotes/master/imgs/suffix-tree.jpg)

```
    1 2 3 4 5 6 7 8
t = C A G T C A G G $

1. Start with last G, we have nothing, so add G
2. Then go to GG, we have a G, so add another G after G
3. Then add AGG
…
4. When we get to AGTCAGG, note we already have AGG, so split this branch -- AG > H & TCAGG
```

To use the tree:

```
Find C:
1. Search to the C branch
2. Search all of the branches off of this (5 and 1)

Find CG:
1. Go to C branch
2. See that this doesn’t exist (need to check chars from every branch)

Find CAGTC:
2. Go to CAG branch, search all children
```

</details>

### Full-text indexing

<details>
 
 <summary>
 </summary>

1. Break a record into words
2. Create a map of words to records

| Sort      | Words             | 
| --------- | ----------------- | 
| Doc 1     | Apple, Ball, Dog  | 
| Doc 2     | Dog, Ball, Car    | 
| Doc 3     | Kite              |

Index -->

| Words      | Docs             | 
| --------- | ----------------- | 
| Apple     | Doc 1             | 
| Ball      | Doc 1, Doc 2      | 
| Car       | Doc 2             |
| Dog       | Doc 1, Doc 2      |
| Kite      | Doc 3             |

(We could do this with chars in words even. E.g., if making an address book, we could create an index of letters > name list, where the name list was sorted by words that started with that letter.)

</details>

### Iterating chars

<details>
 <summary>

We can iterate chars just like ints. For example, to generate every word one char away:

</summary>

```java
for(int i = 0; i < str.length(); i++) {
    for(char c = 'a'; c <= 'z'; c++) {
        System.out.println(str.substring(0,i) + c + str.substring(i+1));
    }
}
```

</details>

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

<details>
 <summary>
 </summary>

```java
doSomething(node);
visit(node.left);
visit(node.right);

// Output: 6, 4, 3, 5, 7, 8
```

__Note:__ Useful for serializing and deserializing a binary tree. Go through the tree adding each node to a queue, and X for null.
Then go through the queue recursively to rebuild the tree.

</details>

### Inorder traversal
<details>

<summary>
</summary>

```java
visit(node.left);
doSomething(node);
visit(node.right);

// Output: 3, 4, 5, 6, 7, 8
```

__Note:__ In a BST, inorder traversal will give you the nodes in sorted order.

</details>

### Postorder traversal

<details>
 <summary>
 </summary>

```java
visit(node.left);
visit(node.right);
doSomething(node);

// Output: 3, 5, 4, 8, 7, 6
```

</details>

### Level-order traversal

<details>
 <summary>
 </summary>
 
 
```
Essentially this boils down a BFS.
1. Put the root on a queue
2. Get the size of the queue
3. Set up a loop to iterate _size_ times
4. On each iteration of the loop, get a node from the tree and add its children to the queue
5. Go to 1
6. Break when the queue is empty
```
This can be used for various things: printing level-order, check if each level is symmetrical, "inverting" the children at each level, etc.

</details>

### Bottom-up recursion

<details>
 <summary>
  For example, to get the height:
 </summary>

Use an inorder traversal.
Go down to the bottom of the tree first, and then count on the way back up.


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

</details>

### Top-down recursion

<details>
 <summary>
  For example, to get the longest increasing sequence:
 </summary>

Use a preorder traversal.
Check the value of this node, and then recurse for left and right.

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

</details>

### Getting distance from the root

<details>
 <summary>
 </summary>
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

</details>

### Total nodes

<details>
 <summary>
 </summary>

The total nodes in a complete tree is (2^k)-1, where k is the height of the tree. E.g., a tree with height 3 will have 2^3  = 8-1 = 7 nodes.

</details>

### Tree Tips
* We often recurse when doing tree problems -- e.g., when getting the height. Can we also do something else while in the recursive method? For example, if finding the max diameter, we are finding the height of the left and right subtrees anyway, so we could also check to see if we have a new max diameter (left + right height) at the same time.

* It can often become confusing trying to pass some value (like ```java int max```) around in a recursive manner for both children. To make this easier for interview purposes, you can declare this value outside of the function.

* Don't forget inorder, preorder, and postorder traversals. These can often be used to find brute force solutions. E.g., find the highest, get in order, compare if trees are equal, check if contains subtree, etc. Just do a traversal and read the results into a list: now you have a list problem (though rarely an optimum solution though).

## Graph Algorithms

### Dijkstra
Finds the shortest path from a vertex to all other vertices.

<details>
 <summary>
 </summary>

```java
1. Set up a distance array
2. Set the distance to the source verex to 0
3. Set the distance to the other vertices to +INF
4. Add the vertex to the PriorityQueue
5. While the queue isn't empty...
6. Get the closest vertex (originally source)
7. Relax every adjacent vertex and put them on the queue

Relax(vertex current, vertex neighbours):
1. If the distance to current + current's distance to neighbour < current distance to neighbour,
   update neighbour's distance and update it's key in the queue if it's in the queue already
2. Set edgeTo[neighbour] = current

```
[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/DijkstrasAlgorithm.java)

Time: V+E(log V)
-- Assuming we use an adjacent list and PQ. We go through each vertex, and then for each edge, we add/remove it to the PQ.

</details>

### Topological Sort

Find an ordering in a list of dependencies

<details>
 
 <summary>
 </summary>

```java

1. For each node in the graph...
2. If it hasn't been visited yet, perform a DFS on it...
3. Popping the order stack will you give you an ordering

DFS:
1. Mark vertex visited and put on recursion stack (a set)
2. For each adjacent vertex...
3. If it's in the recursion stack, we have a loop -- break
4. Otherwise, if it's not visited, visit it
5. Finally, after having visited all adjacent vertices recursively, we remove this node from the recursion stack and add it to the order stack

```

Time: V+E

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/TopologicalSort.java)

</details>

### Union-Find (Disjoint Set)

<details>
 <summary>
 </summary>

Used to check if two components are connected together.

```java

1. Setup an array of size n, with values 0...n for each vertex.
2. Union:
2.1 Find the root of A and B
2.2 Make the root of B = root of A

3. Find:
3.1 Check if A's root == B's root

4. Get root:
Recursively call getRoot with the vertex index, until the vertex index matches the value at that vertex.

```

Time: O(n) -- naive implementation. This turns into n^2 for n union or find operations. But we can be improved to log n (and even inverse Ackermann function) with path compression: e.g., when finding roots, you set the root to be grandparent, etc.
Space: O(n)

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/algorithms/UnionFind.java)

### Minimum Spanning Tree

<details>
 <summary>
 </summary>

The tree with the minimum weight that touches every vertex in a graph.
If all weights are unique, then there will be 1 MST, otherwise there may be multiple.
An MST must have vertices-1 edges.

A few ways to build. Lazy Prim may be easiest...

```java

1. Put the initial vertex on a priority queue and visit it
2. While the queue isn't empty/has vertices-1 edges...
3. Get the minimum edge
4. If both vertices have been visited, continue
5. Else, add this edge to the MST and visit the vertices connected to this edge

Visit:
1. Mark the vertex as visited
2. For each adjacent edge, if the vertex attached to this edge hasn't been visited...
3. Add the edge to the PQ

```
Time: e log e
Space e

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/master/PrincetonA/src/com/pekoto/datastructures/MinimumSpanningTreeLazyPrim.java)

### Segment Tree

<details>
 <summary>
 </summary>

Holds intervals in a tree structure.
Can use used for range sum queries.

Time: n to build, log n to query
Space: n (I think it's 2-4n?)

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/bb669e55523b73b46f62b003adb196b392385901/PrincetonA/src/com/pekoto/challenges/RangeSumSegmentTree.java)

### Binary Indexed Tree

<details>
 <summary>
 </summary>
Like a segement tree. Used for quick range sum queries.

Time: n log n to build, n to update, log n to query
Space: n

</details>

[Source](https://github.com/pekoto/PrincetonA/blob/57270f330468b49bd0570f911ba3ea0dc96f2aa0/PrincetonA/src/com/pekoto/datastructures/BinaryIndexedTree.java)

## Algorithm Patterns

### Finding a Missing Element

<details>
 <summary>
 </summary>

Given an array, or two arrays, find the missing element.
(Variations of this problem crop up a lot.)

There are a number of ways to do this:

1. Just sort the arrays and iterate through them with pointers
2. If the numbers are sum of 1-n, then use ``` (n(n+1))/2 ``` to get the expected value, then substract actual value
3. Likewise you can add both arrays and take the difference
4. You can use a HashMap: go through the smaller array adding counts, then go through the larger array decrementing counts. If the count falls below 0, it is a missing element. (Useful when more than 1 element is missing.)
5. You can also XOR everything together:

```java
// Using XOR to find missing:
a1: 1, 2, 3
a2: 1, 3

01 ^ 10 = 11 (1^2 = 3)
11 ^ 11 = 00 (3^3 = 0)
00 ^ 01 = 01 (0^1 = 1)
01 ^ 11 = 10 (1^3 = 2)

```

</details>

### Sliding Window

<details>
 <summary>
 </summary>

0. If required, set up a map, etc., that can be used to check if your condition is fulfilled. E.g., number of each char, etc.
1. Set up start
2. Set up a loop with end
3. Set up a map to store counts
4. Use end to update your count
5. If your condition is violated, update start until it is valid again (e.g., have 0 unique character left, end-start matches len n, etc.)
6. Now your condition is guaranteed to hold, so check if you have a new max, etc.

</details>

### Calculator/Stack parsing

<details>
 <summary>
 </summary>

When we need to parse an expression, we usually use a stack. Dijkstra suggests have a number and operator stack:

1. When we have a number, put it on the number stack
2. When we have an operator, put it on the operator stack
3. When we hit a right parenthesis, pop 2 numbers and and operator, and put them back on the number stack.

We can actually do this with only 1 stack:

```java

public int calculate(String s) {
    int len;
    if (s == null || (len = s.length()) == 0) {
        return 0;
     }
 
     Stack<Integer> stack = new Stack<Integer>();
     int num = 0;
     char sign = '+';
 
     for (int i = 0; i < len; i++) {
     
         if (Character.isDigit(s.charAt(i))) {
             num = num * 10 + s.charAt(i) - '0';
         }
 
         if ((!Character.isDigit(s.charAt(i)) && ' ' != s.charAt(i)) || i == len - 1) {
              if (sign == '-') {
                  stack.push(-num);
              } else if (sign == '+') {
                  stack.push(num);
              } else if (sign == '*') {
                  stack.push(stack.pop() * num);
              } else if (sign == '/') {
                  stack.push(stack.pop() / num);
              }
              sign = s.charAt(i);
              num = 0;
         }
     }

    int result = 0;
 
    // Add up all the numbers in the stack
    for (int i : stack) {
        result += i;
     }
 
     return result;
}

```

</details>


## Java

<details>
 <summary>
  * PriorityQueue
  * LinkedList
  * Stack
  * HashSet
  * LinkedHashSet
  * TreeSet
  * HashMap
  * LinkedHashMap
  * TreeMap
  
  </summary>

|               | Add                                              | Remove                                                                                                 | Get (n/obj)                                                                                                   | Contains                        | Get min/max                                                | Comment                                              |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| PriorityQueue | log n  ```minHeap.add(1); ```                    | n ```minHeap.remove(1);```                                                                             | n/a                                                                                                           | n ```minHeap.contains(1);```    | log n/1 ```minHeap.poll()/minHeap.peak()```                |                                                      |
| LinkedList    | 1  ```queue.add(1); // adds to end of queue ```  | 1 if first/last node, n is random node ```queue.pollFirst(), queue.pollLast(), queue.remove(1);```     | 1 if first/last node, n if random node ```queue.peekFirst(), queue.peekLast(), queue.get(1);```               | n ```queue.contains(1);```      | n/a                                                        | Can be used as a FIFO or deque                       |
| Stack         | 1  ```stack.push(1); // adds to end of queue ``` | 1 if top node, n is random node ```stack.pop(), stack.remove(1);```                                    | n gets at index ```stack.get(1);```                                                                           | n ```stack.contains(1);```      | n/a                                                        |                                                      |

|               | Add                                              | Remove                                                                                                 | Get (n/obj)                                                                                                   | Contains                        | Get min/max                                                | Comment                                              |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| HashSet       | 1  ```set.add(1); ```                            | 1 ```set.remove(1);```                                                                                 | n/a                                                                                                           | 1 ```set.contains(1);```        | n/a                                                        |                                                      |
| LinkedHashSet | 1  ```set.add(1); ```                            | 1 ```set.remove(1);```                                                                                 | n/a                                                                                                           | 1 ```set.contains(1);```        | n/a| Stores objects in the order they were added           |                                                      |
| TreeSet       | log n  ```set.add(1); ```                        | log n ```set.remove(1);```                                                                             | n/a                                                                                                           | log n ```set.contains(1);```    | log n ```set.first() // min, set.last() // max```          | Stores elements according to natural ordering        |

|               | Add                                              | Remove                                                                                                 | Get (n/obj)                                                                                                   | Contains                        | Get min/max                                                | Comment                                              |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| HashMap       | 1  ```map.put(1, 1); ```                         | 1 ```map.remove(1);```                                                                                 | 1 ```map.get(1);```                                                                                           | 1 ```map.containsKey(1);```     | n/a                                                        | Operations could be n in worst case hash collisions  |
| LinkedHashMap | 1  ```map.put(1, 1); ```                         | 1 ```map.remove(1);```                                                                                 | 1 ```map.get(1);```                                                                                           | 1 ```map.containsKey(1);```     | n/a                                                        | Operations could be n in worst case hash collisions  |
| TreeMap       | 1  ```map.put(1, 1); ```                         | log n ```map.remove(1);```                                                                             | log n ```map.get(1);```                                                                                       | log n ```map.containsKey(1);``` | log n ```map.firstKey(), map.lastKey()```                  |                                                      |

</details>

### Custom Comparator

<details>
 <summary>
 </summary>

```java

class MaxComparator implements Comparator<Integer> {

    @Override
    public int compare(Integer arg0, Integer arg1) {
        return arg1-arg0;
    }
}

PriorityQueue<Integer> maxHeap = new PriorityQueue<>(new MaxComparator());

```


 </details>

### Implementing equals()

(There are more thorough ways to implement this...)

<details>
 <summary>
 </summary>

```java
@Override
public boolean equals(Object o) {
    if (!(o instanceof Name))
        return false;
    Name n = (Name) o;
    
    return n.firstName.equals(firstName) && n.lastName.equals(lastName);
}

public int hashCode() {
    return 31*firstName.hashCode() + lastName.hashCode();
}

```

</details>

### Implementing Comparable

<details>
 <summary>
 </summary>

```java
public int compareTo(Name n) {
    int lastCmp = lastName.compareTo(n.lastName);
    return (lastCmp != 0 ? lastCmp : firstName.compareTo(n.firstName));
}
```

</details>

### Implementing iterator

<details>
 <summary>
 </summary>

Note: Iterators are the only safe way to modify a collection while iterating over it.

```java
public class StackWithArray<T> implements Iterable<T> {

    private int nextElementIndex = 0;
    // ...

    // Iterable implementation
    public Iterator<T> iterator() {
        return new ArrayIterator();
    }

    private class ArrayIterator implements Iterator<T> {

        private int nextElement = nextElementIndex;

        public boolean hasNext() {
            return nextElement > 0;
        }

        public T next() {
            nextElement--;

            return arr[nextElement];
        }

        public void remove() {
            // Remove during iteration not supported here
        }
    }
}

Iterator iterator = collection.iterator();
      
while(iterator.hasNext()) {
    Object element = iterator.next();
    
    if(element.getString().equals("yes") {
        iterator.remove();
    }
}

```

</details>

### String/Int/Char Manipulation

<details>
 <summary>
Turn a char to/from its int value:
 </summary>

```java 
String str = "123";

int n = str.charAt(0) - '0';   // from char to int
char c = (char)(n+'0');   // from int to char value

// n = 1, c = 1

```
</details>


<details>
 <summary>
Turn 'A' into index 0 (for example, to put into a len 26 array for counting):
 </summary>

```java
String str = "ABC";
int n = str.charAt(0) - 'A';

// n = 0
```

</details>

<details>
 
 <summary>

Get least significant digit:
</summary>

```java
int i = 123;
int lsd = i % 10;
i /= 10;

// lsd = 3, i = 12

```
</details>

### Common functions

```java
int i = Integer.parseInt("123");

boolean b = Character.isDigit('5');

// Remember this is exclusive
String s = "Hello";
s.substring(1, 4); // prints "ell"

String [] tokens = s.split(" ");

int firstIndex = s.indexOf('e', 0);

int lastIndex = s.lastIndexOf('e', str.length()-1);

treeMap.floorKey(4);    // returns key that is closest to or equal to 4

treeMap.ceilingKey(4);  // returns key that is closest to or equal to 4

```

### Tips

* PriorityQueue allows dupes. If you want a list of unique things sorted by natural ordering, use a TreeSet or TreeMap.

* PriorityQueue is only partially sorted, since it's a heap. If you need a collection that allows duplicates while keeping natural order, you'll just have to use Collections.sort().

## Big O

<details>
 
 <summary>
 List of common running times in order.
 </summary>

|         |              |
| ------- | ------------ |
| 1       | Constant     |
| log n   | Logarithmic  |
| n       | Linear       |
| n log n | Linearithmic |
| n^2     | Quadratic    |
| 2^n     | Exponential  |
| n!      | Factorial    |

* If the algorithm is do this, and then do that, add the runtimes. If it is do this for every time you do that, multiply the runtimes.

</details>

### Recursive runtimes


<details>
 <summary>
  
* Often drawing out the call tree is the only way to confirm, but often reduce to 

</summary>
```O(branches^depth)```. Consider:


```java
int f(int n) {
    if(n <=1) {
        return 1;
    }

    return f(n-1) + f(n-1)
}

```

You have a call tree like...

```
          f(4)
        /     \
      f(3)       f(3)
     /   \       /    \
    f(2)  f(2) f(2)   f(2)
    
    ...etc.
```

Total calls are 2^0 + 2^1...2^n-1. Recall that the sum of powers of 2 to determine that the total runtime is 2^n.

</details>

* Another way to figure it out is to think about how many function calls you have, and how long each one runs for.

```java

void permutation(String str, String prefix) { 
    if (str.length() == 0) { 
       System.out.println(prefix); 
    } else { 


    for (int i= 0; i < str.length(); i++) {
       String rem = str.substring(0, i) + str.substring(i + 1);
        permutation(rem, prefix + str.charAt(i)); 
    } 
} 

```

We know what there will be n! permutations of a string (first we choose character 7, leaving 6 choices, then 5, etc.)

So we know the base case will be called n! times. But how long do we run before we reach the base case? Well, we have to go through every char, so we run n times. We can imagine a call tree with n! nodes, and a length of n to get there. So we have (n*n!) nodes (function calls) in our tree.

But how what about the time complexity at each node? Well, println will take n time. And taking the substring and creatng the new string will take n time. So each node takes n time.

So in total we have n*(n*n!) time, or (n^2*n!) total.

__Word Break__
Some proofs and ideas:

Let's abbreviate the function call, wordBreak, as wB(s, dict, i) where i is the end of the substring being imagined. Now, imagine a tree of function calls.
wB(s, dict, 0) spawns wB(s, dict, 1), wB(s, dict, 2), ... wB(s, dict, n)
wB(s, dict, 1) spawns wB(s, dict, 2), wB(s, dict, 3), ... wB(s, dict, n)
wB(s, dict, 2) spawns wB(s, dict, 3), wB(s, dict, 4), ... wB(s, dict, n)
and so on. 

Since wB(s, dict, 0) is the root of our recursive call, we see that it spawns n - 1 + 1 = n subroutines. Each of these subroutines spawns at most n (so O(n) in Big-O notation) subroutines as well. So, wB is called recursively n times for each ending index, and each recursive call in turn is called, in the worst case, n times. Therefore, our running time complexity is n multiplied by itself n times => O(n^n). This is definitely a pessimistic estimate, but recall that Big-O notation is worst-case analysis. Hope this helps!

Or slightly tighter bound:

https://leetcode.com/problems/word-break/discuss/169383/The-Time-Complexity-of-The-Brute-Force-Method-Should-Be-O(2n)-and-Prove-It-Below

__Robot Maze Search__
Well, at each point the robot has 2 choices. And the total length he can go is the length of an entire row and column. So the runtime is 2^row+col. 

__Word Search__
When you think about word search, you have m * n cells in the grid, and each cell can make 4 choices for the length of the longest word, so I would guess the running time is m*n*4^L, where L is the length of the longest word.

## Maths

### Permutation, Combination, and Subset Formulas

#### Permutations with repeats
How many ways can you choose k elements from n elements.
Example: How many 4 digit pin numbers are there?

<details>
 <summary>
 </summary>

``` n^k. ```

Example:
How many ways can we choose a 4 digit PIN using 0-9?
10^4 = 10,000

</details>

#### Permutations without repeats
How many permutations of k elements are there from a string containing n elements?

For example:
From ABC, how many length 2 permutations are there?

<details>
 <summary>
 </summary>

``` n!/(n-k)! ```

```
3!/(3-2)! = 6
AB, AC, BA, BC, CA, CB
```

__Note:__ This means for any string, where we choose all elements, there are ``` n! ``` permutations of that string.
3!/(3-3)! = 3!/0! = 6

```
ABC! = 3! = 6

ABC, ACB, BAC, BCA, CAB, CBA
```

</details>

#### Unique permutations from a string with repeats
Given a string with repeated elements, how many unique permutations are there?

<details>
 <summary>
 </summary>

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

</details>

#### Combinations without repeats

<details>
 <summary>
How many ways can you choose k elements from n, if order doesn't matter?
For example, how many ways can you choose 6 lottery numbers from 49.
 </summary>

``` n!/(n-k)!k! ```

49!/(49-6)!6! = 13,983,816

</details>

#### Subsets

<details>
 <summary>
 </summary>
The number of subsets given some superset.
``` 2^n. ```

This is because for each element it can either be in the set or not.

For example, {1, 2, 3} = 2^3 = 8.
{}, {1}, {2}, {3}, {1, 2}, {1,3}, {2,3}, {1,2,3}

</details>

### Generating Permutations

This follows the basic recursive pattern:

<details>
 <summary>
 </summary>
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

</details>

#### String permutations

<details>
 <summary>
 </summary>

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

</details>

### Generating subsets


<details>
 <summary>
 </summary>
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

Complexity: ``` O(n*2^n) ```

</details>

### Powers of 2

| x  | 2^x  | 
| -- | ---- |
| 0  | 1    | 
| 1  | 2    | 
| 2  | 4    | 
| 3  | 8    | 
| 4  | 16   | 
| 5  | 32   |
| 6  | 64   |
| 7  | 128  |
| 8  | 256  |
| 9  | 512  |
| 10 | 1024 |


#### Estimating

<details>
 <summary>
 </summary>
Recall (x^n)*(x^m) = x^n+m.
E.g., 2^2 * 2*3 = 4 * 8 = 32 = 2^5 \[2^(2+3)]

So, to estimate powers of 2, find the lower numbers and multiply them together.

For example, 2^20 = ?
2^10 ~= 1000 --> 10*2 = 20, so 1000*1000 = 1,000,000 (actual 1,048,576)

</details>

#### Summing

<details>
 <summary>
 </summary>
The sum of total powers of 2 is 2^(n+1)-1

E.g., Sum of 2^3 = 2 + 4 + 8 = 15 = (2^4)-1.

Note that this is the same as the nodes in a binary tree. Useful for calculating recursion call tree sizes.

(What if we had 2^31 in an array of 2^31? It would be 2^62, so should fit in long).
</details>

#### Notable Powers


<details>
 <summary>
  * Max value
  * KB
  * MB
  * GB
  * TB
 </summary>

| 2^x          | Value              | Comment                               |
| ------------ | ------------------ | ------------------------------------- |
| 2^31-1 BITS  | Integer.MAX_VALUE  | About 2 billion                       |
| 2^63-1 BITS  | Long.MAX_VALUE     | 9 quintillion something...            | 
| 2^10         | KB                 | ~1,000 bytes)                         |
| 2^20         | MB                 | ~1,000,000 bytes/~1000KB              |
| 2^30         | GB                 | ~1,000,000,000 bytes/~1000MB          |
| 2^40         | TB                 | ~1,000,000,000,000 bytes/~1000GB      |

Using a Bit Array, we could store around 2^31 (about 2 billion values) true/false values in a single int.
We could use an array of 10 values to store 2 billion * 10 true/false values, etc.
Useful when tinking about system design.

</details>

### Sum of 1...n

<details>
 <summary>
 </summary>

``` 
n(n+1)/2

E.g., 1...4 
= 1 + 2 + 3 + 4 = 10
= 4(5)/2 = 20/2 = 2
```

This is useful because it reduces to n^2 when working out runtimes.

```java
for(int i = 0; i < n; i++) {
    for(int j = 0; j < i; j++) {
         ...
    }
}
```

How many times does j run? 0, 1, 2...n times. Therefore the time sums to an n^2 time.

</details>

### Log

<details>
 <summary>
 </summary>
The inverse power function.

log(2)8 = 3 because 2^3 = 8

I.e., 2 to the power what makes 8.

</details>

## Bit Manipulation

### GetBit

<details>
 <summary>
 </summary>
 
```java
public boolean getBit(int n, int bit) {
    return (n & (1 << bit)) != 0;
}

// E.g., 4 = 0100
// getBit(4, 1)
// > 0100 & (0010) = 0000

```
</details>


### SetBitZero

<details>
 <summary>
 </summary>

```java
private int setBitToZero(int n, int bit) {
    return n & ~(1 << bit);
}
// (Same as getBit but inverted)

// E.g., 4 = 0100
// setBitZero(4, 2)
// 0100 & ~(0100)
// > 0100 & 1011
// > 0000

```

</details>

### SetBitOne

<details>
 <summary>
 </summary>

```java
private int setBitToOne(int n, int bit) {
    return n | (1 << bit);
}

// E.g., 4 = 0100
// setBitOne(4, 1)
// 0100 | 0010
// > 0110

```

</details>

### Two's Complement

<details>
 <summary>
 </summary>

A way to represent -ve numbers in binary.
The left-most digit is negative, and the other numbers are positive.

```
           -8 4 2 1
E.g., -5 =  1 0 1 1 = -8 + 2 + 1 = -5
```

To calculate:
``` 
~x + 1 

E.g.,
 2  = 0010
-2 =  1110

= ~2+1
= > 1101 + 0001
= > 1110

```
</details>

(Also useful for Binary Indexed Tree)

### General tips
* Left shifting will multiply by 2.
* Right shifting will divide by 2

## Testing/Edge Cases

### Strings

<details>
 <summary>
 </summary>

1. Null
2. Empty.
3. Length 1
4. Uppercase/lowercase/mixed?
5. Special characters (e.g., accented a)
6. All characters same
7. Whitespace
8. If parsing, what if the token is contained as part of the element we wanted to parse out (e.g., string split by spaces, but name has a space in it)
9. Last part not processed (e.g., imagine calculator app -- it ends in a number and no operator, did you remember to process this last number?)
10. Creating a new string every time instead of using `StringBuffer`

</details>

### Numbers

<details>
 <summary>
 </summary>

1. 0
2. Negatives
3. MAX_VALUE (2^31-1 / 2^63-1)
4. -MIN_VALUE
5. If we have a max that is not MAX_VALUE, then max-1, max, max+1. E.g, if max = 10, check 9, 10, 11.

</details>

### Arrays/Collections/Streams

<details>
 <summary>
 </summary>

1. Null
2. Empty
3. Length 1
4. All duplicates
5. Some duplicates
6. (If contains numbers, see numbers edge case)
7. Check last part of array is processed (e.g., if looping over)
8. Thing contained in last element of array
9. Already sorted

</details>

### Objects
1. Null

### Testing Steps

<details>
 <summary>
 </summary>

#### 1. Get an understanding
1.1  Test the most important functionality first, so what is this being used for? By whom?
1.2 Is the style good? camelCase/descriptive, etc.
1.3 Does the function exist already, if so why aren’t we using that?
1.4 What do we know about the input? Is it sorted, not null, etc.? Is it limited in size?
1.5 If we have errors, are we throwing exceptions, returning an error code, etc.?

#### 2. Check the API
2.1 Are the parameters correct? What counts as an A? (lowercase, uppercase…)
2.1 Think about the return type -- is an int big enough to return what we want?

#### 3. Start writing test cases
(Test case format: No. Input (expected): T/F (actual)
E.g., 1. Banana (3): T (Test case 1, banana, should return 3, true -- does return 3)

##### 3.1 Normal/most important cases
3.1.1 True/false cases (eg., no A’s, 3 A’s)
3.1.2 Test -ves, 0, +ves
(Consider testing one thing at a time -- test this param, now test this param, etc.)

#### 3.2 Start & end
3.2.1 If looking for consecutive numbers/chars, etc., check what happens at the starts and ends. What if the start is 0, etc.
3.2.2 At the end, do you remember to do a final check to see if you got a sequence at the end of the loop?)

### 3.3 Small extremes 
3.3.1 null, empty, length 1 (what counts as “small”?)

#### 3.4 Large extremes
3.4.1 999, 1000, 1001 (what counts as “large”?)

#### 3.5 “Illegal” input
3.5.1 (nulls, etc.)

#### 3.6 “Strange”/Uncommon input
3.6.1 Already sorted, sorted in reverse, all duplicates, element is in last index of array of max size, special characters </a> etc.

#### 3.7 Scalability/concurrency
3.7.1. Spin up tests in a while loop, using different servers

#### 3.8 Security
3.8.1 Can/should the user be able to modify things after creation? Should we be making this immutable?

### Decouple Objects
Test coupled objects individually. For example, if the code uses a random number generator, test the random number generator separately. For example, check that it gives a range of values, doesn't give consecutive sequences.

### Testing Big Data
How would you verify test cases that are so large there is no previous known answer? E.g., count all A's in crawled internet index. Well you could use statistics -- estimate how common A's are, get avg. number of A's on a single page, then multiply by the number of pages scanned and see if your answer is close.

</details>

## SQL

### Wildcards


<details>
 <summary>
 </summary>

* _ = single character
* % = wildcard

```sql

# Find customers with "a" in second position

SELECT *
FROM Customers
WHERE Name LIKE '_a%'

# Find customers where name does not start with "a"

SELECT *
FROM Customers
WHERE Name NOT LIKE 'a%'

```

</details>

### Joins

#### Left join

<details>
 <summary>
 </summary>

Returns everything in the left table, and anything that matches in the right table.

```sql

# Get all customers and any orders they might have

SELECT Customers.CustomerID, Orders.OrderId
FROM Customers
LEFT JOIN Orders ON Customers.CustomerId = Orders.CustomerID
ORDER BY Customers.CustomerID

```

</details>

#### Inner join

<details>
 <summary>
 </summary>

Returns records that have values in both tables.

```sql

SELECT Orders.OrderId, Customers.CustomerID
FROM Orders
INNER JOIN Customers ON Customers.CustomerId = Orders.CustomerId

```

</details>

#### Full outer join

<details>
 <summary>
 </summary>

Returns everything in both tables

```sql

SELECT Customer.CustomerId, Orders.OrderId
FROM Customers
FULL OUTER JOIN Orders On Customer.CustomerId = Orders.CustomerId

```
</details>

### Nested queries

<details>
 <summary>
 </summary>

```sql
SELECT {field}
FROM {table_one}
INNER JOIN
(SELECT {field}
 FROM {table}
 WHERE {condition}
 GROUPBY {field}
 HAVING {condition}) as SomeName
ON table_one.id = SomeName.id

SELECT TenantName
FROM Tenants
INNER JOIN
 (SELECT TenantID FROM AptTenants GROUPBY TenantID HAVING COUNT(*) > 1) as AptCount
ON Tenants.TenantID = AptCount.TenantID


```
</details>

## Big Data


<details>
 <summary>
If data too big to fit in memory, what do?
</summary>


* If data is too big to fit in memory, well, if we can just read one element at a time it doesn't matter how big the data is

* Use an external sort

* Hash each piece of data (e.g., word in a file), and send it to a different file/serverC depending on the hash

</details>


<details>
 <summary>
  MapReduce
 </summary>

* MapReduce: Map, Shuffle, Reduce
E.g. To count words in files:
![MapReduceImg](https://s3-us-west-2.amazonaws.com/content.edupristine.com/images/blogs/mapreduce-example.jpg)

</details>
