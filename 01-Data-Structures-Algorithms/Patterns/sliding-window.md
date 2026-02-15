# Sliding Window Patterns — 5 Problems Each (with JS Solutions)

This reference packs each major sliding-window subpattern with **5 interview-style problems** and **concise JavaScript solutions**. Copy–paste and run.

> Notation: `n = nums.length`, `|s| = s.length`. Complexity given per problem.

---

## 1) Fixed-Size Window (size = K)

Use when window length is fixed.

### Template

```js
// maintain sum (or any aggregable stat) for a window of size k
let sum = 0;
for (let r = 0; r < n; r++) {
  sum += nums[r];
  if (r >= k) sum -= nums[r - k];
  if (r >= k - 1) { /* use current window [r-k+1, r] */ }
}
```

### 1.1 Max Sum of Any Subarray of Size K

**Input:** `nums, k` → **Output:** max sum. **Time:** O(n)

```js
function maxSumK(nums, k) {
  let sum = 0, best = -Infinity;
  for (let r = 0; r < nums.length; r++) {
    sum += nums[r];
    if (r >= k) sum -= nums[r-k];
    if (r >= k-1) best = Math.max(best, sum);
  }
  return best;
}
```

### 1.2 Moving Average of Window Size K

**Output:** array of averages. **Time:** O(n)

```js
function movingAverage(nums, k) {
  const res = []; let sum = 0;
  for (let r = 0; r < nums.length; r++) {
    sum += nums[r];
    if (r >= k) sum -= nums[r-k];
    if (r >= k-1) res.push(sum / k);
  }
  return res;
}
```

### 1.3 Count Windows with Sum ≥ S

**Time:** O(n)

```js
function countWindowsSumAtLeast(nums, k, S) {
  let sum = 0, cnt = 0;
  for (let r = 0; r < nums.length; r++) {
    sum += nums[r];
    if (r >= k) sum -= nums[r-k];
    if (r >= k-1 && sum >= S) cnt++;
  }
  return cnt;
}
```

### 1.4 Max Ones in Any Window of Size K (binary array)

**Time:** O(n)

```js
function maxOnesInWindow(nums, k) {
  let ones = 0, best = 0;
  for (let r = 0; r < nums.length; r++) {
    if (nums[r] === 1) ones++;
    if (r >= k && nums[r-k] === 1) ones--;
    if (r >= k-1) best = Math.max(best, ones);
  }
  return best;
}
```

### 1.5 Distinct Count in Every Window of Size K

**Time:** O(n)

```js
function distinctInWindows(arr, k) {
  const res = [], freq = new Map();
  for (let r = 0; r < arr.length; r++) {
    freq.set(arr[r], (freq.get(arr[r])||0) + 1);
    if (r >= k) {
      const out = arr[r-k];
      const c = freq.get(out) - 1;
      if (c === 0) freq.delete(out); else freq.set(out, c);
    }
    if (r >= k-1) res.push(freq.size);
  }
  return res;
}
```

---

## 2) Variable-Size: Longest Under an Upper Bound

Expand right, shrink left while the constraint is broken.

### 2.1 Longest Subarray with Sum ≤ S (non-negative nums)

**Time:** O(n)

```js
function longestSumLE(nums, S) {
  let l = 0, sum = 0, best = 0;
  for (let r = 0; r < nums.length; r++) {
    sum += nums[r];
    while (sum > S) sum -= nums[l++];
    best = Math.max(best, r - l + 1);
  }
  return best;
}
```

### 2.2 Longest Subarray with Product ≤ K (positive nums)

**Time:** O(n)

```js
function longestProductLE(nums, K) {
  let l = 0, prod = 1, best = 0;
  for (let r = 0; r < nums.length; r++) {
    prod *= nums[r];
    while (prod > K && l <= r) prod /= nums[l++];
    best = Math.max(best, r - l + 1);
  }
  return best;
}
```

### 2.3 Longest Substring with At Most K Distinct Chars

**Time:** O(|s|)

