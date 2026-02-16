# 🎯 DSA Patterns Master Guide

Complete pattern-based approach to master Data Structures & Algorithms for technical interviews.

---

## 📋 Table of Contents

1. [How to Use This Guide](#how-to-use-this-guide)
2. [18 Essential Patterns](#18-essential-patterns)
3. [Learning Path](#learning-path)
4. [Pattern Recognition](#pattern-recognition)
5. [Problem Difficulty System](#problem-difficulty-system)

---

## 🚀 How to Use This Guide

### Pattern-Based Learning

Instead of learning algorithms in isolation, we organize problems by **patterns** - recurring strategies that solve similar types of problems.

**Benefits:**
- ✅ Recognize problem types faster in interviews
- ✅ Apply known templates to new problems
- ✅ Build systematic problem-solving approach
- ✅ Cover 90%+ of interview questions

### For Each Pattern:

1. **Concept**: What is the pattern and when to use it
2. **Template**: Reusable code structure
3. **Trigger Words**: How to recognize the pattern in problems
4. **Problems**: 10-20 problems from Easy → Hard
5. **Common Mistakes**: Pitfalls to avoid

---

## 📚 18 Essential Patterns

### **Tier 1: Fundamentals** (Master these first - Weeks 1-4)

| # | Pattern | Difficulty | Priority | Problems |
|---|---------|------------|----------|----------|
| 1 | [Arrays & Hashing](./Patterns/01-Arrays-and-Hashing/) | ⭐ Easy | 🔥 Critical | 15 |
| 2 | [Two Pointers](./Patterns/02-Two-Pointers/) | ⭐⭐ Medium | 🔥 Critical | 15 |
| 3 | [Sliding Window](./Patterns/03-Sliding-Window/) | ⭐⭐ Medium | 🔥 Critical | 20 |
| 4 | [Stack](./Patterns/04-Stack/) | ⭐⭐ Medium | 🔥 Critical | 12 |
| 5 | [Binary Search](./Patterns/05-Binary-Search/) | ⭐⭐⭐ Hard | 🔥 Critical | 15 |

**Time Commitment**: 4 weeks, 2-3 hours/day

---

### **Tier 2: Data Structures** (Weeks 5-8)

| # | Pattern | Difficulty | Priority | Problems |
|---|---------|------------|----------|----------|
| 6 | [Linked List](./Patterns/06-Linked-List/) | ⭐⭐ Medium | High | 12 |
| 7 | [Trees](./Patterns/07-Trees/) | ⭐⭐⭐ Hard | 🔥 Critical | 20 |
| 8 | [Tries](./Patterns/08-Tries/) | ⭐⭐⭐ Hard | Medium | 8 |
| 9 | [Heap / Priority Queue](./Patterns/09-Heap-PriorityQueue/) | ⭐⭐⭐ Hard | High | 12 |

**Time Commitment**: 4 weeks, 2-3 hours/day

---

### **Tier 3: Advanced Techniques** (Weeks 9-12)

| # | Pattern | Difficulty | Priority | Problems |
|---|---------|------------|----------|----------|
| 10 | [Backtracking](./Patterns/10-Backtracking/) | ⭐⭐⭐ Hard | High | 15 |
| 11 | [Graphs](./Patterns/11-Graphs/) | ⭐⭐⭐ Hard | 🔥 Critical | 18 |
| 12 | [Advanced Graphs](./Patterns/12-Advanced-Graphs/) | ⭐⭐⭐⭐ Very Hard | Medium | 10 |
| 13 | [1D Dynamic Programming](./Patterns/13-1D-Dynamic-Programming/) | ⭐⭐⭐⭐ Very Hard | 🔥 Critical | 15 |
| 14 | [2D Dynamic Programming](./Patterns/14-2D-Dynamic-Programming/) | ⭐⭐⭐⭐ Very Hard | High | 12 |

**Time Commitment**: 4 weeks, 3-4 hours/day

---

### **Tier 4: Specialized Patterns** (Weeks 13-16)

| # | Pattern | Difficulty | Priority | Problems |
|---|---------|------------|----------|----------|
| 15 | [Greedy](./Patterns/15-Greedy/) | ⭐⭐⭐ Hard | Medium | 10 |
| 16 | [Intervals](./Patterns/16-Intervals/) | ⭐⭐⭐ Hard | High | 10 |
| 17 | [Math & Geometry](./Patterns/17-Math-and-Geometry/) | ⭐⭐⭐ Hard | Low | 8 |
| 18 | [Bit Manipulation](./Patterns/18-Bit-Manipulation/) | ⭐⭐⭐ Hard | Low | 8 |

**Time Commitment**: 4 weeks, 2-3 hours/day

---

## 🎯 Learning Path

### **Path 1: Speed Run (8 Weeks) - For Urgent Interviews**

Master the most common patterns:

**Weeks 1-2**: Arrays & Hashing, Two Pointers
**Weeks 3-4**: Sliding Window, Stack, Binary Search
**Weeks 5-6**: Trees, Linked List, Heap
**Weeks 7-8**: Graphs, 1D DP, Backtracking

**Result**: Cover ~70% of interview problems

---

### **Path 2: Complete Mastery (16 Weeks) - Comprehensive Preparation**

**Weeks 1-4**: Tier 1 (Fundamentals)
**Weeks 5-8**: Tier 2 (Data Structures)
**Weeks 9-12**: Tier 3 (Advanced)
**Weeks 13-16**: Tier 4 (Specialized)

**Result**: Cover ~95% of interview problems

---

### **Path 3: FAANG Level (24 Weeks) - Top Company Preparation**

Follow Path 2 + add:

**Weeks 17-20**: Advanced problems from each pattern
**Weeks 21-22**: System design problems with DSA
**Weeks 23-24**: Mock interviews and hard problems

**Result**: Ready for Google, Meta, Amazon, etc.

---

## 🔍 Pattern Recognition - Quick Decision Tree

### Step 1: Identify Data Structure

```
Array/String Problem?
├─ Need subarray/substring? → Sliding Window or Two Pointers
├─ Need all subarrays? → Prefix Sum or DP
├─ Need frequency/count? → Hash Map
└─ Sorted array? → Binary Search or Two Pointers

Tree Problem?
├─ Level by level? → BFS
├─ Path-related? → DFS/Backtracking
└─ BST property? → In-order traversal

Graph Problem?
├─ Shortest path? → BFS or Dijkstra
├─ Connected components? → DFS or Union-Find
└─ All paths/combinations? → Backtracking

Sequence/Optimization?
├─ Overlapping subproblems? → Dynamic Programming
├─ Greedy choice? → Greedy
└─ Constraints satisfaction? → Backtracking
```

### Step 2: Trigger Words Dictionary

| Trigger Words | Likely Pattern |
|---------------|----------------|
| "subarray sum", "substring" | Sliding Window, Prefix Sum |
| "sorted array", "two elements sum to" | Two Pointers, Binary Search |
| "frequency", "anagram", "duplicate" | Hash Map |
| "next greater", "valid parentheses" | Stack |
| "top k", "kth largest/smallest" | Heap |
| "tree path", "tree traversal" | DFS/BFS on Trees |
| "shortest path", "connected components" | BFS/DFS on Graphs |
| "permutations", "combinations", "subsets" | Backtracking |
| "minimum/maximum", "overlapping sub-problems" | Dynamic Programming |
| "intervals", "merge", "overlap" | Intervals |

---

## 📊 Problem Difficulty System

Each problem is rated on multiple dimensions:

### Difficulty Levels:

| Level | LeetCode | Description | Example |
|-------|----------|-------------|---------|
| 🟢 Easy | Easy | Basic pattern application | Two Sum |
| 🟡 Medium | Medium | Pattern + edge cases | Longest Substring Without Repeating |
| 🔴 Hard | Hard | Multiple patterns or advanced | Median of Two Sorted Arrays |
| ⚫ Expert | Hard+ | FAANG-level complexity | Alien Dictionary |

### Frequency Tags:

- 🔥🔥🔥 **Very High** - Asked in 50%+ of interviews
- 🔥🔥 **High** - Asked in 30-50% of interviews
- 🔥 **Medium** - Asked in 10-30% of interviews
- ⚪ **Low** - Asked in <10% of interviews

### Company Tags:

Common company indicators: `[G]` Google, `[F]` Meta, `[A]` Amazon, `[M]` Microsoft, `[N]` Netflix, `[AP]` Apple

---

## 📅 Daily Practice Routine

### Optimal Practice Schedule:

**Daily (2-3 hours):**
1. **15 min**: Review pattern template
2. **60-90 min**: Solve 2-3 problems (1 Easy, 1 Medium, 1 Hard)
3. **30 min**: Review solutions, note mistakes
4. **15 min**: Spaced repetition - redo old problems

**Weekly Review:**
- Saturday: Review all patterns learned this week
- Sunday: Solve 5 random problems mixing all patterns

---

## 🎯 Success Metrics

### After Each Pattern:

- [ ] Can explain pattern in own words
- [ ] Recognize pattern from problem description
- [ ] Code template from memory in <5 minutes
- [ ] Solved 70%+ of Easy problems
- [ ] Solved 50%+ of Medium problems
- [ ] Solved 30%+ of Hard problems
- [ ] Can teach pattern to someone else

### After Completion:

- [ ] 150+ problems solved across all patterns
- [ ] Can solve 80%+ of Easy in <15 min
- [ ] Can solve 60%+ of Medium in <30 min
- [ ] Can solve 30%+ of Hard in <45 min
- [ ] Completed 10+ mock interviews

---

## 🛠️ Tools & Resources

### Practice Platforms:
- **LeetCode** - Main platform (Premium recommended)
- **NeetCode** - Pattern-based organization
- **AlgoExpert** - Video explanations
- **HackerRank** - Company-specific tracks

### Visualization:
- **VisuAlgo** - Algorithm visualizations
- **Algorithm Visualizer** - Interactive demos

### Study Groups:
- LeetCode Discuss
- Reddit r/leetcode
- Discord coding servers

---

## 💡 Pro Tips

### For Beginners:
1. Start with Easy problems - build confidence
2. Understand the pattern before memorizing code
3. Solve same problem in multiple languages
4. Don't look at solution for 30+ minutes

### For Intermediate:
1. Time yourself - aim for interview speed
2. Practice explaining solution out loud
3. Focus on edge cases and optimization
4. Review old problems weekly

### For Advanced:
1. Solve variations of same problem
2. Optimize for time AND space
3. Practice on whiteboard
4. Do mock interviews weekly

---

## 🚨 Common Mistakes to Avoid

1. ❌ **Tutorial Hell** - Watching solutions without trying
2. ❌ **Random Solving** - Solving without pattern focus
3. ❌ **Memorization** - Memorizing code without understanding
4. ❌ **Skipping Easy** - Jumping to Hard too quickly
5. ❌ **No Review** - Not revisiting solved problems
6. ❌ **Solo Study** - Not discussing with others
7. ❌ **Ignoring Edge Cases** - Not testing thoroughly
8. ❌ **Time Pressure** - Not practicing timed solving

---

## 📈 Progress Tracking

Create a spreadsheet with:
- Pattern Name
- Problem Number & Name
- Difficulty
- Date First Attempted
- Date Solved
- Review Dates
- Time Taken
- Notes on Mistakes

---

## 🎬 Next Steps

1. **Choose your path** (Speed Run, Complete, or FAANG)
2. **Start with Pattern 1**: [Arrays & Hashing](./Patterns/01-Arrays-and-Hashing/)
3. **Set up tracking** (spreadsheet or Notion)
4. **Join community** (LeetCode Discuss, Reddit)
5. **Schedule daily practice** (consistency > intensity)

---

**Remember**: Pattern recognition is a skill that improves with practice. Don't get discouraged - every expert was once a beginner!

---

[⬅️ Back to DSA](./README.md)
