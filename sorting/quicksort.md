# Quicksort
Quicksorting is an algorithm in which a random element is selected from the array and then the array is partitioned so that all the numbers less than the element are placed before it and the ones greater than it are placed after it. This algorithm is efficient since swapping two elements in an array is usually a very quick process and it doesn't require using another data structure in intermediate steps. If the randomly selected element isn't near the median, quicksorting can be inefficient.

Similar to Merge Sort, quicksort uses divide-and-conquer so it is a recursive algorithm. In merge sort, the divide step doesn't do too much while the bulk of the work takes place in the combine step. In Quicksort, the bulk of the work takes place in the divide step while the combine step does nothing.

Quicksort works in place and its worst-case run time is as bad as selection sort and insertion sort (n^2). But the average-case run time is as good as merge sort's (nlogn). In practice, quicksort outperforms merge sort, and significantly outperforms selection sort and insertion sort.

## Algorithm
1. Choose an element from the list (pivot) and use it to divide the list into two sub-lists.
2. Reorder all elements around the pivot - the ones with smaller values are placed before it, and the elements greater than the pivot are placed after it. After this step, the pivot is in its final position.
3. We apply the above steps recursively to both sub-lists on the left and right of the pivot.

## Sample Code
```java
public void quickSort(int arr[]) {
	int start = 0;
	int end = arr.length;
	quickSort(arr, start, end);
}
public void quickSort(int arr[], int start, int end) {
	if (start < end) {
		int pivot = partition(arr, start, end);

		quickSort(arr, start, pivot - 1);
		quickSort(arr, pivot + 1, end);
	}
}

private int partition(int arr[], int start, int end) {
	int pivot = arr[end];
	int pivotFinalPos = start - 1;

	for (int j = start; j < end; j++) {
		if (arr[j] <= pivot) {
			swap(arr, pivotFinalPos++, j);
		}
	}
	swap(arr, pivotFinalPos + 1, end);
	return pivotFinalPos + 1;
}

private void swap(int arr[], int firstPos, int secondPos)  {
	int temp;
	temp = arr[firstPos];
	arr[firstPos] = arr[secondPos]; 
	arr[secondpos] = temp; 
}
``

## Space Complexity: O(log(n))

## Time Complexity
| Best          | Average     | Worst |
| --------------|:-----------:| -----:|
| O(n log(n))   | O(n log(n)) | O(N^2)|

* [Animated Quick Sort Display](https://www.toptal.com/developers/sorting-algorithms/quick-sort)