```js
function longestAtMostKDistinct(s, K) {
  let l = 0, best = 0; const freq = new Map();
  for (let r = 0; r < s.length; r++) {
    freq.set(s[r], (freq.get(s[r])||0) + 1);
    while (freq.size > K) {
      const c = s[l++];
      const left = freq.get(c) - 1;
      if (left === 0) freq.delete(c); else freq.set(c, left);
    }
    best = Math.max(best, r - l + 1);
  }
  return best;
}
```

### 2.4 Longest Subarray with At Most K Odds

**Time:** O(n)

```js
function longestAtMostKOdds(nums, K) {
  let l = 0, odd = 0, best = 0;
  for (let r = 0; r < nums.length; r++) {
    if (nums[r] % 2) odd++;
    while (odd > K) if (nums[l++] % 2) odd--;
    best = Math.max(best, r - l + 1);
  }
  return best;
}
```

### 2.5 Longest Substring with At Most K Repeats of a Forbidden Char `x`

**Time:** O(|s|)

```js
function longestWithAtMostKOfX(s, K, x) {
  let l = 0, bad = 0, best = 0;
  for (let r = 0; r < s.length; r++) {
    if (s[r] === x) bad++;
    while (bad > K) if (s[l++] === x) bad--;
    best = Math.max(best, r - l + 1);
  }
  return best;
}
```

---

## 3) Variable-Size: Shortest Meeting a Lower Bound

Grow until valid, then shrink to minimal.

### 3.1 Minimum Length Subarray with Sum ≥ S (positive nums)

**Time:** O(n)

```js
function minLenSumGE(nums, S) {
  let l = 0, sum = 0, best = Infinity;
  for (let r = 0; r < nums.length; r++) {
    sum += nums[r];
    while (sum >= S) {
      best = Math.min(best, r - l + 1);
      sum -= nums[l++];
    }
  }
  return best === Infinity ? 0 : best;
}
```

### 3.2 Shortest Substring with At Least K Distinct Chars

**Time:** O(|s|)

```js
function shortestAtLeastKDistinct(s, K) {
  let l = 0, best = Infinity; const freq = new Map();
  for (let r = 0; r < s.length; r++) {
    freq.set(s[r], (freq.get(s[r])||0) + 1);
    while (freq.size >= K) {
      best = Math.min(best, r - l + 1);
      const c = s[l++];
      const left = freq.get(c) - 1;
      if (left === 0) freq.delete(c); else freq.set(c, left);
    }
  }
  return best === Infinity ? 0 : best;
}
```

### 3.3 Shortest Subarray with Product ≥ P (positive nums)

**Time:** O(n)

```js
function minLenProductGE(nums, P) {
  let l = 0, prod = 1, best = Infinity;
  for (let r = 0; r < nums.length; r++) {
    prod *= nums[r];
    while (prod >= P) {
      best = Math.min(best, r - l + 1);
      prod /= nums[l++];
    }
  }
  return best === Infinity ? 0 : best;
}
```

### 3.4 Shortest Substring Containing All Vowels at Least Once

**Time:** O(|s|)

```js
function shortestAllVowels(s) {
  const need = new Map([..."aeiou"].map(c=>[c,1]));
  const have = new Map(); let needKinds = need.size;
  let l = 0, best = [Infinity,-1,-1];
  for (let r = 0; r < s.length; r++) {
    const c = s[r];
    have.set(c, (have.get(c)||0)+1);
    if (need.has(c) && have.get(c) === need.get(c)) needKinds--;
    while (needKinds === 0) {
      if (r-l+1 < best[0]) best = [r-l+1, l, r];
      const d = s[l++];
      have.set(d, (have.get(d)||0)-1);
      if (need.has(d) && have.get(d) < need.get(d)) needKinds++;
    }
  }
  return best[0] === Infinity ? "" : s.slice(best[1], best[2]+1);
}
```

### 3.5 Shortest Window with At Least T Occurrences of Char `x`

**Time:** O(|s|)

```js
function shortestAtLeastTOcc(s, x, T) {
  let l = 0, cnt = 0, best = Infinity;
  for (let r = 0; r < s.length; r++) {
    if (s[r] === x) cnt++;
    while (cnt >= T) {
      best = Math.min(best, r - l + 1);
      if (s[l++] === x) cnt--;
    }
  }
  return best === Infinity ? 0 : best;
}
```

