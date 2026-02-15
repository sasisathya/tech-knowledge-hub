````markdown
# Matrix Traversal DSA Patterns – Problem Set (Java)

This document collects **core matrix/grid traversal patterns** and representative problems (25 total) with:

- Pattern / algorithm (left)
- Optimized Java solution
- Clear problem statement
- Example input/output

These cover most real interview problems involving 2D arrays / grids.

---

## 🧩 Pattern Index

1. Basic Traversals & Boundaries  
   1.1 Print matrix row-wise  
   1.2 Print matrix in spiral order  
   1.3 Zigzag (snake) traversal  

2. Rotation & Transform  
   2.1 Transpose of a matrix  
   2.2 Rotate matrix 90° clockwise  

3. DFS / BFS – Connected Components  
   3.1 Number of islands (4-direction)  
   3.2 Max area of island  
   3.3 Count closed islands  

4. BFS – Shortest Path in Grid  
   4.1 Shortest path in binary matrix  
   4.2 Shortest path in a maze (4-dir)  

5. Flood Fill & Region Capture  
   5.1 Flood fill  
   5.2 Surrounded regions  

6. Backtracking on Grid  
   6.1 Word search (exist path for word)  
   6.2 Rat in a maze – all paths  

7. DP on Grid (Paths & Costs)  
   7.1 Unique paths  
   7.2 Unique paths with obstacles  
   7.3 Minimum path sum  
   7.4 Maximal square of 1s  

8. 2D Prefix Sum  
   8.1 Immutable 2D range sum query  
   8.2 Count submatrices with sum = target  

9. Multi-source BFS / Simulation  
   9.1 Rotting oranges  
   9.2 Walls and gates  

10. Matrix State Transform  
   10.1 Set matrix zeroes  
   10.2 Game of Life  

---

## 1. Basic Traversals & Boundaries

### 1.1 Print Matrix Row-wise

- **Pattern**: Simple traversal
- **Algorithm**: Two nested loops `O(m·n)`
- **Time**: O(m·n), **Space**: O(1) extra (ignoring output)

**Question**

> Given an `m x n` matrix, print (or return) its elements in row-major order.

**Example**

Input:
```text
matrix = [
  [1, 2, 3],
  [4, 5, 6]
]
````

Output:

```text
[1, 2, 3, 4, 5, 6]
```

**Java Solution**

```java
import java.util.*;

class RowWiseTraversal {
    public List<Integer> traverse(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        int m = matrix.length;
        if (m == 0) return res;
        int n = matrix[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                res.add(matrix[i][j]);
            }
        }
        return res;
    }
}
```

---

### 1.2 Spiral Order Traversal

* **Pattern**: Boundary shrink (top/bottom/left/right)
* **Algorithm**: Traverse edges and shrink bounds
* **Time**: O(m·n), **Space**: O(1) extra

**Question**

> Given an `m x n` matrix, return all elements in spiral order.

**Example**

Input:

```text
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

Output:

```text
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

**Java Solution**

```java
import java.util.*;

class SpiralTraversal {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0) return res;
        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;
        while (top <= bottom && left <= right) {
            for (int j = left; j <= right; j++)
                res.add(matrix[top][j]);
            top++;
            for (int i = top; i <= bottom; i++)
                res.add(matrix[i][right]);
            right--;
            if (top <= bottom) {
                for (int j = right; j >= left; j--)
                    res.add(matrix[bottom][j]);
                bottom--;
            }
            if (left <= right) {
                for (int i = bottom; i >= top; i--)
                    res.add(matrix[i][left]);
                left++;
            }
        }
        return res;
    }
}
```

---

### 1.3 Zigzag (Snake) Traversal

* **Pattern**: Alternating direction per row
* **Algorithm**: Traverse left→right then right→left
* **Time**: O(m·n), **Space**: O(1) extra

**Question**

> Print matrix in “snake” pattern: first row left→right, second row right→left, etc.

**Example**

Input:

```text
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

Output:

```text
[1, 2, 3, 6, 5, 4, 7, 8, 9]
```

**Java Solution**

