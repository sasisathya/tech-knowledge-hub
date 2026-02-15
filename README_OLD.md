# 📚 Data Structures & Algorithms Documentation

<p align="center">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/Algorithms-4CAF50?style=for-the-badge&logo=algorithm&logoColor=white" alt="Algorithms" />
  <img src="https://img.shields.io/badge/Data_Structures-FF6B6B?style=for-the-badge&logo=databricks&logoColor=white" alt="Data Structures" />
</p>

<p align="center">
  <img src="https://img.shields.io/github/stars/sasisathya/dsa_doc?style=social" alt="Stars" />
  <img src="https://img.shields.io/github/forks/sasisathya/dsa_doc?style=social" alt="Forks" />
</p>

## 🎯 Overview

Comprehensive documentation and implementation guide for **Data Structures, Algorithms, MongoDB Design Patterns,** and **Microservices Architecture** - all in JavaScript. This repository serves as a learning resource for developers preparing for technical interviews, studying computer science fundamentals, or building scalable applications.

## ✨ What's Inside

- 📖 **Data Structures** - Complete guide with code examples
- 🧮 **Algorithms** - Problem-solving techniques and implementations
- 🍃 **MongoDB Design Patterns** - Best practices for NoSQL databases
- 🏗️ **Microservices Patterns** - Architecture and design principles
- 💡 **Real-world Examples** - Practical applications of concepts
- 🎓 **Interview Prep** - Common questions with detailed solutions

## 🚀 Quick Links

