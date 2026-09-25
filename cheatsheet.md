# Cheatsheet

Use this chapter as a quick pattern-matching guide. First identify the data structure or shape of the input, then match the question to the “When to use it” column. The problem's [constraints](constraints.md) should confirm whether the resulting runtime is feasible.

## Arrays

| Algorithm or pattern | When to use it |
|---|---|
| [Two Pointers](3a.md) | The input is sorted, you need a pair or range satisfying a condition, two sequences must be compared, or values should be moved in place without extra storage. Pointers may move toward each other or in the same direction. |
| [Sliding Window](3b.md) | The answer concerns a contiguous substring or subarray and the window can be expanded or shrunk while maintaining state such as a sum, length, or frequency map. |
| [Binary Search](3d.md) | The input is sorted, a predicate is monotonic, or the problem asks for the minimum or maximum value that satisfies a condition. |
| [Kadane's Algorithm](3f.md) | Find the maximum or minimum sum of a contiguous subarray in one pass. |
| [Maximum Product Subarray](3f.md) | Find the maximum product of a contiguous subarray; negative values require tracking both the current minimum and maximum products. |
| [Prefix Sum](3f.md) | Answer repeated range-sum queries or count subarrays whose sum satisfies a condition. Combine prefix sums with a hash map when earlier cumulative sums must be found quickly. |

## Stacks

| Algorithm or pattern | When to use it |
|---|---|
| [Stack for Nested Elements](3c.md) | Parse matching parentheses, nested expressions, paths, or structures where the most recently opened element must be closed first. |
| [Monotonic Stack](3c.md) | Find the next or previous greater or smaller element, resolve elements when a boundary appears, or process histogram/temperature-style problems in linear time. |

## Intervals

| Algorithm or pattern | When to use it |
|---|---|
| [Sort by Start Time](3e.md) | Process intervals from left to right to merge overlaps, insert an interval, or compare each interval with the previously processed range. |
| [Sort by End Time](3e.md) | Greedily select the most non-overlapping intervals, minimize removals, or keep the interval that leaves the most room for future choices. |
| [Sweep Line](3e.md) | Count active intervals, find maximum overlap, calculate required resources, or process range additions by converting boundaries into `(event, delta)` pairs. |

## Linked Lists

| Algorithm or pattern | When to use it |
|---|---|
| [Fast and Slow Pointers (Tortoise and Hare)](5.md) | Detect a cycle, find the start of a cycle, locate the middle node, or compare positions reached at different traversal speeds using `O(1)` extra space. |

## Trees

| Algorithm or pattern | When to use it |
|---|---|
| [Depth-First Search](6a.md) | Explore a root-to-leaf path, compute information from subtrees, search deeply, or use preorder, inorder, or postorder relationships. |
| [Breadth-First Search](6a.md) | Process a tree level by level, find minimum depth, obtain a level-order traversal, or solve a shortest-edge-distance problem. |
| [Tree DP](6c.md) | Combine child-subtree results into a result for each parent, such as subtree size, height, diameter, or other bottom-up states. |
| [Rerooting DP](6c.md) | Compute a whole-tree answer for every possible root by solving one root first and transferring its result across each edge. |
| [Trie](6b.md) | Store and query strings by prefix, perform autocomplete, search a dictionary, or share work across many words with common prefixes. |

## Graphs

| Algorithm or pattern | When to use it |
|---|---|
| [Breadth-First Search](7.md) | Explore an unweighted graph level by level, find a shortest path measured in edges, or process all nodes at the same distance together. |
| [Multi-Source BFS](7d.md) | Find the distance to the nearest one of several sources by placing every source in the initial queue. |
| [Depth-First Search](7.md) | Explore connected components, detect or traverse graph structure, search paths, or perform recursive enter/exit processing. |
| [Topological Sorting](7b.md) | Order tasks with directed dependencies, detect a cycle in a directed graph, or process a DAG so every prerequisite comes first. |
| [Topological Sort + DP](7b.md) | Compute longest paths or other dependency-based DP values in a DAG after all incoming states have been processed. |
| [Union Find](7b.md) | Repeatedly merge components and test connectivity, detect redundant undirected edges, or support Kruskal's algorithm. |
| [BFS Shortest Path](7d.md) | Find shortest paths when every edge has the same weight. |
| [Dijkstra's Algorithm](7d.md) | Find shortest paths in a weighted graph when every edge weight is non-negative. |
| [State-Space Dijkstra](7d.md) | The future also depends on state such as coupons used, fuel remaining, keys collected, or obstacles removed. |
| [Bellman–Ford](7d.md) | Negative edge weights may exist, a reachable negative cycle must be detected, or the number of allowed edges is limited. |
| [Prim's Algorithm](7c.md) | Build a minimum spanning tree by repeatedly adding the cheapest edge from the current tree to a new vertex. |
| [Kruskal's Algorithm](7c.md) | Build a minimum spanning tree by sorting edges globally and using Union Find to reject cycles. |

## Heaps

| Algorithm or pattern | When to use it |
|---|---|
| [Heap / Priority Queue](8.md) | Repeatedly access the smallest or largest item, maintain a dynamic top `k`, schedule by priority, merge sorted sources, or power algorithms such as Dijkstra and Prim. |
| [Quickselect](8.md) | Find the `k`th smallest or largest item in expected `O(n)` time when the other items do not need to remain ordered. Prefer a heap when values arrive as a stream or repeated top-`k` access is required. |

## Dynamic Programming

| Algorithm or pattern | When to use it |
|---|---|
| [Top-Down DP with Memoization](9.md) | A recursive recurrence is natural and only some states may be visited. Cache each state so overlapping subproblems are solved once. |
| [Bottom-Up DP with Tabulation](9.md) | The dependency order is known and recursion overhead or recursion depth should be avoided. |
| [1D DP](9b.md) | Each state can be described by one changing index or value, such as a position, amount, or day. |
| [2D Grid DP](9c.md) | A state depends on a row and column, often while counting paths or optimizing movement through a matrix. |
| [2D String DP](9c.md) | Compare prefixes of two strings for subsequences, edit distance, matching, or similar relationships. |
| [0/1 Knapsack](9a.md) | Each item may be chosen at most once while optimizing value or determining whether a capacity or target can be reached. |
| [Unbounded Knapsack](9a.md) | Items may be reused any number of times, as in coin change or repeated cutting/selection problems. |

## Backtracking

| Algorithm or pattern | When to use it |
|---|---|
| [Permutations](10.md) | Generate orderings by choosing one unused option at each decision level. |
| [Combinations and Subsets](10.md) | Generate selections where order does not matter, usually by advancing a start index. |
| [Path-Finding with Backtracking](10.md) | Explore candidate paths while marking a choice, recursing, and undoing the choice so it can be reused by another path. |

Backtracking is most appropriate when the search space is small enough to enumerate and invalid branches can be pruned early. Use dynamic programming instead when many branches reach the same state and only an optimal value or count is needed.
