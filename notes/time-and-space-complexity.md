# Why we need to learn time complexity?

Understanding time complexity is essential because it lets us:

1. Choose the Right Algorithm

- Different algorithms solve the same problem but perform very differently as input sizes grow.

- Knowing their time complexities (e.g., O(1), O(n), O(n log n), O(n²)) helps you pick the one that will scale best.

2. Optimize Code for Performance

- Even if your solution is correct, a poorly chosen algorithm can be so slow that it’s unusable on real-world data.

- By analyzing how your code’s running time grows, you can pinpoint bottlenecks and refactor the expensive parts.

3. Improve User Experience

- Faster code means snappier applications. Users expect instant responses—no one wants to wait for a spinner.

- When your backend or frontend routines run in optimal time, pages load quicker and tasks complete smoothly.

4. Save Resources

- Efficient algorithms consume less CPU time and battery power—critical on mobile devices and in large-scale servers.

- Lower resource use also reduces hosting costs and environmental impact.

5. Make Informed Trade-Offs

- Sometimes you’ll trade space for speed (or vice versa). Understanding time complexity lets you balance these trade-offs thoughtfully.

- You can justify design decisions with concrete performance estimates.

In short, learning time complexity isn’t just academic—it guides you toward writing code that remains fast and responsive as your app and its user base grow.


# What is time complexity

Time complexity is a way to describe how the number of steps your program takes grows as the size of its input grows—no matter what computer you’re on. In other words, instead of worrying about actual seconds or your machine’s speed, you just count how many “basic actions” your code does.

Let’s look at following example:

```c++
for(int i=0; i<n; i++>){
  cout << "Hello World";
} 
```

Because the loop does one print each time through, the total number of prints (and roughly the total steps) grows in direct proportion to n. We call this a linear relationship.

In simple terms:

- When you double n, you double the work.

- When you triple n, you triple the work.

So we say the time complexity is “linear in n” (often written as O(n) in more technical jargon). 

That’s all there is to it! The bigger your input (n), the more steps you’ll take—exactly n steps in this case.


# How to calculate time complexity

1. What each notation means
- Ω (Omega) notation – the best-case scenario.
- Θ (Theta) notation – the average-case scenario.
- O (Big O) notation – the worst-case scenario.

2. Example: Searching for an item in an array
Imagine you look for a number in a list, one by one:

```c++
int findIndex(int arr[], int n, int target) {
  for (int i = 0; i < n; i++) {
    if (arr[i] == target) {
      return i;      // found it
    }
  }
  return -1;         // not found
}
```
- Best case (Ω):
  - The item is at the very first position (i = 0).
  - You check once, stop.
  - Ω(1) (“constant time”)

- Worst case (O):
  - The item is at the last position or not in the list.
  - You check all n elements.
  - O(n) (“linear time”)

- Average case (Θ):
  - On average you’ll find it halfway through.
  - You check roughly n/2 elements.
  - Θ(n) (we still call it linear time)

3. Rules for calculating time complexity

- Always use the worst-case (Big O) when you report time complexity.
- Ignore constant factors (multiplying by 2, adding 5, etc.).
  - e.g. 2·n or n + 10 both become O(n).

Putting it all together in your style

- When you search an array, the best case is Ω(1), average is Θ(n), and worst case is O(n).

- To calculate time complexity, look at how many steps grow when n grows, drop constants, and report the worst-case with Big O.

That’s it—easy as counting the steps your code takes and focusing on how they grow with n!

# Linear complexity

When we say an algorithm runs in linear time, we mean its steps grow one-for-one with the size of the input (n). In notation, that’s O(n).

1. How to recognize and calculate linear complexity
Look for a single loop (or something that visits each item once).

Count the work inside the loop—if it’s a fixed amount per item, the total work is “that amount × n.”

Drop constant factors—we don’t care about the “× 2” or “+5.”

Result: O(n)

2. Simple examples

### Printing every element

```c++ 
for (int i = 0; i < n; i++) {
  cout << arr[i] << endl;
}
```
- Steps per iteration: 1 print
- Total steps: 1 × n → O(n)

