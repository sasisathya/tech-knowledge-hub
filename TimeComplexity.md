# 🔹 1. Why Complexity Analysis?

When we write an algorithm, we want to know:

* **How much time will it take?** (Time Complexity)
* **How much memory will it need?** (Space Complexity)

But we don’t measure in **seconds** (depends on machine, compiler, etc.) — instead, we measure **growth with input size (n)**.

---

# 🔹 2. Asymptotic Notations

These notations describe how an algorithm behaves as input size grows.

### **Big O (O-notation) → Worst Case**

* **Definition**: Upper bound of time.
* Means “in the worst scenario, the algorithm won’t take longer than this.”
* Used most often in interviews.

✅ Example: Linear Search

* Find an element in array of size `n`.
* Worst case = element not found → check all `n`.
* Time = **O(n)**.

---

### **Omega (Ω-notation) → Best Case**

* **Definition**: Lower bound.
* Means “at least this much time is needed.”
* Useful for understanding minimum performance.

✅ Example: Linear Search

* Best case = element is first → just 1 check.
* Time = **Ω(1)**.

---

### **Theta (Θ-notation) → Average / Tight Bound**

* **Definition**: Average-case or tight bound.
* Means “the algorithm grows at this rate in general.”
* If an algorithm always takes about the same time regardless of best/worst → Θ is used.

✅ Example: Linear Search

* On average, element found after `n/2` steps.
* Time ≈ **Θ(n)**.

---

# 🔹 3. Common Time Complexities (Hierarchy)

From best → worst:

1. **O(1)** → Constant time (e.g., accessing array element)
2. **O(log n)** → Logarithmic (binary search)
3. **O(n)** → Linear (traversing array)
4. **O(n log n)** → Linearithmic (merge sort, quicksort avg case)
5. **O(n²)** → Quadratic (nested loops, bubble sort)
6. **O(2ⁿ)** → Exponential (subset generation, recursion without memoization)
7. **O(n!)** → Factorial (permutations, traveling salesman brute force)

---

# 🔹 4. Space Complexity

Same idea, but measures **extra memory** used:

* Variables
* Data structures
* Recursion stack

---
# 🔹 6. Quick Rules of Thumb

* Drop **constants**: O(2n) → O(n)
* Drop **non-dominant terms**: O(n² + n) → O(n²)
* Nested loops multiply complexities
* Sequential statements add complexities (O(n) + O(n²) → O(n²))

---

# 🔹 7. Summary Table

| Notation | Meaning                | Example            |
| -------- | ---------------------- | ------------------ |
| **O**    | Worst case upper bound | O(n) linear search |
| **Ω**    | Best case lower bound  | Ω(1) linear search |
| **Θ**    | Tight bound / average  | Θ(n) linear search |

---
Perfect ✅ — here’s your **DSA Complexity Cheat Sheet (Big O, Ω, Θ)** 🚀
This is a **one-pager style reference** you can keep handy while learning/practicing.

---

# 📌 DSA Complexity Cheat Sheet

## 🔹 Arrays & Strings

| Operation                 | Best (Ω) | Average (Θ) | Worst (O) |
| ------------------------- | -------- | ----------- | --------- |
| Access element            | Ω(1)     | Θ(1)        | O(1)      |
| Search (linear)           | Ω(1)     | Θ(n)        | O(n)      |
| Search (binary, sorted)   | Ω(1)     | Θ(log n)    | O(log n)  |
| Insert at end (amortized) | Ω(1)     | Θ(1)        | O(1)      |
| Insert/delete at position | Ω(1)     | Θ(n)        | O(n)      |
| Reverse string/array      | Ω(n)     | Θ(n)        | O(n)      |

---

## 🔹 Searching & Sorting

