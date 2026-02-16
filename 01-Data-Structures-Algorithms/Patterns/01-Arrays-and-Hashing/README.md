# 📦 Pattern 1: Arrays & Hashing

Master hash maps, hash sets, and array manipulation techniques.

---

## 🎯 When to Use This Pattern

- Need **O(1) lookup** for elements
- **Frequency counting** problems
- **Finding duplicates** or unique elements
- **Group/categorize** data by properties
- **Complement search** (e.g., two numbers that sum to target)

---

## 🚩 Trigger Words

| Trigger Phrase | Likely Technique |
|----------------|------------------|
| "frequency", "count", "most/least frequent" | Hash Map (frequency counter) |
| "anagram", "permutation" | Hash Map or Array (char count) |
| "duplicate", "unique" | Hash Set |
| "pair sums to target" | Hash Map (complement) |
| "group by property" | Hash Map (grouping) |

---

## 📝 Core Concepts

### 1. Hash Map (Dictionary)
- **Purpose**: Key → Value mapping
- **Time**: O(1) average for get/set
- **Use**: Frequency counts, indices, grouping

### 2. Hash Set
- **Purpose**: Unique element storage
- **Time**: O(1) average for add/contains
- **Use**: Deduplication, membership check

### 3. Array as Hash
- **Purpose**: Fixed range counting (0-255 for ASCII)
- **Time**: O(1) guaranteed
- **Use**: Character counts, small integer ranges

---

## 💻 Templates

### Template 1: Frequency Counter
```javascript
function frequencyMap(arr) {
    const freq = new Map();
    for (const item of arr) {
        freq.set(item, (freq.get(item) || 0) + 1);
    }
    return freq;
}
```

### Template 2: Complement Search (Two Sum Pattern)
```javascript
function twoSum(nums, target) {
    const seen = new Map(); // value → index
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        if (seen.has(complement)) {
            return [seen.get(complement), i];
        }
        seen.set(nums[i], i);
    }
    return [-1, -1];
}
```

### Template 3: Grouping by Key
```javascript
function groupByKey(items, keyFn) {
    const groups = new Map();
    for (const item of items) {
        const key = keyFn(item);
        if (!groups.has(key)) groups.set(key, []);
        groups.get(key).push(item);
    }
    return groups;
}
```

---

## 📚 Problems (Easy → Hard)

### 🟢 Easy Problems

#### 1. Contains Duplicate
**LeetCode**: #217 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][A][M]

**Problem**: Return true if any value appears at least twice in array.

**Solution**:
```javascript
function containsDuplicate(nums) {
    const seen = new Set();
    for (const num of nums) {
        if (seen.has(num)) return true;
        seen.add(num);
    }
    return false;
}
// Time: O(n), Space: O(n)
```

**Key Insight**: Set for O(1) membership check

---

#### 2. Valid Anagram
**LeetCode**: #242 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Check if two strings are anagrams.

**Solution 1** (Hash Map):
```javascript
function isAnagram(s, t) {
    if (s.length !== t.length) return false;

    const count = new Map();
    for (const char of s) {
        count.set(char, (count.get(char) || 0) + 1);
    }
    for (const char of t) {
        if (!count.has(char)) return false;
        count.set(char, count.get(char) - 1);
        if (count.get(char) < 0) return false;
    }
    return true;
}
```

**Solution 2** (Array - faster for ASCII):
```javascript
function isAnagram(s, t) {
    if (s.length !== t.length) return false;

    const count = new Array(26).fill(0);
    for (let i = 0; i < s.length; i++) {
        count[s.charCodeAt(i) - 97]++;
        count[t.charCodeAt(i) - 97]--;
    }
    return count.every(c => c === 0);
}
// Time: O(n), Space: O(1) - fixed size array
```

---

#### 3. Two Sum
**LeetCode**: #1 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M][AP]

**Problem**: Find two numbers that add up to target, return indices.

**Solution**:
```javascript
function twoSum(nums, target) {
    const map = new Map(); // value → index
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        if (map.has(complement)) {
            return [map.get(complement), i];
        }
        map.set(nums[i], i);
    }
    return [];
}
// Time: O(n), Space: O(n)
```

**Why Hash Map?** Need to remember index of previously seen numbers.

