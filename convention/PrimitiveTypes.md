
# Primitives

The different primitive types as usual are categorized as bytes of different static or variable length
with different interpretations.

##### Numeric Primitives

```ü
type int
type uint
```

To declare a numeric value, use `int` or `uint` with an optional size in bits of the value behind.
The compiler should optimize numbers with compatible low bit count together to store memory. The rule
is that in structures and combined types, if one number exceeds the size of 8 bits, it will round up
to bytes. If the bit count is less than 8, the number is filled within a structure, starting with the
the largest numbers. Destructuring numbers from a structure is done with an and ask mask and shifts. The
shift can be omitted if the number is passed through and if condition, to optimize for bools.

##### Boolean Primitive

Booleans should be optimized to never shift, unlike ints, because they are not used in the context of
positional values, but as "contains one bit or not".

```ü
type bool = uint1
be true bool = 1
be false bool = 0
```

##### String-related primitives

```
type byte = uint8
type char
```
