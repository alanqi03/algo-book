# Constraints

Problem constraints are not just validation rules. They are clues about which algorithms are fast enough, which data structures fit in memory, and which properties of the input should be used.

Before writing code, translate the largest possible input into an approximate amount of work. This often rules out most approaches immediately.

## Input Size Hints at Runtime

The following table is a rough guide for interview problems. Actual limits depend on the language, time limit, constant factors, and number of test cases.

| Maximum input size | Complexity that may be feasible | Common approaches |
|---|---|---|
| `n <= 10` | `O(n!)` | Generate permutations, exhaustive search |
| `n <= 20` | `O(2^n)` | Subsets, backtracking, bitmask DP |
| `n <= 100` | `O(n^3)` | Floyd–Warshall, interval DP |
| `n <= 2,000` | `O(n^2)` | Compare pairs, 2D DP |
| `n <= 200,000` | `O(n log n)` | Sorting, heaps, balanced trees |
| `n <= 1,000,000` | `O(n)` | Hashing, counting, one-pass scans |
| `n` near `10^9` or larger | `O(log n)` or `O(1)` | Binary search, math, formulas |

These are not guarantees. For example, a simple `O(n^2)` loop may work for a few thousand elements, while an `O(n^2)` algorithm that creates large objects at every step may not.

### Estimate the Work

Substitute the maximum constraint into the complexity:

- If `n = 200,000`, then `n^2` is about `4 * 10^10` operations and is far too slow.
- For the same input, `n log2(n)` is about `3.5 * 10^6`, which is much more realistic.
- If `n = 20`, then `2^n` is about one million, so subset enumeration may be intended.

The constraints do not prove which algorithm to use, but they establish a target complexity.

## Example: Two Sum

Suppose the problem asks whether an array contains two values that add to a target.

If `n <= 1,000`, checking every pair requires about one million comparisons and may be acceptable:

```python
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            return True
```

If `n <= 200,000`, the same `O(n^2)` approach is not viable. The constraint suggests an `O(n)` hash set or an `O(n log n)` sort followed by two pointers:

```{code-block} python
---
linenos:
---
def has_pair_with_sum(nums, target):
    seen = set()

    for num in nums:
        if target - num in seen:
            return True
        seen.add(num)

    return False
```

The maximum input size changed which solution was acceptable even though the problem itself did not change.

## Consider Every Input Dimension

When a problem has multiple inputs, analyze their combined effect rather than looking at each constraint separately.

- Two arrays of sizes `n` and `m` may lead to `O(nm)`, `O(n + m)`, or `O((n + m) log(n + m))` work.
- A graph has both `V` vertices and `E` edges. An adjacency-list traversal is `O(V + E)`, while an adjacency matrix requires `O(V^2)` space.
- An `R x C` matrix contains `RC` cells, so visiting every cell is `O(RC)`.
- An algorithm that performs `k` work for every element is `O(nk)`. A small bound on `k` may make this practical.

Also read constraints across test cases. If there are `t` test cases, `n <= 100,000` for each case sounds large. However, a statement such as “the sum of `n` over all test cases does not exceed `200,000`” means an `O(n log n)` solution per case is usually intended.

## Value Constraints Suggest Data Structures

The range of the values can matter as much as the number of values.

### Small Value Range

If every value is between `0` and `100`, a fixed frequency array may be simpler and faster than a hash map:

```python
frequency = [0] * 101
for value in nums:
    frequency[value] += 1
```

This can suggest counting sort, prefix counts, bucket algorithms, or a bitset.

### Large Coordinates but Few Values

If coordinates can be as large as `10^9` but there are only `10^5` intervals or points, do not allocate an array covering every coordinate. Sort the relevant points, use a sweep line, or apply coordinate compression.

### Small Parameters

A small secondary parameter often belongs in the state:

- `k <= 20` may allow subset enumeration or bitmask DP.
- `k <= 100` may allow `O(nk)` dynamic programming.
- A small number of coupons, stops, or removed obstacles may become an extra graph state.

## Structural Constraints Suggest Algorithms

Certain words in the constraints unlock specific techniques:

| Constraint or property | Useful implication |
|---|---|
| The input is sorted | Binary search or two pointers may apply |
| All numbers are non-negative | Sliding windows and Dijkstra become possible |
| Negative edge weights exist | Dijkstra is invalid; consider Bellman–Ford |
| The graph is a DAG | Topological sorting and DAG dynamic programming apply |
| The graph is a tree | There are `V - 1` edges and a unique simple path between two nodes |
| Values come from a small alphabet | Use a fixed-size frequency array or bitmask |
| Intervals have large endpoints | Sort boundary events instead of iterating through every coordinate |
| A predicate changes from false to true once | Binary search on the answer may apply |

Constraints can also reveal edge cases. Allowing negative numbers may break a sliding window. Allowing duplicates affects whether a set is sufficient. Allowing an empty input or a single element changes initialization and boundary handling.

## Space Constraints Matter Too

An algorithm can be fast enough and still use too much memory.

For `V = 100,000`, an adjacency matrix contains `10^10` entries and is infeasible. An adjacency list uses `O(V + E)` space and stores only edges that exist.

Similarly:

- a 2D DP table uses `O(nm)` space even when its runtime is acceptable;
- many DP tables can be reduced to one or two rows;
- recursion depth may be unsafe for a long linked list, tree, or graph in Python;
- generating every answer requires at least enough time and space to represent the output.

Always distinguish between the input size and the value range. An array of `100,000` numbers whose values reach `10^9` needs `O(n)` storage, not an array of size `10^9`.

## A Constraint-Driven Workflow

1. Identify the maximum values of every input dimension.
2. Estimate the work and memory used by the obvious solution.
3. Reject complexities that cannot fit the limits.
4. Use value and structural constraints to choose candidate techniques.
5. Check whether the total across test cases changes the estimate.
6. Verify boundary cases such as empty inputs, duplicates, negative values, and maximum values.

Constraints narrow the search space for the solution. Instead of asking only “What algorithm solves this problem?”, also ask “What algorithm could possibly finish for the largest allowed input?”
