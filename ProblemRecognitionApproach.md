# Problem Recognition Patterns

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

## __TODO__: 


### Tree problems
We often recurse when doing tree problems -- e.g., when getting the height. Can we also do something else while in the recursive method? For example, if finding the max diameter, we are finding the height of the left and right subtrees anyway, so we could also check to see if we have a new max diameter (left + right height) at the same time.

Don't forget inorder, preorder, and postorder traversals. These can often be used to find brute force solutions. E.g., find the highest, get in order, compare if trees are equal, check if contains subtree, etc. (these are rarely optimum solutions though).

(Recall an inorder traversal will give us the nodes in ascending order.)
_Trees:_
* (pre-/in/post-/level order)
* Get dist from root
* DF traversal (e.g., length)
* Get height

_General problem solving tips from other docs_

_Generate all permutations (string & array/list)_

_Generate all subsets_

_Choose k formulas_

_Recursion & backtracking reminders_

_Sort tips_

(Go through all docs to see what would be useful to summarise)

