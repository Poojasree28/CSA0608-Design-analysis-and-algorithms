## Q3 – Karatsuba Multiplication

### Python Code

```python
def standard_multiply(x, y):

    return x * y


def karatsuba(x, y, threshold=32):

    if x < 0 or y < 0:

        sign = -1 if (x < 0) != (y < 0) else 1

        return sign * karatsuba(abs(x), abs(y), threshold)

    if x < 10**threshold or y < 10**threshold:

        return x * y

    m = max(len(str(x)), len(str(y))) // 2

    B = 10**m

    a, b = divmod(x, B)

    c, d = divmod(y, B)

    z2 = karatsuba(a, c, threshold)

    z0 = karatsuba(b, d, threshold)

    z1 = karatsuba(a + b, c + d, threshold) - z2 - z0

    return z2 * B * B + z1 * B + z0


# Getting input from the user

x = int(input("Enter the first number: "))

y = int(input("Enter the second number: "))

threshold = int(input("Enter the threshold value (default 32): "))

if threshold <= 0:

    print("Please enter a positive threshold value.")

else:

    result1 = standard_multiply(x, y)

    result2 = karatsuba(x, y, threshold)

    print("Standard Multiplication Result:", result1)

    print("Karatsuba Multiplication Result:", result2)

    if result1 == result2:

        print("Both multiplication results are equal.")

    else:

        print("The multiplication results are not equal.")
```


```
