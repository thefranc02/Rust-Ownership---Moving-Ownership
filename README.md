# COMP 211 Checkoff 3 — AI Exploration

## Topic: Rust Ownership — Moving Ownership

**Presentation date:** Wednesday, November 18

### 1. Initial Background and Motivation

I chose Rust Ownership, specifically Moving Ownership, to explore how programming languages manage memory and prevent common memory-management errors.

My existing experience is primarily with C. I have covered pointers, dynamic memory allocation, and functions such as `malloc()`, `calloc()`, and `strcpy()`.

I understand that C requires programmers to manage dynamically allocated memory manually, including deciding when to call `free()`. I also understand how assigning one pointer to another can cause both pointers to reference the same memory allocation.

I have not previously worked with Rust, so its ownership system is a new concept for me.

### 2. Initial Questions

I started my exploration with the following questions:

1. What is ownership in Rust, and why does Rust use it?
2. What happens when ownership is transferred from one variable to another?
3. Why does Rust prevent the original variable from being accessed after a move?
4. How does this compare with assigning pointers in C?
5. How does Rust distinguish between moving a value and copying it?

### 3. Initial Learning Objective

My goal is to understand how Rust's ownership system works, particularly how moving ownership prevents multiple variables from incorrectly managing the same heap allocation.

I also want to connect these concepts to my existing knowledge of C memory management so I can explain the differences with practical examples.

### 4. Discovery 1 — Pointer Aliasing in C

#### Initial Exploration

I started by looking at how C handles multiple pointers
that reference the same dynamically allocated memory.

#### Code Example
```
int main(void) {
  char *a = malloc(10);
  if (a == NULL){
    return 1;
  }
  
  strycpy(a, "hello");
  
  char *b = a;
  
  free(a);
  free(b); // Purposely freeing
  a = b = NULL;
  return 0;
}
```

#### What I Observed
Attempting to free pointers like example above that point to the same memory location leads to a double-free error that causes undefined behavior.

### 5. Discovery 2 — Initial Rust Syntax Exploration

#### Initial Exploration

After seeing how C lets two pointers share one allocation, I tested the same
idea in Rust. `String::from("hello")` allocates the text on the heap. The
variable `a` is not a raw pointer: it is a `String` value on the stack that
stores a pointer to the heap buffer, plus a length and a capacity. (A string
literal like `"hello"` by itself is a `&str` stored in static memory. Only
`String::from` copies it onto the heap.)

The key line is `let b = a;`. In C, `char *b = a;` copies the pointer, so
both `a` and `b` stay valid and both could call `free()`. In Rust, this line
*moves* ownership of the string from `a` to `b`. `a` can no longer be used,
so there is exactly one owner of the heap allocation at any time.

#### Code Examples
Function 1:

```
fn main() {
    let a = String::from("hello");
    let b = a;

    println!("{}", b);
}
```

Function 2:
```
fn main() {
    let a = String::from("hello");
    let b = a;

    println!("{}", a);
}
```

#### What I Observed
I ran both in the Rust Playground.

- Function 1 compiled and printed `hello`.
- Function 2 failed to compile with error E0382, "borrow of moved value: `a`".
```
Compiling playground v0.0.1 (/playground)
error[E0382]: borrow of moved value: `a`
 --> src/main.rs:5:20
  |
2 |     let a = String::from("hello");
  |         - move occurs because `a` has type `String`, which does not implement the `Copy` trait
3 |     let b = a;
  |             - value moved here
4 |
5 |     println!("{}", a);
  |                    ^ value borrowed here after move
  |
help: consider cloning the value if the performance cost is acceptable
  |
3 |     let b = a.clone();
  |              ++++++++

warning: unused variable: `b`
 --> src/main.rs:3:9
  |
3 |     let b = a;
  |         ^ help: if this is intentional, prefix it with an underscore: `_b`
  |
  = note: `#[warn(unused_variables)]` (part of `#[warn(unused)]`) on by default

For more information about this error, try `rustc --explain E0382`.
warning: `playground` (bin "playground") generated 1 warning
error: could not compile `playground` (bin "playground") due to 1 previous error; 1 warning emitted
Standard Output
```
The compiler pointed out that the value moved on the `let b = a;` line and that `String` does not implement the `Copy` trait.

This connects directly to my C example. In C, the double free happens at
runtime because two pointers both think they own the memory. In Rust, only
one variable owns the memory, and it is freed once when that owner goes out
of scope. The compiler rejects Function 2 before the program can run, so
the double-free problem cannot occur.

#### Questions and Follow-ups
From here I prompted my ai of choice, ChatGPT (GPT-5.6 Luna- free user) that explained the key differences in Rust syntax/handling pointers.


