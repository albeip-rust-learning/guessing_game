# guessing_game
URL: https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html

## Useful commands
```
$ cargo new guessing_game
$ cd guessing_game
$ cargo run
```
The file we are going to analyze is: `src\main.rs`
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
We're still working on this line of code:
```rust
io::stdin()
    .read_line(&mut guess)
    .expect("Failed to read line");
```
Although we're now discussing a third line of text, it's still part of a single logical line
of code. The next part is this method:
```rust
    .expect("Failed to read line");
```
As mentioned earlier, `read_line` puts what the user types into the string we're passing it,
but it also return a value &mdash;in this case, an `io::Result`. Rust has a number of types named
`Result` in its standard library: a generic `Result` as well as specific versions for modules,
such as `io::Result`.

The `Result` types are `enumerations`, often referred as *enums*. An enumeration is a type that
can have a fixed set of values, and those values are called the enum's *variants*.

For `Result`, the variant are `Ok` or `Err`.

The `Ok` variant indicates the operation was successful, and inside `Ok` is the successfull
generated value.

The `Err` variant means the operation failed, and `Err` contains information about how or why
the operation failed.

The purpose of these `Result` types is to encode error-handling information. Values of the 
`Result` type, like values of any type, have methods defined on them.

An instance of `io::Result` has an `expect` **method** that you can call. 

If this instance of `io::Result` is an `Err` value, `expect` will cause the program to crash and display
the message that you passed as an argument to `expect`.

If the `read_line` method returns an `Err`, it would likely be the result of an error coming from the
underlying operating system. If this instance of `io::Result` is an `Ok` value, `expect` will take the
return value that `Ok` is holding and return just that value to you so you can use it. In this case, that
value is the number of bytes in what the user entered into standard input.

If you don't call `expect`, the program will compile, but you'll get a warning.

The right way to suppress the warning is to actually write error handling, but because you just want to
crash this program when a problem occurs, you can use `expect`.

## Printing Values with println! Placeholders
There’s only one more line to discuss in the code added so far, which is the following:
```rust
println!("You guessed: {}", guess);
```
This line prints the string we saved the user’s input in. The set of curly brackets, {}, is a placeholder:
think of {} as little crab pincers that hold a value in place. You can print more than one value using
curly brackets: the first set of curly brackets holds the first value listed after the format string,
the second set holds the second value, and so on. Printing multiple values in one call to println! would
look like this:
```rust
let x = 5;
let y = 10;
println!("x = {} and y = {}", x, y);
```
This code would print
```commandline
x = 5 and y = 10
```