```java
import java.util.*;

class ZigzagTraversal {
    public List<Integer> snakeOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        int m = matrix.length;
        if (m == 0) return res;
        int n = matrix[0].length;
        for (int i = 0; i < m; i++) {
            if (i % 2 == 0) {
                for (int j = 0; j < n; j++) res.add(matrix[i][j]);
            } else {
                for (int j = n - 1; j >= 0; j--) res.add(matrix[i][j]);
            }
        }
        return res;
    }
}
```

---

## 2. Rotation & Transform

### 2.1 Transpose of a Matrix (in-place for square)

* **Pattern**: Diagonal swap
* **Algorithm**: Swap `(i,j)` with `(j,i)` for `i < j`
* **Time**: O(n²), **Space**: O(1)

**Question**

> Given an `n x n` matrix, transpose it in-place.

**Example**

Input:

```text
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

Output:

```text
[
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9]
]
```

**Java Solution**

```java
class TransposeMatrix {
    public void transpose(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
}
```

---

### 2.2 Rotate Matrix 90° Clockwise

* **Pattern**: Transpose + reverse rows
* **Algorithm**: In-place transform
* **Time**: O(n²), **Space**: O(1)

**Question**

> Rotate an `n x n` matrix by 90 degrees clockwise in-place.

**Example**

Input:

```text
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

Output:

```text
[
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3]
]
```

**Java Solution**

```java
class RotateMatrix {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        // transpose
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
        // reverse each row
        for (int i = 0; i < n; i++) {
            int l = 0, r = n - 1;
            while (l < r) {
                int tmp = matrix[i][l];
                matrix[i][l] = matrix[i][r];
                matrix[i][r] = tmp;
                l++; r--;
            }
        }
    }
}
```

---

## 3. DFS / BFS – Connected Components

### 3.1 Number of Islands (4-direction DFS)

* **Pattern**: DFS connected components in grid
* **Algorithm**: DFS from each unvisited land cell
* **Time**: O(m·n), **Space**: O(m·n) recursion/stack

**Question**

> Given a 2D grid of `'1'` (land) and `'0'` (water), count the number of islands.
> An island is surrounded by water and formed by connecting adjacent lands horizontally or vertically.

**Example**

Input:

```text
[
  ['1','1','0','0'],
  ['1','0','0','1'],
  ['0','0','1','1']
]
```

Output:

```text
3
```

**Java Solution**

```java
class NumberOfIslands {
    private int m, n;
    private char[][] grid;

    public int numIslands(char[][] grid) {
        this.grid = grid;
        m = grid.length;
        if (m == 0) return 0;
        n = grid[0].length;
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    dfs(i, j);
                    count++;
                }
            }
        }
        return count;
    }

    private void dfs(int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1') return;
        grid[i][j] = '0';
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }
}
```

---

### 3.2 Max Area of Island

* **Pattern**: DFS with area accumulation
* **Time**: O(m·n)

**Question**

> Given a grid of 0s and 1s, return the size of the largest island (connected 1s).

**Example**

Input:

```text
[
  [0,0,1,0],
  [1,1,1,0],
  [0,1,0,0]
]
```

Output:

```text
5
```

**Java Solution**

```java
class MaxAreaOfIsland {
    private int m, n;
    private int[][] grid;

    public int maxAreaOfIsland(int[][] grid) {
        this.grid = grid;
        m = grid.length;
        if (m == 0) return 0;
        n = grid[0].length;
        int max = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    max = Math.max(max, dfs(i, j));
                }
            }
        }
        return max;
    }

    private int dfs(int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != 1) return 0;
        grid[i][j] = 0;
        int area = 1;
        area += dfs(i + 1, j);
        area += dfs(i - 1, j);
        area += dfs(i, j + 1);
        area += dfs(i, j - 1);
        return area;
    }
}
```

---

### 3.3 Count Closed Islands

* **Pattern**: DFS with boundary exclusion
* **Algorithm**: First eliminate islands touching boundary, then count remaining
* **Time**: O(m·n)

**Question**

> Given a grid of 0 (land) and 1 (water), a closed island is land completely surrounded by water and not touching the grid border. Count closed islands.

**Example**

Input:

```text
[
  [1,1,1,1],
  [1,0,0,1],
  [1,0,1,1],
  [1,1,1,1]
]
```

Output:

```text
1
```

**Java Solution**

```java
class ClosedIslands {
    private int[][] grid;
    private int m, n;

    public int closedIsland(int[][] grid) {
        this.grid = grid;
        m = grid.length;
        n = grid[0].length;
        // remove border-connected land
        for (int i = 0; i < m; i++) {
            dfs(i, 0);
            dfs(i, n - 1);
        }
        for (int j = 0; j < n; j++) {
            dfs(0, j);
            dfs(m - 1, j);
        }
        int count = 0;
        for (int i = 1; i < m - 1; i++) {
            for (int j = 1; j < n - 1; j++) {
                if (grid[i][j] == 0) {
                    dfs(i, j);
                    count++;
                }
            }
        }
        return count;
    }

    private void dfs(int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 1) return;
        grid[i][j] = 1;
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }
}
```

---

## 4. BFS – Shortest Path in Grid

### 4.1 Shortest Path in Binary Matrix (8-directions)

* **Pattern**: BFS shortest path
* **Algorithm**: BFS with distance layer
* **Time**: O(m·n)

**Question**

> Given an `n x n` binary matrix, where 0 is free and 1 is blocked, return the length of the shortest path from (0,0) to (n-1,n-1) using 8-direction moves. Return -1 if no path.

**Example**

Input:

```text
[
  [0,1],
  [1,0]
]
```

Output:

```text
2
```

**Java Solution**

```java
import java.util.*;

class ShortestPathBinaryMatrix {
    public int shortestPathBinaryMatrix(int[][] grid) {
        int n = grid.length;
        if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1) return -1;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1},{1,1},{1,-1},{-1,1},{-1,-1}};
        boolean[][] vis = new boolean[n][n];
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{0, 0, 1}); // (i,j,dist)
        vis[0][0] = true;
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int i = cur[0], j = cur[1], d = cur[2];
            if (i == n - 1 && j == n - 1) return d;
            for (int[] dir : dirs) {
                int ni = i + dir[0], nj = j + dir[1];
                if (ni >= 0 && ni < n && nj >= 0 && nj < n &&
                    !vis[ni][nj] && grid[ni][nj] == 0) {
                    vis[ni][nj] = true;
                    q.offer(new int[]{ni, nj, d + 1});
                }
            }
        }
        return -1;
    }
}
```

---

### 4.2 Shortest Path in a Maze (4-direction)

* **Pattern**: BFS shortest path in grid
* **Time**: O(m·n)

**Question**

> Given a grid with 0 = free, 1 = wall, find min steps from (0,0) to (m-1,n-1) moving 4-directions. Return -1 if unreachable.

**Example**

Input:

```text
[
  [0,0,1],
  [1,0,1],
  [0,0,0]
]
```

Output:

```text
4
```

**Java Solution**

```java
import java.util.*;

class ShortestPathMaze {
    public int shortestPath(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        if (grid[0][0] == 1 || grid[m - 1][n - 1] == 1) return -1;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        boolean[][] vis = new boolean[m][n];
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{0, 0, 0});
        vis[0][0] = true;
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int i = cur[0], j = cur[1], d = cur[2];
            if (i == m - 1 && j == n - 1) return d;
            for (int[] dir : dirs) {
                int ni = i + dir[0], nj = j + dir[1];
                if (ni >= 0 && ni < m && nj >= 0 && nj < n &&
                    !vis[ni][nj] && grid[ni][nj] == 0) {
                    vis[ni][nj] = true;
                    q.offer(new int[]{ni, nj, d + 1});
                }
            }
        }
        return -1;
    }
}
```

---

## 5. Flood Fill & Region Capture

### 5.1 Flood Fill

* **Pattern**: DFS/BFS region fill
* **Time**: O(m·n)

**Question**

> Implement flood fill on an image starting at `(sr, sc)` changing target color to `newColor`.

**Example**

Input:

```text
image = [
  [1,1,1],
  [1,1,0],
  [1,0,1]
], sr = 1, sc = 1, newColor = 2
```

Output:

```text
[
  [2,2,2],
  [2,2,0],
  [2,0,1]
]
```

**Java Solution**

```java
class FloodFill {
    private int m, n, oldColor, newColor;
    private int[][] image;

    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        this.image = image;
        m = image.length;
        n = image[0].length;
        this.newColor = newColor;
        oldColor = image[sr][sc];
        if (oldColor == newColor) return image;
        dfs(sr, sc);
        return image;
    }

    private void dfs(int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || image[i][j] != oldColor) return;
        image[i][j] = newColor;
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }
}
```

---

### 5.2 Surrounded Regions

* **Pattern**: DFS from border + flip internal regions
* **Time**: O(m·n)

**Question**

> Given a board of 'X' and 'O', capture all regions of 'O' completely surrounded by 'X' by flipping them to 'X'. 'O's on border or connected to border remain.

**Example**

Input:

```text
[
  ['X','X','X','X'],
  ['X','O','O','X'],
  ['X','X','O','X'],
  ['X','O','X','X']
]
```

Output:

```text
[
  ['X','X','X','X'],
  ['X','X','X','X'],
  ['X','X','X','X'],
  ['X','O','X','X']
]
```

**Java Solution**

```java
class SurroundedRegions {
    private char[][] board;
    private int m, n;

    public void solve(char[][] board) {
        this.board = board;
        m = board.length;
        if (m == 0) return;
        n = board[0].length;
        // mark border-connected 'O's as '#'
        for (int i = 0; i < m; i++) {
            dfs(i, 0);
            dfs(i, n - 1);
        }
        for (int j = 0; j < n; j++) {
            dfs(0, j);
            dfs(m - 1, j);
        }
        // flip inside 'O' → 'X', '#' → 'O'
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                else if (board[i][j] == '#') board[i][j] = 'O';
            }
        }
    }

    private void dfs(int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != 'O') return;
        board[i][j] = '#';
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }
}
```

---

## 6. Backtracking on Grid

### 6.1 Word Search

* **Pattern**: Backtracking on grid
* **Algorithm**: DFS with visited markers
* **Time**: O(m·n·4^L) worst, L = word length

**Question**

> Given a 2D board and a word, check if the word exists in the grid. The word can be constructed from adjacent cells (4-dir) without reusing a cell.

**Example**

Input:

```text
board = [
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
], word = "ABCCED"
```

Output:

```text
true
```

**Java Solution**

```java
class WordSearch {
    private char[][] board;
    private String word;
    private int m, n;

    public boolean exist(char[][] board, String word) {
        this.board = board;
        this.word = word;
        m = board.length;
        n = board[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (dfs(i, j, 0)) return true;
            }
        }
        return false;
    }

    private boolean dfs(int i, int j, int idx) {
        if (idx == word.length()) return true;
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != word.charAt(idx))
            return false;
        char temp = board[i][j];
        board[i][j] = '#';
        boolean found = dfs(i + 1, j, idx + 1) ||
                        dfs(i - 1, j, idx + 1) ||
                        dfs(i, j + 1, idx + 1) ||
                        dfs(i, j - 1, idx + 1);
        board[i][j] = temp;
        return found;
    }
}
```

---

### 6.2 Rat in a Maze – All Paths

* **Pattern**: Backtracking all paths
* **Time**: Exponential in number of paths, optimal backtracking

**Question**

> Given an `n x n` maze where 1 is open and 0 is blocked, starting at (0,0) and moving D/R/U/L, print all possible paths to (n-1,n-1) as strings of directions.

**Example**

Input:

```text
maze = [
  [1,0,0],
  [1,1,0],
  [0,1,1]
]
```

Output (order may vary):

```text
["DRR", "RDR"]
```

**Java Solution**

```java
import java.util.*;

class RatInMaze {
    private int[][] maze;
    private int n;
    private boolean[][] vis;
    private List<String> res;
    private final int[][] dirs = {{1,0},{0,1},{0,-1},{-1,0}};
    private final char[] dirChar = {'D','R','L','U'};

    public List<String> findPaths(int[][] maze) {
        this.maze = maze;
        n = maze.length;
        res = new ArrayList<>();
        if (n == 0 || maze[0][0] == 0 || maze[n - 1][n - 1] == 0) return res;
        vis = new boolean[n][n];
        backtrack(0, 0, new StringBuilder());
        return res;
    }

    private void backtrack(int i, int j, StringBuilder path) {
        if (i == n - 1 && j == n - 1) {
            res.add(path.toString());
            return;
        }
        vis[i][j] = true;
        for (int k = 0; k < 4; k++) {
            int ni = i + dirs[k][0], nj = j + dirs[k][1];
            if (ni >= 0 && ni < n && nj >= 0 && nj < n &&
                maze[ni][nj] == 1 && !vis[ni][nj]) {
                path.append(dirChar[k]);
                backtrack(ni, nj, path);
                path.deleteCharAt(path.length() - 1);
            }
        }
        vis[i][j] = false;
    }
}
```

---

## 7. DP on Grid (Paths & Costs)

### 7.1 Unique Paths (m x n, only right and down)

* **Pattern**: DP on grid
* **Time**: O(m·n), **Space**: O(n) optimized

**Question**

> Robot starts at top-left, can only move right or down. How many unique paths to bottom-right?

**Example**

Input:

```text
m = 3, n = 7
```

Output:

```text
28
```

**Java Solution**

```java
class UniquePaths {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        dp[0] = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] += dp[j - 1];
            }
        }
        return dp[n - 1];
    }
}
```

---

### 7.2 Unique Paths with Obstacles

* **Pattern**: DP with blocked cells
* **Time**: O(m·n), **Space**: O(n)

**Question**

> Same as above, but some cells are obstacles (1). Return number of paths.

**Example**

Input:

```text
obstacleGrid = [
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

Output:

```text
2
```

**Java Solution**

```java
class UniquePathsWithObstacles {
    public int uniquePathsWithObstacles(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[] dp = new int[n];
        dp[0] = grid[0][0] == 1 ? 0 : 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) dp[j] = 0;
                else if (j > 0) dp[j] += dp[j - 1];
            }
        }
        return dp[n - 1];
    }
}
```

---

### 7.3 Minimum Path Sum

* **Pattern**: DP cost minimization
* **Time**: O(m·n), **Space**: O(n)

**Question**

> Given a grid of non-negative numbers, find path from top-left to bottom-right with minimum sum (move only right/down).

**Example**

Input:

```text
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
```

Output:

```text
7
```

**Java Solution**

```java
class MinPathSum {
    public int minPathSum(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[] dp = new int[n];
        dp[0] = grid[0][0];
        for (int j = 1; j < n; j++) {
            dp[j] = dp[j - 1] + grid[0][j];
        }
        for (int i = 1; i < m; i++) {
            dp[0] += grid[i][0];
            for (int j = 1; j < n; j++) {
                dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
            }
        }
        return dp[n - 1];
    }
}
```

---

### 7.4 Maximal Square of 1s

* **Pattern**: DP on grid with neighbor dependency
* **Time**: O(m·n), **Space**: O(n)

**Question**

> Given a binary matrix of '0' and '1', find the area of the largest square containing only 1s.

**Example**

Input:

```text
[
  ['1','0','1','0','0'],
  ['1','0','1','1','1'],
  ['1','1','1','1','1'],
  ['1','0','0','1','0']
]
```

Output:

```text
4
```

**Java Solution**

```java
class MaximalSquare {
    public int maximalSquare(char[][] matrix) {
        int m = matrix.length;
        if (m == 0) return 0;
        int n = matrix[0].length;
        int[] dp = new int[n + 1];
        int maxSide = 0, prev = 0;
        for (int i = 1; i <= m; i++) {
            prev = 0;
            for (int j = 1; j <= n; j++) {
                int temp = dp[j];
                if (matrix[i - 1][j - 1] == '1') {
                    dp[j] = Math.min(Math.min(dp[j], dp[j - 1]), prev) + 1;
                    maxSide = Math.max(maxSide, dp[j]);
                } else {
                    dp[j] = 0;
                }
                prev = temp;
            }
        }
        return maxSide * maxSide;
    }
}
```

---

## 8. 2D Prefix Sum

### 8.1 Immutable 2D Range Sum Query

* **Pattern**: 2D prefix sum
* **Time**: Build O(m·n), Query O(1)

**Question**

> Implement a class `NumMatrix` that given a matrix, returns sum of elements in a given sub-rectangle `(row1,col1)` to `(row2,col2)` inclusive, many queries.

**Example**

Input:

```text
matrix = [
  [3,0,1,4,2],
  [5,6,3,2,1],
  [1,2,0,1,5],
  [4,1,0,1,7],
  [1,0,3,0,5]
]
sumRegion(2,1,4,3) -> 8
```

**Java Solution**

```java
class NumMatrix {
    private int[][] pref;

