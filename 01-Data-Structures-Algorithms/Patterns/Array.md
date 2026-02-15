Got it—here’s a **fast, pattern‑first DSA sequence** that covers ~90% of common interview problems. Follow this order, learn the trigger words, and use the included JS templates.

---

## The 80/20 Pattern Ladder (learn in this sequence)

1. **Arrays & Hashing (Sets/Maps)**

* **Use when:** membership, frequency counts, deduping.
* **Triggers:** “frequency,” “anagram,” “seen before.”
* **Starters:** *Two Sum*, *Valid Anagram*, *Group Anagrams*.
* **Pitfalls:** forgetting O(1) average assumptions; poor key choices.

2. **Two Pointers (incl. fast–slow)**

* **Use when:** sorted arrays/strings; pair/sum; palindromes; removing in‑place.
* **Triggers:** “sorted,” “pair,” “closest,” “remove duplicates.”
* **Starters:** *Remove Duplicates from Sorted Array*, *3Sum*, *Container With Most Water*.
* **Pitfalls:** pointer movement invariants; missing duplicates handling.

3. **Sliding Window (fixed & shrinking)**

* **Use when:** “longest/shortest subarray/substring” with constraint.
* **Triggers:** “at most/at least K,” “no repeats.”
* **Starters:** *Longest Substring Without Repeating Characters*, *Minimum Window Substring*, *Longest Repeating Character Replacement*.
* **Pitfalls:** not shrinking while violating the constraint.

4. **Prefix Sums / Differences**

* **Use when:** subarray sums, ranges, “equals K”.
* **Triggers:** “sum of subarray equals…”, “range updates/queries.”
* **Starters:** *Subarray Sum Equals K*, *Range Sum Query*, *Maximum Size Subarray Sum = K*.
* **Pitfalls:** off‑by‑one indices; not hashing prefix sums.

5. **Intervals (sort + merge / sweep / min‑heap)**

* **Use when:** overlapping times, merging/rooms.
* **Triggers:** “interval,” “overlap,” “meeting rooms.”
* **Starters:** *Merge Intervals*, *Meeting Rooms II*, *Insert Interval*.
* **Pitfalls:** inclusive/exclusive endpoints; sort key choice.

6. **Stack & Monotonic Stack**

* **Use when:** next/previous greater/smaller; spans; histograms; parentheses.
* **Triggers:** “next greater,” “first smaller to left/right.”
* **Starters:** *Daily Temperatures*, *Next Greater Element II*, *Largest Rectangle in Histogram*.
* **Pitfalls:** mixing indices vs values; equal‑value policy (≤ vs <).

7. **Binary Search (array) → Binary Search on Answer (search space)**

* **Use when:** sorted data; or monotonic predicate (“can we do X with M?”).
* **Triggers:** “min/max capacity/time,” “Koko bananas,” “ship within D days.”
* **Starters:** *Search in Rotated Array*, *First/Last Position*, *Koko Eating Bananas*, *Capacity to Ship Packages*.
* **Pitfalls:** mid calc & invariants; proving monotonicity for “answer”.

8. **Linked Lists**

* **Use when:** reverse/merge/find middle/detect cycle.
* **Starters:** *Reverse Linked List*, *Merge Two Sorted Lists*, *Cycle II*, *Reorder List*.
* **Pitfalls:** pointer loss; off‑by‑one for middle; cycle start logic.

9. **Trees (DFS/BFS, BST properties, LCA)**

* **Use when:** hierarchical data, path sums, validity checks.
* **Starters:** *Level Order Traversal*, *Validate BST*, *LCA of BST/Binary Tree*, *Diameter of Binary Tree*.
* **Pitfalls:** null base cases; recursion stack depth.

10. **Heaps / Priority Queue**

* **Use when:** top‑k, k‑way merge, scheduling min/max.
* **Starters:** *Top K Frequent Elements*, *Kth Largest*, *Merge k Sorted Lists*.
* **Pitfalls:** min‑heap vs max‑heap; comparator mistakes.

11. **Backtracking (search with pruning)**

* **Use when:** subsets, permutations, combinations, boards.
* **Starters:** *Subsets*, *Permutations*, *Combination Sum*, *Word Search*.
* **Pitfalls:** not undoing state; missing pruning constraints.

12. **Dynamic Programming**

* **1D DP:** *House Robber*, *Coin Change*, *LIS* (binary‑search variant).
* **2D/Grid/String DP:** *Unique Paths*, *Edit Distance*, *LCS*.
* **Pitfalls:** unclear state definition/transition; order of evaluation; space optimization.

13. **Graphs (BFS/DFS, Toposort) + Union‑Find**

* **Use when:** connectivity, shortest paths (unweighted), cycles, components.
* **Starters:** *Number of Islands*, *Course Schedule*, *Clone Graph*, *Network Delay Time* (Dijkstra), *Number of Provinces*, *Redundant Connection*.
* **Pitfalls:** missing visited set; directed vs undirected; union‑find without path compression.

> **Advanced/optional (after the above):** Trie, Segment Tree/Fenwick (BIT), Bitmask DP, MST (Kruskal/Prim).

---

## Quick JS Templates (drop‑in)

**Sliding Window (at most K distinct)**

```js
function longestKDistinct(s, k) {
  let left = 0, best = 0;
  const cnt = new Map();
  for (let right = 0; right < s.length; right++) {
    cnt.set(s[right], (cnt.get(s[right]) || 0) + 1);
    while (cnt.size > k) {
      const c = s[left++];
      cnt.set(c, cnt.get(c) - 1);
      if (cnt.get(c) === 0) cnt.delete(c);
    }
    best = Math.max(best, right - left + 1);
  }
  return best;
}
```

**Binary Search on Answer (min true)**