---

## 4) Exactly K Distinct via Two “At Most” Windows

`exactlyK = atMost(K) - atMost(K-1)`

### Helper: count substrings with at most K distinct

```js
function atMostKDistinct(s, K) {
  let l = 0, ans = 0; const freq = new Map();
  for (let r = 0; r < s.length; r++) {
    freq.set(s[r], (freq.get(s[r])||0) + 1);
    while (freq.size > K) {
      const c = s[l++];
      const left = freq.get(c) - 1;
      if (left === 0) freq.delete(c); else freq.set(c, left);
    }
    ans += r - l + 1; // all substrings ending at r
  }
  return ans;
}
```

### 4.1 Count Substrings with Exactly K Distinct Chars

```js
function countExactlyKDistinct(s, K) {
  return atMostKDistinct(s, K) - atMostKDistinct(s, K-1);
}
```

### 4.2 Longest Substring with Exactly K Distinct Chars

```js
function longestExactlyKDistinct(s, K) {
  let l = 0, best = 0; const freq = new Map();
  for (let r = 0; r < s.length; r++) {
    freq.set(s[r], (freq.get(s[r])||0) + 1);
    while (freq.size > K) {
      const c = s[l++];
      const left = freq.get(c) - 1;
      if (left === 0) freq.delete(c); else freq.set(c, left);
    }
    if (freq.size === K) best = Math.max(best, r - l + 1);
  }
  return best;
}
```

### 4.3 Count Subarrays with Exactly K Odd Numbers

```js
function countSubarraysExactlyKOdds(nums, K) {
  const atMost = (K) => {
    let l=0, odd=0, ans=0;
    for (let r=0;r<nums.length;r++){
      if (nums[r]%2) odd++;
      while (odd>K) if (nums[l++]%2) odd--;
      ans += r-l+1;
    }
    return ans;
  };
  return atMost(K) - atMost(K-1);
}
```

### 4.4 Count Subarrays with Exactly K Zeros (binary)

```js
function countExactlyKZeros(nums, K) {
  const atMost = K => {
    let l=0, z=0, ans=0;
    for (let r=0;r<nums.length;r++){
      if (nums[r]===0) z++;
      while (z>K) if (nums[l++]===0) z--;
      ans += r-l+1;
    }
    return ans;
  };
  return atMost(K)-atMost(K-1);
}
```

### 4.5 Count Substrings with Exactly K Distinct Vowels

```js
function countSubstringsExactlyKVowels(s, K) {
  const isV = c => 'aeiou'.includes(c);
  const atMost = K => {
    let l=0, ans=0; const f=new Map();
    for (let r=0;r<s.length;r++){
      if (isV(s[r])){
        f.set(s[r], (f.get(s[r])||0)+1);
      }
      while (f.size>K){
        const c=s[l++];
        if (isV(c)){
          const t=f.get(c)-1; if (t===0) f.delete(c); else f.set(c,t);
        }
      }
      ans += r-l+1;
    }
    return ans;
  };
  return atMost(K)-atMost(K-1);
}
```

---

## 5) Frequency / Anagram / Permutation Windows

Maintain `need` and `have` maps; shrink when valid to optimize.

### 5.1 Find All Anagrams of `p` in `s` (indices)

**Time:** O(|s|)

```js
function findAnagrams(s, p) {
  const need = new Map(); for (const c of p) need.set(c,(need.get(c)||0)+1);
  const have = new Map(); let needKinds = need.size;
  const res = []; let l = 0;
  for (let r=0;r<s.length;r++){
    const c=s[r]; have.set(c,(have.get(c)||0)+1);
    if (need.has(c) && have.get(c)===need.get(c)) needKinds--;
    while (r-l+1>p.length){
      const d=s[l++]; have.set(d,(have.get(d)||0)-1);
      if (need.has(d) && have.get(d)<need.get(d)) needKinds++;
    }
    if (r-l+1===p.length && needKinds===0) res.push(l);
  }
  return res;
}
```

### 5.2 Check Inclusion (Permutation in String)

