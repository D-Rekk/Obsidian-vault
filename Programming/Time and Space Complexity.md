# Time and Space Complexity

Generally, there’s always more than one way to solve a problem in computer science. Therefore, it is highly required to use a method to compare the solutions in order to judje which one os more optimal. The method must be:

- Independent of the machine and its configuration
- Shows a direct correlation with the number of inputs
- Can distinguish two algorithms clearly *without ambiguity*

There are two such methods used: **Time Complexity** and **Space Complexity**

---

## Time Complexity

> The time complexity of an algorithm quantifies the amount of **time** taken by an algorithm to run as a function of the length of the given input.
> 

The *time to run* is a **function** of the length of the input, **not the actual execution time of the machine** on which the algorithm is runnin on.

In order to calculate time complexity of an algorithm it is assumed that: 

- A costant time **C** is taken to execute on operation
- The total operation for an input length of **N** are calculated.

Consider an example to understand the process of calculation: 
Suppose a problem is to find whether a pair **(X,Y)** exists in an array **A** of **N** elements whose sum is **X+Y == Z**. 

The simples idea is to consider every pair and check if it satisfies the condition or not:

```jsx
function findPair (A, N, Z) {
	for(let i=0; i<n; i++)
		for(let j=0; i<j; j++)
			if (i!=j && a[i] + a[j] == z) return true;
	return false;
}
//a = [1, -2, 1, 0, 5 ]; z = 9; n = a.length
```

Assume that each operation in the computer takes approximately constant time, let it be **c**. The number of lines of code executed actually depends on the value of **Z**. During analyses of the algorithm, mostly the worst-case scenario is considered(when no pairs of element equals Z). In the worst case:

- **N*C**(length x constant time) operations are required for input.
- The outer loop **i** runs **N** times.
- For each **i**, the inner loop **j** runs **N** times

Total Execution Time is **N*c + (N*N*c) + c**. Let’s ignore the lower order terms since are relatively insignificant for large input, therefore only the highest order term is taken ( without constant) which is **N*N** in this case.

Different notation are used to describe the limiting behavior of a function, but since the worst case is take, [big-O notation](https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/) will be used to represent the time complexity. Hence, the time complexity is **O(N²)** for the above algorithm. 

Note: Time complexity is solely based on the number of elements in the array, so if the length of the array increases, so does the execution time.

---

### Space Complexity

> The time complexity of an algorithm estimates the amount of **space** required by an algorithm to run as a function of the length of the given input.
> 

Consider an example: find the frequency of elements in an array:

```jsx
// Function to count frequencies of array items
function countFreq(arr, n) {
    let freq = new Map();
    arr.sort((a, b) => a - b)
 
    // Traverse through array elements and
    // count frequencies
    for (let i = 0; i < n; i++) {
        if (freq.has(arr[i])) {
            freq.set(arr[i], freq.get(arr[i]) + 1)
        } else {
            freq.set(arr[i], 1)
        }
    }
    // Traverse through map and print frequencies
    for (let x of freq)
        document.write(x[0] + " has " + x[1] + "<br>");
}
```

 Two arrays of length **N**(arr and sortedArr), and variable **i** are used in the algorithm, so the toal space used is **N*c** + **N*c** + **1*c** which equals to **2(N*c)+ c**, where c is a unit space taken. For many input, constant **c** is insignificant, and it can be said that the space complexity is **O(N)**.