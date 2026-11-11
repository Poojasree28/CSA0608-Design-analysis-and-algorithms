### Source Code: Strassen Matrix Multiplication

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