    public NumMatrix(int[][] matrix) {
        int m = matrix.length;
        if (m == 0) return;
        int n = matrix[0].length;
        pref = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            int rowSum = 0;
            for (int j = 1; j <= n; j++) {
                rowSum += matrix[i - 1][j - 1];
                pref[i][j] = pref[i - 1][j] + rowSum;
            }
        }
    }

    public int sumRegion(int r1, int c1, int r2, int c2) {
        r1++; c1++; r2++; c2++;
        return pref[r2][c2] - pref[r1 - 1][c2] - pref[r2][c1 - 1] + pref[r1 - 1][c1 - 1];
    }
}
```

---

### 8.2 Count Submatrices With Sum = Target (Optimized)

* **Pattern**: 2D prefix + 1D subarray sum with HashMap
* **Time**: O(m²·n) or O(n²·m) depending on orientation

**Question**

> Given a matrix and an integer target, count submatrices whose sum equals target.

**Example**

Input:

```text
matrix = [
  [0,1,0],
  [1,1,1],
  [0,1,0]
], target = 2
```

Output:

```text
4
```

**Java Solution**

```java
import java.util.*;

class SubmatrixSumTarget {
    public int numSubmatrixSumTarget(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        // prefix sums by row
        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                matrix[i][j] += matrix[i][j - 1];
            }
        }
        int count = 0;
        for (int left = 0; left < n; left++) {
            for (int right = left; right < n; right++) {
                Map<Integer, Integer> freq = new HashMap<>();
                freq.put(0, 1);
                int sum = 0;
                for (int i = 0; i < m; i++) {
                    int rowSum = matrix[i][right] - (left > 0 ? matrix[i][left - 1] : 0);
                    sum += rowSum;
                    count += freq.getOrDefault(sum - target, 0);
                    freq.put(sum, freq.getOrDefault(sum, 0) + 1);
                }
            }
        }
        return count;
    }
}
```

---

## 9. Multi-source BFS / Simulation

### 9.1 Rotting Oranges

* **Pattern**: Multi-source BFS in grid
* **Time**: O(m·n)

**Question**

> In a grid, 0 = empty, 1 = fresh orange, 2 = rotten. Each minute, rotten oranges turn adjacent fresh ones rotten. Return minutes until no fresh left, or -1 if impossible.

**Example**

Input:

```text
[
  [2,1,1],
  [1,1,0],
  [0,1,1]
]
```

Output:

```text
4
```

**Java Solution**

```java
import java.util.*;

