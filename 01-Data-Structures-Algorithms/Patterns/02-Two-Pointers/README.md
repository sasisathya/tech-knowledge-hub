# ↔️ Pattern 2: Two Pointers

Master the two-pointer technique for efficient array and string problems.

---

## 🎯 When to Use This Pattern

- Working with **sorted arrays** or strings
- Need to find **pairs** with specific properties
- **In-place** operations (no extra space)
- **Palindrome** problems
- **Partitioning** or removing elements
- **Comparing elements** from both ends

---

## 🚩 Trigger Words

| Trigger Phrase | Likely Approach |
|----------------|-----------------|
| "sorted array", "pair sums to..." | Two pointers (opposite ends) |
| "remove duplicates in-place" | Two pointers (slow/fast) |
| "palindrome", "symmetric" | Two pointers (opposite ends) |
| "partition", "move all X to end" | Two pointers (slow/fast) |
| "three sum", "four sum" | Two pointers + iteration |
| "container", "area", "trap water" | Two pointers (greedy choice) |

---

## 📝 Core Concepts

### 1. Opposite Direction (Converging)
- Start from **both ends** of array
- Move pointers toward each other
- **Use**: Sorted array problems, palindromes

### 2. Same Direction (Fast/Slow)
- Both start from **beginning**
- Move at different speeds
- **Use**: In-place modifications, cycle detection

### 3. Fixed Distance
- Maintain **constant gap** between pointers
- Move together through array
- **Use**: Fixed-size window, k-distance problems

---

## 💻 Templates

### Template 1: Opposite Direction
```javascript
function twoPointersOpposite(arr) {
    let left = 0, right = arr.length - 1;

    while (left < right) {
        // Process current pair
        if (condition) {
            // Found answer
            return result;
        } else if (needSmaller) {
            right--;  // Move right pointer left
        } else {
            left++;   // Move left pointer right
        }
    }
    return defaultResult;
}
// Time: O(n), Space: O(1)
```

### Template 2: Same Direction (Slow/Fast)
```javascript
function twoPointersSameDirection(arr) {
    let slow = 0;

    for (let fast = 0; fast < arr.length; fast++) {
        if (shouldKeep(arr[fast])) {
            arr[slow] = arr[fast];
            slow++;
        }
    }
    return slow; // new length or count
}
// Time: O(n), Space: O(1)
```

### Template 3: Three Pointers (3Sum Pattern)
```javascript
function threeSum(nums) {
    nums.sort((a, b) => a - b);
    const result = [];

    for (let i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] === nums[i-1]) continue; // skip duplicates

        let left = i + 1, right = nums.length - 1;
        while (left < right) {
            const sum = nums[i] + nums[left] + nums[right];
            if (sum === target) {
                result.push([nums[i], nums[left], nums[right]]);
                while (left < right && nums[left] === nums[left+1]) left++;
                while (left < right && nums[right] === nums[right-1]) right--;
                left++; right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }
    return result;
}
```

---

## 📚 Problems (Easy → Hard)

### 🟢 Easy Problems

#### 1. Valid Palindrome
**LeetCode**: #125 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M]

**Problem**: Check if string is palindrome (ignoring non-alphanumeric, case-insensitive).

**Solution**:
```javascript
function isPalindrome(s) {
    let left = 0, right = s.length - 1;

    while (left < right) {
        // Skip non-alphanumeric from left
        while (left < right && !isAlphanumeric(s[left])) {
            left++;
        }
        // Skip non-alphanumeric from right
        while (left < right && !isAlphanumeric(s[right])) {
            right--;
        }

        // Compare characters (case-insensitive)
        if (s[left].toLowerCase() !== s[right].toLowerCase()) {
            return false;
        }

        left++;
        right--;
    }
    return true;
}

function isAlphanumeric(char) {
    return /[a-zA-Z0-9]/.test(char);
}
// Time: O(n), Space: O(1)
```

---

#### 2. Two Sum II - Input Array is Sorted
**LeetCode**: #167 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][A][M]

**Problem**: Find two numbers that add up to target in sorted array. Return 1-indexed positions.

**Solution**:
```javascript
function twoSum(numbers, target) {
    let left = 0, right = numbers.length - 1;

    while (left < right) {
        const sum = numbers[left] + numbers[right];

        if (sum === target) {
            return [left + 1, right + 1]; // 1-indexed
        } else if (sum < target) {
            left++;  // Need larger sum
        } else {
            right--; // Need smaller sum
        }
    }
    return [-1, -1]; // No solution found
}
// Time: O(n), Space: O(1)
```

