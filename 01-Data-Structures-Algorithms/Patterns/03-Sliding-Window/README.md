# 🪟 Pattern 3: Sliding Window

Master the sliding window technique for efficient subarray and substring problems.

---

## 🎯 When to Use This Pattern

- Finding **subarray** or **substring** with specific property
- **Longest/shortest** subarray satisfying condition
- Problems with **contiguous** elements
- **At most/at least K** constraint problems
- **Optimization** over all windows of certain type

---

## 🚩 Trigger Words

| Trigger Phrase | Window Type |
|----------------|-------------|
| "subarray/substring of size K" | Fixed-size window |
| "longest substring with..." | Variable-size, expand & shrink |
| "shortest subarray with sum ≥ S" | Variable-size, shrink when valid |
| "at most K distinct characters" | Variable-size with constraint |
| "contains all characters of..." | Variable-size, frequency matching |
| "maximum sum of subarray of size K" | Fixed-size window |

---

## 📝 Core Concepts

### 1. Fixed-Size Window
- Window size is **constant** (K)
- Slide window one position at a time
- **Time**: O(n)

### 2. Variable-Size Window (Expanding)
- Expand right until **valid**
- Contract left while **still valid**
- Track **maximum** valid window

### 3. Variable-Size Window (Shrinking)
- Expand right until **valid**
- Shrink left to **minimum** valid
- Track **minimum** valid window

---

## 💻 Templates

### Template 1: Fixed-Size Window
```javascript
function fixedWindow(arr, k) {
    let windowSum = 0, maxSum = -Infinity;

    for (let right = 0; right < arr.length; right++) {
        windowSum += arr[right]; // Add new element

        // Remove left element if window size exceeded
        if (right >= k) {
            windowSum -= arr[right - k];
        }

        // Process window when it reaches size k
        if (right >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);
        }
    }

    return maxSum;
}
// Time: O(n), Space: O(1)
```

