# JavaScript 07. Algorithms

Category: Algorightms
Created: October 17, 2022 4:29 PM
Status: Open
Updated: November 28, 2022 2:29 PM

# DP: Dynamic Programming

**Dynamic programming** is *an algorithmic optimization over plain recursion*. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming.

The idea is to simply store the results of subproblems so that we don’t have to re-compute them later when needed.

The properties the problem has to have to use dynamic programming paradigm:

- **Optimal Substructure**: A problem is said to have an optimal substructure if we can formulate a recurrence relation.
- **Overlapping Subproblem**: A Problem has an optimal substructure if we can formulate a recurrence relation for it.

> Steps how a Dynamic Program works:
> 
> 1. Breaks down the complex problem into several smaller problems
> 2. Computes a solution to each subproblem
> 3. After calculating the result, it remembers the solution of each subproblem - **Memoization**
> 4. Reutilize stored result to the next problem occurence
> 5. Apply the Memoization pattern to broader problems

---

In **Fibonacci series**, the recursive step is `fib(n) = fib(n-1) + fib(n-2)`. To calculate `fib(5)` we must first compute `fib(4)` and `fib(3)`. Then we’ll have to run yet another series of computation for the calculation of our subproblems.

![https://www.simplilearn.com/ice9/free_resources_article_thumb/Recursion_Call_Stack.png](https://www.simplilearn.com/ice9/free_resources_article_thumb/Recursion_Call_Stack.png)

In this *recursion call stack*, you can see that some **subproblems** have been repeated few times. This means Fibonacci series can be implemented using DP.

[Time and Space Complexity](Time%20and%20Space%20Complexity.md)

$$
Time: O(2^n)\ \ \ Space:O(n)
$$

```jsx
const fib = (n) => {
	if (n <= 1) return n
	return fib(n-1) + fib(n-2)
}
```

It is possible to apply a simple optimization to reduce the  time complexity from **exponential** to **polynomial**. 

---

## [Different Approaches of DP](https://www.enjoyalgorithms.com/blog/top-down-memoization-vs-bottom-up-tabulation)

There are **two** ways to solve and implement dynamic programming problems:

1. **Top-down** approach
2. **Bottom-up** approach

Both perform similarly in one way: *they use extra memory to store the solution to sub-problems*, avoid the recomputation and improve the performance by a huge margin. On another side, both of them are different in so many ways.

---

### Top-Down

In the top-down approach, we implement the solution naturally, *by using recursion* but modified to **save the result of each subproblem** in an array or hash table. This approach will first check whether it has previously solved the subproblem or not. If yes, it returns the stored value and saved the further calculation. It is the **momoized version** of a recursive solution; remembers the prevoius calculation.

```jsx
const fib = (n, memo = {}) => {
	if (memo[n]) return memo[n]
	if (n <= 1) return n
	memo[n] = fib(n-1, memo) + fib(n-2, memo)
  return memo[n]
}
```

$$
Time:O(n)\ \ \ \  Space:O(n)
$$

---

### Bottom-up

The bottom-up approach is just **reverse but an iterative version** of the top-down approach. It depends on a natural idea: the solution of any subproblem depends only on the solution of “smaller” subproblems. *We sort the subproblems by size and solve them in the order of smallest to largest*. When solving a particular subproblem, we have already solved all of the smaller subproblems its solution depends upon.

```jsx
const fib = (n) => {
	let Arr = [1,1]
	for (let i = 2; i <= n; i++){
		Arr[i] = Arr[i-1] + Arr[i-2]
	} 
	return Arr[n]
}
```

$$
Time:O(n)\ \ \ \  Space:O(n)
$$

---

- **TD is a recursive, BU is iterative**. In other words;
The Top-down approach assumes **the subproblems will be solved** using the smaller sub-problem **only once** using recursion.
In a reverse way, Bottom-Up **compose** the subproblems **solution iteratively** using the smaller sub-problems.
- TD is easy to implement because we just need a container (array, object) to store the results during recursion. In the BU approach, we need to define an iterative order to fill the container and take care of several boundary conditions.
- **TD is slower**, because of the overhead of the recursive calls, which cause a **call-stack**. If the recursion tree is very deep, we may run out of *stack space*, causing a crash in the program.
- Both guarantee the same time-complexity, except in unusual circumstanced where TD approach doesn’t actually recurse to examine all possible subproblems.
- TD starts from the large input size problem, reaches the smallest version of the problem (base case) and stores the subproblem solution from the base case to a larger problem.
In BU, we first store the solution for the base case and store the subproblem solutions in particular order from the base case to the larger sub-problem.