### Summing an array

```c++
int sum = 0;
for (int i = 0; i < n; i++) {
  sum += arr[i];
}
```
- Steps per iteration: 1 addition + 1 assignment
- Total steps: ~2 × n → drop “2” → O(n)

### Counting occurrences

```c++
int count = 0;
int target = 8;
for (int i = 0; i < n; i++) {
  if (arr[i] == target) {
    count++;
  }
}
```
- Steps per iteration: 1 comparison + (maybe) 1 increment
- Total steps: ~2 × n → drop “2” → O(n)

### Combining linear steps

If you have two separate loops one after another, it’s still O(n):

```c++
for (int i = 0; i < n; i++) {
  cout << arr[i] << endl;
}
for (int j = 0; j < n; j++) {
  cout << arr[j] << endl;
}
```
- Work: n steps + n steps = 2n → drop “2” → O(n)

3. Why ignore constants and lower-order terms?

- If you did 3 loops, you’d get 3n steps—still O(n).

- If you add a small extra step before the loop (like setting up a counter), that’s a fixed cost and doesn’t change the “grow-rate” as n gets big.


### In a nutshell

- O(n) = “work grows directly with n.”
- **Find any loop that goes 0 → n, count its fixed work per step, multiply by n, then ignore constant multipliers.”



# Logarithmic complexity

When an algorithm cuts the problem size by a constant factor each time—rather than marching through every item—it runs in logarithmic time, written O(log n). That usually happens when your loop variable multiplies or divides itself each step.

1. What “logarithmic time” means

- O(log n) means that each extra step multiplies (or divides) how far you go.
- Doubling or halving your progress each loop means you only need to visit about log₂ n steps before you’ve covered everything.
- As n grows, log n grows very slowly.

2. How to spot logarithmic loops

- Multiplying the loop index by a constant (e.g. i *= 2) each time.
- Dividing the loop index by a constant (e.g. i /= 2) each time.
- In both cases, you stop once you’ve stepped past your limit (≥ n or ≤ 1).

3. Example: growing by multiplication

```c++
void multiplyLoop(int n) {
  for (int i = 1; i < n; i *= 2) {
    cout << i << "\n";
  }
}
```
- i values: 1, 2, 4, 8, 16, …
- You stop when i ≥ n.
- Number of prints ≈ how many times you can double 1 before passing n, i.e. log₂ n.
- Time complexity: O(log n)

4. Example: shrinking by division

```c++
void divideLoop(int n) {
  for (int i = n; i > 0; i /= 2) {
    cout << i << "\n";
  }
}
```
- i values: n, n/2, n/4, n/8, …
- You stop when i ≤ 0 (actually when it drops below 1).
- Number of prints ≈ how many times you can halve n before it reaches 1, again log₂ n.
- Time complexity: O(log n)

5. Why the base doesn’t matter

- Whether you double (×2) or triple (×3), you’ll still get O(log n)—just a different constant factor.
- We ignore those constants when we write O(log n).

### In short

- Logarithmic loops jump in chunks (× or ÷ each time).
- They need about log n steps to finish.
- That’s much faster than doing n steps when n is big.

# Square-Root Time Complexity

Sometimes an algorithm doesn’t run in linear time (O(n)) or logarithmic time (O(log n))—it runs in “square-root time,” written O(√n). You’ll see this pattern whenever you only need to explore up to the square root of your input size, rather than the whole thing.

1. When √n shows up
- √n grows more slowly than n but faster than log n.
- It arises whenever you can exploit a mathematical property—like symmetry around √n—to cut your work dramatically.
- Common example: finding all divisors of an integer.

2. Brute-force vs. √n optimization

2.1 Brute-force search (O(n))

To list all divisors of n, you could check every integer from 1 through n:

```c++
vector<int> divisors;
for (int i = 1; i <= n; i++) {
    if (n % i == 0) {
        divisors.push_back(i);
    }
}
```

- Steps: n checks → O(n)

- Problem: If n = 10^9, that’s a billion mod operations—too slow.

2.2 √n search (O(√n))

