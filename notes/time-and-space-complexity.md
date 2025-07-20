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