| Algorithm      | Best (Ω)   | Average (Θ) | Worst (O)  |
| -------------- | ---------- | ----------- | ---------- |
| Linear Search  | Ω(1)       | Θ(n)        | O(n)       |
| Binary Search  | Ω(1)       | Θ(log n)    | O(log n)   |
| Bubble Sort    | Ω(n)       | Θ(n²)       | O(n²)      |
| Insertion Sort | Ω(n)       | Θ(n²)       | O(n²)      |
| Selection Sort | Ω(n²)      | Θ(n²)       | O(n²)      |
| Merge Sort     | Ω(n log n) | Θ(n log n)  | O(n log n) |
| Quick Sort     | Ω(n log n) | Θ(n log n)  | O(n²)      |
| Heap Sort      | Ω(n log n) | Θ(n log n)  | O(n log n) |
| Counting Sort  | Ω(n+k)     | Θ(n+k)      | O(n+k)     |
| Radix Sort     | Ω(nk)      | Θ(nk)       | O(nk)      |

---

## 🔹 Linked List

| Operation              | Best (Ω) | Average (Θ) | Worst (O) |
| ---------------------- | -------- | ----------- | --------- |
| Search                 | Ω(1)     | Θ(n)        | O(n)      |
| Insert at head/tail    | Ω(1)     | Θ(1)        | O(1)      |
| Delete head/tail       | Ω(1)     | Θ(1)        | O(1)      |
| Insert/delete at index | Ω(1)     | Θ(n)        | O(n)      |

---

## 🔹 Stacks & Queues

| Operation       | Best (Ω) | Average (Θ) | Worst (O) |
| --------------- | -------- | ----------- | --------- |
| Push/Pop        | Ω(1)     | Θ(1)        | O(1)      |
| Enqueue/Dequeue | Ω(1)     | Θ(1)        | O(1)      |
| Peek/Top        | Ω(1)     | Θ(1)        | O(1)      |

---

## 🔹 Hashing (Hash Table / Hash Map)

| Operation | Best (Ω) | Average (Θ) | Worst (O)         |
| --------- | -------- | ----------- | ----------------- |
| Search    | Ω(1)     | Θ(1)        | O(n) (collisions) |
| Insert    | Ω(1)     | Θ(1)        | O(n)              |
| Delete    | Ω(1)     | Θ(1)        | O(n)              |

---

## 🔹 Trees (Binary Tree / BST / Balanced BST)

| Operation                     | Best (Ω) | Average (Θ) | Worst (O) |
| ----------------------------- | -------- | ----------- | --------- |
| Search (BST)                  | Ω(1)     | Θ(log n)    | O(n)      |
| Insert (BST)                  | Ω(1)     | Θ(log n)    | O(n)      |
| Delete (BST)                  | Ω(1)     | Θ(log n)    | O(n)      |
| Balanced BST (AVL, Red-Black) | Ω(log n) | Θ(log n)    | O(log n)  |

---

## 🔹 Heaps (Min/Max Heap)

| Operation       | Best (Ω) | Average (Θ) | Worst (O) |
| --------------- | -------- | ----------- | --------- |
| Insert          | Ω(1)     | Θ(log n)    | O(log n)  |
| Extract Min/Max | Ω(1)     | Θ(log n)    | O(log n)  |
| Heapify         | Ω(n)     | Θ(n)        | O(n)      |

---

## 🔹 Graphs (V = vertices, E = edges)

| Algorithm              | Complexity     |
| ---------------------- | -------------- |
| BFS / DFS              | O(V + E)       |
| Dijkstra (min-heap)    | O((V+E) log V) |
| Bellman-Ford           | O(VE)          |
| Floyd-Warshall         | O(V³)          |
| Kruskal’s (MST)        | O(E log V)     |
| Prim’s (MST, min-heap) | O(E log V)     |

---

## 🔹 Dynamic Programming

| Problem Type                | Typical Complexity |
| --------------------------- | ------------------ |
| Fibonacci (DP)              | O(n)               |
| Knapsack (0/1)              | O(nW)              |
| LCS / Edit Distance         | O(nm)              |
| Matrix Chain Multiplication | O(n³)              |
| Subset Sum / Partition      | O(n \* sum)        |

---


