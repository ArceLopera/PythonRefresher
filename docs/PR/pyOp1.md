
| Operator     | Name           | Description                                            |
|--------------|----------------|--------------------------------------------------------|
| ``a + b``    | Addition       | Sum of ``a`` and ``b``                                 |
| ``a - b``    | Subtraction    | Difference of ``a`` and ``b``                          |
| ``a * b``    | Multiplication | Product of ``a`` and ``b``                             |
| ``a / b``    | True division  | Quotient of ``a`` and ``b``                            |
| ``a // b``   | Floor division | Quotient of ``a`` and ``b``, removing fractional parts |
| ``a % b``    | Modulus        | Integer remainder after division of ``a`` by ``b``     |
| ``a ** b``   | Exponentiation | ``a`` raised to the power of ``b``                     |
| ``-a``       | Negation       | The negative of ``a``                                  |

``` py
a=3**2
b=2**2**3
print(a)
print(b)
print(9**(1/2)) #result is float
print(20//6) # Quotient
print(20%6) # Modulo or remainder
```

```
9
256
3.0
3
2
```

For enhanced precision, the decimal module provides support for fast correctly-rounded decimal floating point arithmetic.

``` py
from decimal import *
getcontext().prec = 6
Decimal(1) / Decimal(7)
```
```
Decimal('0.142857')
```