### Template 2: Variable Window (Longest with Constraint)
```javascript
function longestWindowWithConstraint(arr, constraint) {
    let left = 0, maxLength = 0;
    let windowState = {}; // Track window properties

    for (let right = 0; right < arr.length; right++) {
        // Add arr[right] to window
        updateWindowState(arr[right]);

        // Shrink window while constraint violated
        while (constraintViolated(windowState, constraint)) {
            removeFromWindow(arr[left]);
            left++;
        }

        // Update maximum
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

### Template 3: Variable Window (Shortest Meeting Target)
```javascript
function shortestWindowMeetingTarget(arr, target) {
    let left = 0, minLength = Infinity;
    let windowSum = 0;

    for (let right = 0; right < arr.length; right++) {
        windowSum += arr[right];

        // Shrink window while valid
        while (windowSum >= target) {
            minLength = Math.min(minLength, right - left + 1);
            windowSum -= arr[left];
            left++;
        }
    }

    return minLength === Infinity ? 0 : minLength;
}
```

---

## 📚 Problems (Easy → Hard)

### 🟢 Easy Problems

#### 1. Maximum Average Subarray I
**LeetCode**: #643 | **Frequency**: 🔥🔥 | **Companies**: [G][A]

**Problem**: Find max average of contiguous subarray of size k.

**Solution**:
```javascript
function findMaxAverage(nums, k) {
    let sum = 0;

    // Initial window
    for (let i = 0; i < k; i++) {
        sum += nums[i];
    }

    let maxSum = sum;

    // Slide window
    for (let i = k; i < nums.length; i++) {
        sum = sum + nums[i] - nums[i - k];
        maxSum = Math.max(maxSum, sum);
    }

    return maxSum / k;
}
// Time: O(n), Space: O(1)
```

---

#### 2. Contains Duplicate II
**LeetCode**: #219 | **Frequency**: 🔥 | **Companies**: [A]

**Problem**: Check if array contains duplicates within k distance.

**Solution**:
```javascript
function containsNearbyDuplicate(nums, k) {
    const window = new Set();

    for (let i = 0; i < nums.length; i++) {
        // Check if duplicate in current window
        if (window.has(nums[i])) {
            return true;
        }

        window.add(nums[i]);

        // Maintain window size of k
        if (window.size > k) {
            window.delete(nums[i - k]);
        }
    }

    return false;
}
// Time: O(n), Space: O(k)
```

---

### 🟡 Medium Problems

#### 3. Longest Substring Without Repeating Characters
**LeetCode**: #3 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M][AP]

**Problem**: Find length of longest substring without repeating characters.

**Solution 1** (Sliding Window with Set):
```javascript
function lengthOfLongestSubstring(s) {
    const charSet = new Set();
    let left = 0, maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        // Shrink window while duplicate exists
        while (charSet.has(s[right])) {
            charSet.delete(s[left]);
            left++;
        }

        charSet.add(s[right]);
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
// Time: O(n), Space: O(min(n, alphabet_size))
```

**Solution 2** (Optimized with Map):
```javascript
function lengthOfLongestSubstring(s) {
    const lastSeen = new Map(); // char -> last index
    let left = 0, maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        const char = s[right];

        // If char seen and in current window, move left
        if (lastSeen.has(char) && lastSeen.get(char) >= left) {
            left = lastSeen.get(char) + 1;
        }

        lastSeen.set(char, right);
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
// Time: O(n), Space: O(min(n, alphabet_size))
```

---

#### 4. Longest Repeating Character Replacement
**LeetCode**: #424 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Replace at most k characters to get longest substring of same character.

**Solution**:
```javascript
function characterReplacement(s, k) {
    const count = new Array(26).fill(0);
    let left = 0, maxCount = 0, maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        const idx = s.charCodeAt(right) - 65; // 'A' = 65
        count[idx]++;
        maxCount = Math.max(maxCount, count[idx]);

        // Window size - most frequent char = chars to replace
        // If that exceeds k, shrink window
        while (right - left + 1 - maxCount > k) {
            const leftIdx = s.charCodeAt(left) - 65;
            count[leftIdx]--;
            left++;
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
// Time: O(n), Space: O(1) - fixed 26 letters
```

**Key Insight**: (window_size - max_frequency) = characters that need replacement.

---

#### 5. Permutation in String
**LeetCode**: #567 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][M]

**Problem**: Check if s2 contains permutation of s1.

**Solution**:
```javascript
function checkInclusion(s1, s2) {
    if (s1.length > s2.length) return false;

    const need = new Array(26).fill(0);
    const window = new Array(26).fill(0);

    // Count frequencies in s1
    for (const char of s1) {
        need[char.charCodeAt(0) - 97]++;
    }

    // Sliding window of size s1.length
    for (let right = 0; right < s2.length; right++) {
        window[s2.charCodeAt(right) - 97]++;

        // Remove left character if window too large
        if (right >= s1.length) {
            window[s2.charCodeAt(right - s1.length) - 97]--;
        }

        // Check if window matches
        if (right >= s1.length - 1) {
            if (arraysEqual(need, window)) {
                return true;
            }
        }
    }

    return false;
}

function arraysEqual(arr1, arr2) {
    return arr1.every((val, idx) => val === arr2[idx]);
}
// Time: O(n), Space: O(1)
```

---

#### 6. Find All Anagrams in a String
**LeetCode**: #438 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Find all start indices of p's anagrams in s.

**Solution**:
```javascript
function findAnagrams(s, p) {
    const result = [];
    if (p.length > s.length) return result;

    const pCount = new Array(26).fill(0);
    const sCount = new Array(26).fill(0);

    // Count frequencies
    for (let i = 0; i < p.length; i++) {
        pCount[p.charCodeAt(i) - 97]++;
        sCount[s.charCodeAt(i) - 97]++;
    }

    // Check first window
    if (arraysEqual(pCount, sCount)) {
        result.push(0);
    }

    // Slide window
    for (let i = p.length; i < s.length; i++) {
        // Add new char
        sCount[s.charCodeAt(i) - 97]++;
        // Remove old char
        sCount[s.charCodeAt(i - p.length) - 97]--;

        if (arraysEqual(pCount, sCount)) {
            result.push(i - p.length + 1);
        }
    }

    return result;
}

function arraysEqual(arr1, arr2) {
    return arr1.every((val, idx) => val === arr2[idx]);
}
// Time: O(n), Space: O(1)
```

---

#### 7. Minimum Size Subarray Sum
**LeetCode**: #209 | **Frequency**: 🔥🔥 | **Companies**: [G][F][A]

**Problem**: Find minimal length of contiguous subarray with sum ≥ target.

**Solution**:
```javascript
function minSubArrayLen(target, nums) {
    let left = 0, sum = 0, minLen = Infinity;

    for (let right = 0; right < nums.length; right++) {
        sum += nums[right];

        // Shrink window while sum >= target
        while (sum >= target) {
            minLen = Math.min(minLen, right - left + 1);
            sum -= nums[left];
            left++;
        }
    }

    return minLen === Infinity ? 0 : minLen;
}
// Time: O(n), Space: O(1)
```

**Why O(n)?** Each element added once, removed once. Total 2n operations.

---

#### 8. Longest Substring with At Most K Distinct Characters
**LeetCode**: #340 (Premium) | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Find length of longest substring with at most K distinct characters.

**Solution**:
```javascript
function lengthOfLongestSubstringKDistinct(s, k) {
    const charCount = new Map();
    let left = 0, maxLen = 0;

    for (let right = 0; right < s.length; right++) {
        // Add character to window
        const char = s[right];
        charCount.set(char, (charCount.get(char) || 0) + 1);

        // Shrink window if too many distinct chars
        while (charCount.size > k) {
            const leftChar = s[left];
            charCount.set(leftChar, charCount.get(leftChar) - 1);
            if (charCount.get(leftChar) === 0) {
                charCount.delete(leftChar);
            }
            left++;
        }

        maxLen = Math.max(maxLen, right - left + 1);
    }

    return maxLen;
}
// Time: O(n), Space: O(k)
```

---

#### 9. Fruit Into Baskets
**LeetCode**: #904 | **Frequency**: 🔥🔥 | **Companies**: [G][A]

**Problem**: Pick max fruits with at most 2 types (same as K=2 distinct).

**Solution**:
```javascript
function totalFruit(fruits) {
    const basket = new Map(); // fruit type -> count
    let left = 0, maxFruits = 0;

    for (let right = 0; right < fruits.length; right++) {
        const fruit = fruits[right];
        basket.set(fruit, (basket.get(fruit) || 0) + 1);

        // More than 2 types, shrink window
        while (basket.size > 2) {
            const leftFruit = fruits[left];
            basket.set(leftFruit, basket.get(leftFruit) - 1);
            if (basket.get(leftFruit) === 0) {
                basket.delete(leftFruit);
            }
            left++;
        }

        maxFruits = Math.max(maxFruits, right - left + 1);
    }

    return maxFruits;
}
// Time: O(n), Space: O(1) - at most 2 types
```

---

### 🔴 Hard Problems

#### 10. Minimum Window Substring
**LeetCode**: #76 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M][AP]

**Problem**: Find minimum window in s containing all characters from t.

**Solution**:
```javascript
function minWindow(s, t) {
    const need = new Map();
    const have = new Map();

    // Count required characters
    for (const char of t) {
        need.set(char, (need.get(char) || 0) + 1);
    }

    let left = 0, minLen = Infinity, minStart = 0;
    let formed = 0; // Count of chars with correct frequency

    for (let right = 0; right < s.length; right++) {
        const char = s[right];
        have.set(char, (have.get(char) || 0) + 1);

        // If frequency matches requirement
        if (need.has(char) && have.get(char) === need.get(char)) {
            formed++;
        }

        // Try to shrink window while valid
        while (formed === need.size) {
            // Update minimum window
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minStart = left;
            }

            // Remove left character
            const leftChar = s[left];
            have.set(leftChar, have.get(leftChar) - 1);
            if (need.has(leftChar) && have.get(leftChar) < need.get(leftChar)) {
                formed--;
            }
            left++;
        }
    }

    return minLen === Infinity ? "" : s.substring(minStart, minStart + minLen);
}
// Time: O(|s| + |t|), Space: O(|s| + |t|)
```

---

#### 11. Sliding Window Maximum
**LeetCode**: #239 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M]

**Problem**: Return max of each sliding window of size k.

**Solution** (Monotonic Deque):
```javascript
function maxSlidingWindow(nums, k) {
    const result = [];
    const deque = []; // Store indices, decreasing order of values

    for (let right = 0; right < nums.length; right++) {
        // Remove indices outside window
        while (deque.length && deque[0] <= right - k) {
            deque.shift();
        }

        // Remove smaller elements from back
        while (deque.length && nums[deque[deque.length - 1]] < nums[right]) {
            deque.pop();
        }

        deque.push(right);

        // Add to result when window is full
        if (right >= k - 1) {
            result.push(nums[deque[0]]);
        }
    }

    return result;
}
// Time: O(n), Space: O(k)
```

**Key**: Deque maintains indices of potentially maximum elements in decreasing order.

---

## ⚠️ Common Mistakes

1. **Off-by-One Errors**: Window size calculations
2. **Forgetting to Shrink**: Not moving left pointer when needed
3. **Wrong Loop Structure**: Using nested loops instead of two pointers
4. **Not Handling Edge Cases**: Empty strings, k > array length
5. **Inefficient State Tracking**: Using O(n) check inside O(n) loop

---

## 💡 Pro Tips

1. **Two Pointers**: Sliding window is a special case of two pointers
2. **Amortized O(n)**: Each element added once, removed once
3. **Hash Map vs Array**: Array faster for small alphabets (26 letters)
4. **Valid Window**: Know when window is "valid" vs "invalid"
5. **Shrink Condition**: While invalid vs while valid (depends on problem)

---

## 🎯 Pattern Variations

### 1. Fixed vs Variable Size
- **Fixed**: Size given in problem
- **Variable**: Find optimal size (longest/shortest)

### 2. Expand Strategy
- **At most K**: Expand until K+1, then shrink
- **At least K**: Expand until K, then try to shrink
- **Exactly K**: Use "at most K" - "at most K-1"

### 3. State Tracking
- **Count/Sum**: Simple integer
- **Frequency**: Hash map or array
- **Distinct**: Set or map size
- **Max/Min**: Deque or heap

---

## ✅ Mastery Checklist

- [ ] Understand fixed vs variable window
- [ ] Can identify expand vs shrink problems
- [ ] Know when to use Map vs Array
- [ ] Understand amortized O(n) complexity
- [ ] Master frequency-matching pattern
- [ ] Solved 80% of Easy problems
- [ ] Solved 60% of Medium problems
- [ ] Solved 40% of Hard problems

---

[⬅️ Back to Patterns](../) | [← Previous: Two Pointers](../02-Two-Pointers/) | [Next: Stack →](../04-Stack/)
