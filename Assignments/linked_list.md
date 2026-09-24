# Linked Lists: Implementation & Algorithms Assignment

## How to use this assignment
- Questions are **cumulative**: later questions reuse code from earlier ones. Keep everything in one module (`linked_list.py`) and add to it as you go.
- Write **iterative** solutions first. Do the recursive version only where asked (Python's recursion limit is about 1000).
- For every question, write tests covering: empty list, single node, two nodes, even/odd length, duplicates, and the head/tail cases.
- State the **time and space complexity** of each solution in a comment.
- Do not convert to a Python `list` and back unless the question says so. That defeats the purpose.

## Setup: helpers used throughout
```python
class Node:
    __slots__ = ("val", "next")
    def __init__(self, val=0, next=None):
        self.val, self.next = val, next

def build(values):
    """Python list -> linked list, returns head."""
    dummy = tail = Node()
    for v in values:
        tail.next = Node(v)
        tail = tail.next
    return dummy.next

def to_list(head):
    """Linked list -> Python list (for testing only)."""
    out = []
    while head:
        out.append(head.val)
        head = head.next
    return out
```
Every problem below is tested as `assert to_list(solution(build([...]))) == [...]`.

---

# Part 1: Foundations (Node, traversal, basic operations)

**Q1. Build and print.**
Implement `build`, `to_list`, and `print_list(head)` that prints `1 -> 2 -> 3 -> None`. Then implement `length(head)`.

**Q2. Search and access.**
Implement `get(head, i)` (supports negative indexes, raises `IndexError`), `find(head, x)` (returns the index of the first `x` or `-1`), and `count(head, x)`.
*Builds on Q1: use the traversal pattern.*

**Q3. Insertion.**
Implement all three, each returning the new head:
- `insert_front(head, val)`
- `insert_back(head, val)` (O(n), no tail pointer)
- `insert_at(head, index, val)` (clamp out-of-range indexes to the ends)

**Q4. Deletion.**
Implement, each returning the new head:
- `delete_front(head)`
- `delete_back(head)`
- `delete_at(head, index)`
- `delete_value(head, x)` (first occurrence only)

**Q5. Dummy head refactor.**
Rewrite Q3 `insert_at` and Q4 `delete_at` / `delete_value` using a **dummy (sentinel) head** so the head is no longer a special case. Compare code length and number of `if` branches with your first versions.

**Q6. Delete all occurrences (LeetCode 203).**
`remove_all(head, x)` removes every node whose value is `x`. Must be a single pass.

**Q7. Delete a node given only that node (LeetCode 237).**
`delete_node(node)` where you are handed a node in the middle (never the tail) and not the head. *Hint: copy the next node's value, then skip it.* Explain in a comment why this fails for the tail.

**Q8. Wrap it in a class.**
Create `LinkedList` with `head`, `tail`, `_size` and the methods `append`, `prepend`, `insert`, `pop`, `pop_front`, `remove`, `index`, `count`, `clear`, `__len__`, `__iter__`, `__getitem__`, `__contains__`, `__repr__`.
*Builds on Q1-Q6. Target: `append`, `prepend`, `pop_front`, `len` are O(1).*

---

# Part 2: Reversal (the most reused technique)

**Q9. Reverse iteratively (LeetCode 206).**
`reverse(head)` in O(n) time and O(1) space using `prev`, `cur`, `nxt`.

**Q10. Reverse recursively.**
Same problem, recursive version. Explain the call-stack cost and why it can fail on a list with 10,000 nodes.

**Q11. Reverse a sub-range (LeetCode 92).**
`reverse_between(head, left, right)` reverses nodes from position `left` to `right` (1-indexed) in one pass.
*Builds on Q9 and Q5 (dummy head).*

**Q12. Reverse in groups of k (LeetCode 25).**
`reverse_k_group(head, k)` reverses every consecutive group of `k` nodes. Leftover nodes (fewer than `k`) stay as they are.
*Builds on Q9 and Q11.*

**Q13. Swap nodes in pairs (LeetCode 24).**
`swap_pairs(head)` by changing pointers, not values. This is the `k = 2` special case of Q12; implement it directly, then verify against `reverse_k_group(head, 2)`.

**Q14. Print in reverse without modifying the list.**
`print_reverse(head)` in two ways: (a) recursion, (b) an explicit stack. Discuss the O(n) space cost of each, then explain why "reverse, print, reverse back" gives O(1) space.

---

# Part 3: Two-Pointer (slow / fast) Techniques

**Q15. Middle node (LeetCode 876).**
`middle(head)`. For even lengths return the **second** middle. Then write `middle_first(head)` that returns the first middle.

**Q16. k-th node from the end (LeetCode 19).**
`kth_from_end(head, k)` in one pass, then `remove_kth_from_end(head, k)`.
*Builds on Q5 (dummy head) and Q4.*

**Q17. Cycle detection (LeetCode 141).**
`has_cycle(head)` using Floyd's tortoise and hare, with O(1) space. Also write a version with a `set` of visited nodes and compare space.

**Q18. Find the cycle start (LeetCode 142).**
`cycle_start(head)` returns the node where the cycle begins, or `None`.
*Builds on Q17. Write a short proof (in comments) of why resetting one pointer to the head works.*

**Q19. Cycle length and removal.**
`cycle_length(head)` and `remove_cycle(head)` (make the list acyclic by fixing the last node's `next`).
*Builds on Q18.*

**Q20. Palindrome check (LeetCode 234).**
`is_palindrome(head)` in O(n) time and O(1) extra space: find the middle (Q15), reverse the second half (Q9), compare, then **restore** the list.

**Q21. Intersection of two lists (LeetCode 160).**
`get_intersection(a, b)` returns the shared node (by identity, not value) or `None`, in O(1) space. Implement (a) the length-difference approach and (b) the two-pointer switch-heads trick.
*Builds on Q1 (length).*

---

# Part 4: Merging and Sorting

**Q22. Merge two sorted lists (LeetCode 21).**
`merge(a, b)` iteratively with a dummy head, reusing the existing nodes. Then write the recursive version.

**Q23. Remove duplicates from a sorted list (LeetCode 83).**
`dedupe_sorted(head)` keeps one copy of each value.

**Q24. Remove all duplicated values (LeetCode 82).**
`dedupe_strict(head)` removes every value that appears more than once, keeping only values that appeared exactly once.
*Builds on Q23 and Q5.*

**Q25. Remove duplicates from an unsorted list.**
`dedupe_unsorted(head)`: (a) O(n) time with a `set`, (b) O(1) space and O(n²) time with nested pointers. Discuss the trade-off.

**Q26. Insertion sort on a list (LeetCode 147).**
`insertion_sort(head)`. O(n²), but stable and useful on nearly sorted data.
*Builds on Q3 (insert into a sorted position).*

**Q27. Merge sort on a list (LeetCode 148).**
`sort_list(head)` in O(n log n) time. Steps: split at the middle (Q15), sort each half recursively, merge (Q22). Explain why merge sort suits linked lists better than quicksort or heapsort.
*Builds on Q15 and Q22.*

**Q28. Bottom-up merge sort.**
Rewrite Q27 iteratively for O(1) extra space (no recursion stack). This is the hard version of `sort_list`.

**Q29. Merge k sorted lists (LeetCode 23).**
`merge_k(lists)` using (a) a min-heap with `heapq` (tie-break with an index so nodes are never compared), and (b) divide and conquer using Q22. Compare O(N log k) for both.
*Builds on Q22.*

**Q30. Partition around a value (LeetCode 86).**
`partition(head, x)` puts all nodes `< x` before nodes `>= x`, preserving relative order. Use two dummy heads.

---

# Part 5: Rearrangement

**Q31. Odd-even list (LeetCode 328).**
`odd_even(head)` groups nodes at odd positions first, then even positions, in O(1) space.

**Q32. Rotate right by k (LeetCode 61).**
`rotate_right(head, k)`. Handle `k >= length` using modulo. *Hint: temporarily make the list circular.*

**Q33. Reorder list (LeetCode 143).**
`reorder(head)` turns `L0 -> L1 -> ... -> Ln` into `L0 -> Ln -> L1 -> Ln-1 -> ...` in place.
*Combines Q15 (middle), Q9 (reverse), and an interleaving merge. Good checkpoint question.*

**Q34. Split into k parts (LeetCode 725).**
`split_parts(head, k)` returns `k` lists whose sizes differ by at most 1, with earlier parts larger.

**Q35. Split into halves and alternate.**
`alternating_split(head)` returns two lists (nodes at even positions, nodes at odd positions). Then write `shuffle_merge(a, b)` that interleaves two lists, and confirm it inverts the split.

---

# Part 6: Arithmetic on Lists

**Q36. Add two numbers, digits in reverse order (LeetCode 2).**
`add_reverse(a, b)`: `2 -> 4 -> 3` plus `5 -> 6 -> 4` gives `7 -> 0 -> 8` (342 + 465 = 807). Handle carry and different lengths.

**Q37. Add two numbers, digits in normal order (LeetCode 445).**
`add_forward(a, b)` **without** reversing the input lists. Use stacks, or the length-alignment technique with recursion.
*Builds on Q36 and Q14.*

**Q38. Increment a number stored in a list.**
`plus_one(head)`: `1 -> 2 -> 9` becomes `1 -> 3 -> 0`. Handle `9 -> 9` (needs a new head).

**Q39. Multiply by a single digit.**
`multiply_digit(head, d)` for a number stored in reverse order. Then implement `to_int(head)` / `from_int(n)` for testing.

---

# Part 7: Doubly and Circular Linked Lists

**Q40. Doubly linked list class.**
Implement `DoublyLinkedList` with `head`, `tail`, `_size`, and all Q8 operations. Now `pop()` (from the back) and `remove_node(node)` must be **O(1)**.

**Q41. Reverse a doubly linked list.**
`reverse()` in place by swapping `prev` and `next` on every node, then fixing `head` and `tail`.

**Q42. Flatten a multilevel doubly linked list (LeetCode 430).**
Each node has `prev`, `next`, and `child`. Flatten so that child lists appear right after their parent. Implement iteratively with a stack, then recursively.

**Q43. Circular singly linked list.**
Implement `CircularList` with only a `tail` pointer (so `tail.next` is the head). Support `append`, `prepend`, `pop_front`, `rotate(k)`, and iteration that stops after one full lap.

**Q44. Insert into a sorted circular list (LeetCode 708).**
`insert_sorted_circular(head, val)`. Handle: empty list, single node, value smaller than the min, larger than the max, and all-equal values.

**Q45. Josephus problem.**
`josephus(n, k)`: `n` people in a circle, every `k`-th is eliminated. Return the survivor's position. Simulate with your `CircularList`, then compare with the closed-form recurrence `J(n) = (J(n-1) + k) mod n`.

---

# Part 8: Advanced Problems and Data-Structure Design

**Q46. Copy a list with random pointers (LeetCode 138).**
Each node has `next` and `random`. Return a deep copy in (a) O(n) space with a `dict`, and (b) O(1) extra space by interleaving copies.

**Q47. Clone a list with a cycle.**
Extend Q46 so it also works when the list contains a cycle (avoid infinite loops).
*Builds on Q17 and Q46.*

**Q48. Sort a list of 0s, 1s, and 2s.**
`sort_012(head)` in one pass by re-linking nodes (no value swapping, no counting).
*Builds on Q30 (multiple dummy heads).*

**Q49. Find the loop, then the intersection.**
Given two lists that may each have a cycle, decide if they intersect. Cases: both acyclic (Q21), same cycle, different cycles. Return the meeting node when it exists.
*Builds on Q18, Q19, Q21.*

**Q50. Skip list (search structure).**
Implement a simple `SkipList` with `insert`, `search`, `delete` using randomized levels. Explain how it achieves expected O(log n).
*Builds on the doubly and multi-pointer node ideas.*

**Q51. LRU Cache (LeetCode 146).**
Implement `LRUCache(capacity)` with O(1) `get` and `put` using a `dict` plus your doubly linked list from Q40.
*Capstone for Q40.*

**Q52. Stack and Queue from linked lists.**
Implement `LinkedStack` (push, pop, peek) and `LinkedQueue` (enqueue, dequeue, peek) using your list, all O(1). Then implement `MinStack` (O(1) `get_min`) on top of `LinkedStack`.

**Q53. Unrolled linked list (bonus).**
Each node stores a small array of up to `B` items. Implement `insert(index, val)` and `get(index)`. Analyze the trade-off between array-like cache locality and list-like insertion.

**Q54. Benchmark (capstone).**
Compare your `LinkedList`, Python `list`, and `collections.deque` using `timeit` for: append, prepend, pop from the front, pop from the back, insert in the middle, random access, and iteration, at n = 10³, 10⁴, 10⁵. Plot or tabulate the results and explain each observation (cache locality, pointer chasing, amortized resizing).

---

# Concept Coverage Checklist

| Concept | Questions |
|---|---|
| Traversal, search, count | Q1, Q2 |
| Insertion and deletion (head, tail, index, value) | Q3, Q4, Q6, Q7 |
| Dummy / sentinel node | Q5 and reused throughout |
| Reversal (iterative, recursive, range, k-group) | Q9-Q14 |
| Slow/fast pointers | Q15-Q19 |
| Palindrome, intersection | Q20, Q21 |
| Merge, dedupe | Q22-Q25 |
| Sorting (insertion, merge, bottom-up) | Q26-Q28 |
| k-way merge and heap | Q29 |
| Partition, rearrange, rotate, split | Q30-Q35 |
| Arithmetic on lists | Q36-Q39 |
| Doubly linked lists | Q40-Q42 |
| Circular lists | Q43-Q45 |
| Random pointer, cycles, deep copy | Q46-Q49 |
| Skip list, LRU cache | Q50, Q51 |
| Stack/queue/min-stack on lists | Q52 |
| Performance analysis | Q54 |

---

# Suggested Schedule
| Week | Parts | Goal |
|---|---|---|
| 1 | 1, 2 | Pointer manipulation confidence, dummy-head habit |
| 2 | 3 | Two-pointer intuition |
| 3 | 4, 5 | Merge and sort mastery |
| 4 | 6, 7 | Arithmetic, doubly and circular lists |
| 5 | 8 | Design problems and benchmarking |

# Grading Rubric (per question)
| Criterion | Weight |
|---|---|
| Correctness on all edge cases | 50% |
| Meets the stated time and space complexity | 20% |
| Code clarity (naming, comments, helper reuse) | 15% |
| Tests written | 15% |

---

# Resources

## Books
- **CLRS, *Introduction to Algorithms*:** Chapter 10 (elementary data structures: linked lists, sentinels, stacks, queues).
- **Skiena, *The Algorithm Design Manual*:** the sections on containers and dictionaries.
- **Sedgewick & Wayne, *Algorithms* (4th ed.):** the linked-list section of Chapter 1.3 (bags, queues, stacks).
- **McDowell, *Cracking the Coding Interview*:** the Linked Lists chapter, which has classic interview problems with solutions.

## Interactive visualizations
- **VisuAlgo** (visualgo.net): search for "Linked List" to step through insert, delete, and search animations.
- **Python Tutor** (pythontutor.com): paste your own code to watch pointers and objects change line by line. Very useful for debugging.
- **USFCA Data Structure Visualizations** (cs.usfca.edu/~galles/visualization): search for "Linked List" and "Skip List".

## Tutorials and articles
- **Real Python:** "Linked Lists in Python: An Introduction" (search the title on realpython.com).
- **GeeksforGeeks:** the "Linked List Data Structure" topic page, including sections on Floyd's cycle detection, merge sort on lists, and the LRU cache.
- **Python docs:** `collections.deque` and `heapq` pages at docs.python.org.
- **Wikipedia:** "Linked list", "Cycle detection" (Floyd's and Brent's algorithms), "Merge sort", "Skip list", "Unrolled linked list", "Josephus problem".

## Practice platforms
- **LeetCode:** the *Linked List* topic tag, plus the "Linked List" Explore card. The problem numbers cited above are LeetCode numbers.
- **NeetCode** (neetcode.io): the *Linked List* section of the NeetCode 150 list, with video walkthroughs.
- **HackerRank:** the *Linked Lists* subdomain under Data Structures.
- **GeeksforGeeks Practice:** filter by "Linked List".

## Video courses
- **MIT 6.006 *Introduction to Algorithms*** (MIT OpenCourseWare, YouTube): the data-structures lectures.
- **CS50 (Harvard):** the lecture on data structures (linked lists in C, but the pointer ideas carry over).
- **NeetCode's** and **Abdul Bari's** YouTube channels: search "linked list" for step-by-step walkthroughs.

## Algorithms to look up by name
| Algorithm | Search term | Used in |
|---|---|---|
| Floyd's tortoise and hare | "Floyd cycle detection" | Q17-Q19 |
| Brent's cycle detection | "Brent's algorithm" | Q17 (alternative) |
| Merge sort on linked lists | "merge sort linked list bottom-up" | Q27, Q28 |
| Dutch national flag | "Dutch national flag problem" | Q48 |
| Josephus recurrence | "Josephus problem recurrence" | Q45 |
| Skip lists | "William Pugh skip lists paper" | Q50 |
| LRU cache design | "LRU cache doubly linked list hashmap" | Q51 |

## Study tips
1. Draw the pointers on paper for every question **before** coding. Most bugs are pointer-order mistakes.
2. Use the dummy-head technique by default. Add special cases only if you must.
3. Always test with lists of length 0, 1, 2, and 3.
4. After solving, re-solve after a few days without looking, then read the top solutions and compare.
5. Use Python Tutor to visualize any solution that misbehaves.