```js
function checkInclusion(p, s) {
  return findAnagrams(s, p).length > 0;
}
```

### 5.3 Minimum Window Substring (cover counts of `t`)

```js
function minWindow(s, t) {
  const need = new Map(); for (const c of t) need.set(c,(need.get(c)||0)+1);
  const have = new Map(); let needKinds = need.size;
  let l = 0, best=[Infinity,-1,-1];
  for (let r=0;r<s.length;r++){
    const c=s[r]; have.set(c,(have.get(c)||0)+1);
    if (need.has(c) && have.get(c)===need.get(c)) needKinds--;
    while (needKinds===0){
      if (r-l+1<best[0]) best=[r-l+1,l,r];
      const d=s[l++]; have.set(d,(have.get(d)||0)-1);
      if (need.has(d) && have.get(d)<need.get(d)) needKinds++;
    }
  }
  return best[0]===Infinity?"":s.slice(best[1],best[2]+1);
}
```

### 5.4 Smallest Substring Covering a Set of Unique Characters `T`

```js
function minWindowSet(s, T) {
  const need = new Map([...new Set(T)].map(c=>[c,1]));
  const have = new Map(); let needKinds = need.size;
  let l=0, best=[Infinity,-1,-1];
  for (let r=0;r<s.length;r++){
    const c=s[r]; have.set(c,(have.get(c)||0)+1);
    if (need.has(c) && have.get(c)===1) needKinds--;
    while (needKinds===0){
      if (r-l+1<best[0]) best=[r-l+1,l,r];
      const d=s[l++]; have.set(d,(have.get(d)||0)-1);
      if (need.has(d) && have.get(d)===0) needKinds++;
    }
  }
  return best[0]===Infinity?"":s.slice(best[1],best[2]+1);
}
```

### 5.5 Minimum Window Subarray Covering Integer Counts

```js
function minWindowSubarray(nums, needArr) {
  // needArr: array of [value, count]
  const need = new Map(needArr);
  const have = new Map(); let needKinds = 0;
  need.forEach((v,k)=>{ if (v>0) needKinds++; });
  let l=0, best=[Infinity,-1,-1];
  for (let r=0;r<nums.length;r++){
    const x=nums[r]; have.set(x,(have.get(x)||0)+1);
    if (need.has(x) && have.get(x)===need.get(x)) needKinds--;
    while (needKinds===0){
      if (r-l+1<best[0]) best=[r-l+1,l,r];
      const d=nums[l++]; have.set(d,(have.get(d)||0)-1);
      if (need.has(d) && have.get(d)<need.get(d)) needKinds++;
    }
  }
  return best[0]===Infinity?[-1,-1]:[best[1],best[2]];
}
```

---

## 6) Monotonic Deque (Max/Min in O(1) per step)

Maintain a deque of indices with values in decreasing (for max) or increasing (for min) order.

### 6.1 Sliding Window Maximum

```js
function maxSlidingWindow(nums, k) {
  const dq = [], out = [];
  for (let r=0;r<nums.length;r++){
    while (dq.length && nums[dq[dq.length-1]] <= nums[r]) dq.pop();
    dq.push(r);
    if (dq[0] <= r-k) dq.shift();
    if (r >= k-1) out.push(nums[dq[0]]);
  }
  return out;
}
```

### 6.2 Sliding Window Minimum

```js
function minSlidingWindow(nums, k) {
  const dq = [], out = [];
  for (let r=0;r<nums.length;r++){
    while (dq.length && nums[dq[dq.length-1]] >= nums[r]) dq.pop();
    dq.push(r);
    if (dq[0] <= r-k) dq.shift();
    if (r >= k-1) out.push(nums[dq[0]]);
  }
  return out;
}
```

### 6.3 Range (Max − Min) per Window

```js
function rangePerWindow(nums, k) {
  const max = [], min = [], out = [];
  for (let r=0;r<nums.length;r++){
    while (max.length && nums[max[max.length-1]] <= nums[r]) max.pop();
    max.push(r);
    while (min.length && nums[min[min.length-1]] >= nums[r]) min.pop();
    min.push(r);
    if (max[0] <= r-k) max.shift();
    if (min[0] <= r-k) min.shift();
    if (r >= k-1) out.push(nums[max[0]] - nums[min[0]]);
  }
  return out;
}
```

