# Recursion

([Back to menu](/README.md))

## About

Recursion is when a function calls itself. This requires at least O(n) memory usage for the stack storing the function calls. [Here](https://www.youtube.com/watch?v=k0bb7UYy0pY) is a great explanation of stack usage in recursive functions.

### Recursion Example

```java
public int fib(int n) {
    if (n <= 1) {
        return n;
    }
    return fib(n - 1) + fib(n - 2);
}
```

## Memoization

Memoization is often useful in recursion. This is when the results of a function call are remembered so they can be used again in later function calls. This is like caching your results to use again.

### Memoization Example

```java
public int fib(int n) {
 if (n <= 1) {
  return n;
 }
    int memo[] = new int[n];
    memo[0] = 0;
    memo[1] = [1];
    for (int i = 2; i <= n; i++) {
        memo[i] = memo[i - 1] + memo[i - 2];
    }
    return memo[n];
}
```

## Tail Recursion

Tail recursion is where calculations are performed first and then the recursive call is executed. Some programming languages, usually functional ones, optimize tail calls so they take up less room on the call stack.

### Tail Recursion Example

```java
public int fib(int n, int a, int b) {
    if (n === 0) {
        return a;
    }
    if (n === 1) {
        return b;
    }
    return fib(n - 1, b, a + b);
}

public int factorial(int n, int runningTotal) {
    if (n <= 1) {
        return runningTotal;
    }
    return factorial(n - 1, n * runningTotal);
}
```

## Practice Problems

[See how many ways given coins can add up to a sum](https://www.hackerrank.com/challenges/ctci-coin-change)
[See how many ways someone can walk up stairs](https://www.hackerrank.com/challenges/ctci-recursive-staircase)
[Generate the nth number in the fibonacci sequence](https://www.hackerrank.com/challenges/ctci-fibonacci-numbers)
[Find the number of ways numbers to the nth power can add up to a given number](https://www.hackerrank.com/challenges/the-power-sum)
[Add the digits of a number until there is only one digit left](https://www.hackerrank.com/challenges/recursive-digit-sum/)
[Calculate how fast an advertisement goes viral](https://www.hackerrank.com/challenges/strange-advertising)
