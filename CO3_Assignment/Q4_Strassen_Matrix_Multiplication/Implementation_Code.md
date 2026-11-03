## Q4 – Strassen's Matrix Multiplication

### Python Code

```python
def conventional(A, B):

    n = len(A)

    return [[sum(A[i][k] * B[k][j] for k in range(n))
             for j in range(n)] for i in range(n)]


def add(X, Y):

    n = len(X)

    return [[X[i][j] + Y[i][j] for j in range(n)] for i in range(n)]


def sub(X, Y):

    n = len(X)

    return [[X[i][j] - Y[i][j] for j in range(n)] for i in range(n)]


def strassen(A, B, threshold=2):

    n = len(A)

    if n <= threshold:
        return conventional(A, B)

    if n % 2:
        raise ValueError("Pad matrix to an even size before recursion")

    m = n // 2

    def split(X):

        return ([row[:m] for row in X[:m]],
                [row[m:] for row in X[:m]],
                [row[:m] for row in X[m:]],
                [row[m:] for row in X[m:]])

    A11, A12, A21, A22 = split(A)
    B11, B12, B21, B22 = split(B)

    M1 = strassen(add(A11, A22), add(B11, B22), threshold)
    M2 = strassen(add(A21, A22), B11, threshold)
    M3 = strassen(A11, sub(B12, B22), threshold)
    M4 = strassen(A22, sub(B21, B11), threshold)
    M5 = strassen(add(A11, A12), B22, threshold)
    M6 = strassen(sub(A21, A11), add(B11, B12), threshold)
    M7 = strassen(sub(A12, A22), add(B21, B22), threshold)

    C11 = add(sub(add(M1, M4), M5), M7)
    C12 = add(M3, M5)
    C21 = add(M2, M4)
    C22 = add(sub(add(M1, M3), M2), M6)

    return [C11[i] + C12[i] for i in range(m)] + \
           [C21[i] + C22[i] for i in range(m)]


def strassen_padded(A, B, threshold=2):

    n, m = len(A), 1

    while m < n:
        m *= 2

    Ap = [row[:] + [0] * (m - n) for row in A] + \
         [[0] * m for _ in range(m - n)]

    Bp = [row[:] + [0] * (m - n) for row in B] + \
         [[0] * m for _ in range(m - n)]

    Cp = strassen(Ap, Bp, threshold)

    return [row[:n] for row in Cp[:n]]


# Getting input from the user

n = int(input("Enter the size of the square matrices: "))

if n <= 0:

    print("Please enter a valid matrix size.")

else:

    print("Enter the elements of Matrix A row by row:")

    A = []

    for i in range(n):
        row = list(map(int, input().split()))
        A.append(row)

    print("Enter the elements of Matrix B row by row:")

    B = []

    for i in range(n):
        row = list(map(int, input().split()))
        B.append(row)

    if any(len(row) != n for row in A + B):

        print("Each row must contain exactly", n, "elements.")

    else:

        result1 = conventional(A, B)
        result2 = strassen_padded(A, B)

        print("Conventional Multiplication Result:")

        for row in result1:
            print(row)

        print("Strassen Multiplication Result:")

        for row in result2:
            print(row)

        print("Results are equal:", result1 == result2)
```


```
