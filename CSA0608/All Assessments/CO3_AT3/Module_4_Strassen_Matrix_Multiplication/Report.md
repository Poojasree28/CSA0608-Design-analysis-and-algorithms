# MODULE 4 – STRASSEN'S MATRIX MULTIPLICATION FOR RECOMMENDATION SCORES

## 1. Aim

To design and implement Strassen's Matrix Multiplication using the Divide-and-Conquer technique to calculate product recommendation scores efficiently by multiplying two matrices.

## 2. Problem Statement

KartIQ calculates recommendation scores for every product and customer segment.

The score matrix is calculated using:

\[
C = A \times B
\]

**Where:**

- A represents the segment-feature preference matrix.
- B represents the feature-product matrix.
- C represents the final recommendation score matrix.

In production, both matrices have dimensions **1024 × 1024**.

Conventional matrix multiplication requires O(n³) time. Strassen's algorithm reduces the number of recursive matrix multiplications from eight to seven.

### Sample Matrices

**Matrix A:**

\[
A =
\begin{bmatrix}
1 & 7\\
3 & 5
\end{bmatrix}
\]

**Matrix B:**

\[
B =
\begin{bmatrix}
1 & 3\\
7 & 5
\end{bmatrix}
\]

## 3. Algorithm Explanation

Strassen's algorithm is a Divide-and-Conquer matrix multiplication technique.

It divides two square matrices into four smaller submatrices and performs seven recursive multiplications instead of eight.

### Three Main Operations

**1. Divide**

Divide both matrices into four equal-sized submatrices.

\[
A =
\begin{bmatrix}
A_{11} & A_{12}\\
A_{21} & A_{22}
\end{bmatrix}
\]

\[
B =
\begin{bmatrix}
B_{11} & B_{12}\\
B_{21} & B_{22}
\end{bmatrix}
\]

**2. Conquer**

Calculate seven intermediate products.

\[
M_1 = (A_{11}+A_{22})(B_{11}+B_{22})
\]

\[
M_2 = (A_{21}+A_{22})B_{11}
\]

\[
M_3 = A_{11}(B_{12}-B_{22})
\]

\[
M_4 = A_{22}(B_{21}-B_{11})
\]

\[
M_5 = (A_{11}+A_{12})B_{22}
\]

\[
M_6 = (A_{21}-A_{11})(B_{11}+B_{12})
\]

\[
M_7 = (A_{12}-A_{22})(B_{21}+B_{22})
\]

**3. Combine**

Use the seven intermediate products to reconstruct the final result matrix.

\[
C_{11} = M_1+M_4-M_5+M_7
\]

\[
C_{12} = M_3+M_5
\]

\[
C_{21} = M_2+M_4
\]

\[
C_{22} = M_1-M_2+M_3+M_6
\]

**Final Matrix:**

\[
C =
\begin{bmatrix}
C_{11} & C_{12}\\
C_{21} & C_{22}
\end{bmatrix}
\]

## 4. Pseudocode

**Algorithm: STRASSEN**

```text
STRASSEN(A, B, n)

    IF n = 1 THEN
        RETURN A[0][0] * B[0][0]
    END IF

    Divide A into A11, A12, A21, A22

    Divide B into B11, B12, B21, B22

    M1 = STRASSEN(
         A11 + A22,
         B11 + B22
    )

    M2 = STRASSEN(
         A21 + A22,
         B11
    )

    M3 = STRASSEN(
         A11,
         B12 - B22
    )

    M4 = STRASSEN(
         A22,
         B21 - B11
    )

    M5 = STRASSEN(
         A11 + A12,
         B22
    )

    M6 = STRASSEN(
         A21 - A11,
         B11 + B12
    )

    M7 = STRASSEN(
         A12 - A22,
         B21 + B22
    )

    C11 = M1 + M4 - M5 + M7

    C12 = M3 + M5

    C21 = M2 + M4

    C22 = M1 - M2 + M3 + M6

    Combine C11, C12, C21, C22

    RETURN C

END
```

## 5. Flowchart

The flowchart follows these steps:

