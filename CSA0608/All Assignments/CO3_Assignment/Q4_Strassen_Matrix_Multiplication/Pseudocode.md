## Q4 – Strassen's Matrix Multiplication

### Pseudocode

```text
STRASSEN(A, B):

    if matrix size is below threshold:
        return conventional_multiply(A, B)

    if size is odd or not a power of two:
        pad A and B with zero rows/columns to a suitable size

    split A and B into four blocks

    compute M1 through M7

    reconstruct C11, C12, C21, C22

    join the four C blocks

    remove padding and return the original-size result
```