✅ With this cheat sheet, you can **quickly recall complexity bounds** for almost all standard DSA problems.

---
Perfect 🚀 — let’s turn this into a **visual DSA Roadmap Chart** that connects **topics → complexities**.

Since I can’t draw directly here, I’ll give you a **structured roadmap flow diagram (text-visual)**. You can literally print or convert this into a **mindmap / flowchart** in tools like Excalidraw, Miro, Notion, or even on paper.

---

# 📌 DSA Complexity Roadmap (Theory → Problems)

```
START
  |
  ├── Complexity Basics
  |     ├── Big O → Worst Case
  |     ├── Ω → Best Case
  |     └── Θ → Tight/Average Case
  |
  ├── Arrays & Strings (O(n), O(n²))
  |     ├── Traversals → O(n)
  |     ├── Sliding Window → O(n)
  |     ├── Two Pointers → O(n)
  |     └── Substring/Anagram → O(n)
  |
  ├── Searching & Sorting
  |     ├── Linear Search → O(n)
  |     ├── Binary Search → O(log n)
  |     ├── Bubble/Selection/Insertion → O(n²)
  |     ├── MergeSort/QuickSort → O(n log n)
  |     └── HeapSort → O(n log n)
  |
  ├── Recursion & Backtracking
  |     ├── Subset/Permutations → O(2ⁿ) / O(n!)
  |     ├── Divide & Conquer (QuickSelect) → O(n) avg
  |     └── N-Queens/Sudoku → O(2ⁿ)
  |
  ├── Linked List (O(n))
  |     ├── Access/Search → O(n)
  |     ├── Insert/Delete (head/tail) → O(1)
  |     └── Reverse/Cycle Detection → O(n)
  |
  ├── Stacks & Queues
  |     ├── Push/Pop/Enqueue/Dequeue → O(1)
  |     └── Monotonic Stack/Queue → O(n)
  |
  ├── Hashing
  |     ├── Insert/Search/Delete → O(1) avg, O(n) worst
  |     └── Frequency Counting → O(n)
  |
  ├── Trees & BSTs
  |     ├── Traversals → O(n)
  |     ├── BST Search/Insert/Delete → O(log n) avg, O(n) worst
  |     └── Balanced BST (AVL/Red-Black) → O(log n)
  |
  ├── Heaps & Priority Queue
  |     ├── Insert/Delete → O(log n)
  |     ├── Heapify → O(n)
  |     └── Kth largest/smallest → O(n log k)
  |
  ├── Graphs
  |     ├── BFS/DFS → O(V+E)
  |     ├── Dijkstra → O((V+E) log V)
  |     ├── Bellman-Ford → O(VE)
  |     ├── Floyd-Warshall → O(V³)
  |     └── MST (Kruskal/Prim) → O(E log V)
  |
  ├── Dynamic Programming
  |     ├── Fibonacci DP → O(n)
  |     ├── Knapsack (0/1) → O(nW)
  |     ├── LCS/Edit Distance → O(nm)
  |     ├── Matrix Chain Multiplication → O(n³)
  |     └── Subset Sum → O(n * sum)
  |
  └── Advanced
        ├── Tries → O(L) (L = length of word)
        ├── Segment Trees/Fenwick → O(log n) per query
        ├── DSU (Union-Find) → O(α(n)) ≈ O(1)
        └── Bit Manipulation → O(1) per op
```

---

# 🔹 How to Use This

* **Weekdays (theory):** Pick a section (e.g., Arrays & Strings), study complexity + algorithms.
* **Weekends (practice):** Solve problems of that category, focusing on those complexities.
* As you move down the chart, problems get progressively **harder**.

---

✅ With this roadmap:

* You’ll **cover all DSA topics in order of importance**
* You’ll **know the exact complexity class** each problem belongs to
* You’ll avoid confusion about best/worst/average cases

---

👉 Do you want me to **turn this into a visual mindmap image** (like a clean chart with arrows and complexity tags) so you can keep it as a quick reference poster?

