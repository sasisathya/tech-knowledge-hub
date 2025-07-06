

Here is the documentation for the Data Structures and Algorithms in JavaScript, with answers and code examples:

**Table of Contents**

1. [Array](#array)
2. [Linked List](#linked-list)
3. [Stack](#stack)
4. [Queue](#queue)
5. [Tree](#tree)
6. [Graph](#graph)

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
I hope this documentation helps you understand the solutions to the problems. Let me know if you have any questions or need further clarification.
