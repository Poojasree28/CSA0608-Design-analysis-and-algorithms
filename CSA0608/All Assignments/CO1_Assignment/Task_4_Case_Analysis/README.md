# TASK 4 – ANALYSE BEST, AVERAGE AND WORST-CASE BEHAVIOUR 
## 4.1 Introduction

Best-case, average-case and worst-case analyses describe how many operations a searching algorithm performs under different input conditions. The number of comparisons depends on the position of the required registration number and the arrangement of the data.

## 4.2 Linear Search

**Best Case:**

The best case occurs when the required registration number is present at the first position of the array. The algorithm finds the key in a single comparison.

\[
C_{\text{best}}(n)=1
\]

Therefore, the best-case time complexity is \(O(1)\).

**Average Case:**

Assume that the key is present and is equally likely to occur at any of the \(n\) positions. The algorithm performs between 1 and \(n\) comparisons.

\[
C_{\text{avg}}(n)=\frac{1+2+\cdots+n}{n}
\]

\[
C_{\text{avg}}(n)=\frac{n+1}{2}
\]

Therefore, the average-case time complexity is \(O(n)\).

**Worst Case:**

The worst case occurs when the key is at the last position or is not present in the array. The algorithm must examine all \(n\) elements.

\[
C_{\text{worst}}(n)=n
\]

Therefore, the worst-case time complexity is \(O(n)\).

**Why these differences occur:** Linear Search checks elements sequentially. The number of comparisons depends directly on how far the algorithm must travel through the array.

## 4.3 Iterative Binary Search

Binary Search requires the registration numbers to be sorted in ascending order.

**Best Case:**

The best case occurs when the required registration number matches the middle element in the first iteration. Only one key comparison is required.

\[
C_{\text{best}}(n)=1
\]

Therefore, the best-case time complexity is \(O(1)\).

**Average Case:**

For a successful search with keys distributed uniformly among the sorted positions, Binary Search follows different search depths depending on the key's position. Its average number of comparisons grows logarithmically with \(n\).

\[
C_{\text{avg}}(n)=O(\log n)
\]

**Worst Case:**

The worst case occurs when the key is absent or is found only after the maximum number of search iterations. Each iteration eliminates approximately half of the remaining elements.

After \(k\) iterations, the remaining search interval is approximately:

\[
\frac{n}{2^k}
\]

The search ends when this interval becomes empty or contains the key. Therefore, the maximum number of iterations is bounded by:

\[
C_{\text{worst}}(n)
\leq \lfloor\log_2 n\rfloor+1
\]

Hence, the worst-case time complexity is \(O(\log n)\).

**Why these differences occur:** Binary Search uses the middle element to decide which half to examine next. If the key is in the middle, the search finishes immediately; otherwise, the search continues through progressively smaller intervals.

## 4.4 Recursive Binary Search

Recursive Binary Search also requires sorted data and follows the same search decisions as Iterative Binary Search.

**Best Case:**

The best case occurs when the key matches the middle element during the first recursive call.

\[
C_{\text{best}}(n)=1
\]

Therefore, the best-case time complexity is \(O(1)\).

**Average Case:**

For a successful search across uniformly distributed key positions, the number of comparisons grows logarithmically because each recursive call reduces the search interval by approximately half.

\[
C_{\text{avg}}(n)=O(\log n)
\]

**Worst Case:**

The worst case occurs when the key is absent or requires the maximum number of recursive calls before it is found. The interval is repeatedly divided by two.

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

Solving the recurrence gives:

\[
T(n)=O(\log n)
\]

Therefore, the worst-case time complexity is \(O(\log n)\).

**Why these differences occur:** Recursive Binary Search eliminates half of the remaining search interval at every call. It has the same asymptotic search complexity as Iterative Binary Search, but it uses additional function-call stack space.

## 4.5 Comparison of Case Behaviour

| Algorithm | Best case | Average case | Worst case |
|---|---|---|---|
| Linear Search | 1 comparison, \(O(1)\) | \((n+1)/2\) comparisons, \(O(n)\) | \(n\) comparisons, \(O(n)\) |
| Iterative Binary Search | 1 comparison, \(O(1)\) | \(O(\log n)\) | \(O(\log n)\) |
| Recursive Binary Search | 1 comparison, \(O(1)\) | \(O(\log n)\) | \(O(\log n)\) |

## 4.6 Application to the University Database

For a database containing 1,000,000 student records and receiving 50,000 search requests per hour, Binary Search is more suitable when the records are maintained in sorted order.

For \(n=1,000,000\):

\[
\log_2(1,000,000)\approx 19.93
\]

Thus, Binary Search requires at most approximately 20 iterations under the usual balanced-halving analysis, whereas Linear Search may require up to 1,000,000 element checks.

This difference makes Binary Search more efficient for frequent searches, provided that the data is sorted and kept updated as new student records are added.

## 4.7 Conclusion

Linear Search performs well when the required registration number is near the beginning of the array, but its comparison count may increase linearly with input size. Iterative and Recursive Binary Search can find a middle element immediately and otherwise reduce the search interval by half. Both have logarithmic average- and worst-case search complexity, making them more suitable for large, sorted student databases.