Observe that divisors come in pairs `(i, n/i)`. Once you pass √n, you’re just re-visiting the other half of the pairs. So you only need to loop while `i * i <= n`:

```c++
vector<int> divisors;
for (int i = 1; i * i <= n; i++) {
    if (n % i == 0) {
        divisors.push_back(i);
        if (i != n / i)            // avoid double-counting perfect square root
            divisors.push_back(n / i);
    }
}
sort(divisors.begin(), divisors.end());
```
- Condition: `i * i <= n`
- Why it works:
  - If `i` ≤ √n, then `n/i` ≥ √n.
  - Every divisor > √n is paired with one < √n.

- Steps: about √n checks → O(√n)

3. Example in action
Let n = 36:

- √36 = 6, so the loop runs i = 1,2,3,4,5,6 (six iterations).
- On each iteration we check:
  - i=1 → divisors 1 and 36
  - i=2 → divisors 2 and 18
  - i=3 → divisors 3 and 12
  - i=4 → divisors 4 and 9
  - i=5 → no new divisor
  - i=6 → divisors 6 (since 6 == 36/6, we add only once)

- Total checks: 6 instead of 36.

4. Calculating √n complexity
- Identify that your work pairs off beyond √n.
- Switch your loop to `for (i = 1; i * i <= n; i++)`.
- Count steps: you’ll execute ~√n iterations.
- Report: O(√n) in worst-case.

5. Why √n matters

- Scales to large inputs: If n = 10¹², √n = 10⁶—one million checks vs. a trillion.
- Common in number-theory tasks: primality tests, divisor sums, factorization steps.
- Practical speed-ups: Brute-force becomes usable for much bigger n.

6. Five Real-World Use Cases of O(√n) Algorithms
Here are five practical scenarios where you only need to do about √n work—turning otherwise huge scans into something much faster:

1. Primality Testing with Trial Division

- To check if a number `n` is prime, you only need to test divisibility by integers up to √n.
- Once you reach any divisor ≤ √n, you’ve proven compositeness; if none divide, `n` must be prime.
- This is exactly the same `for (i * i <= n; i++)` pattern we saw for divisors—but you stop as soon as you find one.

2. Divisor Enumeration

- As shown earlier, listing all factors of n can be done in O(√n) by pairing each small divisor `i` (≤√n) with its counterpart `n/i`.

- Instead of n checks, you do only about √n checks, then emit two results per hit.

3. Small-Key RSA Factorization

- In cryptanalysis of weak RSA keys (e.g. 32- or 64-bit), attackers use trial division up to √n to find one of the prime factors.

- Even though √n is large for modern keys, for small educational keys this method works in minutes instead of centuries.

4. Range-Sum Queries via √-Decomposition

- Suppose you have an array of length N and need to answer “sum from L to R” queries, plus occasional updates.

- By precomputing sums of blocks of size B = √N, each query can look at at most two partial blocks plus O(√N/B)=O(√N) whole-block sums—overall O(√N) per query.

- This trades O(N) rebuilds for O(√N) queries and updates, a big win when N is huge but the number of queries is larger.

5. Collision Detection in 2D Games

- If you have N moving objects on a 2D map, naively checking every pair for overlap is O(N²).

- Instead, divide the world into a √N×√N grid: on average, each object shares a cell with only O(√N) neighbors.

- You only test collisions against those √N possible overlaps, yielding O(N·√N) overall or O(√N) per object.

6. Five Real-World Software Use Cases of O(√n)
Here are five concrete examples where production-grade software exploits √n algorithms to stay efficient:

1. Cryptographic Key Validation (OpenSSL, BoringSSL)

- What happens: When generating or validating RSA keys, the library does a quick trial-division pass over small prime candidates up to √n before switching to more advanced tests.

- Why √n: Checking divisibility by every integer up to √n weeds out common composite keys extremely fast, avoiding the huge cost of full-fledged primality proofs on obviously non-prime numbers.

2. Primality Checks in Math Libraries (Sympy, GMP)

- What happens: Python’s Sympy and the GMP (C/C++) libraries implement an isprime(n) function that first does a loop

