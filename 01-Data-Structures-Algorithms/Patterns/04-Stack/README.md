# 📚 Pattern 4: Stack

Master stack data structure and monotonic stack for efficient problem solving.

## 🎯 When to Use

- **Parentheses** matching/validation
- **Next/Previous greater/smaller** element
- **Nested** structures
- **Undo/Redo** operations
- **Expression** evaluation
- **Histogram/Area** problems

## 🚩 Trigger Words

- "valid parentheses", "balanced brackets"
- "next greater element", "next smaller"
- "largest rectangle", "histogram"
- "daily temperatures", "stock span"
- "evaluate expression", "calculator"
- "nested", "most recent"

## 💻 Templates

### Template 1: Basic Stack
```javascript
const stack = [];
stack.push(item);      // Add to top
const top = stack[stack.length - 1];  // Peek
const item = stack.pop();  // Remove from top
const isEmpty = stack.length === 0;
```

### Template 2: Monotonic Stack (Next Greater)
```javascript
function nextGreater(nums) {
    const result = new Array(nums.length).fill(-1);
    const stack = []; // Stores indices

    for (let i = 0; i < nums.length; i++) {
        while (stack.length && nums[stack[stack.length-1]] < nums[i]) {
            const idx = stack.pop();
            result[idx] = nums[i];
        }
        stack.push(i);
    }
    return result;
}
```

## 📚 Key Problems

### 🟢 Easy

**1. Valid Parentheses** (LC #20) 🔥🔥🔥
```javascript
function isValid(s) {
    const stack = [];
    const pairs = {'(':')', '[':']', '{':'}'};

    for (const char of s) {
        if (char in pairs) {
            stack.push(char);
        } else {
            if (!stack.length || pairs[stack.pop()] !== char) {
                return false;
            }
        }
    }
    return stack.length === 0;
}
// Time: O(n), Space: O(n)
```

**2. Min Stack** (LC #155) 🔥🔥
```javascript
class MinStack {
    constructor() {
        this.stack = [];
        this.minStack = [];
    }

    push(val) {
        this.stack.push(val);
        const min = this.minStack.length === 0
            ? val
            : Math.min(val, this.minStack[this.minStack.length-1]);
        this.minStack.push(min);
    }

    pop() {
        this.stack.pop();
        this.minStack.pop();
    }

    top() {
        return this.stack[this.stack.length-1];
    }

    getMin() {
        return this.minStack[this.minStack.length-1];
    }
}
// All operations: O(1)
```

### 🟡 Medium

**3. Daily Temperatures** (LC #739) 🔥🔥🔥
```javascript
function dailyTemperatures(temperatures) {
    const result = new Array(temperatures.length).fill(0);
    const stack = []; // indices

    for (let i = 0; i < temperatures.length; i++) {
        while (stack.length && temperatures[stack[stack.length-1]] < temperatures[i]) {
            const idx = stack.pop();
            result[idx] = i - idx;
        }
        stack.push(i);
    }
    return result;
}
// Time: O(n), Space: O(n)
```

**4. Evaluate Reverse Polish Notation** (LC #150) 🔥🔥
```javascript
function evalRPN(tokens) {
    const stack = [];
    const ops = {
        '+': (a,b) => a+b,
        '-': (a,b) => a-b,
        '*': (a,b) => a*b,
        '/': (a,b) => Math.trunc(a/b)
    };

    for (const token of tokens) {
        if (token in ops) {
            const b = stack.pop();
            const a = stack.pop();
            stack.push(ops[token](a, b));
        } else {
            stack.push(parseInt(token));
        }
    }
    return stack[0];
}
```

### 🔴 Hard

**5. Largest Rectangle in Histogram** (LC #84) 🔥🔥🔥
```javascript
function largestRectangleArea(heights) {
    const stack = [];
    let maxArea = 0;
    heights.push(0); // Sentinel

    for (let i = 0; i < heights.length; i++) {
        while (stack.length && heights[stack[stack.length-1]] > heights[i]) {
            const h = heights[stack.pop()];
            const w = stack.length === 0 ? i : i - stack[stack.length-1] - 1;
            maxArea = Math.max(maxArea, h * w);
        }
        stack.push(i);
    }
    return maxArea;
}
// Time: O(n), Space: O(n)
```

## ✅ Mastery Checklist

- [ ] Understand LIFO principle
- [ ] Know monotonic stack pattern
- [ ] Can solve parentheses problems
- [ ] Solved Next Greater variants
- [ ] Understand histogram pattern

[⬅️ Back to Patterns](../)
