# 🌳 Pattern 7: Trees

Master tree traversals, binary search trees, and tree algorithms.

## 🎯 When to Use

- **Hierarchical** data structures
- **Path** problems in trees
- **Level-order** traversal needed
- **Binary Search Tree** operations
- **Ancestor/Descendant** relationships

## 🚩 Trigger Words

- "tree", "binary tree", "BST"
- "path from root to leaf"
- "level order", "zigzag traversal"
- "lowest common ancestor"
- "validate BST", "inorder traversal"
- "serialize/deserialize"

## 💻 Tree Node Definition
```javascript
class TreeNode {
    constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

## 📝 Core Traversals

### DFS Traversals (Recursive)
```javascript
// Inorder: Left -> Root -> Right
function inorder(root) {
    if (!root) return;
    inorder(root.left);
    console.log(root.val);
    inorder(root.right);
}

// Preorder: Root -> Left -> Right
function preorder(root) {
    if (!root) return;
    console.log(root.val);
    preorder(root.left);
    preorder(root.right);
}

// Postorder: Left -> Right -> Root
function postorder(root) {
    if (!root) return;
    postorder(root.left);
    postorder(root.right);
    console.log(root.val);
}
```

### BFS (Level Order)
```javascript
function levelOrder(root) {
    if (!root) return [];
    const result = [];
    const queue = [root];

    while (queue.length) {
        const level = [];
        const size = queue.length;

        for (let i = 0; i < size; i++) {
            const node = queue.shift();
            level.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        result.push(level);
    }
    return result;
}
```

## 📚 Key Problems

### 🟢 Easy

**1. Maximum Depth** (LC #104) 🔥🔥🔥
```javascript
function maxDepth(root) {
    if (!root) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
// Time: O(n), Space: O(h) where h = height
```

**2. Same Tree** (LC #100) 🔥🔥
```javascript
function isSameTree(p, q) {
    if (!p && !q) return true;
    if (!p || !q || p.val !== q.val) return false;
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

**3. Invert Binary Tree** (LC #226) 🔥🔥🔥
```javascript
function invertTree(root) {
    if (!root) return null;
    [root.left, root.right] = [invertTree(root.right), invertTree(root.left)];
    return root;
}
```

### 🟡 Medium

**4. Validate Binary Search Tree** (LC #98) 🔥🔥🔥
```javascript
function isValidBST(root) {
    function validate(node, min, max) {
        if (!node) return true;
        if (node.val <= min || node.val >= max) return false;
        return validate(node.left, min, node.val) &&
               validate(node.right, node.val, max);
    }
    return validate(root, -Infinity, Infinity);
}
// Time: O(n), Space: O(h)
```

**5. Kth Smallest in BST** (LC #230) 🔥🔥🔥
```javascript
function kthSmallest(root, k) {
    const stack = [];
    let curr = root;

    while (curr || stack.length) {
        while (curr) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        k--;
        if (k === 0) return curr.val;
        curr = curr.right;
    }
}
// Time: O(h + k), Space: O(h)
```

**6. Lowest Common Ancestor of BST** (LC #235) 🔥🔥🔥
```javascript
function lowestCommonAncestor(root, p, q) {
    while (root) {
        if (p.val < root.val && q.val < root.val) {
            root = root.left;
        } else if (p.val > root.val && q.val > root.val) {
            root = root.right;
        } else {
            return root;
        }
    }
}
// Time: O(h), Space: O(1)
```

**7. Binary Tree Level Order Traversal** (LC #102) 🔥🔥🔥
```javascript
function levelOrder(root) {
    if (!root) return [];
    const result = [];
    const queue = [root];

    while (queue.length) {
        const level = [];
        const size = queue.length;

        for (let i = 0; i < size; i++) {
            const node = queue.shift();
            level.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        result.push(level);
    }
    return result;
}
// Time: O(n), Space: O(n)
```

**8. Binary Tree Right Side View** (LC #199) 🔥🔥
```javascript
function rightSideView(root) {
    if (!root) return [];
    const result = [];
    const queue = [root];

    while (queue.length) {
        const size = queue.length;
        for (let i = 0; i < size; i++) {
            const node = queue.shift();
            if (i === size - 1) result.push(node.val); // Last node in level
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }
    return result;
}
```

**9. Count Good Nodes** (LC #1448) 🔥🔥
```javascript
function goodNodes(root) {
    function dfs(node, maxSoFar) {
        if (!node) return 0;
        let count = node.val >= maxSoFar ? 1 : 0;
        maxSoFar = Math.max(maxSoFar, node.val);
        count += dfs(node.left, maxSoFar);
        count += dfs(node.right, maxSoFar);
        return count;
    }
    return dfs(root, root.val);
}
```

### 🔴 Hard

**10. Binary Tree Maximum Path Sum** (LC #124) 🔥🔥🔥
```javascript
function maxPathSum(root) {
    let maxSum = -Infinity;

    function dfs(node) {
        if (!node) return 0;

        // Only include positive contributions
        const left = Math.max(0, dfs(node.left));
        const right = Math.max(0, dfs(node.right));

        // Path through current node
        maxSum = Math.max(maxSum, node.val + left + right);

        // Return max path ending at current node
        return node.val + Math.max(left, right);
    }

    dfs(root);
    return maxSum;
}
// Time: O(n), Space: O(h)
```

**11. Serialize and Deserialize Binary Tree** (LC #297) 🔥🔥🔥
```javascript
class Codec {
    serialize(root) {
        const result = [];
        function dfs(node) {
            if (!node) {
                result.push('null');
                return;
            }
            result.push(node.val.toString());
            dfs(node.left);
            dfs(node.right);
        }
        dfs(root);
        return result.join(',');
    }

    deserialize(data) {
        const values = data.split(',');
        let i = 0;

        function dfs() {
            if (values[i] === 'null') {
                i++;
                return null;
            }
            const node = new TreeNode(parseInt(values[i++]));
            node.left = dfs();
            node.right = dfs();
            return node;
        }

        return dfs();
    }
}
```

## 💡 Pro Tips

1. **Recursion**: Most tree problems solved recursively
2. **Base Case**: Always handle `null` node
3. **Return Value**: Know what each recursive call returns
4. **Global Variable**: Use for aggregating results (max sum, count)
5. **BST Property**: Inorder traversal gives sorted order
6. **Level Order**: Use queue (BFS)
7. **DFS**: Use stack or recursion

## ✅ Mastery Checklist

- [ ] Master all three DFS traversals
- [ ] Understand BFS/level order
- [ ] Can validate BST
- [ ] Solve path sum problems
- [ ] Know LCA algorithms
- [ ] Solved 80% Easy problems
- [ ] Solved 60% Medium problems

[⬅️ Back to Patterns](../)
