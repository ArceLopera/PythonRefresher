In Python, bitwise operators are used to performing bitwise calculations on integers. The integers are first converted into binary and then operations are performed on bit by bit, hence the name bitwise operators. Then the result is returned in decimal format.

Note: Python bitwise operators work only on integers.

| Operator     | Name           | Description                                            |
|--------------|----------------|--------------------------------------------------------|
| ``a & b``    | Bitwise AND       | Returns 1 if both the bits are 1 else 0        |
| ``a | b``    | Bitwise OR       |  Returns 1 if either of the bit is 1 else 0        |
| ``a ~ b``    | Bitwise NOT       | Returns one’s complement of the number        |
| ``a ^ b``    | Bitwise XOR       |  Returns 1 if one of the bits is 1 and the other is 0 else returns false        |
| ``a >> b``    | Bitwise right shift       | Returns 1 if both the bits are 1 else 0        |
| ``a << b``    | Bitwise left shift       | Returns 1 if both the bits are 1 else 0        |

##**Shift Operators**

These operators are used to shift the bits of a number left or right thereby multiplying or dividing the number by two respectively. They can be used when we have to multiply or divide a number by two. 

###**Bitwise right shift** 
Shifts the bits of the number to the right and fills 0 on voids left as a result. Similar effect as of dividing the number with some power of two.

###**Bitwise left shift** 
Shifts the bits of the number to the left and fills 0 on voids left as a result. Similar effect as of multiplying the number with some power of two.

``` py
a = 10   #1010(Binary)
b = 4    #0100(Binary)
 
# Print bitwise AND operation
print("a & b =", a & b)   #0000(Binary)
 
# Print bitwise OR operation
print("a | b =", a | b)   #1110(Binary)=14(Decimal)
 
# Print bitwise NOT operation
print("~a =", ~a)         #-(1010+1)(Binary)=-(1011)=-11(Decimal)
 
# print bitwise XOR operation
print("a ^ b =", a ^ b)   # 1110(Binary)=14(Decimal)

a = 10
b = -10
 
# print bitwise right shift operator
print("a >> 1 =", a >> 1)
print("b >> 1 =", b >> 1)
 
a = 5
b = -10
 
# print bitwise left shift operator
print("a << 1 =", a << 1)
print("b << 1 =", b << 1)

#Hexidecimal
x=0x0a
y=0x02
z=x&y
print(f'(hex) x is {x:02x}, y is {y:02x}, z is {z:02x}')
print(f'(bin) x is {x:08b}, y is {y:08b}, z is {z:08b}')
z=x<<y
print(f'(bin) x is {x:08b}, y is {y:08b}, z is {z:08b}')
```
```
a & b = 0
a | b = 14
~a = -11
a ^ b = 14
a >> 1 = 5
b >> 1 = -5
a << 1 = 10
b << 1 = -20
(hex) x is 0a, y is 02, z is 02
(bin) x is 00001010, y is 00000010, z is 00000010
(bin) x is 00001010, y is 00000010, z is 00101000
```
