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

✅ Example:

* Iterative Fibonacci → O(1) space.
* Recursive Fibonacci → O(n) space (stack frames).

---

# 🔹 5. Practical Example

### Example 1: Binary Search

```cpp
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

* Best case (element at mid first try): **Ω(1)**
* Worst case (logarithmic splits until found/not found): **O(log n)**
* Average case: **Θ(log n)**

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

✅ With this, you’ll be able to **analyze any algorithm**.
Next, when we move into Arrays & Strings, we’ll **apply these notations** directly to real problems (sliding window, hashing, sorting, etc.).

---

👉 Do you want me to also create a **cheat sheet of complexities** for the most common algorithms & data structures (searching, sorting, stacks, queues, heaps, trees, graphs, DP) that you can keep handy while studying?
