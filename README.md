# guessing_game
Useful commands
```
$ cargo new guessing_game
$ cd guessing_game
$ cargo run
```
## Declare a library
The `io` library comes from the standard library (which is known as std):
```rust
use std::io;
```
## Define the main function 
The main function is the entry point into the program:
```rust
fn main() {
//     
}
```
The `fn` syntax declares a new function, the parentheses,`()`, indicate there are no parameters,
and the curly bracket, `{`, starts the body of the function.

## Print values to the screen

`println!` is a macro that prints a string to the screen:
```rust
println!("Guess the number!");
println!("Please input your guess");
```

## Storing Values with Variables
```rust
let mut guess = String::new();
```
There's a lot going on in this little line.

`let` statement is used to create a *variable*. In Rust, variables are immutable by default.
```rust
let     foo = 5; // immutable
let mut bar = 5; // mutable
```
On the other side of the equal sign (`=`) is the value that `guess` is bound to, which is the result of 
calling `String::new`, a function that returns a new instance of String. `String` is a string type
provided by the standard library that is a growable, UTF-8 encoded bit of text.

The `::` syntax in the `::new` line indicates that `new` is an *associated function* of the `String` type.
An *associated function* is implemented on a type, in this case `String`, rather than on a particular
instance of a `String`. Some languages call this a *static method*.

The `new` function creates a new, empty string. You'll find a `new` function on many types, because it's a
common name for a function that makes a new value of some kind.

To summarize, the `let mut guess = String::new();` line has created a mutable variable that is currently
bound to a new, empty instance of a `String`.  

## Read a line
We included the input/output functionality from the standard library with `use std::io;` on the first line
of the program. Now we'll call the `stdin` function from the `io` module:
```rust
io::stdin()
    .read_line(&mut guess)
```
If we hadn't put the `use std::io` line at the beginning of the program, we could have written this
function call as `std::io::stdin`. The `stdin` function returns an instance of `std::io::Stdin`, which is
a type that represents a handle to the standard input for your terminal.

The next part of the code, `.read_line(&mut guess)`, calls `read_line` method on  the standard input handle
to get input from the user. We'are also passing one argument to `read_line`: `&mut guess`.

The job of `read_line` is to take whatever the user types into standard input and place that into a string,
so it takes that string as an argument. The string argument needs to be mutable so the method can change
the string’s content by adding the user input.

The `&` indicates that this argument is a reference, which gives you a way to let multiple parts of your
code access one piece of data without needing to copy that data into memory multiple times.

For now, all you need to know is that like variables, references are immutable by default.
Hence, you need to write `&mut guess` rather than `&guess` to make it mutable.

## Handling Potential Failure with the `Result` Type