**Why Two Pointers?** Sorted array allows greedy decision: if sum too small, increase left; if too large, decrease right.

---

#### 3. Remove Duplicates from Sorted Array
**LeetCode**: #26 | **Frequency**: 🔥🔥 | **Companies**: [G][F][M]

**Problem**: Remove duplicates in-place, return new length.

**Solution**:
```javascript
function removeDuplicates(nums) {
    if (nums.length === 0) return 0;

    let slow = 0; // Position for next unique element

    for (let fast = 1; fast < nums.length; fast++) {
        if (nums[fast] !== nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }

    return slow + 1; // Length of unique elements
}
// Time: O(n), Space: O(1)
```

**Key Pattern**: Slow pointer = write position, Fast pointer = read position.

---

#### 4. Move Zeroes
**LeetCode**: #283 | **Frequency**: 🔥🔥 | **Companies**: [F][A]

**Problem**: Move all zeros to end while maintaining order of non-zeros.

**Solution**:
```javascript
function moveZeroes(nums) {
    let slow = 0; // Position for next non-zero

    // Move all non-zeros to front
    for (let fast = 0; fast < nums.length; fast++) {
        if (nums[fast] !== 0) {
            nums[slow] = nums[fast];
            slow++;
        }
    }

    // Fill remaining with zeros
    while (slow < nums.length) {
        nums[slow] = 0;
        slow++;
    }
}
// Time: O(n), Space: O(1)
```

**Alternative** (Swap version):
```javascript
function moveZeroes(nums) {
    let slow = 0;

    for (let fast = 0; fast < nums.length; fast++) {
        if (nums[fast] !== 0) {
            [nums[slow], nums[fast]] = [nums[fast], nums[slow]];
            slow++;
        }
    }
}
```

---

### 🟡 Medium Problems

#### 5. 3Sum
**LeetCode**: #15 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M][AP]

**Problem**: Find all unique triplets that sum to zero.

**Solution**:
```javascript
function threeSum(nums) {
    nums.sort((a, b) => a - b); // Must sort first
    const result = [];

    for (let i = 0; i < nums.length - 2; i++) {
        // Skip duplicates for first number
        if (i > 0 && nums[i] === nums[i-1]) continue;

        // Two sum on remaining array
        let left = i + 1, right = nums.length - 1;
        const target = -nums[i];

        while (left < right) {
            const sum = nums[left] + nums[right];

            if (sum === target) {
                result.push([nums[i], nums[left], nums[right]]);

                // Skip duplicates for second number
                while (left < right && nums[left] === nums[left+1]) left++;
                // Skip duplicates for third number
                while (left < right && nums[right] === nums[right-1]) right--;

                left++;
                right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }

    return result;
}
// Time: O(n²), Space: O(1) - not counting output
```

**Key Insights**:
- Sort first to enable two-pointer technique
- Skip duplicates to avoid duplicate triplets
- Convert to Two Sum II for each fixed element

---

#### 6. Container With Most Water
**LeetCode**: #11 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M]

**Problem**: Find two lines that together with x-axis form container with max water.

**Solution**:
```javascript
function maxArea(height) {
    let left = 0, right = height.length - 1;
    let maxWater = 0;

    while (left < right) {
        // Water limited by shorter line
        const width = right - left;
        const currentWater = Math.min(height[left], height[right]) * width;
        maxWater = Math.max(maxWater, currentWater);

        // Move pointer with shorter height (greedy)
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }

    return maxWater;
}
// Time: O(n), Space: O(1)
```

**Why Greedy Works?** Moving the shorter pointer is the only way to potentially increase area.

---

#### 7. Sort Colors (Dutch National Flag)
**LeetCode**: #75 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A]

**Problem**: Sort array of 0s, 1s, 2s in-place in one pass.

**Solution** (Three Pointers):
```javascript
function sortColors(nums) {
    let low = 0;      // Next position for 0
    let mid = 0;      // Current element
    let high = nums.length - 1; // Next position for 2

    while (mid <= high) {
        if (nums[mid] === 0) {
            [nums[low], nums[mid]] = [nums[mid], nums[low]];
            low++;
            mid++;
        } else if (nums[mid] === 1) {
            mid++; // Already in correct position
        } else { // nums[mid] === 2
            [nums[mid], nums[high]] = [nums[high], nums[mid]];
            high--;
            // Don't increment mid - need to check swapped element
        }
    }
}
// Time: O(n), Space: O(1)
```

**Invariants**:
- `[0...low)` = all 0s
- `[low...mid)` = all 1s
- `[mid...high]` = unprocessed
- `(high...n)` = all 2s

---

