# Trait Type

A trait is a type with a collection of functions, that's why it is easily remembered annotated with
`type fn`, the trait name, and the method bodies. 

```ü
type fn New {
    fn new () -> T(self)
}

type fn Length {
    fn len(self) -> uint
}
```

Trait methods are always public, as they should be, and it is possible to define static methods in
a trait. This allows traits to be used as pattern implementations, too, such as `Singleton`.

To form inheritance among traits, you can use the keyword `use` in a trait, as in "using the methods
from"

```
type fn List {
    use New
    use Length
    use Push
    use Pop
    use Iter
}
```

Traits can be implemented for a type with the grammar `T1 use T2` where `T1` is a type that gets
extended with `T2`.

```ü
Option use Length {
    fn len(self) {
        if self is None
            ret 0
        ret 1
    }
}
```

##### Special Traits

You can selectively override primitive operations for a type, such as arithmetic or logical for a
`Position` type. For binary operations you can use both the function definition `(self, other Type)`
as well as `(left Type, right TypeTwo)`. The compiler should infer if self is used and assign it
the self type.

```ü
Position use Add<Position, Position> {
    fn add (left Position, right Position) {
        be (x1, y1) = left
        be (x2, y2) = right
        ret (x1 + x2, y1 + y2)
    }
}
```

Here is a list of symbols that should be overridable.
TODO Make unary special

```py
Operator  | Function                 | Explanation

   +      | fn '+' (self, T1) -> T2  | self + T1
   +      | fn '+' (self) -> T       | + self      # Unary
   -      | fn '-' (self, T1) -> T2  | self - T1
   -      | fn '-' (self) -> T       | - self      # Unary
   *      | fn '*' (self, T1) -> T2  | self * T2
   /      | fn '/' (self, T1) -> T2  | self / T2
   %      | fn '%' (self, T1) -> T2  | self % T2
   ^      | fn '^' (self, T1) -> T2  | self ^ T2
   <<     | fn '<<' (self, T1) -> T2  | self << T2
   >>     | fn '>>' (self, T1) -> T2  | self >> T2

   &&     | fn '&&' (self, T1) -> T2 | self && T1
   ||     | fn '||' (self, T1) -> T2 | self || T1
   !      | fn '!' (self) -> T       | !self       # Unary
   ==     | fn '==' (self, T1) -> T2 | self == T1
   !=     | fn '!=' (self, T1) -> T2 | self != T1
   >=     | fn '>=' (self, T1) -> T2 | self >= T1
   >      | fn '>' (self, T1) -> T2  | self > T1
   <=     | fn '<=' (self, T1) -> T2 | self <= T1
   <      | fn '<' (self, T1) -> T2  | self < T1

   =      | fn '=' (self, T1) -> T2  | self = T1
   +=     | fn '+=' (self, T1) -> T2 | self += T1
   -=     | fn '-=' (self, T1) -> T2 | self -= T1
   *=     | fn '*=' (self, T1) -> T2 | self *= T2
   /=     | fn '/=' (self, T1) -> T2 | self /= T2
   %=     | fn '%=' (self, T1) -> T2 | self %= T2
   ^=     | fn '^=' (self, T1) -> T2 | self ^= T2
   <<=    | fn '<<=' (self, T1) -> T2| self <<= T2
   >>=    | fn '>>=' (self, T1) -> T2| self >>= T2
   &&=    | fn '&&=' (self, T1) -> T2| self &&= T1
   ||=    | fn '||=' (self, T1) -> T2| self ||= T1

   ?      | fn '?' (self) -> T       | self?       # Unary, from behind
   .      | fn '.' (self, str) -> T  | self.mA     # Member Access, `mA` is provided as String
```