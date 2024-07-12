# Type Structs

```ü
type Test
```

The most simple kind of type is a type with no particular definition, it does not contain any value or
data, but can be extended with static methods or used as a namespace with private global variables, or
be used in an entity-component system. To export the type, you need to add the `pub` keyword. You will
later read on type methods: Without the `pub` method you can selectively hide the type implementation
or some type methods.

##### Enumerables

```ü
type Option<V> = Some (V) | null
type Vec<V> = (V, Vec<V>) | Leaf
```

Enumrables are defined like in Rust or OCaml, with the possibility of matching and destructuring in an
if condition.

The type `Option` is registered as a special type and can be used in variable declarations with a 
question mark as a shortcut.

```ü
be response Option<String> = Option.Some("Hello, World!")
be response Option<String> = Option.null
be response String? = "Hello, World!"
be response String? = null
```

Note, that here `null` is not a typical null-value, but the unpacked constructor from `Option`. The `?`
operator allows to declare a variale without constantly using the prefix `Option`.

##### Structures

```ü
type Position = (int8, int8)
type Position = (
    x int8 = 0,
    y int8 = 0
)
```

Structures are defined as tuples or as named data, both have values separated by comma and specify the
value types. The difference is, that tuples do not need to give names to their entries. Optionally, you
can define private attributes by starting the variable identifier with `_`. Default values can be defined
with a `=`.

Tuples can be unpacked intuitively with `be (a1, a2, ...) = ...`, structures can selectively unpack attributes
like `be (a1, a2) = ...` without specifying all variables.

# Type Methods

To declare methods within a type scope, you can simple write the type name followed by curly brackets.
Within this scope you are allowed to perform the magic of accessing private attributes. To export the
methods, you need still need to add the `pub` keyword before the scope. To create private methods, you
need a second scope without the `pub` keyword.

```ü
pub Option<V> {
    fn is_some(self) {
        ret self be Some(x)
    }
}
```