#### 8. 3Sum Closest
**LeetCode**: #16 | **Frequency**: 🔥🔥 | **Companies**: [G][A][M]

**Problem**: Find triplet sum closest to target.

**Solution**:
```javascript
function threeSumClosest(nums, target) {
    nums.sort((a, b) => a - b);
    let closest = nums[0] + nums[1] + nums[2];

    for (let i = 0; i < nums.length - 2; i++) {
        let left = i + 1, right = nums.length - 1;

        while (left < right) {
            const sum = nums[i] + nums[left] + nums[right];

            // Update closest if current sum is closer
            if (Math.abs(sum - target) < Math.abs(closest - target)) {
                closest = sum;
            }

            if (sum === target) {
                return sum; // Can't get closer than exact match
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }

    return closest;
}
// Time: O(n²), Space: O(1)
```

---

#### 9. Trapping Rain Water
**LeetCode**: #42 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M][AP]

**Problem**: Calculate how much rainwater can be trapped.

**Solution 1** (Two Pointers - Optimal):
```javascript
function trap(height) {
    let left = 0, right = height.length - 1;
    let leftMax = 0, rightMax = 0;
    let water = 0;

    while (left < right) {
        if (height[left] < height[right]) {
            // Process left side
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                water += leftMax - height[left];
            }
            left++;
        } else {
            // Process right side
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                water += rightMax - height[right];
            }
            right--;
        }
    }

    return water;
}
// Time: O(n), Space: O(1)
```

**Key Insight**: Water at position depends on min(leftMax, rightMax). Process side with smaller max.

---

### 🔴 Hard Problems

#### 10. Minimum Window Substring
**LeetCode**: #76 | **Frequency**: 🔥🔥🔥 | **Companies**: [G][F][A][M]

**Problem**: Find minimum window in S that contains all characters from T.

**Note**: This is actually a Sliding Window problem, but uses two pointers!

**Solution**:
```javascript
function minWindow(s, t) {
    const need = new Map();
    for (const char of t) {
        need.set(char, (need.get(char) || 0) + 1);
    }

    const have = new Map();
    let left = 0, minLen = Infinity, minStart = 0;
    let formed = 0; // Number of unique chars with correct frequency

    for (let right = 0; right < s.length; right++) {
        const char = s[right];
        have.set(char, (have.get(char) || 0) + 1);

        if (need.has(char) && have.get(char) === need.get(char)) {
            formed++;
        }

        // Shrink window while valid
        while (formed === need.size) {
            // Update minimum
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minStart = left;
            }

            // Try to shrink from left
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
// Time: O(|S| + |T|), Space: O(|S| + |T|)
```

---

## ⚠️ Common Mistakes

1. **Forgetting to Sort**: Many two-pointer problems require sorted input
2. **Infinite Loops**: Not updating pointers in all branches
3. **Duplicate Handling**: Forgetting to skip duplicates in nSum problems
4. **Boundary Conditions**: Not checking `left < right` properly
5. **Index Confusion**: Mixing 0-indexed and 1-indexed returns

---

## 💡 Pro Tips

1. **Sort First**: If problem allows, sorting often enables two-pointer approach
2. **Opposite vs Same**: Choose based on problem:
   - Opposite: Pairs, palindromes, sorted arrays
   - Same: In-place modification, partitioning
3. **Greedy Decisions**: Know why moving each pointer is correct
4. **Skip Duplicates**: In problems requiring unique results (3Sum, 4Sum)
5. **Fast/Slow = Write/Read**: Think of slow as write pointer, fast as read pointer

---

## 🎯 Pattern Variations

### 1. nSum Problems (3Sum, 4Sum)
- Sort + fix one element + two pointers on rest
- Time: O(n^(k-1)) for kSum

### 2. Partition Problems
- Dutch National Flag (3-way partition)
- Quick Select partition

### 3. Palindrome Variations
- Check palindrome
- Make palindrome with deletions
- Longest palindromic substring

### 4. Container/Area Problems
- Max area, trapped water
- Always involves greedy pointer movement

---

## ✅ Mastery Checklist

- [ ] Can identify when to use opposite vs same direction
- [ ] Understand why sorting enables two pointers
- [ ] Can handle duplicates in nSum problems
- [ ] Know Dutch National Flag algorithm
- [ ] Solved 80% of Easy problems
- [ ] Solved 60% of Medium problems
- [ ] Solved 40% of Hard problems
- [ ] Can explain time complexity of solutions

---

[⬅️ Back to Patterns](../) | [← Previous: Arrays & Hashing](../01-Arrays-and-Hashing/) | [Next: Sliding Window →](../03-Sliding-Window/)
