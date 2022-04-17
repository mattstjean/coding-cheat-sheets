# Bubble Sort

Bubble sorting is one of the simplest sorting algorithms. In order to implement this sort, the script starts on the left of the array and swaps elements that are next to each other if they are in the wrong order. This usually requires multiple passes, unless the array is already sorted.

## Sample Code - quadratic, brute force
This will always run O(n^2) even if the array is sorted.
```java
public void bubbleSort(int arr[]) {
	for (int i = 0; i < arr.length - 1; i++) {
		for (int j = 0; j < arr.length - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				swap(arr, j, j + 1);
			}
		}
	}
}
private void swap(int arr[], int firstPos, int secondPos)  {
	int temp;
	temp = arr[firstPos];
	arr[firstPos] = arr[secondPos]; 
	arr[secondpos] = temp; 
}
```
## Sample Code - optimized, 
```java
public void bubbleSort(int arr[]) {
	int temp;
	boolean swapped;
	for (int i = 0; i < arr.length - 1; i++) {
		swapped = false;
		for (int j = 0; j < arr.length - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				swap(arr, j, j + 1);
				swapped = true;
			}
		}
		if (swapped === false) {
			break;
		}
	}
}

```

## Space Complexity: O(1)

## Time Complexity
| Best | Average| Worst |
| -----|:------:| -----:|
| O(N) | O(N^2) | O(N^2)|

## Additional Links
* [Animated Bubble Sort Display](https://www.toptal.com/developers/sorting-algorithms/bubble-sort)
