# TASK 6 – FORMULATE THE RECURRENCE RELATION 

## 6.1 Introduction

A recurrence relation represents the running time of a recursive algorithm in terms of the running time of a smaller subproblem. Recursive Binary Search searches a sorted array by dividing the search interval into two halves and recursively processing only one half.

## 6.2 Identification of Components

**1. Input Size of the Original Problem**

Let \(n\) be the number of student registration numbers in the current search interval.

**2. Size of the Recursive Subproblem**

At each recursive call, Binary Search reduces the search interval to approximately half its previous size.

\[
n_{\text{new}}=\frac{n}{2}
\]

**3. Number of Recursive Calls**

The algorithm makes at most one recursive call at each level. It searches either the left half or the right half, not both.

**4. Work Performed Outside the Recursive Call**

Before making the recursive call, the algorithm:

- Checks whether the search interval is empty.
- Calculates the middle index.
- Compares the middle element with the search key.
- Determines which half should be searched next.

This work takes constant time, represented by \(c\).

**5. Base Case**

The recursion stops when either:

- The search interval is empty, meaning the key is absent (`low > high`).
- The key matches the middle element, meaning the search is successful.

Both conditions require constant time.

## 6.3 Derivation of the Recurrence Relation

From the algorithm, the total running time consists of the work performed in the current call and the time required to search one half of the interval.

Therefore,

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

where \(c\) is the constant work performed during each recursive call.

For the base case, when the search interval contains one element or becomes empty, the algorithm terminates in constant time:

\[
T(1)=c_0
\]

Here, \(c_0\) is a constant representing the base-case cost.

The recurrence relation can therefore be expressed as:

\[
T(n)=
\begin{cases}
c_0, & n\leq 1\\
T(\lfloor n/2\rfloor)+c, & n>1
\end{cases}
\]

The floor function accounts for the fact that the number of elements may not divide evenly into two halves.

## 6.4 Conclusion

Recursive Binary Search makes at most one recursive call per level, reducing the search interval by approximately half each time. The constant work performed outside the recursive call leads to the recurrence relation \(T(n)=T(\lfloor n/2\rfloor)+c\), with a constant-time base case. Solving this recurrence gives a worst-case time complexity of \(O(\log n)\).
