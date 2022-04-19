# Merge Sort

([Back to menu](/README.md))

Merge sorting is usually more efficient than bubble sorting unless the array is pre-sorted. It always has O(n log(n)) complexity. The algorithm involves using **divide and conquer** recursion to split an array until it consists of many arrays with lengths of one. It then merges those sub-arrays back together incrementally, moving the smallest number to the far left and the largest to the far right.

Algorithm:

1. **Divide** by finding the number qqq of the position midway between *p* and *r*. Do this step the same way we found the midpoint in binary search: add *p* and *r*, divide by 2, and round down.
2. **Conquer** by recursively sorting the subarrays in each of the two subproblems created by the divide step. That is, recursively sort the subarray array[p..q] and recursively sort the subarray array[q+1..r].
3. **Combine** by merging the two sorted subarrays back into the single sorted subarray array[p..r].

The base case is a subarray containing fewer than two elements, that is, when *p >= r*, since a subarray with no elements or just one element is already sorted. So divide-conquer-combine only when *p<r*.

## Sample code

```java
public void mergeSort(int arr[]) {
 if (arr.length < 2) {
  return;
 }

 int mid = arr.length / 2;
 int left[] = new int[mid];
 int right[] = new int[arr.length - mid];

 for (int i = 0; i < mid; i++) {
  left[i] = arr[i];
 }

 for (int i = mid; i < arr.length; i++) {
  right[i - mid] = arr[i];
 }

 mergeSort(left);
 mergeSort(right);
 merge(arr, left, right);
}

public void merge(int arr[], int[] left, int[] right) {
 int i = 0, j = 0, k = 0;
 while (i < left.length && j < right.length) {
  if (left[i] <= right[j]) {
   arr[k++] = left[i++];
  } else {
   arr[k++] = right[j++];
  }
 }

 while (i < left) {
  arr[k++] = left[i++];
 }
 
 while (j < right) {
  arr[k++] = right[j++];
 }
}

```

## Space Complexity: O(n)

This is because we're creating temporary arrays in every recursive call.

## Time Complexity: O(n log(n))

## Additional Links

* [Animated Merge Sort Display](https://www.toptal.com/developers/sorting-algorithms/merge-sort)
