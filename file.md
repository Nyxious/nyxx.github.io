# Asymptotic Notation
- $O, \Omega, \Theta$
- Use limits to determine rate of growth:
	- $f(n) = O(g(n)) \Leftrightarrow \lim_{n \to \infty} \frac{g(n)}{f(n)} = c \text{ or } \infty$ 
	- $f(n) = \Omega(g(n)) \Leftrightarrow \lim_{n\to\infty} \frac{g(n)}{f(n)} = c \text{ or } 0$
	- $f(n) = \Theta(g(n)) \Leftrightarrow \lim_{n\to\infty} \frac{g(n)}{f(n)} = c$ 
- Arrange functions by rate of growth
	- Constants: 
		- $1$
		- $100$
		- $10000$
		- $1 + \frac1n$
		- $1 + \frac1{\log_2(n)}$
	- Polylogs: 
		- $\log_2(\log_2(n))$
		- $\log_2(n)$
		- $\log_2(n^k)$
		- $(\log_2(n))^k$
	- Polynomials:
		- $\sqrt[3]{n}$
		- $\sqrt{n}$
		- $2^{\log_2(n)}$
			- Equal to $n$, $2$ and $log_2$ cancel out.
		- $n$
		- $n \log_2(n)$
		- $\log_2(n!)$
		- $n\sqrt{n}$
		- $n^2$
		- $n^3$
		- $n^k$
	- Exponentials
		- $1.1^n$
		- $2^\frac{n}2$
		- $2^n$
		- $3^n$
		- $2^{2n}$
		- $4^n$
	- Super-exponentials
		- $(\log_2(n))^n$
		- $n^n$
		- $n!$
- Series
	- Arithmetic: $1 + 2 + 3 + ... + n = n(n+1)/2$
	- Geometric: $1 + 2^1 + x^2 + ... + 2^{n-1} = (2^n - 1)$
# Sorting and Searching
- Search
	- Linear: Worst case, average case $\Theta(n)$
	- Binary: Worst case, average case $\Theta(\log_2(n))$
- In place - at most constant # of elements of input array are ever stored outside the array - helps with space efficiency
- Insertion, merge, heap, and quick sort are based on using comparisons
- Counting, Radix, and Bucket sort use the properties of the keys being sorted.
- Stable - two equal elements retain their original order in sorted output
- Heaps and priority queues
	- Heap - data structure storing elements in a partial order
		- Max heap, min heap
	- Operations: left, right, parent max-heapify, build-max-heap, max-heap-maximum, max-heap,extract-max, max-heap-increase-key, max-heap-insert
	- used to implement priority queue ADT
- Algorithm design techniques
	- Brute-force
	- Incremental
	- Divide-and-conquer
	- Using a data structure to manage the information

# Practice:
Recursion
```
ADD(A)
1. sum = 0
2. for i = 1 to n
3.      sum = sum + A[i]
4. return sum
```

```
ADD(A, index)
// A[1:index] is the array
1. if index == 1
2.      return A[index]
3. else return ADD(A, index - 1) + A[index]
```

Analysis of looped one:
1. $\Theta(1)$
2. $\Theta(n)$
3. $\Theta(1)$
4. $\Theta(1)$
Total runtime: $\Theta(n$)

Analysis of recursive one:
$T(n) = T(n-1) + \Theta(1)$
- $T(n-1) = T(n-2) + \Theta(1)$
- $T(n) = T(n-2) + \Theta(1) + \Theta(1)$
- $T(n-2) = T(n-3) + \Theta(1)$
- $T(n) = T(n-3) + \Theta(1) + \Theta(1) + \Theta(1)$
- $T(n) = T(n-k) + k\Theta(1)$
- Stop when $k=n-1$
- $T(n) = T(n-(n-1)) + (n-1)\Theta(1)$
	- $=\Theta(1) + (n-1)\Theta(1)$
	- $=\Theta(n-1) = \Theta(n)$ 

$T(n) = T(n-1) + \Theta(1) \Rightarrow \Theta(n)$
$T(n) = T(n-1) + \Theta(n) \Rightarrow \Theta(n^2)$
$T(n) = 2T(\frac{n}2) + \Theta(n) \Rightarrow \Theta(n\log_2(n))$
$T(n) = T(\frac{n}2) + \Theta(1) \Rightarrow \Theta(log_2(n))$
# Pseudocode
```
FILL-SPREAD-SHEET(S, n)
1. for t = 1 to n
2.      for row = 1 to n
3.           for col = 1 to n
4.                recompute cell[row, col] in tab t 
```
Assume line 4 is $\Theta(1)$. The runtime would be $\Theta(n^3)$

```
RANDOM-SEARCH(A, n, k)
// Do k random searches in unsorted A[1:n] (values in 1:n)
1. for i = 1 to k
2.      key = random(1,n)
3.      location = LINEAR-SEARCH(A, key)
4.      print key, location
```

1. $\Theta(k) \Rightarrow \Theta(kn)$
2. $\Theta(1)$
3. $\Theta(n)$
4. $\Theta(1)$

Overall: $\Theta(kn)$
- $k = \Theta(n) \Rightarrow \Theta(n^2)$
- $k = \Theta(1) \Rightarrow \Theta(n)$

To make it faster, you could run a sorting function, and replace linear search with binary search
```
1. Sort(A)
2. for i = 1 to k
3.      key = random(1,n)
4.      location = BINARY-SEARCH(A, key)
5.      print key, location
```
1. $\Theta(n\log_2(n))$
2. $\Theta(k)$
3. $\Theta(1)$
4. $\Theta(\log_2(n))$
5. $\Theta(1)$

Overall: $\Theta(k\log_2(n) + n\log_2(n))$

