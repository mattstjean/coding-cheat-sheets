# Dynamic Programming
Dynamic programming is an optimization over plain recursion. Whenever we see a repeated recursive call for a smaller subproblem, we can optimize that recursive call with the help of dynamic programming. The idea is simply to store the result so that we don't have to re-compute the subproblem again and again.

Dynamic programming = recursion + memorization

The sample code below demonstrates returning the nth Fibonacci Number.

For the recursive method, we are calling the function for (n-1) and (n-2) until the base condition is hit, adding to get another new number. The recursive runtime is exponention (O(n^2)).

For the dynamic programming method, we store the previous values in the storage array. It has linear time complexity.

## Sample Code (Fibonacci)
```java
// Recursion
public int fib(int n) {
    if (n <= 1) {
        return n;
    }
    return fib(n - 1) + fib(n - 2);
}

// Dynamic Programming
public int fib(int n) {
    int storage[] = new int[n];
    storage[0] = 0;
    storage[1] = [1];
    for (int i = 2; i <= n; i++) {
        storage[i] = storage[i - 1] + storage[i - 2];
    }
    return storage[n];
}
```