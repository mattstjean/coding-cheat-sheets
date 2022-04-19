# Bitwise operators

([Back to menu](/README.md))

These operators are used to perform the manipulation of individual bits of a number. They cna be used with any integral type.

- byte (8 bit)
- short (16 bit)
- int (32 bit)
- long (64 bit)
- char (16 bit)

## Bitwise OR ( | )

Binary operator that returns bit-by-bit OR of inputs. If either of the bits is a 1, it gives 1, otherwise it gives 0.

```text
a = 5 = 0101 (In Binary)
b = 7 = 0111 (In Binary)

Bitwise OR Operation of 5 and 7
  0101
| 0111
------
  0111 = 7 (in decimal)
```

## Bitwise AND ( & )

Binary operator that returns bit-by-bit AND of inputs. If both bits are 1, it gives 1, otherwise it gives 0.

```text
a = 5 = 0101
b = 7 = 0111

Bitwise AND operation of 5 and 7
  0101
& 0111
------
  0101 = 5
```

## Bitwise XOR ( ^ )

Binary operator that returns bit-by-bit XOR of input values. If corresponding bits are different, it gives 1, otherwise it gives 0.

```text
a = 5 = 0101
b = 7 = 0111

Bitwise XOR operation of 5 and 7
  0101
^ 0111
------
  0010 = 2
```

## Bitwise Compliment ( ~ )

Unary operator that returns the complement represention of the input value. All bits are inverted, ie every 0 becomes 1, and every 1 becomes 0.

```text
a = 5 = 0101

Bitwise Compliment operation of 5
~ 0101
-------
  1010 = 10
```

The Java Compiler will return 2's complement of 1010, -6. Note, this is explained in [Bit-Shift Operators](./bit_shift_operators.md). Essentially, Java represents negative numbers by negating (flipping) all bits and then adding 1. If the leftmost bit is 1, it's negative.

Because we're working with 32 bits here...
00000000 00000000 00000000 00000101   = 5
Flip it:
11111111 11111111 11111111 11111010
Add one:
11111111 11111111 11111111 11110101   = -6 (2s complement representation)
