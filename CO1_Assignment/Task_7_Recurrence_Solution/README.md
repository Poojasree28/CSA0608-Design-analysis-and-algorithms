# TASK 7 – SOLVE THE RECURRENCE RELATION 
## 7.1 Introduction

Recursive Binary Search divides a sorted array into two halves and recursively searches only the half that may contain the required registration number. The recurrence relation derived in Task 6 is:

\[
T(n)=T\left(\left\lfloor\frac{n}{2}\right\rfloor\right)+c
\]

where \(c\) represents the constant amount of work performed in each recursive call.

The base case is:

\[
T(1)=c_0
\]

where \(c_0\) is a constant.

## 7.2 Selected Method: Iteration Method

The iteration method is suitable because each recursive call reduces the problem size by approximately half, making it easy to expand the recurrence repeatedly until the base case is reached.

## 7.3 Step-by-Step Solution

**Step 1: Write the recurrence relation**

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

**Step 2: Expand the recurrence**

Substitute the recurrence relation into itself:

\[
T(n)=T\left(\frac{n}{2}\right)+c
\]

Expanding \(T(n/2)\):

\[
T(n)=T\left(\frac{n}{4}\right)+c+c
\]

Therefore,

\[
T(n)=T\left(\frac{n}{4}\right)+2c
\]

Expanding again:

\[
T(n)=T\left(\frac{n}{8}\right)+3c
\]

After \(k\) expansions:

\[
T(n)=T\left(\frac{n}{2^k}\right)+kc
\]

**Step 3: Find the number of recursive levels**

The recursion stops when the problem size becomes 1.

\[
\frac{n}{2^k}=1
\]

Therefore,

\[
n=2^k
\]

Taking logarithms to base 2:

\[
k=\log_2 n
\]

**Step 4: Substitute the value of \(k\)**

Substituting \(k=\log_2 n\) into the expanded recurrence gives:

\[
T(n)=T(1)+c\log_2 n
\]

Since \(T(1)=c_0\):

\[
T(n)=c_0+c\log_2 n
\]

Here, \(c_0\) and \(c\) are constants.

**Step 5: Determine the final complexity**

Ignoring constant factors and lower-order terms:

\[
\boxed{T(n)=\Theta(\log n)}
\]

Therefore, the worst-case time complexity of Recursive Binary Search is \(O(\log n)\).

## 7.4 Interpretation of the Result

The solution shows that the number of recursive calls grows logarithmically as the number of student registration numbers increases. Each recursive call eliminates approximately half of the remaining search interval.

For a database containing 1,000,000 student records:

\[
\log_2(1,000,000)\approx19.93
\]

Thus, Binary Search requires at most approximately 20 iterations under the usual balanced-halving analysis.

This makes Recursive Binary Search efficient for large university databases, provided the registration numbers are sorted. Its auxiliary stack space grows as \(O(\log n)\) because each recursive call uses additional stack space.

## 7.5 Conclusion

The iteration method expands the recurrence relation until the base case is reached and reveals that the number of recursive levels is proportional to \(\log_2 n\). Hence, Recursive Binary Search has a worst-case time complexity of \(\Theta(\log n)\). Its logarithmic growth makes it suitable for searching large, sorted student databases.