```js
function minTrue(low, high, ok) {
  while (low < high) {
    const mid = Math.floor((low + high) / 2);
    if (ok(mid)) high = mid;
    else low = mid + 1;
  }
  return low;
}
```

**Monotonic Stack (next greater index)**

```js
function nextGreaterIndices(nums) {
  const n = nums.length, res = Array(n).fill(-1), st = [];
  for (let i = 0; i < n; i++) {
    while (st.length && nums[st[st.length - 1]] < nums[i]) {
      res[st.pop()] = i;
    }
    st.push(i);
  }
  return res;
}
```

**Union‑Find (DSU)**

```js
class DSU {
  constructor(n) { this.p = Array.from({length:n}, (_,i)=>i); this.r = Array(n).fill(0); }
  find(x){ return this.p[x] === x ? x : (this.p[x] = this.find(this.p[x])); }
  union(a,b){
    a = this.find(a); b = this.find(b);
    if (a === b) return false;
    if (this.r[a] < this.r[b]) [a,b] = [b,a];
    this.p[b] = a;
    if (this.r[a] === this.r[b]) this.r[a]++;
    return true;
  }
}
```

**Backtracking (subsets)**

```js
function subsets(nums) {
  const res = [], path = [];
  (function dfs(i){
    if (i === nums.length) { res.push([...path]); return; }
    dfs(i + 1);
    path.push(nums[i]);
    dfs(i + 1);
    path.pop();
  })(0);
  return res;
}
```

---

## 14‑Day “Fast Track” Plan

* **Day 1:** Arrays & Hashing
* **Day 2:** Two Pointers
* **Day 3:** Sliding Window
* **Day 4:** Prefix Sums
* **Day 5:** Intervals
* **Day 6:** Stack / Monotonic
* **Day 7:** Binary Search (+ on Answer)
* **Day 8:** Linked Lists
* **Day 9:** Trees (DFS/BFS, BST)
* **Day 10:** Heaps / PQ
* **Day 11:** Backtracking
* **Day 12:** DP 1D
* **Day 13:** DP Grid/String
* **Day 14:** Graphs + Union‑Find + review

**Daily routine (2–3 hrs):**

1. 15m: read cheat‑sheet for the pattern (triggers + template).
2. 60–90m: 2 easy → 2 medium from the “Starters”.
3. 20m: re‑solve one from memory; note mistakes.
4. 20m: spaced repetition: tag problems by pattern and re‑do next day.

---

## Pattern Triggers (diagnostic cheat‑sheet)

* **“subarray/substring + longest/shortest + constraint”** → Sliding Window.
* **“sum equals K / count subarrays”** → Prefix Sums (+ Map).
* **“sorted / pair / closest / dedupe in-place”** → Two Pointers.
* **“overlap / merge / rooms / calendar”** → Intervals (sort + sweep/min‑heap).
* **“next/previous greater/smaller, histogram, parentheses”** → Monotonic Stack.
* **“top‑k / kth / merge k”** → Heap or Quickselect.
* **“min/max capacity/time with feasibility check”** → Binary Search on Answer.
* **“connected components / islands / provinces”** → BFS/DFS or Union‑Find.
* **“order with prerequisites”** → Topological Sort (DAG).
* **“optimize under constraints with overlapping subproblems”** → DP.
* **“cycle detection”** → fast–slow (linked list) or DFS/Union‑Find (graph).

---

## Common pitfalls to avoid

* Off‑by‑one (windows and prefix sums).
* Missing **visited** set in graphs → infinite loops.
* Binary search invariants (decide on `[lo, hi]` contract and stick to it).
* DP without a clear state/transition; write them down first.
* Monotonic stack equality rule: choose `<` vs `<=` deliberately.

---

If you’d like, I can tailor this into a **one‑page cheat sheet** or a **week-by-week plan** for a specific timeframe and language (JS, Python, etc.)—just say the word and I’ll generate it now.

## 🔑 Arrays & Hashing (Sets/Maps) Pattern

### ✅ When to Use

* **Membership check** → "Have we seen this before?"
* **Frequency counts** → "How many times does this occur?"
* **Deduplication** → "Remove duplicates while preserving logic."
* **Fast lookups** → O(1) on average with hash tables.

---

### 🚩 Common Triggers in Problem Statements

* Mentions of **“frequency,” “count,” “duplicate,” “anagram,” “pair,” “unique,” “first occurrence.”**
* Questions like:

  * “Does this element already exist?”
  * “How many times does each element appear?”
  * “Can we group by a property/key?”

---

### ⚡ Core Starter Problems

1. **Two Sum** → Hash map for complement lookup.
2. **Valid Anagram** → Frequency count comparison.
3. **Group Anagrams** → Hashing sorted strings/char counts.
4. **Contains Duplicate** → Set membership.
5. **Top K Frequent Elements** → Hash map + heap/bucket sort.

---

### ⚠️ Pitfalls & Mistakes

* Assuming **O(1) lookup always holds** (collisions can degrade performance in worst case).
* Using the **wrong key structure** (e.g., mutable objects as keys, forgetting to normalize case/ordering).
* Not handling **negative numbers, Unicode chars, or large ranges** in counting arrays vs hash maps.
* Forgetting to reset or clear hash maps in iterative solutions.

---

### 🧠 Pro Tips

* **Set** = presence/absence check.
* **Map/Dict** = frequency counts, index mapping, group classification.
* **Counter (Python) / defaultdict** saves boilerplate.
* For **anagrams**, sort or use **char frequency tuple** as the key.
* For **subarrays**, hash prefix sums to track seen differences.

---

👉 Would you like me to also build a **pattern-to-problem roadmap** (like 10–15 problems from easy → hard) for Arrays & Hashing, similar to what we started for sliding window?
