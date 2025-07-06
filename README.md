

Here is a comprehensive document covering 20 DSA (Data Structures and Algorithms) questions and answers for each of the following patterns:

**Patterns:**

1. **Array**
2. **Linked List**
3. **Stack**
4. **Queue**
5. **Tree**
6. **Graph**

**Pattern-wise Description and Questions:**

### Array

**Description:** An array is a collection of elements of the same data type stored in contiguous memory locations.

**Sequence:**

1. **Basic Operations:**
	* Accessing an element
	* Updating an element
	* Inserting an element
	* Deleting an element
2. **Searching:**
	* Linear Search
	* Binary Search
3. **Sorting:**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions:**

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

**Answers:**

1. Find the maximum element in an array: `max = arr[0]; for (i = 1; i < n; i++) { if (arr[i] > max) max = arr[i]; }`
2. Find the minimum element in an array: `min = arr[0]; for (i = 1; i < n; i++) { if (arr[i] < min) min = arr[i]; }`
3. Search for an element in an array using linear search: `for (i = 0; i < n; i++) { if (arr[i] == target) return i; } return -1;`
4. Search for an element in an array using binary search: `low = 0; high = n - 1; while (low <= high) { mid = (low + high) / 2; if (arr[mid] == target) return mid; else if (arr[mid] < target) low = mid + 1; else high = mid - 1; } return -1;`
5. Sort an array using bubble sort: `for (i = 0; i < n - 1; i++) { for (j = 0; j < n - i - 1; j++) { if (arr[j] > arr[j + 1]) { temp = arr[j]; arr[j] = arr[j + 1]; arr[j + 1] = temp; } } }`
6. Sort an array using selection sort: `for (i = 0; i < n - 1; i++) { min = i; for (j = i + 1; j < n; j++) { if (arr[j] < arr[min]) min = j; } temp = arr[i]; arr[i] = arr[min]; arr[min] = temp; }`
7. Sort an array using insertion sort: `for (i = 1; i < n; i++) { key = arr[i]; j = i - 1; while (j >= 0 && arr[j] > key) { arr[j + 1] = arr[j]; j--; } arr[j + 1] = key; }`
8. Sort an array using merge sort: `mergeSort(arr, 0, n - 1);`
9. Sort an array using quick sort: `quickSort(arr, 0, n - 1);`
10. Find the first duplicate element in an array: `for (i = 0; i < n; i++) { if (arr[i] == arr[i + 1]) return arr[i]; } return -1;`
11. Find the first missing positive integer in an array: `for (i = 0; i < n; i++) { if (arr[i] > 0) { if (arr[i] != i + 1) return i + 1; } } return n + 1;`
12. Find the maximum sum subarray in an array: `max = arr[0]; sum = arr[0]; for (i = 1; i < n; i++) { sum = max(sum, sum + arr[i]); max = max(max, sum); } return max;`
13. Find the minimum sum subarray in an array: `min = arr[0]; sum = arr[0]; for (i = 1; i < n; i++) { sum = min(sum, sum + arr[i]); min = min(min, sum); } return min;`
14. Find the maximum length subarray with equal number of 0s and 1s: `max = 0; sum = 0; for (i = 0; i < n; i++) { if (arr[i] == 0) sum--; else sum++; if (sum == 0) max = max(max, i + 1); } return max;`
15. Find the minimum length subarray with equal number of 0s and 1s: `min = n; sum = 0; for (i = 0; i < n; i++) { if (arr[i] == 0) sum--; else sum++; if (sum == 0) min = min(min, i + 1); } return min;`
16. Find the maximum frequency element in an array: `max = 0; count = 0; for (i = 0; i < n; i++) { if (arr[i] == arr[i + 1]) count++; else { if (count > max) max = count; count = 0; } } return max;`
17. Find the minimum frequency element in an array: `min = n; count = 0; for (i = 0; i < n; i++) { if (arr[i] == arr[i + 1]) count++; else { if (count < min) min = count; count = 0; } } return min;`
18. Find the maximum sum of a subarray with a given size: `max = 0; sum = 0; for (i = 0; i < k; i++) sum += arr[i]; max = sum; for (i = k; i < n; i++) { sum = sum - arr[i - k] + arr[i]; if (sum > max) max = sum; } return max;`
19. Find the minimum sum of a subarray with a given size: `min = 0; sum = 0; for (i = 0; i < k; i++) sum += arr[i]; min = sum; for (i = k; i < n; i++) { sum = sum - arr[i - k] + arr[i]; if (sum < min) min = sum; } return min;`
20. Find the maximum product of a subarray with a given size: `max = 1; product = 1; for (i = 0; i < k; i++) product *= arr[i]; max = product; for (i = k; i < n; i++) { product = product / arr[i - k] * arr[i]; if (product > max) max = product; } return max;`

### Linked List

**Description:** A linked list is a dynamic collection of elements, where each element points to the next element.

**Sequence:**

1. **Basic Operations:**
	* Insertion
	* Deletion
	* Traversal
2. **Searching:**
	* Linear Search
	* Binary Search
3. **Sorting:**
	* Bubble Sort
	* Selection Sort
	* Insertion Sort
	* Merge Sort
	* Quick Sort

**Questions:**

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
17. Find the minimum sum subarray in a linked list
