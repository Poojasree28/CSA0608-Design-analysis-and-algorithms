# TASK 3 – DERIVE THE TIME-COMPLEXITY FUNCTION MATHEMATICALLY 

## 3.1 Introduction

Time complexity measures how the execution time of an algorithm increases with the input size. Let \(n\) represent the number of student registration numbers in the database.

The basic operation considered in this analysis is the comparison between a registration number and the search key. The time-complexity function is derived by counting these comparisons.

## 3.2 Algorithm 1: Linear Search

**Step 1: Identify the input size**

Let \(n\) be the total number of student registration numbers.

**Step 2: Count the basic operation**

Linear Search compares the search key with each element, starting from the first element.

- Best case: The key is at the first position, requiring 1 comparison.
- Average case: Assuming the key is equally likely to occur at any position, the average number of comparisons for a successful search is:

\[
C_{\text{avg}}(n)=\frac{1+2+\cdots+n}{n}
\]

Using the arithmetic series formula:

\[
C_{\text{avg}}(n)=\frac{n(n+1)}{2n}
=\frac{n+1}{2}
\]

- Worst case: The key is at the last position or is absent, requiring \(n\) comparisons.

**Step 3: Derive the time-complexity function**

For the worst case:

\[
T(n)=an+b
\]

where \(a\) is the time required for each comparison and \(b\) represents fixed overhead.

Therefore,

\[
T(n)=an+b
\]

As \(n\) increases, the number of comparisons increases linearly.

**Step 4: Preprocessing cost**

Linear Search does not require sorting. Therefore,

\[
P(n)=0
\]

The total cost is:

\[
T_{\text{total}}(n)=P(n)+T(n)
\]

\[
T_{\text{total}}(n)=0+an+b
\]

**Result:** Best-case time complexity is \(O(1)\), and average- and worst-case time complexity are \(O(n)\).

## 3.3 Algorithm 2: Iterative Binary Search

**Step 1: Identify the input size**

Let \(n\) be the number of registration numbers in the sorted array.

**Step 2: Count the basic operation**

Binary Search compares the key with the middle element and eliminates approximately half of the remaining elements in each iteration.

After \(k\) iterations, the remaining search interval is approximately:

\[
\frac{n}{2^k}
\]

The search ends when the interval contains at most one candidate:

\[
\frac{n}{2^k}\leq 1
\]

Therefore,

\[
n\leq 2^k
\]

Taking logarithms to base 2:

\[
\log_2 n\leq k
\]

Hence,

\[
k\geq \log_2 n
\]

The maximum number of iterations is bounded by:

\[
k_{\max}=\lfloor\log_2 n\rfloor+1
\]

Thus, the number of key comparisons grows logarithmically.

**Step 3: Derive the time-complexity function**

Let \(a\) represent the cost per iteration and \(b\) represent fixed overhead.

\[
T(n)=a\lfloor\log_2 n\rfloor+b
\]

Ignoring constant factors and lower-order terms:

\[
T(n)=O(\log n)
\]

**Step 4: Preprocessing cost**

Binary Search requires the registration numbers to be sorted in ascending order.

If the records are initially unsorted and comparison-based merge sort is used, the sorting cost is:

\[
P(n)=O(n\log n)
\]

If the data is already sorted, the additional sorting cost is zero.

**Step 5: Overall cost**

For initially unsorted data, using merge sort:

\[
T_{\text{total}}(n)=O(n\log n)+O(\log n)
\]

Therefore,

\[
T_{\text{total}}(n)=O(n\log n)
\]

For already sorted data:

\[
T_{\text{total}}(n)=O(\log n)
\]

## 3.4 Algorithm 3: Recursive Binary Search

**Step 1: Identify the input size**

Let \(n\) represent the number of registration numbers in the sorted array.

**Step 2: Formulate the recurrence relation**

Each recursive call performs a constant amount of comparison and index-calculation work, then searches at most half of the remaining array.

Therefore, the recurrence relation is:

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

where \(c\) represents the constant work in each call.

The base case is:

\[
T(1)=c_0
\]

where \(c_0\) is a constant.

**Step 3: Solve the recurrence**

Expanding the recurrence:

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

\[
T(n)=T\left(\frac{n}{4}\right)+2c
\]

\[
T(n)=T\left(\frac{n}{8}\right)+3c
\]

After \(k\) expansions:

\[
T(n)=T\left(\frac{n}{2^k}\right)+kc
\]

The recursion reaches the base case when:

\[
\frac{n}{2^k}=1
\]

Therefore,

\[
k=\log_2 n
\]

Substituting this into the recurrence:

\[
T(n)=T(1)+c\log_2 n
\]

Since \(T(1)\) and \(c\) are constants:

\[
T(n)=O(\log n)
\]

**Step 4: Preprocessing cost**

Recursive Binary Search also requires sorted data.

If merge sort is required:

\[
P(n)=O(n\log n)
\]

If the array is already sorted:

\[
P(n)=0
\]

**Step 5: Overall cost**

For initially unsorted data:

\[
T_{\text{total}}(n)=O(n\log n)+O(\log n)
\]

Therefore,

\[
T_{\text{total}}(n)=O(n\log n)
\]

For already sorted data:

\[
T_{\text{total}}(n)=O(\log n)
\]

Recursive Binary Search also requires \(O(\log n)\) auxiliary stack space in the worst case.

## 3.5 Comparison of Mathematical Results

| Algorithm | Best-case comparisons | Worst-case comparisons | Search time | Preprocessing |
|---|---:|---:|---|---|
| Linear Search | 1 | \(n\) | \(O(n)\) worst case | None |
| Iterative Binary Search | 1 | \(\lfloor\log_2 n\rfloor+1\) | \(O(\log n)\) worst case | Sorting if needed |
| Recursive Binary Search | 1 | \(O(\log n)\) | \(O(\log n)\) worst case | Sorting if needed |

For Binary Search, the best case occurs when the key is the middle element of the current search interval. For Linear Search, the best case occurs when the key is the first element.

## 3.6 Conclusion

The mathematical analysis shows that Linear Search has linear worst-case time complexity because it may examine every registration number. Iterative and Recursive Binary Search have logarithmic worst-case search complexity because each step reduces the search interval by half. However, Binary Search requires sorted data. When sorting is necessary, its preprocessing cost must be included in the overall analysis. Therefore, Binary Search is particularly efficient when the database is already sorted or when the sorting cost can be shared across many searches.