### 6.4 First Negative in Every Window

```js
function firstNegativeInWindows(nums, k) {
  const neg = [], out = [];
  for (let r=0;r<nums.length;r++){
    if (nums[r] < 0) neg.push(r);
    while (neg.length && neg[0] <= r-k) neg.shift();
    if (r >= k-1) out.push(neg.length ? nums[neg[0]] : 0);
  }
  return out;
}
```

### 6.5 Sum of Max + Min Over All Windows of Size K

```js
function sumMaxPlusMin(nums, k) {
  const max = [], min = []; let sum = 0;
  for (let r=0;r<nums.length;r++){
    while (max.length && nums[max[max.length-1]] <= nums[r]) max.pop();
    max.push(r);
    while (min.length && nums[min[min.length-1]] >= nums[r]) min.pop();
    min.push(r);
    if (max[0] <= r-k) max.shift();
    if (min[0] <= r-k) min.shift();
    if (r >= k-1) sum += nums[max[0]] + nums[min[0]];
  }
  return sum;
}
```

---

## 7) Replacement / Transform Windows (≤ K changes allowed)

Track changes needed; shrink when needed > K.

### 7.1 Longest Repeating Character Replacement (LC 424)

```js
function characterReplacement(s, K) {
  const cnt = new Array(26).fill(0); const base = 'A'.charCodeAt(0);
  let l=0, best=0, maxFreq=0;
  for (let r=0;r<s.length;r++){
    const idx = s.charCodeAt(r)-base;
    maxFreq = Math.max(maxFreq, ++cnt[idx]);
    while (r-l+1 - maxFreq > K) {
      cnt[s.charCodeAt(l)-base]--; l++;
    }
    best = Math.max(best, r-l+1);
  }
  return best;
}
```

### 7.2 Max Consecutive Ones III (flip ≤ K zeros)

```js
function longestOnes(nums, K) {
  let l=0, zero=0, best=0;
  for (let r=0;r<nums.length;r++){
    if (nums[r]===0) zero++;
    while (zero>K) if (nums[l++]===0) zero--;
    best = Math.max(best, r-l+1);
  }
  return best;
}
```

### 7.3 Longest of 'T'/'F' After ≤ K Changes (LC 2024)

```js
function maxConsecutiveAnswers(answerKey, K) {
  const solve = ch => {
    let l=0, bad=0, best=0;
    for (let r=0;r<answerKey.length;r++){
      if (answerKey[r]!==ch) bad++;
      while (bad>K) if (answerKey[l++]!==ch) bad--;
      best = Math.max(best, r-l+1);
    }
    return best;
  };
  return Math.max(solve('T'), solve('F'));
}
```

### 7.4 Longest Substring Where s and t Differ in ≤ K Positions

```js
function longestKDiff(s, t, K) {
  let l=0, diff=0, best=0;
  for (let r=0;r<s.length;r++){
    if (s[r]!==t[r]) diff++;
    while (diff>K) if (s[l]!==t[l++]) diff--;
    best = Math.max(best, r-l+1);
  }
  return best;
}
```

### 7.5 Longest Vowel-Only After ≤ K Consonant Replacements

```js
function longestVowelAfterKRepl(s, K) {
  const isV=c=>'aeiou'.includes(c);
  let l=0, cons=0, best=0;
  for (let r=0;r<s.length;r++){
    if (!isV(s[r])) cons++;
    while (cons>K) if (!isV(s[l++])) cons--;
    best = Math.max(best, r-l+1);
  }
  return best;
}
```

---

## 8) No-Repeat Windows (All elements unique inside window)

### 8.1 Longest Substring Without Repeating Characters

```js
function lengthOfLongestSubstring(s) {
  let l=0, best=0; const last = new Map();
  for (let r=0;r<s.length;r++){
    if (last.has(s[r]) && last.get(s[r]) >= l) l = last.get(s[r]) + 1;
    last.set(s[r], r);
    best = Math.max(best, r-l+1);
  }
  return best;
}
```

