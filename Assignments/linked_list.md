# Linked Lists: Implementation Assignment

**Goal:** build the data structure yourself and understand how it works. No algorithm puzzles here. Each task builds on the previous one, so keep everything in one file (`linked_list.py`).

**Rules**
- Write the code yourself first, then compare with a reference.
- Draw the pointers on paper before coding each method.
- After each task, test with: empty list, 1 element, 2 elements, and several elements.
- Add a comment with the time complexity of every method.

---

## Task 1: Node and manual list
Create a `Node` class with `val` and `next`. Without any list class, build `10 -> 20 -> 30 -> None` by hand and write a loop that prints it.

**You learn:** what a node is, how `head` gives access to everything.

## Task 2: Singly linked list class (basics)
Create `LinkedList` with `head` and `_size`. Implement:
- `prepend(val)`
- `append(val)` (walk to the end)
- `__len__`
- `__iter__` (using `yield`)
- `__repr__` (prints `10 -> 20 -> 30 -> None`)

**You learn:** traversal, and how `__iter__` lets you use `for x in ll` and `list(ll)`.

## Task 3: Access and search
Add:
- `__getitem__(i)` and `__setitem__(i, val)` (support negative indexes, raise `IndexError`)
- `__contains__(val)`
- `index(val)` and `count(val)`

**You learn:** why indexing is O(n) here but O(1) in a Python `list`.

## Task 4: Insert and remove
Add:
- `insert(index, val)`
- `pop_front()`
- `pop(index=-1)`
- `remove(val)` (first occurrence, raise `ValueError` if missing)
- `clear()`

**You learn:** pointer rewiring, and the head and empty-list edge cases.

## Task 5: Add a tail pointer
Add `self.tail` and update every method from Tasks 2 and 4 so it stays correct. Make `append` O(1).

**You learn:** how one extra pointer changes complexity, and how easy it is to forget updating it (when the last node is removed, or the list becomes empty).

## Task 6: Python-style extras
Add:
- `extend(iterable)` and a constructor `LinkedList([1, 2, 3])`
- `reverse()` (in place)
- `copy()`
- `__eq__`
- `__bool__` (or rely on `__len__`)

**You learn:** making your class behave like a real Python container.

## Task 7: Doubly linked list
Create `DoublyLinkedList` with `prev` and `next` on each node, plus `head`, `tail`, `_size`. Implement all Task 2 to 6 methods, and make these **O(1)**:
- `pop()` (from the back)
- `remove_node(node)` (given a node reference)

Also add `__reversed__` that iterates from tail to head.

**You learn:** why doubly linked lists cost more memory but allow O(1) deletion and backward traversal.

## Task 8: Circular linked list
Create `CircularLinkedList` using only a `tail` pointer (`tail.next` is the head). Implement `append`, `prepend`, `pop_front`, `rotate(k)`, and an `__iter__` that stops after one full lap.

**You learn:** circular structure, and how to avoid infinite loops.

## Task 9: Stack and queue on top of your list
- `LinkedStack`: `push`, `pop`, `peek`, `is_empty`
- `LinkedQueue`: `enqueue`, `dequeue`, `peek`, `is_empty`

Both must be O(1). Decide which end of the list each uses and why.

**You learn:** how abstract data types sit on top of a concrete structure.

## Task 10: Test and compare
1. Write tests with `pytest` or plain `assert` for every method.
2. Use `timeit` to compare your `LinkedList`, Python `list`, and `collections.deque` for: append, insert at front, pop from front, and index access (n = 10,000 and 100,000).
3. Write 3 to 5 sentences explaining the results.

**You learn:** why Python's `list` often wins in practice despite the theory (cache locality), and why `deque` exists.

---

## Checklist
| Concept | Tasks |
|---|---|
| Node and `head` | 1, 2 |
| Traversal and iterator protocol | 2, 3 |
| Insert and remove (head, middle, tail) | 4 |
| Tail pointer | 5 |
| Pythonic container behavior | 6 |
| Doubly and circular variants | 7, 8 |
| Building ADTs (stack, queue) | 9 |
| Testing and performance | 10 |

## Resources
- **Visualizations:** VisuAlgo (visualgo.net, "Linked List"), Python Tutor (pythontutor.com, paste your code to see the nodes and pointers), USFCA Data Structure Visualizations.
- **Tutorial:** Real Python, "Linked Lists in Python: An Introduction".
- **Reference:** GeeksforGeeks "Linked List Data Structure" page; Python docs for `collections.deque` and the data model (`__iter__`, `__getitem__`, `__len__`).
- **Book:** CLRS, Chapter 10 (elementary data structures).
- **Video:** NeetCode or Abdul Bari on YouTube, search "linked list".
