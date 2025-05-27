## BubbleSort
# the bubble sort algorithm performs operations based on comparisons between adjacent elements
```
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    let swapped = false;
    for (let j = 0; j < arr.length - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j + 1];
        arr[j + 1] = arr[j];
        arr[j] = temp;
        swapped = true;
      }
    }
    if (!swapped) {
      break; // Exit if no swaps were made in the entire pass
    }
  }
}
```
## SelectionSort
# The algorithm proceeds by finding the smallest (or largest, depending on sorting order) element from the unsorted sublist, swapping it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right

```
function selectionSort(arr) {
  let isSorted = true;

  for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
        isSorted = false;
      }
    }
    if (min !== i) {
      [arr[i], arr[min]] = [arr[min], arr[i]];
    }
    // If no swaps were made, the array is already sorted
    if (isSorted) break;
    isSorted = true; // Reset for the next iteration
  }
  return arr;
}
```
## InsertionSort
# The Insertion Sort algorithm uses one part of the array to hold the sorted values, and the other part of the array to hold values that are not sorted yet.
```
function insertionSort(arr) {
  let n = arr.length; 
  for(let i = 1;i < n; i++) {
    let j = i;
    while(j > 0 && arr[j] < arr[j-1]) {
        int temp = arr[j];
        arr[j] = arr[j-1];
        arr[j-1] = temp;
        j--;
    }
}
  return arr;
}
```
## QuickSort
# QuickSort is a sorting algorithm based on the Divide and Conquer that picks an element as a pivot and partitions the given array around the picked pivot.
```
function quickSort(arr, start, end) {
    if(start >= end) return;
    let pt = partition(arr, start, end);
    quickSort(arr, start, pt-1); // Fixed: should be pt-1 to avoid infinite recursion
    quickSort(arr, pt+1, end);   // Fixed: typo in "quickSort"
}

function partition(arr, low, high) {
    let pivot = arr[high];
    let left = low; 
    let right = high-1;
    
    while(left <= right) {       // Fixed: use <= to handle equal case
        while(arr[left] < pivot) {
            left++;
        }
        while(arr[right] > pivot) {
            right--;             // Fixed: decrement right (not increment)
        }
        if(left >= right) {      // Fixed: use >= instead of >
            break;
        }
        // Swap elements
        let temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        
        left++;                  // Added: advance pointers after swap
        right--;                 // Added: advance pointers after swap
    }
    
    // Swap pivot into final position
    let temp = arr[left];
    arr[left] = arr[high];
    arr[high] = temp;
    
    return left;
}
```