---

#### 4. Majority Element
**LeetCode**: #169 | **Frequency**: 🔥🔥 | **Companies**: [G][A][M]

**Problem**: Find element appearing > n/2 times.

**Solution 1** (Hash Map):
```javascript
function majorityElement(nums) {
    const freq = new Map();
    const majority = Math.floor(nums.length / 2);

    for (const num of nums) {
        freq.set(num, (freq.get(num) || 0) + 1);
        if (freq.get(num) > majority) return num;
    }
}
// Time: O(n), Space: O(n)
```

**Solution 2** (Boyer-Moore - Optimal):
```javascript
function majorityElement(nums) {
    let candidate = null, count = 0;
    for (const num of nums) {
        if (count === 0) candidate = num;
        count += (num === candidate) ? 1 : -1;
    }
    return candidate;
}
// Time: O(n), Space: O(1)
```

---

### 🟡 Medium Problems

#### 5. Group Anagrams
**LeetCode**: #49 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M]

**Problem**: Group strings that are anagrams.

**Solution**:
```javascript
function groupAnagrams(strs) {
    const groups = new Map();

    for (const str of strs) {
        // Key: sorted string
        const key = str.split('').sort().join('');
        if (!groups.has(key)) groups.set(key, []);
        groups.get(key).push(str);
    }

    return Array.from(groups.values());
}
// Time: O(n * k log k) where k = max string length
// Space: O(n * k)
```

**Alternative Key** (Faster - no sorting):
```javascript
function groupAnagrams(strs) {
    const groups = new Map();

    for (const str of strs) {
        // Key: char frequency as string "1a2b3c"
        const count = new Array(26).fill(0);
        for (const char of str) {
            count[char.charCodeAt(0) - 97]++;
        }
        const key = count.join(',');
        if (!groups.has(key)) groups.set(key, []);
        groups.get(key).push(str);
    }

    return Array.from(groups.values());
}
// Time: O(n * k), Space: O(n * k)
```

---

#### 6. Top K Frequent Elements
**LeetCode**: #347 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Return k most frequent elements.

**Solution 1** (Heap - General):
```javascript
function topKFrequent(nums, k) {
    // Count frequencies
    const freq = new Map();
    for (const num of nums) {
        freq.set(num, (freq.get(num) || 0) + 1);
    }

    // Sort by frequency and take top k
    return Array.from(freq.entries())
        .sort((a, b) => b[1] - a[1])
        .slice(0, k)
        .map(([num, _]) => num);
}
// Time: O(n log n), Space: O(n)
```

**Solution 2** (Bucket Sort - Optimal):
```javascript
function topKFrequent(nums, k) {
    const freq = new Map();
    for (const num of nums) {
        freq.set(num, (freq.get(num) || 0) + 1);
    }

    // Bucket: index = frequency, value = numbers with that frequency
    const buckets = Array.from({length: nums.length + 1}, () => []);
    for (const [num, count] of freq.entries()) {
        buckets[count].push(num);
    }

    // Collect from highest frequency
    const result = [];
    for (let i = buckets.length - 1; i >= 0 && result.length < k; i--) {
        result.push(...buckets[i]);
    }
    return result.slice(0, k);
}
// Time: O(n), Space: O(n)
```

---

#### 7. Product of Array Except Self
**LeetCode**: #238 | **Frequency**: 🔥🔥🔥 | **Companies**: [F][A][M]

**Problem**: Return array where output[i] = product of all elements except nums[i]. No division allowed.

**Solution**:
```javascript
function productExceptSelf(nums) {
    const n = nums.length;
    const result = new Array(n);

    // Left products
    result[0] = 1;
    for (let i = 1; i < n; i++) {
        result[i] = result[i-1] * nums[i-1];
    }

    // Right products (on the fly)
    let right = 1;
    for (let i = n - 1; i >= 0; i--) {
        result[i] *= right;
        right *= nums[i];
    }

    return result;
}
// Time: O(n), Space: O(1) - output array doesn't count
```

---

#### 8. Valid Sudoku
**LeetCode**: #36 | **Frequency**: 🔥🔥 | **Companies**: [G][A][AP]

**Problem**: Check if 9x9 Sudoku board is valid.