```python
for i in range(2, int(sqrt(n))+1):
    if n % i == 0:
        return False
return True
```

- Why √n: This inexpensive pass catches most composites quickly. Only numbers that survive up to i·i > n need more expensive probabilistic or deterministic tests.

3. Piece Tables / Ropes in Text Editors (VS Code, IntelliJ IDEA)

- What happens: To support fast insertion, deletion, and substring operations on very large files, editors often break the document into chunks of size ~√N.

- Why √n: Operations that need to scan or splice text only touch one or two chunks—O(√N) work—instead of re-writing the entire buffer of length N.

4. Spatial Hashing for Collision Detection (Unity, Unreal Engine)

- What happens: A scene with N objects is partitioned into a grid of roughly √N×√N cells. Each object is hashed into its cell, and collision checks are performed only among the handful of neighbors in that cell.

- Why √n: Instead of O(N²) pairwise checks, each object looks at O(√N) potential collisions, yielding an overall O(N·√N) workload—vastly faster in dense scenes.

5. √-Decomposition in Analytics / Time-Series Engines (Elasticsearch, ClickHouse)

- What happens: To accelerate range-sum or point-update queries over a huge array of log data, the system divides the array into B = √N blocks and precomputes each block’s sum.

- Why √n: Each query touches at most two partial blocks plus O(√N) whole blocks, giving O(√N) query time. That’s a big win when N is in the billions and queries arrive in real time.

### In short: whenever your problem has a natural pairing or symmetry around √n, you can often reduce an O(n) scan to O(√n) by stopping your loop at `i * i <= n`. This simple trick turns billion-step loops into million-step loops—and that difference is huge in practice.

# Quadratic Time Complexity (O(n²))
When an algorithm’s running time grows in proportion to the square of its input size, we call it quadratic time, written O(n²). This often feels like the difference between “usable for hundreds” and “unusable beyond a few thousand.”

1. When O(n²) arises
- Nested loops over the same data set
- Not when you run two independent loops back-to-back (that’s still O(n))
- Typical pattern:
```c++
for (int i = 0; i < n; i++) {
  for (int j = 0; j < n; j++) {
    // constant-time work here
  }
}
```
  1. Outer loop: n iterations
  2. Inner loop: n iterations per outer → n × n = n² total iterations

2. Nested vs. Sequential Loops
Pattern	                      Steps	      Complexity
Two loops one after another:  n + n = 2n	  O(n)
Two nested loops:	            n × n = n²	  O(n²)

Key point: Only nested iterations multiply their costs.

3. Calculating O(n²)
- Count the loops: two loops over n → n×n steps.
- Drop constants: 1·n² → O(n²).
- Ignore lower-order terms: n² + 5n + 10 → O(n²).

4. Five Practical Use Cases
  1. Bubble Sort / Selection Sort
  - Compare and possibly swap every pair in the list.
  - ≈ n²/2 comparisons → O(n²).

  2. Pairwise Distance Matrix
  - Computing distances between every pair in a set of n points.
  - Useful in small-scale clustering prototypes.

  3. Naive String Matching
  - For each position in the text (n) compare up to pattern length (m≈n) → O(n·m) ≈ O(n²).
  
  4. Checking All Pairs for Duplicates
  - Compare each element to every other → O(n²).
  - Common in small scripts or one-off data-cleaning tasks.

  5. Matrix Multiplication (Naïve)
  - Three nested loops, but if you fix one dimension equal to n, two loops dominate → O(n²) per output row (overall O(n³) for square matrices).

5. Five Real-Life Software Use Cases

  1. Spreadsheet “Find Duplicates” Macro
  - A VBA macro that does two nested loops over all rows to highlight repeated entries.

  2. Naïve CSV Join in a Script
  - Python script that loads two small CSVs into lists and does nested loops to match keys, rather than using a hash or database join.

  3. Basic Brute-Force Collision in Game Prototypes
  - Early prototype in Unity or Godot where each object checks collision against every other object, fine for <100 entities.

  4. Simple Recommendation Engine
  - For a small set of items, compute similarity score between every pair to suggest “people who liked X also liked Y.”

  5. Legacy UI Rendering Engines
  - Older browsers or custom widgets that naïvely compare each style rule against each DOM element (n rules × n elements) before applying styles.