1. START.
2. Read Matrix A and Matrix B.
3. Check matrix size.
4. Check whether n = 1.
5. If YES, multiply the single elements.
6. If NO, divide matrices into four submatrices.
7. Calculate seven products M1–M7.
8. Reconstruct C11, C12, C21 and C22.
9. Display the result matrix.
10. STOP.

## 6. Complete C Program

**File name:** `strassen.c`

This program:

- Accepts matrices from the user.
- Supports square matrices.
- Pads non-power-of-two dimensions with zeros.
- Uses seven recursive Strassen products.
- Uses ordinary multiplication as the base case.
- Displays the resulting matrix.

```c
#include <stdio.h>
#include <stdlib.h>

typedef long long ll;

ll *createMatrix(int n)
{
    ll *p = (ll *)calloc((size_t)n * n, sizeof(ll));

    if (p == NULL)
    {
        printf("Memory allocation failed.\n");
        exit(1);
    }

    return p;
}

void addMatrix(ll *A, ll *B, ll *C, int n)
{
    int i;

    for (i = 0; i < n * n; i++)
        C[i] = A[i] + B[i];
}

void subtractMatrix(ll *A, ll *B, ll *C, int n)
{
    int i;

    for (i = 0; i < n * n; i++)
        C[i] = A[i] - B[i];
}

void strassen(ll *A, ll *B, ll *C, int n)
{
    int i, j, h;

    if (n == 1)
    {
        C[0] = A[0] * B[0];
        return;
    }

    h = n / 2;

    /* Eight submatrices */
    ll *q[8];

    for (i = 0; i < 8; i++)
        q[i] = createMatrix(h);

    /* Ten temporary matrices */
    ll *s[10];

    for (i = 0; i < 10; i++)
        s[i] = createMatrix(h);

    /* Seven Strassen products */
    ll *m[7];

    for (i = 0; i < 7; i++)
        m[i] = createMatrix(h);

    /* Divide matrices into quadrants */

    for (i = 0; i < h; i++)
    {
        for (j = 0; j < h; j++)
        {
            q[0][i*h+j] = A[i*n+j];
            q[1][i*h+j] = A[i*n+j+h];

            q[2][i*h+j] = A[(i+h)*n+j];
            q[3][i*h+j] = A[(i+h)*n+j+h];

            q[4][i*h+j] = B[i*n+j];
            q[5][i*h+j] = B[i*n+j+h];

            q[6][i*h+j] = B[(i+h)*n+j];
            q[7][i*h+j] = B[(i+h)*n+j+h];
        }
    }

    /* Calculate the ten temporary matrices */

    addMatrix(q[0], q[3], s[0], h);
    addMatrix(q[4], q[7], s[1], h);

    addMatrix(q[2], q[3], s[2], h);

    subtractMatrix(q[5], q[7], s[3], h);
    subtractMatrix(q[6], q[4], s[4], h);

    addMatrix(q[0], q[1], s[5], h);

    subtractMatrix(q[2], q[0], s[6], h);
    addMatrix(q[4], q[5], s[7], h);

    subtractMatrix(q[1], q[3], s[8], h);
    addMatrix(q[6], q[7], s[9], h);

    /* Seven recursive multiplications */

    strassen(s[0], s[1], m[0], h);

    strassen(s[2], q[4], m[1], h);

    strassen(q[0], s[3], m[2], h);

    strassen(q[3], s[4], m[3], h);

    strassen(s[5], q[7], m[4], h);

    strassen(s[6], s[7], m[5], h);

    strassen(s[8], s[9], m[6], h);

    /* Reconstruct the result matrix */

    for (i = 0; i < h; i++)
    {
        for (j = 0; j < h; j++)
        {
            int k = i * h + j;

            ll C11 = m[0][k] + m[3][k]
                   - m[4][k] + m[6][k];

            ll C12 = m[2][k] + m[4][k];

            ll C21 = m[1][k] + m[3][k];

            ll C22 = m[0][k] - m[1][k]
                   + m[2][k] + m[5][k];

            C[i*n+j] = C11;
            C[i*n+j+h] = C12;

            C[(i+h)*n+j] = C21;
            C[(i+h)*n+j+h] = C22;
        }
    }

    /* Free allocated memory */

    for (i = 0; i < 8; i++)
        free(q[i]);

    for (i = 0; i < 10; i++)
        free(s[i]);

    for (i = 0; i < 7; i++)
        free(m[i]);
}

int nextPowerOfTwo(int n)
{
    int p = 1;

    while (p < n)
        p *= 2;

    return p;
}

int main()
{
    int n, p, i, j;

    printf("STRASSEN MATRIX MULTIPLICATION\n");

    printf("Enter matrix size: ");
    scanf("%d", &n);

    if (n <= 0 || n > 1024)
    {
        printf("Enter a matrix size between 1 and 1024.\n");
        return 1;
    }

    p = nextPowerOfTwo(n);

    ll *A = createMatrix(p);
    ll *B = createMatrix(p);
    ll *C = createMatrix(p);

    printf("\nEnter Matrix A elements:\n");

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%lld", &A[i*p+j]);
        }
    }

    printf("\nEnter Matrix B elements:\n");

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%lld", &B[i*p+j]);
        }
    }

    strassen(A, B, C, p);

    printf("\nRESULT MATRIX C = A x B\n");

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            printf("%lld ", C[i*p+j]);
        }

        printf("\n");
    }

    free(A);
    free(B);
    free(C);

    return 0;
}
```