### 8.2 Longest Subarray with Unique Integers

```js
function longestUniqueArray(nums) {
  let l=0, best=0; const pos=new Map();
  for (let r=0;r<nums.length;r++){
    if (pos.has(nums[r]) && pos.get(nums[r])>=l) l=pos.get(nums[r])+1;
    pos.set(nums[r], r);
    best=Math.max(best, r-l+1);
  }
  return best;
}
```

### 8.3 Smallest Window Containing All Unique Chars of `s`

```js
function minWindowAllUnique(s) {
  const uniq = new Set(s); const need = new Map([...uniq].map(c=>[c,1]));
  const have = new Map(); let needKinds = need.size;
  let l=0, best=[Infinity,-1,-1];
  for (let r=0;r<s.length;r++){
    const c=s[r]; have.set(c,(have.get(c)||0)+1);
    if (need.has(c) && have.get(c)===1) needKinds--;
    while (needKinds===0){
      if (r-l+1<best[0]) best=[r-l+1,l,r];
      const d=s[l++]; have.set(d,(have.get(d)||0)-1);
      if (need.has(d) && have.get(d)===0) needKinds++;
    }
  }
  return best[0]===Infinity?"":s.slice(best[1],best[2]+1);
}
```

### 8.4 Count Substrings with All Unique Characters

```js
function countUniqueSubstrings(s) {
  let l=0, ans=0; const last=new Map();
  for (let r=0;r<s.length;r++){
    if (last.has(s[r]) && last.get(s[r])>=l) l=last.get(s[r])+1;
    last.set(s[r], r);
    ans += r-l+1;
  }
  return ans;
}
```

### 8.5 Return the Longest Unique Subarray Itself

```js
function longestUniqueSubarray(nums) {
  let l=0, best=[0, -1, -1]; const pos=new Map();
  for (let r=0;r<nums.length;r++){
    if (pos.has(nums[r]) && pos.get(nums[r])>=l) l=pos.get(nums[r])+1;
    pos.set(nums[r], r);
    if (r-l+1>best[0]) best=[r-l+1, l, r];
  }
  return nums.slice(best[1], best[2]+1);
}
```

---

## 9) Circular Windows (wrap-around)

Duplicate the array/string (or index modulo `n`) and **cap window length ≤ n** to avoid full duplication counts.

### 9.1 Max Sum of Size K in Circular Array

```js
function maxSumKCircle(nums, k) {
  const n=nums.length; const A=nums.concat(nums);
  let sum=0, best=-Infinity, l=0;
  for (let r=0;r<A.length && r-l+1<=n+k-1;r++){
    sum+=A[r];
    if (r-l+1>k) sum-=A[l++];
    if (r-l+1===k) best=Math.max(best,sum);
  }
  return best;
}
```

### 9.2 Longest Run of 1s in Circular Binary Array

```js
function longestOnesCircle(nums) {
  const n=nums.length; const A=nums.concat(nums);
  let l=0, ones=0, best=0;
  for (let r=0;r<A.length;r++){
    if (A[r]===1) ones++; else ones=0, l=r+1; // reset on zero
    if (r-l+1>n) { // shrink if beyond n
      if (A[l]===1) ones--; l++;
    }
    best=Math.max(best, ones);
  }
  return Math.min(best, n);
}
```

### 9.3 Sliding Window Maximum on Circular Array (via doubling)

```js
function maxWindowCircle(nums, k) {
  const n=nums.length; const A=nums.concat(nums);
  const dq=[]; const out=[]; let l=0;
  for (let r=0;r<A.length && r<n+k-1;r++){
    while (dq.length && A[dq[dq.length-1]]<=A[r]) dq.pop();
    dq.push(r);
    while (dq[0] < l) dq.shift();
    if (r-l+1>k) l++;
    if (r-l+1===k) out.push(A[dq[0]]);
  }
  return out.slice(0, n); // first n windows
}
```

### 9.4 Count Windows of Size K with Sum ≥ S in Circular Array

