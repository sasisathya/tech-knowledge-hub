# 🔁 Sliding Window - Array Problems (10 Essential Patterns)

This GitHub-style guide contains 10 essential array-based sliding window problems, covering both fixed and variable window techniques.

Each entry includes:

* 📌 Problem summary
* 🔗 LeetCode link
* 🧠 Pattern type
* 💡 Explanation
* ✅ JavaScript solution

---

## 1. Maximum Sum Subarray of Size K

* 🔗 [LeetCode 643](https://leetcode.com/problems/maximum-average-subarray-i/)
* 📌 Find max sum of any subarray of size `k`
* 🧠 Fixed-size window

```js
function maxSumSubarrayK(nums, k) {
  let windowSum = 0, maxSum = 0;

  for (let i = 0; i < k; i++) windowSum += nums[i];
  maxSum = windowSum;

  for (let i = k; i < nums.length; i++) {
    windowSum += nums[i] - nums[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}
```

---

## 2. Minimum Size Subarray Sum

* 🔗 [LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/)
* 📌 Find the smallest subarray with sum ≥ target
* 🧠 Variable-size window

```js
function minSubArrayLen(target, nums) {
  let left = 0, sum = 0, minLen = Infinity;

  for (let right = 0; right < nums.length; right++) {
    sum += nums[right];
    while (sum >= target) {
      minLen = Math.min(minLen, right - left + 1);
      sum -= nums[left++];
    }
  }

  return minLen === Infinity ? 0 : minLen;
}
```

---

## 3. Longest Subarray with Sum ≤ K

* 📌 Longest subarray with sum ≤ `k` (non-negative numbers)
* 🧠 Variable-size window (custom variant)

```js
function longestSubarraySumLEK(nums, k) {
  let left = 0, sum = 0, maxLen = 0;

  for (let right = 0; right < nums.length; right++) {
    sum += nums[right];
    while (sum > k) {
      sum -= nums[left++];
    }
    maxLen = Math.max(maxLen, right - left + 1);
  }

  return maxLen;
}
```

---

## 4. Longest Substring with At Most K Distinct Characters

* 🔗 [LeetCode 340](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
* 📌 Longest substring with ≤ `k` distinct characters
* 🧠 Variable window + HashMap

```js
function lengthOfLongestSubstringKDistinct(s, k) {
  let left = 0, maxLen = 0;
  const map = new Map();

  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    map.set(char, (map.get(char) || 0) + 1);

    while (map.size > k) {
      const leftChar = s[left];
      map.set(leftChar, map.get(leftChar) - 1);
      if (map.get(leftChar) === 0) map.delete(leftChar);
      left++;
    }

    maxLen = Math.max(maxLen, right - left + 1);
  }

  return maxLen;
}
```

---

## 5. Longest Subarray with Equal Number of 0s and 1s

* 🔗 [LeetCode 525](https://leetcode.com/problems/contiguous-array/)
* 📌 Replace 0 → -1, then find longest subarray with sum = 0
* 🧠 Prefix sum + HashMap

```js
function findMaxLength(nums) {
  const map = new Map();
  map.set(0, -1);

  let maxLen = 0, sum = 0;

  for (let i = 0; i < nums.length; i++) {
    sum += nums[i] === 0 ? -1 : 1;
    if (map.has(sum)) {
      maxLen = Math.max(maxLen, i - map.get(sum));
    } else {
      map.set(sum, i);
    }
  }

  return maxLen;
}
```

---

## 6. Number of Subarrays with Product Less Than K

* 🔗 [LeetCode 713](https://leetcode.com/problems/subarray-product-less-than-k/)
* 📌 Count all subarrays with product < `k`
* 🧠 Variable-size window with product

```js
function numSubarrayProductLessThanK(nums, k) {
  if (k <= 1) return 0;

  let left = 0, product = 1, count = 0;

  for (let right = 0; right < nums.length; right++) {
    product *= nums[right];

    while (product >= k) {
      product /= nums[left++];
    }

    count += right - left + 1;
  }

  return count;
}
```

---

## 7. Maximum Number of Vowels in a Substring of Given Length

* 🔗 [LeetCode 1456](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)
* 📌 Max vowels in any substring of size `k`
* 🧠 Fixed-size window

```js
function maxVowels(s, k) {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']);
  let count = 0, maxCount = 0;

  for (let i = 0; i < k; i++) {
    if (vowels.has(s[i])) count++;
  }
  maxCount = count;

  for (let i = k; i < s.length; i++) {
    if (vowels.has(s[i])) count++;
    if (vowels.has(s[i - k])) count--;
    maxCount = Math.max(maxCount, count);
  }

  return maxCount;
}
```

---

## 8. Max Consecutive Ones III

* 🔗 [LeetCode 1004](https://leetcode.com/problems/max-consecutive-ones-iii/)
* 📌 Max 1s by flipping at most `k` 0s
* 🧠 Variable-size window with zero count

```js
function longestOnes(nums, k) {
  let left = 0, maxLen = 0, zeros = 0;

  for (let right = 0; right < nums.length; right++) {
    if (nums[right] === 0) zeros++;

    while (zeros > k) {
      if (nums[left++] === 0) zeros--;
    }

    maxLen = Math.max(maxLen, right - left + 1);
  }

  return maxLen;
}
```

---

## 9. Longest Substring Without Repeating Characters

* 🔗 [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
* 📌 Longest substring with unique characters
* 🧠 Set + sliding window

```js
function lengthOfLongestSubstring(s) {
  const set = new Set();
  let left = 0, maxLen = 0;

  for (let right = 0; right < s.length; right++) {
    while (set.has(s[right])) {
      set.delete(s[left++]);
    }
    set.add(s[right]);
    maxLen = Math.max(maxLen, right - left + 1);
  }

  return maxLen;
}
```

---

## 10. Sliding Window Maximum

* 🔗 [LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/)
* 📌 Max value in each window of size `k`
* 🧠 Monotonic deque

```js
function maxSlidingWindow(nums, k) {
  const deque = [], result = [];

  for (let i = 0; i < nums.length; i++) {
    if (deque.length && deque[0] <= i - k) deque.shift();

    while (deque.length && nums[i] >= nums[deque[deque.length - 1]]) {
      deque.pop();
    }

    deque.push(i);

    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }

  return result;
}
```

---

> ✅ You're now ready to master sliding window problems on arrays. Next up: Linked Lists, Strings, Trees!