## 7. Sample Input

```text
2

MATRIX A:

1 7
3 5

MATRIX B:

1 3
7 5
```

## 8. Expected Output

```text
STRASSEN MATRIX MULTIPLICATION

Enter matrix size: 2

Enter Matrix A elements:
1 7
3 5

Enter Matrix B elements:
1 3
7 5

RESULT MATRIX C = A x B

50 38
38 34
```

## 9. Execution Trace

**Given:**

\[
A =
\begin{bmatrix}
1 & 7\\
3 & 5
\end{bmatrix}
\]

\[
B =
\begin{bmatrix}
1 & 3\\
7 & 5
\end{bmatrix}
\]

Let:

```text
a = 1, b = 7

c = 3, d = 5

e = 1, f = 3

g = 7, h = 5
```

### Step 1: Calculate Seven Products

**M1**

\[
M_1 = (a+d)(e+h)
\]

\[
= (1+5)(1+5)
\]

\[
= 6 \times 6
\]

\[
= 36
\]

**M2**

\[
M_2 = (c+d)e
\]

\[
= (3+5) \times 1
\]

\[
= 8
\]

**M3**

\[
M_3 = a(f-h)
\]

\[
= 1 \times (3-5)
\]

\[
= -2
\]

**M4**

\[
M_4 = d(g-e)
\]

\[
= 5 \times (7-1)
\]

\[
= 30
\]

**M5**

\[
M_5 = (a+b)h
\]

\[
= (1+7) \times 5
\]

\[
= 40
\]

**M6**

\[
M_6 = (c-a)(e+f)
\]

\[
= (3-1)(1+3)
\]

\[
= 2 \times 4
\]

\[
= 8
\]

**M7**

\[
M_7 = (b-d)(g+h)
\]

\[
= (7-5)(7+5)
\]

\[
= 2 \times 12
\]

\[
= 24
\]

### Step 2: Reconstruct the Result Matrix

**C11**

\[
C_{11} = M_1+M_4-M_5+M_7
\]

\[
= 36+30-40+24
\]

\[
= 50
\]

**C12**

\[
C_{12} = M_3+M_5
\]

\[
= -2+40
\]

\[
= 38
\]

**C21**

\[
C_{21} = M_2+M_4
\]

\[
= 8+30
\]

\[
= 38
\]

**C22**

\[
C_{22} = M_1-M_2+M_3+M_6
\]

\[
= 36-8-2+8
\]

\[
= 34
\]

### Step 3: Final Result

\[
C =
\begin{bmatrix}
50 & 38\\
38 & 34
\end{bmatrix}
\]

