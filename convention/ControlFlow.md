# Control Flow

##### Variable Declarations

Variable declarations follow the grammar `be` → Identifier → Type? → Question Mark? → and can optionally
follow with an instant initialization `=` → Value

##### Functions

Functions can be defined with the grammar `fn` → Struct → (`->` Type)? → CodeBody and the type of a function
is simply `T(` ... `)` surrounded around the function header.

##### Comparisons

In Ü, the type of `a < b` is not directly a bool but it's first seen as a group of several arguments `'<' (a, b)`
simply to treat it as an extendable structure. This way `0 <= n < inf` should be a possible experssion, where
`inf` is a constant and `n` a variable. The same will go for `==`, but not for `!=` (not transitive) or `&&` (is
already logical expression)

##### Loops and Jumps

Traditional for loops are possible, however not recommended, just like you know them without the brackets.

```ü
for be i = 0; i < 10; i += 1 {
    stdout.println(`{i}`)
}
```

To create a while loop, you use `for` with a conditional expression, and to loop indefinitely, you use `for`
with the code block directly attached.

Conditional jumps can be done with `if`, `el if` and `el` traditionally. You don't use brackets for the conditions.

Combining a while loop in an if-chain will do as follows: If the for loop was executed at least once, it counts as
a successful if branch and leaves, but if the condition was wrong from the start, you jump to the next `el`-statement.
Here is an example where you want to empty all elements of a scheduler and do something, if the scheduler didn't have
elements but was called to run.

```
# Scheduler scope ...
fn runScheduler(self) {
    for self.items.len() > 0 {
        self.items.pop_and_run()
    } el {
        # Scheduler is not alive
    }
}
```