class RottingOranges {
    public int orangesRotting(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        Queue<int[]> q = new LinkedList<>();
        int fresh = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) q.offer(new int[]{i, j});
                else if (grid[i][j] == 1) fresh++;
            }
        }
        if (fresh == 0) return 0;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        int minutes = -1;
        while (!q.isEmpty()) {
            int size = q.size();
            minutes++;
            for (int s = 0; s < size; s++) {
                int[] cur = q.poll();
                for (int[] d : dirs) {
                    int ni = cur[0] + d[0], nj = cur[1] + d[1];
                    if (ni >= 0 && ni < m && nj >= 0 && nj < n && grid[ni][nj] == 1) {
                        grid[ni][nj] = 2;
                        fresh--;
                        q.offer(new int[]{ni, nj});
                    }
                }
            }
        }
        return fresh == 0 ? minutes : -1;
    }
}
```

---

### 9.2 Walls and Gates

* **Pattern**: Multi-source BFS from gates
* **Time**: O(m·n)

**Question**

> Rooms grid: -1 = wall, 0 = gate, INF = empty room. Fill each empty room with distance to nearest gate.

**Example**

Input:

```text
[
  [INF, -1, 0, INF],
  [INF, INF, INF, -1],
  [INF, -1, INF, -1],
  [0, -1, INF, INF]
]
```

Output:

```text
[
  [3, -1, 0, 1],
  [2, 2, 1, -1],
  [1, -1, 2, -1],
  [0, -1, 3, 4]
]
```

**Java Solution**

```java
import java.util.*;