## 10. Verification Using Conventional Matrix Multiplication

For verification:

\[
C_{11} = (1 \times 1)+(7 \times 7)=50
\]

\[
C_{12} = (1 \times 3)+(7 \times 5)=38
\]

\[
C_{21} = (3 \times 1)+(5 \times 7)=38
\]

\[
C_{22} = (3 \times 3)+(5 \times 5)=34
\]

Both methods produce the same result.

Therefore, Strassen's implementation is verified for the given sample matrices.

## 11. Recurrence Relation

Strassen's method divides each matrix into four submatrices but performs only seven recursive matrix multiplications.

The recurrence relation is:

\[
T(n) = 7T(n/2)+O(n^2)
\]

**Where:**

- 7T(n/2) represents seven recursive multiplications.
- O(n²) represents matrix additions and subtractions.

### Using the Master Theorem

\[
a=7
\]

\[
b=2
\]

\[
f(n)=O(n^2)
\]

Calculate:

\[
n^{\log_2 7} \approx n^{2.8074}
\]

Since 2.8074 is greater than 2, the recursive multiplication term dominates.

**Therefore:**

\[
T(n)=O(n^{2.8074})
\]

## 12. Comparison with Conventional Matrix Multiplication

Conventional matrix multiplication performs:

\[
n^3
\]

scalar multiplications.

Strassen's algorithm performs:

\[
n^{\log_2 7}
\]

scalar multiplications.

### For Production

\[
n=1024
\]

Since:

\[
1024=2^{10}
\]

**Conventional Method**

\[
1024^3
\]

\[
=1,073,741,824
\]

Scalar multiplications.

**Strassen's Method**

\[
7^{10}
\]

\[
=282,475,249
\]

Scalar multiplications.

### Comparison Table

| Parameter | Conventional | Strassen |
|---|---|---|
| Matrix size | 1024 × 1024 | 1024 × 1024 |
| Scalar multiplications | 1,073,741,824 | 282,475,249 |
| Time complexity | O(n³) | O(n^2.8074) |
| Recursive products | 8 | 7 |
| Additional operations | Standard additions | More intermediate additions/subtractions |

### Reduction in Scalar Multiplications

\[
1,073,741,824-282,475,249
\]

\[
=791,266,575
\]

### Percentage Reduction

\[
\frac{791,266,575}{1,073,741,824}\times100
\]

\[
\approx73.69\%
\]

Strassen's method reduces the scalar multiplication count by approximately **73.69%**.

These figures count scalar multiplications only, not the total execution time.

## 13. Memory Requirement

Strassen's algorithm requires additional memory for:

- Matrix sub-blocks.
- Temporary matrices.
- Seven intermediate products.
- Recursive function calls.

Its practical memory usage is higher than conventional matrix multiplication.

With careful workspace reuse, auxiliary memory can be managed in O(n²) space.

The provided educational implementation allocates temporary matrices recursively and therefore has substantial memory overhead.

## 14. Why Strassen May Not Be Faster in Practice

Although Strassen's algorithm performs fewer scalar multiplications, it may not always execute faster.

**Reasons include:**

1. Matrix additions and subtractions introduce extra operations.
2. Recursive calls introduce function-call overhead.
3. Temporary matrices require additional memory.
4. Memory allocation and copying can reduce performance.
5. Conventional multiplication can be highly optimised by modern processors.
6. Small matrices may be faster with the conventional method.

## 15. Practical Hybrid Recommendation

KartIQ should use a hybrid matrix multiplication approach.

1. Divide large matrices using Strassen's method.
2. Continue recursive multiplication while matrix dimensions are large.
3. When the matrix size reaches a selected threshold, switch to conventional matrix multiplication.
4. Reuse temporary memory wherever possible.
5. Benchmark different thresholds on production hardware.

For example, an implementation might use a threshold of 64, but the actual threshold should be selected through testing.

## Conclusion

Strassen's method is appropriate for large recommendation matrices because it reduces the number of scalar multiplications. A hybrid approach is recommended to balance computation time, memory consumption and recursion overhead.