### Conclusion

Quadratic algorithms are intuitive and easy to implement but rapidly become impractical as n grows. Whenever you spot nested loops over the same data, ask:

- Can I break the work apart?
- Use hashing or sorting to reduce comparisons (e.g., from O(n²) to O(n log n) or O(n)).
- Leverage data structures (sets, maps) or divide-and-conquer techniques to avoid the full n×n scan.

Mastering the difference between O(n), O(n²), and beyond helps you choose the right approach—and keep your software running smoothly, even on large inputs.

# Linearithmic Time Complexity (O(n log n))
Linearithmic algorithms combine linear and logarithmic growth: their running time grows in proportion to n × log n. You see this pattern whenever you have a loop over n items and, inside it, a process that itself takes O(log n) time.

1. Where the Name Comes From
- Linear (n): you process each of the n elements once (or a constant number of times).
- Logarithmic (log n): within that per-element work, you perform an operation that shrinks the problem by a constant factor each step—like binary search or heap operations.
- Multiply the two to get n × log n.
- Hence “linearithmic”—a mash-up of linear and logarithmic.

2. Explanation: A Nested Logarithmic Loop
Imagine you have:
```c++
for (int i = 0; i < n; i++) {       // O(n) outer loop
    int j = n;
    while (j > 0) {                 // O(log n) inner loop
        // do O(1) work
        j /= 2;
    }
}
```
- Outer loop runs n times.
- Inner loop halves `j` each iteration, so it runs about log₂ n steps before hitting 0.
- Total steps ≈ n × log₂ n → O(n log n).

3. Five Practical Use Cases
  1. Sorting Large Arrays
  - Algorithms like mergesort, heapsort, and quicksort (average case) run in O(n log n).

  2. Binary Heap Operations
  - Building a heap takes O(n), but each insert or extract takes O(log n), so sorting via heap (heapsort) is O(n log n).

  3. Balanced Binary Search Trees

  - Inserting or deleting n items into an AVL or red-black tree costs O(log n) each, totalling O(n log n).

  4. Divide-and-Conquer on Coordinates
  - Finding the closest pair of points in 2D runs in O(n log n) by recursively splitting and merging.

  5. Fast Fourier Transform (FFT)
  - The Cooley–Tukey FFT algorithm computes discrete Fourier transforms in O(n log n).

4. Five Real-Life Software Use Cases
  1. Standard Library Sort (C++ `std::sort`, Java `Arrays.sort`)
  - Under the hood: introsort (quick + heap + insertion) guarantees O(n log n) worst-case.

  2. Python’s Timsort (`list.sort()`, `sorted()`)
  - A hybrid stable sort used by CPython, optimized for real-world data, runs in O(n log n).

  3. Elasticsearch / Lucene Indexing
  - Sorting search results by relevance or timestamp uses O(n log n) algorithms to merge postings lists.

  4. Game Engines’ Scene Graph Updates
  - Rebalancing spatial partition trees (octrees or BVH) after object moves often costs O(n log n).

  5. Database ORDER BY and GROUP BY
  - SQL engines sort result sets using external merge-sort or quicksort variations, costing O(n log n) for large datasets.

5. Conclusion

Linearithmic complexity sits at the sweet spot between simple linear scans and more expensive quadratic routines. Whenever you can structure your algorithm to do a logarithmic-time subtask inside a linear sweep—or apply divide-and-conquer—the result is O(n log n). These algorithms power everything from efficient sorting and search to advanced signal processing and database engines, making them a fundamental tool in any software engineer’s toolkit.


# Comparison of best worst complexity

### Comparison of Operation Counts for n = 1000