class WallsAndGates {
    private static final int INF = 2147483647;

    public void wallsAndGates(int[][] rooms) {
        int m = rooms.length;
        if (m == 0) return;
        int n = rooms[0].length;
        Queue<int[]> q = new LinkedList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) q.offer(new int[]{i, j});
            }
        }
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            for (int[] d : dirs) {
                int ni = cur[0] + d[0], nj = cur[1] + d[1];
                if (ni >= 0 && ni < m && nj >= 0 && nj < n &&
                    rooms[ni][nj] == INF) {
                    rooms[ni][nj] = rooms[cur[0]][cur[1]] + 1;
                    q.offer(new int[]{ni, nj});
                }
            }
        }
    }
}
```

---

## 10. Matrix State Transform

### 10.1 Set Matrix Zeroes

* **Pattern**: In-place marking using first row/col
* **Time**: O(m·n), **Space**: O(1)

**Question**

> If an element is 0, set its entire row and column to 0. Do it in-place.

**Example**

Input:

```text
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
```

Output:

```text
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**Java Solution**

```java
class SetMatrixZeroes {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;
        boolean firstRowZero = false, firstColZero = false;
        for (int j = 0; j < n; j++)
            if (matrix[0][j] == 0) firstRowZero = true;
        for (int i = 0; i < m; i++)
            if (matrix[i][0] == 0) firstColZero = true;

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for (int i = 1; i < m; i++) {
            if (matrix[i][0] == 0) {
                for (int j = 1; j < n; j++) matrix[i][j] = 0;
            }
        }
        for (int j = 1; j < n; j++) {
            if (matrix[0][j] == 0) {
                for (int i = 1; i < m; i++) matrix[i][j] = 0;
            }
        }
        if (firstRowZero) {
            for (int j = 0; j < n; j++) matrix[0][j] = 0;
        }
        if (firstColZero) {
            for (int i = 0; i < m; i++) matrix[i][0] = 0;
        }
    }
}
```

