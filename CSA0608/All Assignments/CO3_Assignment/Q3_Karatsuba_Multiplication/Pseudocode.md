## Q3 – Karatsuba Multiplication

### Pseudocode

```text
KARATSUBA(x, y):

    if x or y is small:
        return x * y

    m = ceil(max(number_of_digits(x), number_of_digits(y)) / 2)

    B = 10^m

    a, b = divmod(x, B)

    c, d = divmod(y, B)

    z2 = KARATSUBA(a, c)

    z0 = KARATSUBA(b, d)

    z1 = KARATSUBA(a+b, c+d) - z2 - z0

    return z2*B*B + z1*B + z0
```