- [Array](https://github.com/sasisathya/dsa_doc?tab=readme-ov-file#array)
- [Linked List](#linked-list)
- [Stack](#stack)
- [Queue](#queue)
- [Tree](#tree)
- [Graph](#graph)
- [Hash Table](#hash-table)
- [Heap](#heap)
- [Trie](#trie)
- [MongoDB Design Patterns](https://github.com/sasisathya/dsa_doc/tree/main/mongodb#readme)
- [Microservices Design Patterns](https://github.com/sasisathya/dsa_doc/tree/main/Design%20Patterns)

---



Here is the documentation for the Data Structures and Algorithms in JavaScript, with answers and code examples:

**Table of Contents**

1. [Array](#array)
2. [Linked List](#linked-list)
3. [Stack](#stack)
4. [Queue](#queue)
5. [Tree](#tree)
6. [Graph](#graph)
7. [Hash Table](#hash-table)
8. [Heap](#heap)
9. [Trie](#trie) 

**Array**
================

### Description

An array is a collection of elements of the same data type stored in contiguous memory locations.

### Sequence

1. **Basic Operations**
	* Accessing an element
	* Updating an element
	* Inserting an element
	* Deleting an element
2. **Searching**
	* Linear Search
	* Binary Search
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

### Questions

1. Find the maximum element in an array.
2. Find the minimum element in an array.
3. Search for an element in an array using linear search.
4. Search for an element in an array using binary search.
5. Sort an array using bubble sort.
6. Sort an array using selection sort.
7. Sort an array using insertion sort.
8. Sort an array using merge sort.
9. Sort an array using quick sort.
10. Find the first duplicate element in an array.
11. Find the first missing positive integer in an array.
12. Find the maximum sum subarray in an array.
13. Find the minimum sum subarray in an array.
14. Find the maximum length subarray with equal number of 0s and 1s.
15. Find the minimum length subarray with equal number of 0s and 1s.
16. Find the maximum frequency element in an array.
17. Find the minimum frequency element in an array.
18. Find the maximum sum of a subarray with a given size.
19. Find the minimum sum of a subarray with a given size.
20. Find the maximum product of a subarray with a given size.

### Answers

1. Find the maximum element in an array:
```javascript
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}
```
2. Find the minimum element in an array:
```javascript
function findMin(arr) {
  let min = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < min) {
      min = arr[i];
    }
  }
  return min;
}
```
3. Search for an element in an array using linear search:
```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}
```
4. Search for an element in an array using binary search:
```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  while (left <= right) {
    let mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return -1;
}
```
5. Sort an array using bubble sort:
       Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order.
```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```
6. Sort an array using selection sort:
      Selection Sort is a comparison-based sorting algorithm. It sorts an array by repeatedly selecting the smallest (or largest) element from the unsorted portion.
```javascript
function selectionSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
      }
    }
    let temp = arr[i];
    arr[i] = arr[min];
    arr[min] = temp;
  }
  return arr;
}
```
7. Sort an array using insertion sort:
       Insertion sort is a simple sorting algorithm that works by iteratively inserting each element of an unsorted list into its correct position in a sorted portion
```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let key = arr[i];
    let j = i - 1;
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
  return arr;
}
```
8. Sort an array using merge sort:
```javascript
function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  let mid = Math.floor(arr.length / 2);
  let left = arr.slice(0, mid);
  let right = arr.slice(mid);
  left = mergeSort(left);
  right = mergeSort(right);
  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  while (left.length > 0 && right.length > 0) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  return result.concat(left).concat(right);
}
```
9. Sort an array using quick sort:
```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  let pivot = arr[0];
  let less = [];
  let greater = [];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] <= pivot) {
      less.push(arr[i]);
    } else {
      greater.push(arr[i]);
    }
  }
  return quickSort(less).concat(pivot, quickSort(greater));
}
```


Here is the rest of the documentation:

**10. Find the first duplicate element in an array:**
```javascript
function findFirstDuplicate(arr) {
  let seen = {};
  for (let i = 0; i < arr.length; i++) {
    if (seen[arr[i]]) {
      return arr[i];
    }
    seen[arr[i]] = true;
  }
  return null;
}
```
**11. Find the first missing positive integer in an array:**
```javascript
function findFirstMissingPositive(arr) {
  let set = new Set(arr);
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**12. Find the maximum sum subarray in an array:**
```javascript
function findMaxSumSubarray(arr) {
  let max = arr[0];
  let sum = arr[0];
  for (let i = 1; i < arr.length; i++) {
    sum = Math.max(arr[i], sum + arr[i]);
    max = Math.max(max, sum);
  }
  return max;
}
```
**13. Find the minimum sum subarray in an array:**
```javascript
function findMinSumSubarray(arr) {
  let min = arr[0];
  let sum = arr[0];
  for (let i = 1; i < arr.length; i++) {
    sum = Math.min(arr[i], sum + arr[i]);
    min = Math.min(min, sum);
  }
  return min;
}
```
**14. Find the maximum length subarray with equal number of 0s and 1s:**
```javascript
function findMaxLengthSubarray(arr) {
  let max = 0;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i] === 0 ? -1 : 1;
    if (map.has(sum)) {
      max = Math.max(max, i - map.get(sum));
    } else {
      map.set(sum, i);
    }
  }
  return max;
}
```
**15. Find the minimum length subarray with equal number of 0s and 1s:**
```javascript
function findMinLengthSubarray(arr) {
  let min = arr.length;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i] === 0 ? -1 : 1;
    if (map.has(sum)) {
      min = Math.min(min, i - map.get(sum));
    } else {
      map.set(sum, i);
    }
  }
  return min;
}
```
**16. Find the maximum frequency element in an array:**
```javascript
function findMaxFrequencyElement(arr) {
  let max = 0;
  let map = new Map();
  for (let i = 0; i < arr.length; i++) {
    map.set(arr[i], (map.get(arr[i]) || 0) + 1);
    max = Math.max(max, map.get(arr[i]));
  }
  return max;
}
```
**17. Find the minimum frequency element in an array:**
```javascript
function findMinFrequencyElement(arr) {
  let min = arr.length;
  let map = new Map();
  for (let i = 0; i < arr.length; i++) {
    map.set(arr[i], (map.get(arr[i]) || 0) + 1);
    min = Math.min(min, map.get(arr[i]));
  }
  return min;
}
```
**18. Find the maximum sum of a subarray with a given size:**
```javascript
function findMaxSumSubarrayOfSize(arr, size) {
  let max = 0;
  let sum = 0;
  for (let i = 0; i < size; i++) {
    sum += arr[i];
  }
  max = sum;
  for (let i = size; i < arr.length; i++) {
    sum = sum - arr[i - size] + arr[i];
    max = Math.max(max, sum);
  }
  return max;
}
```
**19. Find the minimum sum of a subarray with a given size:**
```javascript
function findMinSumSubarrayOfSize(arr, size) {
  let min = 0;
  let sum = 0;
  for (let i = 0; i < size; i++) {
    sum += arr[i];
  }
  min = sum;
  for (let i = size; i < arr.length; i++) {
    sum = sum - arr[i - size] + arr[i];
    min = Math.min(min, sum);
  }
  return min;
}
```
**20. Find the maximum product of a subarray with a given size:**
```javascript
function findMaxProductSubarrayOfSize(arr, size) {
  let max = 0;
  let product = 1;
  for (let i = 0; i < size; i++) {
    product *= arr[i];
  }
  max = product;
  for (let i = size; i < arr.length; i++) {
    product = product / arr[i - size] * arr[i];
    max = Math.max(max, product);
  }
  return max;
}
```

Here is the rest of the documentation:

**Linked List**
================

### Description

A linked list is a dynamic collection of elements, where each element points to the next element.

### Sequence

1. **Basic Operations**
	* Insertion
	* Deletion
	* Traversal
2. **Searching**
	* Linear Search
	* Binary Search
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

### Questions

1. Insert a node at the beginning of a linked list.
2. Insert a node at the end of a linked list.
3. Delete a node from a linked list.
4. Traverse a linked list.
5. Search for a node in a linked list using linear search.
6. Search for a node in a linked list using binary search.
7. Sort a linked list using bubble sort.
8. Sort a linked list using selection sort.
9. Sort a linked list using insertion sort.
10. Sort a linked list using merge sort.
11. Sort a linked list using quick sort.
12. Find the middle element of a linked list.
13. Find the nth node from the end of a linked list.
14. Find the first duplicate node in a linked list.
15. Find the first missing positive integer in a linked list.
16. Find the maximum sum subarray in a linked list.
17. Find the minimum sum subarray in a linked list.
18. Find the maximum length subarray with equal number of 0s and 1s in a linked list.
19. Find the minimum length subarray with equal number of 0s and 1s in a linked list.
20. Find the maximum frequency node in a linked list.

### Answers

1. Insert a node at the beginning of a linked list:
```javascript
function insertAtBeginning(head, data) {
  let newNode = new Node(data);
  newNode.next = head;
  return newNode;
}
```
2. Insert a node at the end of a linked list:
```javascript
function insertAtEnd(head, data) {
  let newNode = new Node(data);
  if (head === null) {
    return newNode;
  }
  let temp = head;
  while (temp.next !== null) {
    temp = temp.next;
  }
  temp.next = newNode;
  return head;
}
```
3. Delete a node from a linked list:
```javascript
function deleteNode(head, data) {
  if (head === null) {
    return null;
  }
  if (head.data === data) {
    return head.next;
  }
  let temp = head;
  while (temp.next !== null) {
    if (temp.next.data === data) {
      temp.next = temp.next.next;
      return head;
    }
    temp = temp.next;
  }
  return head;
}
```
4. Traverse a linked list:
```javascript
function traverse(head) {
  let temp = head;
  while (temp !== null) {
    console.log(temp.data);
    temp = temp.next;
  }
}
```
5. Search for a node in a linked list using linear search:
```javascript
function linearSearch(head, data) {
  let temp = head;
  while (temp !== null) {
    if (temp.data === data) {
      return true;
    }
    temp = temp.next;
  }
  return false;
}
```
6. Search for a node in a linked list using binary search:
```javascript
function binarySearch(head, data) {
  let low = 0;
  let high = length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let temp = head;
    for (let i = 0; i < mid; i++) {
      temp = temp.next;
    }
    if (temp.data === data) {
      return true;
    } else if (temp.data < data) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return false;
}
```
7. Sort a linked list using bubble sort:
```javascript
function bubbleSort(head) {
  let swapped = true;
  while (swapped) {
    swapped = false;
    let temp = head;
    while (temp.next !== null) {
      if (temp.data > temp.next.data) {
        let tempData = temp.data;
        temp.data = temp.next.data;
        temp.next.data = tempData;
        swapped = true;
      }
      temp = temp.next;
    }
  }
  return head;
}
```
8. Sort a linked list using selection sort:
```javascript
function selectionSort(head) {
  let temp = head;
  while (temp !== null) {
    let min = temp;
    let temp2 = temp.next;
    while (temp2 !== null) {
      if (temp2.data < min.data) {
        min = temp2;
      }
      temp2 = temp2.next;
    }
    let tempData = temp.data;
    temp.data = min.data;
    min.data = tempData;
    temp = temp.next;
  }
  return head;
}
```
9. Sort a linked list using insertion sort:
```javascript
function insertionSort(head) {
  let temp = head;
  while (temp !== null) {
    let key = temp.data;
    let temp2 = temp;
    while (temp2 !== null && temp2.data < key) {
      temp2 = temp2.next;
    }
    if (temp2 !== null) {
      let tempData = temp.data;
      temp.data = temp2.data;
      temp2.data = tempData;
    }
    temp = temp.next;
  }
  return head;
}
```




Here is the rest of the documentation:

**10. Sort a linked list using merge sort:**
```javascript
function mergeSort(head) {
  if (head === null || head.next === null) {
    return head;
  }
  let mid = getMiddle(head);
  let midNext = mid.next;
  mid.next = null;
  let left = mergeSort(head);
  let right = mergeSort(midNext);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}

function getMiddle(head) {
  let slow = head;
  let fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```
**11. Sort a linked list using quick sort:**
```javascript
function quickSort(head) {
  if (head === null || head.next === null) {
    return head;
  }
  let pivot = head.data;
  let left = new Node(0);
  let right = new Node(0);
  let leftHead = left;
  let rightHead = right;
  let temp = head.next;
  while (temp !== null) {
    if (temp.data < pivot) {
      left.next = temp;
      left = left.next;
    } else {
      right.next = temp;
      right = right.next;
    }
    temp = temp.next;
  }
  left.next = null;
  right.next = null;
  left = quickSort(leftHead.next);
  right = quickSort(rightHead.next);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}
```
**12. Find the middle element of a linked list:**
```javascript
function findMiddle(head) {
  let slow = head;
  let fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow.data;
}
```
**13. Find the nth node from the end of a linked list:**
```javascript
function findNthFromEnd(head, n) {
  let main = head;
  let ref = head;
  for (let i = 0; i < n; i++) {
    ref = ref.next;
  }
  while (ref !== null) {
    main = main.next;
    ref = ref.next;
  }
  return main.data;
}
```
**14. Find the first duplicate node in a linked list:**
```javascript
function findFirstDuplicate(head) {
  let set = new Set();
  let temp = head;
  while (temp !== null) {
    if (set.has(temp.data)) {
      return temp.data;
    }
    set.add(temp.data);
    temp = temp.next;
  }
  return null;
}
```
**15. Find the first missing positive integer in a linked list:**
```javascript
function findFirstMissingPositive(head) {
  let set = new Set();
  let temp = head;
  while (temp !== null) {
    set.add(temp.data);
    temp = temp.next;
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**16. Find the maximum sum subarray in a linked list:**
```javascript
function findMaxSumSubarray(head) {
  let max = head.data;
  let sum = head.data;
  let temp = head.next;
  while (temp !== null) {
    sum = Math.max(temp.data, sum + temp.data);
    max = Math.max(max, sum);
    temp = temp.next;
  }
  return max;
}
```
**17. Find the minimum sum subarray in a linked list:**
```javascript
function findMinSumSubarray(head) {
  let min = head.data;
  let sum = head.data;
  let temp = head.next;
  while (temp !== null) {
    sum = Math.min(temp.data, sum + temp.data);
    min = Math.min(min, sum);
    temp = temp.next;
  }
  return min;
}
```
**18. Find the maximum length subarray with equal number of 0s and 1s in a linked list:**
```javascript
function findMaxLengthSubarray(head) {
  let max = 0;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  let temp = head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      max = Math.max(max, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return max;
}
```




Here is the rest of the documentation:

**19. Find the minimum length subarray with equal number of 0s and 1s in a linked list:**
```javascript
function findMinLengthSubarray(head) {
  let min = head.data;
  let sum = head.data;
  let map = new Map();
  map.set(0, -1);
  let temp = head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      min = Math.min(min, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return min;
}
```
**20. Find the maximum frequency node in a linked list:**
```javascript
function findMaxFrequencyNode(head) {
  let max = 0;
  let map = new Map();
  let temp = head;
  while (temp !== null) {
    if (map.has(temp.data)) {
      map.set(temp.data, map.get(temp.data) + 1);
    } else {
      map.set(temp.data, 1);
    }
    max = Math.max(max, map.get(temp.data));
    temp = temp.next;
  }
  return max;
}
```

**Stack**
================

A stack is a linear data structure that follows the LIFO (Last In First Out) principle. This means that the last element added to the stack will be the first one to be removed.

**Sequence**

1. **Basic Operations**
	* Push
	* Pop
	* Peek
2. **Searching**
	* Linear Search
	* Binary Search
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a stack using an array.
2. Implement a stack using a linked list.
3. Push an element onto the stack.
4. Pop an element from the stack.
5. Peek at the top element of the stack.
6. Search for an element in the stack using linear search.
7. Search for an element in the stack using binary search.
8. Sort the stack using bubble sort.
9. Sort the stack using selection sort.
10. Sort the stack using insertion sort.
11. Sort the stack using merge sort.
12. Sort the stack using quick sort.
13. Find the maximum element in the stack.
14. Find the minimum element in the stack.
15. Find the first duplicate element in the stack.
16. Find the first missing positive integer in the stack.
17. Find the maximum sum subarray in the stack.
18. Find the minimum sum subarray in the stack.
19. Find the maximum length subarray with equal number of 0s and 1s in the stack.
20. Find the minimum length subarray with equal number of 0s and 1s in the stack.

**Answers**

1. Implement a stack using an array:
```javascript
class Stack {
  constructor() {
    this.array = [];
  }

  push(element) {
    this.array.push(element);
  }

  pop() {
    return this.array.pop();
  }

  peek() {
    return this.array[this.array.length - 1];
  }
}
```
2. Implement a stack using a linked list:
```javascript
class Stack {
  constructor() {
    this.head = null;
  }

  push(element) {
    let newNode = new Node(element);
    newNode.next = this.head;
    this.head = newNode;
  }

  pop() {
    let temp = this.head;
    this.head = this.head.next;
    return temp.data;
  }

  peek() {
    return this.head.data;
  }
}

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```
3. Push an element onto the stack:
```javascript
stack.push(element);
```
4. Pop an element from the stack:
```javascript
stack.pop();
```
5. Peek at the top element of the stack:
```javascript
stack.peek();
```
6. Search for an element in the stack using linear search:
```javascript
function linearSearch(stack, element) {
  let temp = stack.head;
  while (temp !== null) {
    if (temp.data === element) {
      return true;
    }
    temp = temp.next;
  }
  return false;
}
```
7. Search for an element in the stack using binary search:
```javascript
function binarySearch(stack, element) {
  let low = 0;
  let high = stack.array.length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (stack.array[mid] === element) {
      return true;
    } else if (stack.array[mid] < element) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return false;
}
```
8. Sort the stack using bubble sort:
```javascript
function bubbleSort(stack) {
  let swapped = true;
  while (swapped) {
    swapped = false;
    let temp = stack.head;
    while (temp.next !== null) {
      if (temp.data > temp.next.data) {
        let tempData = temp.data;
        temp.data = temp.next.data;
        temp.next.data = tempData;
        swapped = true;
      }
      temp = temp.next;
    }
  }
}
```

**9. Sort the stack using selection sort:**
```javascript
function selectionSort(stack) {
  let temp = stack.head;
  while (temp !== null) {
    let min = temp;
    let temp2 = temp.next;
    while (temp2 !== null) {
      if (temp2.data < min.data) {
        min = temp2;
      }
      temp2 = temp2.next;
    }
    let tempData = temp.data;
    temp.data = min.data;
    min.data = tempData;
    temp = temp.next;
  }
}
```
**10. Sort the stack using insertion sort:**
```javascript
function insertionSort(stack) {
  let temp = stack.head;
  while (temp !== null) {
    let key = temp.data;
    let temp2 = temp;
    while (temp2 !== null && temp2.data < key) {
      temp2 = temp2.next;
    }
    if (temp2 !== null) {
      let tempData = temp.data;
      temp.data = temp2.data;
      temp2.data = tempData;
    }
    temp = temp.next;
  }
}
```
**11. Sort the stack using merge sort:**
```javascript
function mergeSort(stack) {
  if (stack.head === null || stack.head.next === null) {
    return stack;
  }
  let mid = getMiddle(stack.head);
  let midNext = mid.next;
  mid.next = null;
  let left = mergeSort(stack);
  let right = mergeSort(midNext);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}

function getMiddle(head) {
  let slow = head;
  let fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```
**12. Sort the stack using quick sort:**
```javascript
function quickSort(stack) {
  if (stack.head === null || stack.head.next === null) {
    return stack;
  }
  let pivot = stack.head.data;
  let left = new Node(0);
  let right = new Node(0);
  let leftHead = left;
  let rightHead = right;
  let temp = stack.head.next;
  while (temp !== null) {
    if (temp.data < pivot) {
      left.next = temp;
      left = left.next;
    } else {
      right.next = temp;
      right = right.next;
    }
    temp = temp.next;
  }
  left.next = null;
  right.next = null;
  left = quickSort(leftHead.next);
  right = quickSort(rightHead.next);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}
```
**13. Find the maximum element in the stack:**
```javascript
function findMax(stack) {
  let max = stack.head.data;
  let temp = stack.head.next;
  while (temp !== null) {
    if (temp.data > max) {
      max = temp.data;
    }
    temp = temp.next;
  }
  return max;
}
```
**14. Find the minimum element in the stack:**
```javascript
function findMin(stack) {
  let min = stack.head.data;
  let temp = stack.head.next;
  while (temp !== null) {
    if (temp.data < min) {
      min = temp.data;
    }
    temp = temp.next;
  }
  return min;
}
```
**15. Find the first duplicate element in the stack:**
```javascript
function findFirstDuplicate(stack) {
  let set = new Set();
  let temp = stack.head;
  while (temp !== null) {
    if (set.has(temp.data)) {
      return temp.data;
    }
    set.add(temp.data);
    temp = temp.next;
  }
  return null;
}
```
**16. Find the first missing positive integer in the stack:**
```javascript
function findFirstMissingPositive(stack) {
  let set = new Set();
  let temp = stack.head;
  while (temp !== null) {
    set.add(temp.data);
    temp = temp.next;
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```

**17. Find the maximum sum subarray in the stack:**
```javascript
function findMaxSumSubarray(stack) {
  let max = stack.head.data;
  let sum = stack.head.data;
  let temp = stack.head.next;
  while (temp !== null) {
    sum = Math.max(temp.data, sum + temp.data);
    max = Math.max(max, sum);
    temp = temp.next;
  }
  return max;
}
```
**18. Find the minimum sum subarray in the stack:**
```javascript
function findMinSumSubarray(stack) {
  let min = stack.head.data;
  let sum = stack.head.data;
  let temp = stack.head.next;
  while (temp !== null) {
    sum = Math.min(temp.data, sum + temp.data);
    min = Math.min(min, sum);
    temp = temp.next;
  }
  return min;
}
```
**19. Find the maximum length subarray with equal number of 0s and 1s in the stack:**
```javascript
function findMaxLengthSubarray(stack) {
  let max = 0;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  let temp = stack.head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      max = Math.max(max, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return max;
}
```
**20. Find the minimum length subarray with equal number of 0s and 1s in the stack:**
```javascript
function findMinLengthSubarray(stack) {
  let min = stack.head.data;
  let sum = stack.head.data;
  let map = new Map();
  map.set(0, -1);
  let temp = stack.head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      min = Math.min(min, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return min;
}
```

**Queue**
================

A queue is a linear data structure that follows the FIFO (First In First Out) principle. This means that the first element added to the queue will be the first one to be removed.

**Sequence**

1. **Basic Operations**
	* Enqueue
	* Dequeue
	* Peek
2. **Searching**
	* Linear Search
	* Binary Search
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a queue using an array.
2. Implement a queue using a linked list.
3. Enqueue an element into the queue.
4. Dequeue an element from the queue.
5. Peek at the front element of the queue.
6. Search for an element in the queue using linear search.
7. Search for an element in the queue using binary search.
8. Sort the queue using bubble sort.
9. Sort the queue using selection sort.
10. Sort the queue using insertion sort.
11. Sort the queue using merge sort.
12. Sort the queue using quick sort.
13. Find the maximum element in the queue.
14. Find the minimum element in the queue.
15. Find the first duplicate element in the queue.
16. Find the first missing positive integer in the queue.
17. Find the maximum sum subarray in the queue.
18. Find the minimum sum subarray in the queue.
19. Find the maximum length subarray with equal number of 0s and 1s in the queue.
20. Find the minimum length subarray with equal number of 0s and 1s in the queue.

**Answers**

1. Implement a queue using an array:
```javascript
class Queue {
  constructor() {
    this.array = [];
  }

  enqueue(element) {
    this.array.push(element);
  }

  dequeue() {
    return this.array.shift();
  }

  peek() {
    return this.array[0];
  }
}
```
2. Implement a queue using a linked list:
```javascript
class Queue {
  constructor() {
    this.head = null;
  }

  enqueue(element) {
    let newNode = new Node(element);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let temp = this.head;
      while (temp.next !== null) {
        temp = temp.next;
      }
      temp.next = newNode;
    }
  }

  dequeue() {
    if (this.head === null) {
      return null;
    }
    let temp = this.head;
    this.head = this.head.next;
    return temp.data;
  }

  peek() {
    return this.head.data;
  }
}

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```
3. Enqueue an element into the queue:
```javascript
queue.enqueue(element);
```
4. Dequeue an element from the queue:
```javascript
queue.dequeue();
```
5. Peek at the front element of the queue:
```javascript
queue.peek();
```
6. Search for an element in the queue using linear search:
```javascript
function linearSearch(queue, element) {
  let temp = queue.head;
  while (temp !== null) {
    if (temp.data === element) {
      return true;
    }
    temp = temp.next;
  }
  return false;
}
```

**7. Search for an element in the queue using binary search:**
```javascript
function binarySearch(queue, element) {
  let low = 0;
  let high = queue.array.length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (queue.array[mid] === element) {
      return true;
    } else if (queue.array[mid] < element) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return false;
}
```
**8. Sort the queue using bubble sort:**
```javascript
function bubbleSort(queue) {
  let swapped = true;
  while (swapped) {
    swapped = false;
    let temp = queue.head;
    while (temp.next !== null) {
      if (temp.data > temp.next.data) {
        let tempData = temp.data;
        temp.data = temp.next.data;
        temp.next.data = tempData;
        swapped = true;
      }
      temp = temp.next;
    }
  }
}
```
**9. Sort the queue using selection sort:**
```javascript
function selectionSort(queue) {
  let temp = queue.head;
  while (temp !== null) {
    let min = temp;
    let temp2 = temp.next;
    while (temp2 !== null) {
      if (temp2.data < min.data) {
        min = temp2;
      }
      temp2 = temp2.next;
    }
    let tempData = temp.data;
    temp.data = min.data;
    min.data = tempData;
    temp = temp.next;
  }
}
```
**10. Sort the queue using insertion sort:**
```javascript
function insertionSort(queue) {
  let temp = queue.head;
  while (temp !== null) {
    let key = temp.data;
    let temp2 = temp;
    while (temp2 !== null && temp2.data < key) {
      temp2 = temp2.next;
    }
    if (temp2 !== null) {
      let tempData = temp.data;
      temp.data = temp2.data;
      temp2.data = tempData;
    }
    temp = temp.next;
  }
}
```
**11. Sort the queue using merge sort:**
```javascript
function mergeSort(queue) {
  if (queue.head === null || queue.head.next === null) {
    return queue;
  }
  let mid = getMiddle(queue.head);
  let midNext = mid.next;
  mid.next = null;
  let left = mergeSort(queue);
  let right = mergeSort(midNext);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}

function getMiddle(head) {
  let slow = head;
  let fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```
**12. Sort the queue using quick sort:**
```javascript
function quickSort(queue) {
  if (queue.head === null || queue.head.next === null) {
    return queue;
  }
  let pivot = queue.head.data;
  let left = new Node(0);
  let right = new Node(0);
  let leftHead = left;
  let rightHead = right;
  let temp = queue.head.next;
  while (temp !== null) {
    if (temp.data < pivot) {
      left.next = temp;
      left = left.next;
    } else {
      right.next = temp;
      right = right.next;
    }
    temp = temp.next;
  }
  left.next = null;
  right.next = null;
  left = quickSort(leftHead.next);
  right = quickSort(rightHead.next);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}
```
**13. Find the maximum element in the queue:**
```javascript
function findMax(queue) {
  let max = queue.head.data;
  let temp = queue.head.next;
  while (temp !== null) {
    if (temp.data > max) {
      max = temp.data;
    }
    temp = temp.next;
  }
  return max;
}
```
**14. Find the minimum element in the queue:**
```javascript
function findMin(queue) {
  let min = queue.head.data;
  let temp = queue.head.next;
  while (temp !== null) {
    if (temp.data < min) {
      min = temp.data;
    }
    temp = temp.next;
  }
  return min;
}
```

**15. Find the first duplicate element in the queue:**
```javascript
function findFirstDuplicate(queue) {
  let set = new Set();
  let temp = queue.head;
  while (temp !== null) {
    if (set.has(temp.data)) {
      return temp.data;
    }
    set.add(temp.data);
    temp = temp.next;
  }
  return null;
}
```
**16. Find the first missing positive integer in the queue:**
```javascript
function findFirstMissingPositive(queue) {
  let set = new Set();
  let temp = queue.head;
  while (temp !== null) {
    set.add(temp.data);
    temp = temp.next;
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**17. Find the maximum sum subarray in the queue:**
```javascript
function findMaxSumSubarray(queue) {
  let max = queue.head.data;
  let sum = queue.head.data;
  let temp = queue.head.next;
  while (temp !== null) {
    sum = Math.max(temp.data, sum + temp.data);
    max = Math.max(max, sum);
    temp = temp.next;
  }
  return max;
}
```
**18. Find the minimum sum subarray in the queue:**
```javascript
function findMinSumSubarray(queue) {
  let min = queue.head.data;
  let sum = queue.head.data;
  let temp = queue.head.next;
  while (temp !== null) {
    sum = Math.min(temp.data, sum + temp.data);
    min = Math.min(min, sum);
    temp = temp.next;
  }
  return min;
}
```
**19. Find the maximum length subarray with equal number of 0s and 1s in the queue:**
```javascript
function findMaxLengthSubarray(queue) {
  let max = 0;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  let temp = queue.head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      max = Math.max(max, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return max;
}
```
**20. Find the minimum length subarray with equal number of 0s and 1s in the queue:**
```javascript
function findMinLengthSubarray(queue) {
  let min = queue.head.data;
  let sum = queue.head.data;
  let map = new Map();
  map.set(0, -1);
  let temp = queue.head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      min = Math.min(min, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return min;
}
```

**Tree**
================

A tree is a data structure that consists of nodes, where each node has a value and zero or more child nodes.

**Sequence**

1. **Basic Operations**
	* Insert
	* Delete
	* Search
2. **Traversal**
	* In-order
	* Pre-order
	* Post-order
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a tree using an array.
2. Implement a tree using a linked list.
3. Insert a node into the tree.
4. Delete a node from the tree.
5. Search for a node in the tree.
6. Traverse the tree using in-order traversal.
7. Traverse the tree using pre-order traversal.
8. Traverse the tree using post-order traversal.
9. Sort the tree using bubble sort.
10. Sort the tree using selection sort.
11. Sort the tree using insertion sort.
12. Sort the tree using merge sort.
13. Sort the tree using quick sort.
14. Find the maximum element in the tree.
15. Find the minimum element in the tree.
16. Find the first duplicate element in the tree.
17. Find the first missing positive integer in the tree.
18. Find the maximum sum subarray in the tree.
19. Find the minimum sum subarray in the tree.
20. Find the maximum length subarray with equal number of 0s and 1s in the tree.

**Answers**

1. Implement a tree using an array:
```javascript
class Tree {
  constructor() {
    this.array = [];
  }

  insert(element) {
    this.array.push(element);
  }

  delete(element) {
    let index = this.array.indexOf(element);
    if (index !== -1) {
      this.array.splice(index, 1);
    }
  }

  search(element) {
    return this.array.includes(element);
  }
}
```






Here is the rest of the documentation:

**2. Implement a tree using a linked list:**
```javascript
class Tree {
  constructor() {
    this.head = null;
  }

  insert(element) {
    let newNode = new Node(element);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let temp = this.head;
      while (temp.next !== null) {
        temp = temp.next;
      }
      temp.next = newNode;
    }
  }

  delete(element) {
    if (this.head === null) {
      return;
    }
    if (this.head.data === element) {
      this.head = this.head.next;
    } else {
      let temp = this.head;
      while (temp.next !== null) {
        if (temp.next.data === element) {
          temp.next = temp.next.next;
          return;
        }
        temp = temp.next;
      }
    }
  }

  search(element) {
    let temp = this.head;
    while (temp !== null) {
      if (temp.data === element) {
        return true;
      }
      temp = temp.next;
    }
    return false;
  }
}

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```
**3. Insert a node into the tree:**
```javascript
tree.insert(element);
```
**4. Delete a node from the tree:**
```javascript
tree.delete(element);
```
**5. Search for a node in the tree:**
```javascript
tree.search(element);
```
**6. Traverse the tree using in-order traversal:**
```javascript
function inOrderTraversal(tree) {
  let temp = tree.head;
  while (temp !== null) {
    console.log(temp.data);
    temp = temp.next;
  }
}
```
**7. Traverse the tree using pre-order traversal:**
```javascript
function preOrderTraversal(tree) {
  let temp = tree.head;
  while (temp !== null) {
    console.log(temp.data);
    temp = temp.next;
  }
}
```
**8. Traverse the tree using post-order traversal:**
```javascript
function postOrderTraversal(tree) {
  let temp = tree.head;
  while (temp !== null) {
    console.log(temp.data);
    temp = temp.next;
  }
}
```
**9. Sort the tree using bubble sort:**
```javascript
function bubbleSort(tree) {
  let swapped = true;
  while (swapped) {
    swapped = false;
    let temp = tree.head;
    while (temp.next !== null) {
      if (temp.data > temp.next.data) {
        let tempData = temp.data;
        temp.data = temp.next.data;
        temp.next.data = tempData;
        swapped = true;
      }
      temp = temp.next;
    }
  }
}
```
**10. Sort the tree using selection sort:**
```javascript
function selectionSort(tree) {
  let temp = tree.head;
  while (temp !== null) {
    let min = temp;
    let temp2 = temp.next;
    while (temp2 !== null) {
      if (temp2.data < min.data) {
        min = temp2;
      }
      temp2 = temp2.next;
    }
    let tempData = temp.data;
    temp.data = min.data;
    min.data = tempData;
    temp = temp.next;
  }
}
```
**11. Sort the tree using insertion sort:**
```javascript
function insertionSort(tree) {
  let temp = tree.head;
  while (temp !== null) {
    let key = temp.data;
    let temp2 = temp;
    while (temp2 !== null && temp2.data < key) {
      temp2 = temp2.next;
    }
    if (temp2 !== null) {
      let tempData = temp.data;
      temp.data = temp2.data;
      temp2.data = tempData;
    }
    temp = temp.next;
  }
}
```
**12. Sort the tree using merge sort:**
```javascript
function mergeSort(tree) {
  if (tree.head === null || tree.head.next === null) {
    return tree;
  }
  let mid = getMiddle(tree.head);
  let midNext = mid.next;
  mid.next = null;
  let left = mergeSort(tree);
  let right = mergeSort(midNext);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}

function getMiddle(head) {
  let slow = head;
  let fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```






Here is the rest of the documentation:

**13. Sort the tree using quick sort:**
```javascript
function quickSort(tree) {
  if (tree.head === null || tree.head.next === null) {
    return tree;
  }
  let pivot = tree.head.data;
  let left = new Node(0);
  let right = new Node(0);
  let leftHead = left;
  let rightHead = right;
  let temp = tree.head.next;
  while (temp !== null) {
    if (temp.data < pivot) {
      left.next = temp;
      left = left.next;
    } else {
      right.next = temp;
      right = right.next;
    }
    temp = temp.next;
  }
  left.next = null;
  right.next = null;
  left = quickSort(leftHead.next);
  right = quickSort(rightHead.next);
  return merge(left, right);
}

function merge(left, right) {
  let dummy = new Node(0);
  let current = dummy;
  while (left !== null && right !== null) {
    if (left.data < right.data) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }
  if (left !== null) {
    current.next = left;
  } else {
    current.next = right;
  }
  return dummy.next;
}
```
**14. Find the maximum element in the tree:**
```javascript
function findMax(tree) {
  let max = tree.head.data;
  let temp = tree.head.next;
  while (temp !== null) {
    if (temp.data > max) {
      max = temp.data;
    }
    temp = temp.next;
  }
  return max;
}
```
**15. Find the minimum element in the tree:**
```javascript
function findMin(tree) {
  let min = tree.head.data;
  let temp = tree.head.next;
  while (temp !== null) {
    if (temp.data < min) {
      min = temp.data;
    }
    temp = temp.next;
  }
  return min;
}
```
**16. Find the first duplicate element in the tree:**
```javascript
function findFirstDuplicate(tree) {
  let set = new Set();
  let temp = tree.head;
  while (temp !== null) {
    if (set.has(temp.data)) {
      return temp.data;
    }
    set.add(temp.data);
    temp = temp.next;
  }
  return null;
}
```
**17. Find the first missing positive integer in the tree:**
```javascript
function findFirstMissingPositive(tree) {
  let set = new Set();
  let temp = tree.head;
  while (temp !== null) {
    set.add(temp.data);
    temp = temp.next;
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**18. Find the maximum sum subarray in the tree:**
```javascript
function findMaxSumSubarray(tree) {
  let max = tree.head.data;
  let sum = tree.head.data;
  let temp = tree.head.next;
  while (temp !== null) {
    sum = Math.max(temp.data, sum + temp.data);
    max = Math.max(max, sum);
    temp = temp.next;
  }
  return max;
}
```
**19. Find the minimum sum subarray in the tree:**
```javascript
function findMinSumSubarray(tree) {
  let min = tree.head.data;
  let sum = tree.head.data;
  let temp = tree.head.next;
  while (temp !== null) {
    sum = Math.min(temp.data, sum + temp.data);
    min = Math.min(min, sum);
    temp = temp.next;
  }
  return min;
}
```
**20. Find the maximum length subarray with equal number of 0s and 1s in the tree:**
```javascript
function findMaxLengthSubarray(tree) {
  let max = 0;
  let sum = 0;
  let map = new Map();
  map.set(0, -1);
  let temp = tree.head;
  while (temp !== null) {
    sum += temp.data === 0 ? -1 : 1;
    if (map.has(sum)) {
      max = Math.max(max, temp.data - map.get(sum));
    } else {
      map.set(sum, temp.data);
    }
    temp = temp.next;
  }
  return max;
}
```

**Graph**
================

A graph is a non-linear data structure consisting of nodes or vertices connected by edges.

**Sequence**

1. **Basic Operations**
	* Insert
	* Delete
	* Search
2. **Traversal**
	* Breadth-First Search (BFS)
	* Depth-First Search (DFS)
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a graph using an adjacency matrix.
2. Implement a graph using an adjacency list.
3. Insert a node into the graph.
4. Delete a node from the graph.
5. Search for a node in the graph.
6. Traverse the graph using BFS.
7. Traverse the graph using DFS.
8. Sort the graph using bubble sort.
9. Sort the graph using selection sort.
10. Sort the graph using insertion sort.
11. Sort the graph using merge sort.
12. Sort the graph using quick sort.
13. Find the maximum element in the graph.
14. Find the minimum element in the graph.
15. Find the first duplicate element in the graph.
16. Find the first missing positive integer in the graph.
17. Find the maximum sum subarray in the graph.
18. Find the minimum sum subarray in the graph.
19. Find the maximum length subarray with equal number of 0s and 1s in the graph.
20. Find the minimum length subarray with equal number of 0s and 1s in the graph.

**Answers**

**1. Implement a graph using an adjacency matrix:**
```javascript
class Graph {
  constructor() {
    this.matrix = [];
  }

  addNode(node) {
    this.matrix.push([]);
    for (let i = 0; i < this.matrix.length; i++) {
      this.matrix[i].push(0);
    }
  }

  addEdge(node1, node2) {
    this.matrix[node1][node2] = 1;
  }

  removeEdge(node1, node2) {
    this.matrix[node1][node2] = 0;
  }

  hasEdge(node1, node2) {
    return this.matrix[node1][node2] === 1;
  }
}
```
**2. Implement a graph using an adjacency list:**
```javascript
class Graph {
  constructor() {
    this.list = {};
  }

  addNode(node) {
    this.list[node] = [];
  }

  addEdge(node1, node2) {
    this.list[node1].push(node2);
  }

  removeEdge(node1, node2) {
    let index = this.list[node1].indexOf(node2);
    if (index !== -1) {
      this.list[node1].splice(index, 1);
    }
  }

  hasEdge(node1, node2) {
    return this.list[node1].includes(node2);
  }
}
```
**3. Insert a node into the graph:**
```javascript
graph.addNode(node);
```
**4. Delete a node from the graph:**
```javascript
graph.removeNode(node);
```
**5. Search for a node in the graph:**
```javascript
graph.hasNode(node);
```
**6. Traverse the graph using BFS:**
```javascript
function bfs(graph, startNode) {
  let visited = new Set();
  let queue = [startNode];
  while (queue.length > 0) {
    let node = queue.shift();
    if (!visited.has(node)) {
      visited.add(node);
      console.log(node);
      for (let neighbor of graph.list[node]) {
        if (!visited.has(neighbor)) {
          queue.push(neighbor);
        }
      }
    }
  }
}
```
**7. Traverse the graph using DFS:**
```javascript
function dfs(graph, startNode) {
  let visited = new Set();
  function recursiveDfs(node) {
    visited.add(node);
    console.log(node);
    for (let neighbor of graph.list[node]) {
      if (!visited.has(neighbor)) {
        recursiveDfs(neighbor);
      }
    }
  }
  recursiveDfs(startNode);
}
```
**8. Sort the graph using bubble sort:**
```javascript
function bubbleSort(graph) {
  let nodes = Object.keys(graph.list);
  for (let i = 0; i < nodes.length; i++) {
    for (let j = 0; j < nodes.length - i - 1; j++) {
      if (graph.list[nodes[j]].length > graph.list[nodes[j + 1]].length) {
        let temp = nodes[j];
        nodes[j] = nodes[j + 1];
        nodes[j + 1] = temp;
      }
    }
  }
  return nodes;
}
```
**9. Sort the graph using selection sort:**
```javascript
function selectionSort(graph) {
  let nodes = Object.keys(graph.list);
  for (let i = 0; i < nodes.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < nodes.length; j++) {
      if (graph.list[nodes[j]].length < graph.list[nodes[minIndex]].length) {
        minIndex = j;
      }
    }
    let temp = nodes[i];
    nodes[i] = nodes[minIndex];
    nodes[minIndex] = temp;
  }
  return nodes;
}
```
**10. Sort the graph using insertion sort:**
```javascript
function insertionSort(graph) {
  let nodes = Object.keys(graph.list);
  for (let i = 1; i < nodes.length; i++) {
    let key = nodes[i];
    let j = i - 1;
    while (j >= 0 && graph.list[nodes[j]].length > graph.list[key].length) {
      nodes[j + 1] = nodes[j];
      j--;
    }
    nodes[j + 1] = key;
  }
  return nodes;
}
```
**11. Sort the graph using merge sort:**
```javascript
function mergeSort(graph) {
  let nodes = Object.keys(graph.list);
  if (nodes.length <= 1) {
    return nodes;
  }
  let mid = Math.floor(nodes.length / 2);
  let left = mergeSort(graph, nodes.slice(0, mid));
  let right = mergeSort(graph, nodes.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  let i = 0;
  let j = 0;
  while (i < left.length && j < right.length) {
    if (left[i].length < right[j].length) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }
  return result.concat(left.slice(i)).concat(right.slice(j));
}
```
**12. Sort the graph using quick sort:**
```javascript
function quickSort(graph) {
  let nodes = Object.keys(graph.list);
  if (nodes.length <= 1) {
    return nodes;
  }
  let pivot = nodes[0];
  let left = [];
  let right = [];
  for (let i = 1; i < nodes.length; i++) {
    if (graph.list[nodes[i]].length < graph.list[pivot].length) {
      left.push(nodes[i]);
    } else {
      right.push(nodes[i]);
    }
  }
  return quickSort(graph, left).concat(pivot, quickSort(graph, right));
}
```


Here is the rest of the documentation:

**13. Find the maximum element in the graph:**
```javascript
function findMax(graph) {
  let max = -Infinity;
  for (let node in graph.list) {
    if (graph.list[node].length > max) {
      max = graph.list[node].length;
    }
  }
  return max;
}
```
**14. Find the minimum element in the graph:**
```javascript
function findMin(graph) {
  let min = Infinity;
  for (let node in graph.list) {
    if (graph.list[node].length < min) {
      min = graph.list[node].length;
    }
  }
  return min;
}
```
**15. Find the first duplicate element in the graph:**
```javascript
function findFirstDuplicate(graph) {
  let set = new Set();
  for (let node in graph.list) {
    if (set.has(graph.list[node].length)) {
      return graph.list[node].length;
    }
    set.add(graph.list[node].length);
  }
  return null;
}
```
**16. Find the first missing positive integer in the graph:**
```javascript
function findFirstMissingPositive(graph) {
  let set = new Set();
  for (let node in graph.list) {
    set.add(graph.list[node].length);
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**17. Find the maximum sum subarray in the graph:**
```javascript
function findMaxSumSubarray(graph) {
  let max = -Infinity;
  for (let node in graph.list) {
    let sum = 0;
    for (let neighbor of graph.list[node]) {
      sum += neighbor.length;
    }
    if (sum > max) {
      max = sum;
    }
  }
  return max;
}
```
**18. Find the minimum sum subarray in the graph:**
```javascript
function findMinSumSubarray(graph) {
  let min = Infinity;
  for (let node in graph.list) {
    let sum = 0;
    for (let neighbor of graph.list[node]) {
      sum += neighbor.length;
    }
    if (sum < min) {
      min = sum;
    }
  }
  return min;
}
```
**19. Find the maximum length subarray with equal number of 0s and 1s in the graph:**
```javascript
function findMaxLengthSubarray(graph) {
  let max = 0;
  for (let node in graph.list) {
    let sum = 0;
    for (let neighbor of graph.list[node]) {
      sum += neighbor.length;
    }
    if (sum % 2 === 0 && sum > max) {
      max = sum;
    }
  }
  return max;
}
```
**20. Find the minimum length subarray with equal number of 0s and 1s in the graph:**
```javascript
function findMinLengthSubarray(graph) {
  let min = Infinity;
  for (let node in graph.list) {
    let sum = 0;
    for (let neighbor of graph.list[node]) {
      sum += neighbor.length;
    }
    if (sum % 2 === 0 && sum < min) {
      min = sum;
    }
  }
  return min;
}
```

**Hash Table**
================

A hash table is a data structure that stores key-value pairs in an array using a hash function to map keys to indices of the array.

**Sequence**

1. **Basic Operations**
	* Insert
	* Delete
	* Search
2. **Hash Functions**
	* Division Method
	* Multiplication Method
	* Folding Method
3. **Collision Resolution**
	* Chaining
	* Open Addressing
4. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a hash table using an array.
2. Implement a hash table using a linked list.
3. Insert a key-value pair into the hash table.
4. Delete a key-value pair from the hash table.
5. Search for a key in the hash table.
6. Implement a hash function using the division method.
7. Implement a hash function using the multiplication method.
8. Implement a hash function using the folding method.
9. Resolve collisions using chaining.
10. Resolve collisions using open addressing.
11. Sort the hash table using bubble sort.
12. Sort the hash table using selection sort.
13. Sort the hash table using insertion sort.
14. Sort the hash table using merge sort.
15. Sort the hash table using quick sort.
16. Find the maximum element in the hash table.
17. Find the minimum element in the hash table.
18. Find the first duplicate element in the hash table.
19. Find the first missing positive integer in the hash table.
20. Find the maximum sum subarray in the hash table.

**Answers**

1. Implement a hash table using an array:
```javascript
class HashTable {
  constructor() {
    this.array = [];
  }

  insert(key, value) {
    let index = this.hashFunction(key);
    this.array[index] = value;
  }

  delete(key) {
    let index = this.hashFunction(key);
    this.array[index] = null;
  }

  search(key) {
    let index = this.hashFunction(key);
    return this.array[index];
  }

  hashFunction(key) {
    return key % this.array.length;
  }
}
```
2. Implement a hash table using a linked list:
```javascript
class HashTable {
  constructor() {
    this.list = {};
  }

  insert(key, value) {
    let index = this.hashFunction(key);
    if (!this.list[index]) {
      this.list[index] = [];
    }
    this.list[index].push(value);
  }

  delete(key) {
    let index = this.hashFunction(key);
    if (this.list[index]) {
      for (let i = 0; i < this.list[index].length; i++) {
        if (this.list[index][i] === key) {
          this.list[index].splice(i, 1);
          break;
        }
      }
    }
  }

  search(key) {
    let index = this.hashFunction(key);
    if (this.list[index]) {
      for (let i = 0; i < this.list[index].length; i++) {
        if (this.list[index][i] === key) {
          return this.list[index][i];
        }
      }
    }
    return null;
  }

  hashFunction(key) {
    return key % Object.keys(this.list).length;
  }
}
```
3. Insert a key-value pair into the hash table:
```javascript
hashTable.insert(key, value);
```
4. Delete a key-value pair from the hash table:
```javascript
hashTable.delete(key);
```
5. Search for a key in the hash table:
```javascript
hashTable.search(key);
```
6. Implement a hash function using the division method:
```javascript
function hashFunction(key) {
  return key % array.length;
}
```
7. Implement a hash function using the multiplication method:
```javascript
function hashFunction(key) {
  return (key * prime) % array.length;
}
```
8. Implement a hash function using the folding method:
```javascript
function hashFunction(key) {
  return (key + key.length) % array.length;
}
```
9. Resolve collisions using chaining:
```javascript
function resolveCollision(key, value) {
  let index = hashFunction(key);
  if (array[index]) {
    array[index].push(value);
  } else {
    array[index] = [value];
  }
}
```
10. Resolve collisions using open addressing:
```javascript
function resolveCollision(key, value) {
  let index = hashFunction(key);
  while (array[index]) {
    index = (index + 1) % array.length;
  }
  array[index] = value;
}
```
11. Sort the hash table using bubble sort:
```javascript
function bubbleSort() {
  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < array.length - i - 1; j++) {
      if (array[j] > array[j + 1]) {
        let temp = array[j];
        array[j] = array[j + 1];
        array[j + 1] = temp;
      }
    }
  }
}
```
12. Sort the hash table using selection sort:
```javascript
function selectionSort() {
  for (let i = 0; i < array.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }
    }
    let temp = array[i];
    array[i] = array[minIndex];
    array[minIndex] = temp;
  }
}
```




Here is the rest of the documentation:

**14. Sort the hash table using merge sort:**
```javascript
function mergeSort() {
  if (array.length <= 1) {
    return array;
  }
  let mid = Math.floor(array.length / 2);
  let left = mergeSort(array.slice(0, mid));
  let right = mergeSort(array.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  while (left.length > 0 && right.length > 0) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  return result.concat(left).concat(right);
}
```
**15. Sort the hash table using quick sort:**
```javascript
function quickSort() {
  if (array.length <= 1) {
    return array;
  }
  let pivot = array[0];
  let left = [];
  let right = [];
  for (let i = 1; i < array.length; i++) {
    if (array[i] <= pivot) {
      left.push(array[i]);
    } else {
      right.push(array[i]);
    }
  }
  return quickSort(left).concat(pivot, quickSort(right));
}
```
**16. Find the maximum element in the hash table:**
```javascript
function findMax() {
  let max = -Infinity;
  for (let i = 0; i < array.length; i++) {
    if (array[i] > max) {
      max = array[i];
    }
  }
  return max;
}
```
**17. Find the minimum element in the hash table:**
```javascript
function findMin() {
  let min = Infinity;
  for (let i = 0; i < array.length; i++) {
    if (array[i] < min) {
      min = array[i];
    }
  }
  return min;
}
```
**18. Find the first duplicate element in the hash table:**
```javascript
function findFirstDuplicate() {
  let set = new Set();
  for (let i = 0; i < array.length; i++) {
    if (set.has(array[i])) {
      return array[i];
    }
    set.add(array[i]);
  }
  return null;
}
```
**19. Find the first missing positive integer in the hash table:**
```javascript
function findFirstMissingPositive() {
  let set = new Set();
  for (let i = 0; i < array.length; i++) {
    set.add(array[i]);
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
```
**20. Find the maximum sum subarray in the hash table:**
```javascript
function findMaxSumSubarray() {
  let max = -Infinity;
  let sum = 0;
  for (let i = 0; i < array.length; i++) {
    sum += array[i];
    if (sum > max) {
      max = sum;
    }
    if (sum < 0) {
      sum = 0;
    }
  }
  return max;
}
```



Here is the rest of the documentation:

**Heap**
================

A heap is a specialized tree-based data structure that satisfies the heap property: the parent node is either greater than (in a max heap) or less than (in a min heap) its child nodes.

**Sequence**

1. **Basic Operations**
	* Insert
	* Delete
	* Search
2. **Heapify**
	* Build Heap
	* Heapify Up
	* Heapify Down
3. **Sorting**
	* Heap Sort
4. **Priority Queue**
	* Enqueue
	* Dequeue

**Questions**

1. Implement a max heap.
2. Implement a min heap.
3. Insert an element into the heap.
4. Delete an element from the heap.
5. Search for an element in the heap.
6. Build a heap from an array.
7. Heapify up an element in the heap.
8. Heapify down an element in the heap.
9. Sort an array using heap sort.
10. Implement a priority queue using a heap.

**Answers**

1. Implement a max heap:
```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  insert(element) {
    this.heap.push(element);
    this.heapifyUp(this.heap.length - 1);
  }

  delete(element) {
    let index = this.heap.indexOf(element);
    if (index !== -1) {
      this.heap[index] = this.heap[this.heap.length - 1];
      this.heap.pop();
      this.heapifyDown(index);
    }
  }

  search(element) {
    return this.heap.indexOf(element) !== -1;
  }

  heapifyUp(index) {
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      if (this.heap[parentIndex] >= this.heap[index]) {
        break;
      }
      let temp = this.heap[parentIndex];
      this.heap[parentIndex] = this.heap[index];
      this.heap[index] = temp;
      index = parentIndex;
    }
  }

  heapifyDown(index) {
    while (true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let largestIndex = index;
      if (leftChildIndex < this.heap.length && this.heap[leftChildIndex] > this.heap[largestIndex]) {
        largestIndex = leftChildIndex;
      }
      if (rightChildIndex < this.heap.length && this.heap[rightChildIndex] > this.heap[largestIndex]) {
        largestIndex = rightChildIndex;
      }
      if (largestIndex === index) {
        break;
      }
      let temp = this.heap[largestIndex];
      this.heap[largestIndex] = this.heap[index];
      this.heap[index] = temp;
      index = largestIndex;
    }
  }
}
```
2. Implement a min heap:
```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(element) {
    this.heap.push(element);
    this.heapifyUp(this.heap.length - 1);
  }

  delete(element) {
    let index = this.heap.indexOf(element);
    if (index !== -1) {
      this.heap[index] = this.heap[this.heap.length - 1];
      this.heap.pop();
      this.heapifyDown(index);
    }
  }

  search(element) {
    return this.heap.indexOf(element) !== -1;
  }

  heapifyUp(index) {
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      if (this.heap[parentIndex] <= this.heap[index]) {
        break;
      }
      let temp = this.heap[parentIndex];
      this.heap[parentIndex] = this.heap[index];
      this.heap[index] = temp;
      index = parentIndex;
    }
  }

  heapifyDown(index) {
    while (true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let smallestIndex = index;
      if (leftChildIndex < this.heap.length && this.heap[leftChildIndex] < this.heap[smallestIndex]) {
        smallestIndex = leftChildIndex;
      }
      if (rightChildIndex < this.heap.length && this.heap[rightChildIndex] < this.heap[smallestIndex]) {
        smallestIndex = rightChildIndex;
      }
      if (smallestIndex === index) {
        break;
      }
      let temp = this.heap[smallestIndex];
      this.heap[smallestIndex] = this.heap[index];
      this.heap[index] = temp;
      index = smallestIndex;
    }
  }
}
```
3. Insert an element into the heap:
```javascript
heap.insert(element);
```
4. Delete an element from the heap:
```javascript
heap.delete(element);
```
5. Search for an element in the heap:
```javascript
heap.search(element);
```
6. Build a heap from an array:
```javascript
function buildHeap(array) {
  let heap = new MaxHeap();
  for (let element of array) {
    heap.insert(element);
  }
  return heap;
}
```
7. Heapify up an element in the heap:
```javascript
heap.heapifyUp(index);
```
8. Heapify down an element in the heap:
```javascript
heap.heapifyDown(index);
```
9. Sort an array using heap sort:
```javascript
function heapSort(array) {
  let heap = buildHeap(array);
  let sortedArray = [];
  while (heap.heap.length > 0) {
    sortedArray.push(heap.heap[0]);
    heap.delete(heap.heap[0]);
  }
  return sortedArray;
}
```
10. Implement a priority queue using a heap:
```javascript
class PriorityQueue {
  constructor() {
    this.heap = new MaxHeap();
  }

  enqueue(element) {
    this.heap.insert(element);
  }

  dequeue() {
    return this.heap.delete(this.heap.heap[0]);
  }

  peek() {
    return this.heap.heap[0];
  }
}
```




Here is the rest of the documentation:

**Trie**
================

A trie is a tree-like data structure that is often used to store a dynamic set or associative array where the keys are usually strings.

**Sequence**

1. **Basic Operations**
	* Insert
	* Delete
	* Search
2. **Traversal**
	* Depth-First Search (DFS)
	* Breadth-First Search (BFS)
3. **Sorting**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions**

1. Implement a trie using an object.
2. Implement a trie using an array.
3. Insert a string into the trie.
4. Delete a string from the trie.
5. Search for a string in the trie.
6. Traverse the trie using DFS.
7. Traverse the trie using BFS.
8. Sort the trie using bubble sort.
9. Sort the trie using selection sort.
10. Sort the trie using insertion sort.
11. Sort the trie using merge sort.
12. Sort the trie using quick sort.
13. Find the maximum element in the trie.
14. Find the minimum element in the trie.
15. Find the first duplicate element in the trie.
16. Find the first missing positive integer in the trie.
17. Find the maximum sum subarray in the trie.
18. Find the minimum sum subarray in the trie.
19. Find the maximum length subarray with equal number of 0s and 1s in the trie.
20. Find the minimum length subarray with equal number of 0s and 1s in the trie.

**Answers**

1. Implement a trie using an object:
```javascript
class Trie {
  constructor() {
    this.root = {};
  }

  insert(string) {
    let node = this.root;
    for (let char of string) {
      if (!node[char]) {
        node[char] = {};
      }
      node = node[char];
    }
    node.endOfWord = true;
  }

  delete(string) {
    function deleteNode(node, string, index) {
      if (index === string.length) {
        if (!node.endOfWord) {
          return false;
        }
        node.endOfWord = false;
        return Object.keys(node).length === 0;
      }
      let char = string[index];
      if (!node[char]) {
        return false;
      }
      if (deleteNode(node[char], string, index + 1)) {
        delete node[char];
        return Object.keys(node).length === 0;
      }
      return false;
    }
    deleteNode(this.root, string, 0);
  }

  search(string) {
    let node = this.root;
    for (let char of string) {
      if (!node[char]) {
        return false;
      }
      node = node[char];
    }
    return node.endOfWord === true;
  }
}
```
2. Implement a trie using an array:
```javascript
class Trie {
  constructor() {
    this.root = new Array(26);
  }

  insert(string) {
    let node = this.root;
    for (let char of string) {
      let index = char.charCodeAt(0) - 'a'.charCodeAt(0);
      if (!node[index]) {
        node[index] = new Array(26);
      }
      node = node[index];
    }
    node[26] = true;
  }

  delete(string) {
    function deleteNode(node, string, index) {
      if (index === string.length) {
        if (!node[26]) {
          return false;
        }
        node[26] = false;
        return node.every((child) => child === undefined);
      }
      let char = string[index];
      let charCode = char.charCodeAt(0) - 'a'.charCodeAt(0);
      if (!node[charCode]) {
        return false;
      }
      if (deleteNode(node[charCode], string, index + 1)) {
        node[charCode] = undefined;
        return node.every((child) => child === undefined);
      }
      return false;
    }
    deleteNode(this.root, string, 0);
  }

  search(string) {
    let node = this.root;
    for (let char of string) {
      let charCode = char.charCodeAt(0) - 'a'.charCodeAt(0);
      if (!node[charCode]) {
        return false;
      }
      node = node[charCode];
    }
    return node[26] === true;
  }
}
```
3. Insert a string into the trie:
```javascript
trie.insert(string);
```
4. Delete a string from the trie:
```javascript
trie.delete(string);
```
5. Search for a string in the trie:
```javascript
trie.search(string);
```
6. Traverse the trie using DFS:
```javascript
function dfs(node) {
  if (node.endOfWord) {
    console.log(node);
  }
  for (let child in node) {
    if (child !== 'endOfWord') {
      dfs(node[child]);
    }
  }
}
dfs(trie.root);
```
7. Traverse the trie using BFS:
```javascript
function bfs(node) {
  let queue = [node];
  while (queue.length > 0) {
    let currentNode = queue.shift();
    if (currentNode.endOfWord) {
      console.log(currentNode);
    }
    for (let child in currentNode) {
      if (child !== 'endOfWord') {
        queue.push(currentNode[child]);
      }
    }
  }
}
bfs(trie.root);
```




Here is the rest of the documentation:

**8. Sort the trie using bubble sort:**
```javascript
function bubbleSort(node) {
  let children = Object.keys(node);
  for (let i = 0; i < children.length; i++) {
    for (let j = 0; j < children.length - i - 1; j++) {
      if (children[j] > children[j + 1]) {
        let temp = children[j];
        children[j] = children[j + 1];
        children[j + 1] = temp;
      }
    }
  }
  for (let child of children) {
    bubbleSort(node[child]);
  }
}
bubbleSort(trie.root);
```
**9. Sort the trie using selection sort:**
```javascript
function selectionSort(node) {
  let children = Object.keys(node);
  for (let i = 0; i < children.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < children.length; j++) {
      if (children[j] < children[minIndex]) {
        minIndex = j;
      }
    }
    let temp = children[i];
    children[i] = children[minIndex];
    children[minIndex] = temp;
  }
  for (let child of children) {
    selectionSort(node[child]);
  }
}
selectionSort(trie.root);
```
**10. Sort the trie using insertion sort:**
```javascript
function insertionSort(node) {
  let children = Object.keys(node);
  for (let i = 1; i < children.length; i++) {
    let key = children[i];
    let j = i - 1;
    while (j >= 0 && children[j] > key) {
      children[j + 1] = children[j];
      j--;
    }
    children[j + 1] = key;
  }
  for (let child of children) {
    insertionSort(node[child]);
  }
}
insertionSort(trie.root);
```
**11. Sort the trie using merge sort:**
```javascript
function mergeSort(node) {
  let children = Object.keys(node);
  if (children.length <= 1) {
    return children;
  }
  let mid = Math.floor(children.length / 2);
  let left = mergeSort(node, children.slice(0, mid));
  let right = mergeSort(node, children.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  while (left.length > 0 && right.length > 0) {
    if (left[0] < right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  return result.concat(left).concat(right);
}
mergeSort(trie.root);
```
**12. Sort the trie using quick sort:**
```javascript
function quickSort(node) {
  let children = Object.keys(node);
  if (children.length <= 1) {
    return children;
  }
  let pivot = children[0];
  let left = [];
  let right = [];
  for (let i = 1; i < children.length; i++) {
    if (children[i] < pivot) {
      left.push(children[i]);
    } else {
      right.push(children[i]);
    }
  }
  return quickSort(node, left).concat(pivot, quickSort(node, right));
}
quickSort(trie.root);
```




Here is the rest of the documentation:

**13. Find the maximum element in the trie:**
```javascript
function findMax(node) {
  let max = -Infinity;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let value = findMax(node[child]);
      if (value > max) {
        max = value;
      }
    } else if (node[child] === true) {
      max = Math.max(max, child);
    }
  }
  return max;
}
findMax(trie.root);
```
**14. Find the minimum element in the trie:**
```javascript
function findMin(node) {
  let min = Infinity;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let value = findMin(node[child]);
      if (value < min) {
        min = value;
      }
    } else if (node[child] === true) {
      min = Math.min(min, child);
    }
  }
  return min;
}
findMin(trie.root);
```
**15. Find the first duplicate element in the trie:**
```javascript
function findFirstDuplicate(node) {
  let set = new Set();
  for (let child in node) {
    if (child !== 'endOfWord') {
      let value = findFirstDuplicate(node[child]);
      if (value !== null) {
        return value;
      }
    } else if (node[child] === true) {
      if (set.has(child)) {
        return child;
      }
      set.add(child);
    }
  }
  return null;
}
findFirstDuplicate(trie.root);
```
**16. Find the first missing positive integer in the trie:**
```javascript
function findFirstMissingPositive(node) {
  let set = new Set();
  for (let child in node) {
    if (child !== 'endOfWord') {
      let value = findFirstMissingPositive(node[child]);
      if (value !== null) {
        return value;
      }
    } else if (node[child] === true) {
      set.add(child);
    }
  }
  let i = 1;
  while (set.has(i)) {
    i++;
  }
  return i;
}
findFirstMissingPositive(trie.root);
```
**17. Find the maximum sum subarray in the trie:**
```javascript
function findMaxSumSubarray(node) {
  let max = -Infinity;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let sum = findMaxSumSubarray(node[child]);
      if (sum > max) {
        max = sum;
      }
    } else if (node[child] === true) {
      max = Math.max(max, child);
    }
  }
  return max;
}
findMaxSumSubarray(trie.root);
```
**18. Find the minimum sum subarray in the trie:**
```javascript
function findMinSumSubarray(node) {
  let min = Infinity;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let sum = findMinSumSubarray(node[child]);
      if (sum < min) {
        min = sum;
      }
    } else if (node[child] === true) {
      min = Math.min(min, child);
    }
  }
  return min;
}
findMinSumSubarray(trie.root);
```




Here is the rest of the documentation:

**19. Find the maximum length subarray with equal number of 0s and 1s in the trie:**
```javascript
function findMaxLengthSubarray(node) {
  let max = 0;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let length = findMaxLengthSubarray(node[child]);
      if (length > max) {
        max = length;
      }
    } else if (node[child] === true) {
      let count0 = 0;
      let count1 = 0;
      for (let i = 0; i < child.length; i++) {
        if (child[i] === '0') {
          count0++;
        } else {
          count1++;
        }
      }
      if (count0 === count1) {
        max = Math.max(max, child.length);
      }
    }
  }
  return max;
}
findMaxLengthSubarray(trie.root);
```
**20. Find the minimum length subarray with equal number of 0s and 1s in the trie:**
```javascript
function findMinLengthSubarray(node) {
  let min = Infinity;
  for (let child in node) {
    if (child !== 'endOfWord') {
      let length = findMinLengthSubarray(node[child]);
      if (length < min) {
        min = length;
      }
    } else if (node[child] === true) {
      let count0 = 0;
      let count1 = 0;
      for (let i = 0; i < child.length; i++) {
        if (child[i] === '0') {
          count0++;
        } else {
          count1++;
        }
      }
      if (count0 === count1) {
        min = Math.min(min, child.length);
      }
    }
  }
  return min;
}
findMinLengthSubarray(trie.root);
```