---

### 10.2 Game of Life

* **Pattern**: In-place state encoding
* **Algorithm**: Use bits to encode old/new state
* **Time**: O(m·n), **Space**: O(1) extra

**Question**

> Implement Conway’s Game of Life for one step on a board in-place.

**Example**

Input:

```text
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
```

Output (one step):

```text
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```

**Java Solution**

```java
class GameOfLife {
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1},{1,1},{1,-1},{-1,1},{-1,-1}};
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int liveNeighbors = 0;
                for (int[] d : dirs) {
                    int ni = i + d[0], nj = j + d[1];
                    if (ni >= 0 && ni < m && nj >= 0 && nj < n &&
                        (board[ni][nj] & 1) == 1) {
                        liveNeighbors++;
                    }
                }
                if ((board[i][j] & 1) == 1) {
                    if (liveNeighbors == 2 || liveNeighbors == 3)
                        board[i][j] |= 2; // live next
                } else {
                    if (liveNeighbors == 3)
                        board[i][j] |= 2; // become live
                }
            }
        }
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] >>= 1;
            }
        }
    }
}
```

---

## ✅ Summary

This set of 25 problems shows the **main matrix traversal sub-patterns**:

* Simple traversals & boundary shrink
* DFS/BFS components, shortest paths, multi-source BFS
* Backtracking on grid (word search, paths)
* DP on grids (paths, minimal cost, largest area)
* 2D prefix sums & submatrix counting
* In-place state transforms and simulations