**Solution**:
```javascript
function isValidSudoku(board) {
    const rows = Array.from({length: 9}, () => new Set());
    const cols = Array.from({length: 9}, () => new Set());
    const boxes = Array.from({length: 9}, () => new Set());

    for (let r = 0; r < 9; r++) {
        for (let c = 0; c < 9; c++) {
            const val = board[r][c];
            if (val === '.') continue;

            const boxIdx = Math.floor(r / 3) * 3 + Math.floor(c / 3);

            if (rows[r].has(val) || cols[c].has(val) || boxes[boxIdx].has(val)) {
                return false;
            }

            rows[r].add(val);
            cols[c].add(val);
            boxes[boxIdx].add(val);
        }
    }
    return true;
}
// Time: O(1) - fixed 9x9, Space: O(1)
```

---

#### 9. Encode and Decode Strings
**LeetCode**: #271 (Premium) | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F]

**Problem**: Encode list of strings to single string, then decode back.

**Solution**:
```javascript
class Codec {
    // Encode: "4#abc5#hello" for ["abc", "hello"]
    encode(strs) {
        return strs.map(s => `${s.length}#${s}`).join('');
    }

    decode(s) {
        const result = [];
        let i = 0;
        while (i < s.length) {
            // Find length
            let j = i;
            while (s[j] !== '#') j++;
            const len = parseInt(s.substring(i, j));

            // Extract string
            const str = s.substring(j + 1, j + 1 + len);
            result.push(str);
            i = j + 1 + len;
        }
        return result;
    }
}
// Time: O(n), Space: O(1) extra
```

---

### 🔴 Hard Problems

#### 10. Longest Consecutive Sequence
**LeetCode**: #128 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Find length of longest consecutive sequence in unsorted array. Must be O(n).

**Solution**:
```javascript
function longestConsecutive(nums) {
    const numSet = new Set(nums);
    let longest = 0;

    for (const num of numSet) {
        // Only start counting if num is start of sequence
        if (!numSet.has(num - 1)) {
            let length = 1;
            let current = num;

            while (numSet.has(current + 1)) {
                current++;
                length++;
            }

            longest = Math.max(longest, length);
        }
    }

    return longest;
}
// Time: O(n), Space: O(n)
```

**Key Insight**: Each number visited only once in the while loop across all iterations.

---

#### 11. Subarray Sum Equals K
**LeetCode**: #560 | **Frequency**: 🔥🔥🔥 | **Companies**: [F][G][A]

**Problem**: Count subarrays with sum = k.

**Solution** (Prefix Sum + Hash Map):
```javascript
function subarraySum(nums, k) {
    const prefixSums = new Map([[0, 1]]); // sum → count
    let sum = 0, count = 0;

    for (const num of nums) {
        sum += num;
        // If (sum - k) exists, we found subarray(s) summing to k
        if (prefixSums.has(sum - k)) {
            count += prefixSums.get(sum - k);
        }
        prefixSums.set(sum, (prefixSums.get(sum) || 0) + 1);
    }

    return count;
}
// Time: O(n), Space: O(n)
```

---

## ⚠️ Common Mistakes

1. **Wrong Key Type**: Using mutable objects as keys
2. **Forgetting Edge Cases**: Empty arrays, single elements
3. **Not Handling Collisions**: Assuming hash is perfect
4. **Overcomplicating**: Using Map when Set suffices
5. **Integer Overflow**: In languages without BigInt

---

## 💡 Pro Tips

1. **Array vs Map**: If range ≤ 256, use array for better performance
2. **Sorted String Key**: Common for anagram problems
3. **Prefix Sum Hash**: Standard for "subarray sum = k" problems
4. **Set for Existence**: Don't use Map if you only care about presence

---

## ✅ Mastery Checklist

- [ ] Can implement frequency counter in <2 min
- [ ] Recognize Two Sum pattern variants
- [ ] Know when to use Set vs Map
- [ ] Understand prefix sum + hash technique
- [ ] Can group items by custom keys
- [ ] Solved 80% of Easy problems
- [ ] Solved 60% of Medium problems
- [ ] Solved 40% of Hard problems

---

[⬅️ Back to Patterns](../) | [Next Pattern: Two Pointers →](../02-Two-Pointers/)
