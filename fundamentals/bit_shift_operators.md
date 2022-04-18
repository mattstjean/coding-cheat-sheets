# Bit-Shift Operators
Shift operators are used to shift the bits of a number left or right, thereby multiplying or dividing the number by two, respectively. They can be used when we have to multiply or divide a number by two. Even though you can shift all integral types, they will be promoted to 32-bit integers before shifting. The right operand (num positions to shift) is reduced to mod 32, ex. 5<<35 is the same as 5<<3.

Binary representation does not provide information about whether a number is negative so there needs to be a rule to define how to represent negative numbers in binary. One solution is to use the leftmost bit as a sign bit but one disadvantage is that there will be two ways to represent 0. Java uses another approach, *two's compliment*. Negative numbers are represented by negating (flipping) all the bits, and then adding 1. If the leftmost bit is 0, the number is positive otherwise it's negative.

Syntax:  num  shift_operator  num_places_to_shift

Types:
1. Signed Right shift operator (>>)
2. Unsigned Right shift operator (>>>)
3. Left shift operator (<<)

## Signed Right Shift
The right shift operator moves all bits by a given number of bits to the right. When the value of a number is shifted to the right, the rightmost bits are lost, and the sign bit is filled in the leftmost place.

```
a = 8 = 1000

Signed right shift by two bits
1000 >> 2
-------
   0010 = 2
```

## Unsigned Right Shift
It is the same as the signed right shift, but it does not care about the sign bits and just pads the result with zeros from the left. When performed on negative numbers, the result is always positive. Signed and unsigned right shifts have the same result for positive numbers.

```
a = 8  = 0000 1000

Unsigned right shift by two bits
1000 >>> 2
----------
0010 = 2

```

## Signed Left Shift
The left shift operator moves all bits by a given number of bits to the left. When the value of a number is shifted to the left two places, the leftmost two bits are lost.

```
a = 2 = 0010

Signed left shift by two bits
0010 >> 2
-------
1000 = 8
```

## Unsigned Left Shift
This does not exist. The logical (<<) and arithmetic (<<<) operations are identical.