Complexity	            Big-O	                  Approx. Work (n = 1000)
Constant	              O(1)	                        1
Logarithmic	            O(log n)	                    log₂(1000) ≈ 10
Square-Root	            O(√n)	                        √1000 ≈ 32
Linear	                O(n)	                        1000
Linearithmic	          O(n log n)	                  1000·10 = 10000
Quadratic	              O(n²)	                        1000² = 1000000

### Ordering from “Fastest” to “Slowest” (for n = 1000)

- Constant (1)
- Logarithmic (~10)
- Square-Root (~32)
- Linear (1000)
- Linearithmic (10000)
- Quadratic (1000000)

### Conclusion

- Best-case algorithms (O(1), O(log n), O(√n)) remain extremely fast even as n grows—adding another factor of 10 or 100 makes almost no practical difference.
- Middle-of-the-road (O(n), O(n log n)) scale well for moderate n but can become noticeable at very large inputs.
- Worst-case (O(n²) and above) quickly become infeasible: at n = 10⁶, a quadratic algorithm would need ~10¹² steps—far beyond any real machine’s capability.

Takeaway: always strive for the lowest-order complexity you can—especially for large data—because what looks “small” at n=1000 explodes into impossibility at higher scales.


# Calculating Real Running Time from Time Complexity
Understanding how to turn a Big–O bound into an actual wall-clock estimate is crucial when you’re working under strict time limits (like 1 second per test). Let’s walk through a concrete example and see how to decide if your approach will finish in time.

1. The 10⁷-Operations-Per-Second Rule of Thumb

- Empirical fact: A single-threaded C++ program can safely be assumed to execute on the order of 10⁷ “basic operations” per second.

- Conversion formula:

estimated_time (s) ≈ estimated_operations/10^7

 
2. Problem Statement (Codeforces-Style)

```text
Binary search
Time limit per test 1 second
Memory limit per test 256  mb

Given 2 numbers N and Q, array A of N number and Q queries each one contains a number X.
For each query print a single line that contains "found" if the number X exists in array A otherwise, print "not found".

Input 
First line contains two number N, Q(1<=N, Q<=10^5)
Second line contains N numbers (1<=Ai<=10^9)
next Q lines contains X(1<=X<=10^9)

Output 
Print the answer for each query in a single line. 

Example
input
5 3
1 5 4 3 2
5
3
6
Output
found 
found 
not found
```
- Input limits
  - N, Q up to 10⁵
  - Array A of N integers
  - Then Q queries, each a number X
- Task
  - For each X, print “found” if X ∈ A, else “not found.”
- Constraints
  - Time limit: 1 second
  - Memory limit: 256 MB

3. Brute-Force Solution (O(N·Q))

```cpp
// Read N, Q, and A[]
int N, Q;
cin >> N >> Q;
vector<int> A(N);
for (int i = 0; i < N; i++) cin >> A[i];

// For each query, scan the entire array
while (Q--) {
    int X; 
    cin >> X;
    bool found = false;
    for (int i = 0; i < N; i++) {
        if (A[i] == X) {
            found = true;
            break;
        }
    }
    cout << (found ? "found\n" : "not found\n");
}
```

- Work per query: up to N comparisons
- Total work: N comparisons × Q queries → O(N·Q)

4. Estimating the Operation Count
- Worst-case N = Q = 10⁵
- Comparisons ≈ 10⁵ × 10⁵ = 10¹⁰
- Time ≈ 10¹⁰ / 10⁷ = 10³ seconds ≈ 16.7 minutes

Clearly, Brute-Force (O(N·Q)) will not finish under a 1 second limit when N and Q are at their maximum.

5. Conclusion: Pick a Faster Algorithm
Because brute-force is too slow, we need something like Binary Search:

- Sort A in O(N log N) → ~10⁵·17 = 1.7·10⁶ ops
- Answer each query in O(log N) → 10⁵·17 = 1.7·10⁶ ops
- Total ≈ 3.4·10⁶ ops → 0.34 s

This fits comfortably within a 1 second time limit.

### Key Takeaway

- Translate your Big-O into an estimated operation count using the input bounds.
- Divide by 10⁷ ops / s to predict seconds needed.
- Decide if that meets your time limit—if not, choose a more efficient algorithm!