```js
function countWindowsCircle(nums, k, S) {
  const n=nums.length; const A=nums.concat(nums);
  let sum=0, l=0, cnt=0;
  for (let r=0;r<A.length && r<n+k-1;r++){
    sum+=A[r];
    if (r-l+1>k) sum-=A[l++];
    if (r-l+1===k && sum>=S) cnt++;
  }
  return cnt;
}
```

### 9.5 Longest Subarray with At Most K Distinct in Circular Array

```js
function longestAtMostKDistinctCircle(s, K) {
  const n=s.length; const A=s+s; let l=0, best=0; const f=new Map();
  for (let r=0;r<A.length && r<n+n-1;r++){
    f.set(A[r], (f.get(A[r])||0)+1);
    while (f.size>K || r-l+1>n){
      const c=A[l++]; const t=f.get(c)-1; if (t===0) f.delete(c); else f.set(c,t);
    }
    best=Math.max(best, r-l+1);
  }
  return best;
}
```

---

## 10) When Classic Window Fails (negatives present) → Prefix Sums + Monotonic Deque / HashMap

These are **related advanced patterns** (not classic windows) that fix issues when negatives break monotonicity.

### 10.1 Shortest Subarray with Sum ≥ K (can have negatives) — Monotonic Prefix Deque

**Time:** O(n)

```js
function shortestSubarraySumGE(nums, K) {
  const pre=[0]; for (const x of nums) pre.push(pre[pre.length-1]+x);
  const dq=[]; let best=Infinity;
  for (let r=0;r<pre.length;r++){
    while (dq.length && pre[r] - pre[dq[0]] >= K) {
      best = Math.min(best, r - dq.shift());
    }
    while (dq.length && pre[r] <= pre[dq[dq.length-1]]) dq.pop();
    dq.push(r);
  }
  return best===Infinity? -1 : best;
}
```

### 10.2 Existence of Any Subarray with Sum ≥ K (negatives allowed)

```js
function existsSubarraySumGE(nums, K) {
  return shortestSubarraySumGE(nums, K) !== -1;
}
```

### 10.3 Longest Subarray with Sum ≤ S (negatives allowed)

Use prefix sums `pre` and for each `r` find smallest `l` with `pre[r]-pre[l] ≤ S` ⇒ `pre[l] ≥ pre[r]-S`. Maintain a **monotone increasing deque of candidate indices by prefix sum**.

```js
function longestSumLEWithNeg(nums, S) {
  const pre=[0]; for (const x of nums) pre.push(pre[pre.length-1]+x);
  let best=0; const dq=[]; // store indices with increasing pre
  for (let r=0;r<pre.length;r++){
    while (dq.length && pre[r] - pre[dq[0]] > S) dq.shift();
    if (dq.length) best = Math.max(best, r - dq[0]);
    while (dq.length && pre[r] <= pre[dq[dq.length-1]]) dq.pop();
    dq.push(r);
  }
  return best;
}
```

### 10.4 Min Length Subarray with Sum Exactly K (negatives allowed) — HashMap

```js
function minLenSumEqK(nums, K) {
  const idx = new Map([[0, -1]]);
  let sum=0, best=Infinity;
  for (let i=0;i<nums.length;i++){
    sum += nums[i];
    if (idx.has(sum - K)) best = Math.min(best, i - idx.get(sum - K));
    if (!idx.has(sum)) idx.set(sum, i);
  }
  return best===Infinity? -1 : best;
}
```

### 10.5 Count Subarrays with Sum Exactly K (negatives allowed) — HashMap

```js
function countSubarraysSumK(nums, K) {
  const freq = new Map([[0,1]]);
  let sum=0, ans=0;
  for (const x of nums){
    sum += x;
    ans += (freq.get(sum - K) || 0);
    freq.set(sum, (freq.get(sum)||0) + 1);
  }
  return ans;
}
```

---

## How to Use This Sheet

1. Identify the subpattern from the prompt (fixed K, at most K distinct, min window cover, monotone deque, etc.).
2. Grab the closest solution skeleton above.
3. Tweak small details (sum/product/char counts) to match the exact constraint.

If you want, I can derive **TypeScript types**, add **unit tests** (Jest) for each function, or generate a **practice plan (5/day)** around these 50 problems.
