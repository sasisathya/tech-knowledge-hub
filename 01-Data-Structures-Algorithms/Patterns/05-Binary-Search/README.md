# 🔍 Pattern 5: Binary Search

Master binary search on arrays and search space for O(log n) solutions.

## 🎯 When to Use

- **Sorted array** search
- **Find position** in sorted data
- **Minimize/Maximize** with monotonic function
- **Search space** can be binary searched
- **First/Last occurrence** problems

## 🚩 Trigger Words

- "sorted array"
- "find target", "search"
- "first occurrence", "last occurrence"
- "minimum/maximum capacity"
- "Koko eating bananas", "ship packages in D days"
- "search in rotated sorted array"

## 💻 Templates

### Template 1: Basic Binary Search
```javascript
function binarySearch(nums, target) {
    let left = 0, right = nums.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1; // Not found
}
// Time: O(log n), Space: O(1)
```

### Template 2: Find First/Last Occurrence
```javascript
function findFirst(nums, target) {
    let left = 0, right = nums.length - 1;
    let result = -1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            result = mid;
            right = mid - 1; // Continue searching left
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return result;
}
```

### Template 3: Binary Search on Answer
```javascript
function binarySearchOnAnswer(arr, constraint) {
    let left = minPossible, right = maxPossible;

    while (left < right) {
        const mid = Math.floor((left + right) / 2);

        if (isPossible(mid, arr, constraint)) {
            right = mid; // Try smaller (for minimum)
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

## 📚 Key Problems

### 🟢 Easy

**1. Binary Search** (LC #704) 🔥🔥
```javascript
function search(nums, target) {
    let left = 0, right = nums.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        if (nums[mid] === target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

### 🟡 Medium

**2. Search in Rotated Sorted Array** (LC #33) 🔥🔥🔥
```javascript
function search(nums, target) {
    let left = 0, right = nums.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) return mid;

        // Check which half is sorted
        if (nums[left] <= nums[mid]) {
            // Left half is sorted
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
            // Right half is sorted
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    return -1;
}
// Time: O(log n)
```

**3. Find Minimum in Rotated Sorted Array** (LC #153) 🔥🔥🔥
```javascript
function findMin(nums) {
    let left = 0, right = nums.length - 1;

    while (left < right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] > nums[right]) {
            // Minimum is in right half
            left = mid + 1;
        } else {
            // Minimum is in left half (including mid)
            right = mid;
        }
    }
    return nums[left];
}
```

**4. Koko Eating Bananas** (LC #875) 🔥🔥🔥
```javascript
function minEatingSpeed(piles, h) {
    let left = 1, right = Math.max(...piles);

    while (left < right) {
        const k = Math.floor((left + right) / 2);

        if (canFinish(piles, h, k)) {
            right = k; // Try slower speed
        } else {
            left = k + 1; // Need faster speed
        }
    }
    return left;
}

function canFinish(piles, h, k) {
    let hours = 0;
    for (const pile of piles) {
        hours += Math.ceil(pile / k);
    }
    return hours <= h;
}
// Time: O(n * log(max_pile))
```

### 🔴 Hard

**5. Median of Two Sorted Arrays** (LC #4) 🔥🔥🔥
```javascript
function findMedianSortedArrays(nums1, nums2) {
    if (nums1.length > nums2.length) {
        [nums1, nums2] = [nums2, nums1]; // Ensure nums1 is smaller
    }

    const m = nums1.length, n = nums2.length;
    let left = 0, right = m;

    while (left <= right) {
        const partition1 = Math.floor((left + right) / 2);
        const partition2 = Math.floor((m + n + 1) / 2) - partition1;

        const maxLeft1 = partition1 === 0 ? -Infinity : nums1[partition1-1];
        const minRight1 = partition1 === m ? Infinity : nums1[partition1];
        const maxLeft2 = partition2 === 0 ? -Infinity : nums2[partition2-1];
        const minRight2 = partition2 === n ? Infinity : nums2[partition2];

        if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
            // Found correct partition
            if ((m + n) % 2 === 0) {
                return (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2;
            } else {
                return Math.max(maxLeft1, maxLeft2);
            }
        } else if (maxLeft1 > minRight2) {
            right = partition1 - 1;
        } else {
            left = partition1 + 1;
        }
    }
}
// Time: O(log(min(m,n)))
```

## ✅ Mastery Checklist

- [ ] Master basic binary search
- [ ] Understand search space concept
- [ ] Can find first/last occurrence
- [ ] Solved rotated array problems
- [ ] Know "binary search on answer" pattern

[⬅️ Back to Patterns](../)
