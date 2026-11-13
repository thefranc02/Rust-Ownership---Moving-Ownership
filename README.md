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
#include <stdlib.h>
#include <string.h>

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

#### Additional Understanding

I also considered why Rust requires `.clone()` to be called explicitly instead of automatically duplicating values during assignment.

I learned that automatically cloning heap-allocated data could introduce unnecessary memory allocations and copying. In cases where a programmer only wants to transfer ownership, duplicating the data would waste memory and processing time.

By making cloning explicit, Rust allows programmers to choose when duplicating data is necessary and when moving ownership is sufficient.

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
of scope. In safe Rust, the compiler prevents this particular ownership mistake before the program runs. By enforcing a single owner of the String, Rust prevents the same allocation from being freed twice through this pattern.

#### Clarification - Variables, Ownership, and References
During my exploration, I clarified the distinction between a variable binding and a reference in Rust. 

A variable binding associates a name with a value. Assigning a non-copy value to another binding transfers ownership: 
```
let a = String::("hello");
let b = a;
```
A reference, on the other hand, is created using the `&` operator:
```
let a = String::from("hello");
let b = &a;
```
Here, a retains ownership while b borrows a reference to its value.
This distinction helped me understand that Rust does not prohibit multiple references to the same data. Instead, its borrowing rules regular how references can access data to maintain memory safety.

#### Questions and Follow-ups

I used ChatGPT to clarify the differences between C pointer assignment and Rust ownership. I wanted to understand what happened internally when a value was moved and why Rust prevented the original variable from being used afterward.

**Questions I explored:**

1. What exactly happens internally when `let b = a;` executes?
2. Does Rust copy the actual String data, or does it transfer ownership?
3. Why does Rust prevent me from accessing `a` after the move?
4. What does the `Copy` trait mean, and why doesn't `String` implement it?
5. How does Rust determine which variable is responsible for cleaning up the allocated memory?

**Follow-up exploration:**

I used the Rust Playground to test the difference between using the destination variable after a move and attempting to use the original variable. I examined the E0382 compiler error to identify exactly where ownership was transferred and why the original variable was no longer valid.

### 6. Discovery 3 — The Copy Trait vs. Moving Ownership

#### Initial Exploration

After testing how Rust transfers ownership of a `String`, I wanted to determine whether every variable assignment in Rust makes the original variable unusable.

I tested the same assignment pattern using an integer (`i32`) instead of a `String` to see whether Rust handled different types differently.

#### Code Example

```rust
fn main() {
    let a = 5;
    let b = a;

    println!("a = {}, b = {}", a, b);
}
```

#### What I Observed

The program compiled successfully and printed both values:

```text
a = 5, b = 5
```

Unlike the previous `String` example, Rust allowed me to continue using `a` after assigning its value to `b`.

This introduced me to the `Copy` trait. The `i32` type implements `Copy`, meaning its value is copied rather than moved. As a result, both variables remain valid after the assignment.

#### Questions and Follow-ups

After discovering that the integer example compiled successfully even though the original `String` example did not, I wanted to understand why Rust treated the two types differently.

**Questions I explored:**

1. What is `i32`, and what does the number 32 represent?
2. What exactly is the `Copy` trait in Rust?
3. Why does `i32` implement `Copy`, but `String` does not?
4. Why does Rust provide different integer types?
5. Can custom structs implement the `Copy` trait, or is it limited to built-in types?

**Follow-up exploration:**

I learned that `i32` is a signed 32-bit integer type and that it implements the `Copy` trait. This means assigning an `i32` to another variable copies its value, allowing the original variable to remain usable.

I then explored why `String` behaves differently. Unlike an integer, a `String` owns a dynamically allocated heap buffer. Automatically copying its ownership could result in multiple variables attempting to manage and free the same allocation.

I also investigated whether custom structs and vectors could implement `Copy`. I learned that custom structs can implement `Copy` if all their fields implement `Copy` and the struct does not implement `Drop`. Vectors do not implement `Copy` because they own dynamically allocated memory and require cleanup.

### 7. Discovery 4 — Explicit Cloning with `.clone()`

#### Initial Exploration

After learning that assigning a `String` to another variable transfers ownership, I wanted to understand how Rust allows programmers to intentionally duplicate a value without making the original variable unusable.

In the previous experiments, assigning a `String` using `let b = a` moved ownership from `a` to `b`. The original variable could no longer be accessed.

I wanted to see whether Rust provided a way to duplicate the value while allowing both variables to remain valid.

#### Code Example 1 — Using `.clone()`

```rust
fn main() {
    let a = String::from("hello");
    let b = a.clone();

    println!("a = {}", a);
    println!("b = {}", b);
}
```

#### What I Observed

The program compiled successfully and printed:

```text
a = hello
b = hello
```

Unlike the previous example using `let b = a`, the original variable `a` remained usable after creating `b`.

This introduced me to the `Clone` trait. `Clone` is a trait that defines how a type can explicitly duplicate itself. The `.clone()` method calls the implementation provided by that type.

For a `String`, calling `.clone()` creates a separate `String` with its own heap allocation and contents. Both variables therefore own independent allocations and remain valid.

When the variables go out of scope, Rust automatically cleans up both allocations.

#### Comparison — Moving vs. Cloning

The two approaches produce different ownership behavior:

**Moving ownership:**

```rust
let a = String::from("hello");
let b = a;
```

- Ownership transfers from `a` to `b`.
- The original binding `a` can no longer be used.
- No second `String` allocation is needed.

**Explicit cloning:**

```rust
let a = String::from("hello");
let b = a.clone();
```

- A separate `String` is created for `b`.
- Both `a` and `b` remain usable.
- Each variable owns its own allocation.

This helped me understand that Rust does not prohibit duplicating heap-allocated data. Instead, it requires the programmer to explicitly request duplication rather than implicitly copying ownership.

#### Questions and Follow-ups

After confirming that `.clone()` allowed both variables to remain usable, I wanted to understand what was happening behind the method and why Rust required an explicit call.

**Questions I explored:**

1. Is `Clone` a trait like `Drop`, or is `.clone()` simply a library function?
2. Do primitive types such as `i32` also implement `Clone`?
3. Why does Rust require explicit cloning instead of automatically duplicating heap-allocated data?
4. What happens when `.clone()` attempts to allocate memory but the allocation fails?
5. Does Rust throw an exception, retry the allocation, or handle the failure another way?

#### Follow-up 1 — Understanding the `Clone` Trait

I learned that `Clone` is a trait, just like `Drop`, but the two traits serve different purposes.

- `Clone` defines how a type explicitly duplicates itself.
- `.clone()` is the method used to invoke that duplication.
- `Drop` defines cleanup behavior when a value goes out of scope.

I also learned that `Clone` is not limited to heap-allocated types. Primitive types such as `i32` implement both `Copy` and `Clone`.

For example:

```rust
let a: i32 = 5;
let b = a.clone();
```

Both variables remain valid. However, an `i32` does not need `.clone()` for ordinary assignment because it implements `Copy`, which allows its value to be copied implicitly.

This helped me distinguish between the traits: `Copy` allows implicit copying during assignment, while `Clone` provides an explicit way to duplicate a value.

#### Follow-up 2 — Why Is Cloning Explicit?

I considered why Rust requires `.clone()` to be called explicitly instead of automatically duplicating values during assignment.

I learned that automatically cloning heap-allocated data could introduce unnecessary memory allocations and copying. In cases where a programmer only wants to transfer ownership, duplicating the data would waste memory and processing time.

By making cloning explicit, Rust allows programmers to choose when duplicating data is necessary and when moving ownership is sufficient.

This also helped me understand why `String` implements `Clone` but not `Copy`. A `String` owns dynamically allocated memory and requires cleanup. Automatically copying its ownership could result in multiple variables attempting to manage the same allocation.

#### Follow-up 3 — What Happens if Cloning Fails?

I also wondered whether Rust handles memory allocation failures when `.clone()` creates a new heap allocation.

I learned that ownership and memory allocation are separate concerns. Rust's ownership system manages who is responsible for allocated memory and when it is cleaned up, but it does not guarantee that a new allocation will succeed.

For a standard `String::clone()`, an unrecoverable allocation failure normally invokes Rust's allocation error handler, which terminates the process rather than returning a recoverable `Result`.

Rust does not use conventional exceptions for this operation, and `String::clone()` does not provide a `Result` that allows the caller to recover from an allocation failure.

This helped me understand that Rust automates memory management, but it does not eliminate resource limitations.

#### What I Learned

Through this discovery, I learned that Rust provides different mechanisms for handling values depending on whether they need to be transferred or duplicated.

- Moving ownership transfers responsibility without creating another allocation.
- `Clone` allows a type to explicitly duplicate itself.
- `Copy` allows certain types to be copied implicitly.
- `Drop` handles cleanup when a value goes out of scope.

The most important distinction I took away is that Rust makes potentially expensive duplication explicit. This gives programmers control over memory allocation while allowing the language to manage ownership and cleanup automatically.

### AI Conversation Permalink
1. https://chatgpt.com/share/6af62a4b-e144-83e9-8fda-46b7778f5382
2. https://chatgpt.com/share/6af62a44-99dc-83e9-a9e1-d3b2a39277a2
3. https://chatgpt.com/share/6af62a3e-c278-83e9-9178-ff73a77af6d1
4. https://chatgpt.com/share/6af71b50-80a8-83e8-913d-cc7fb1c5f577

### Earlier AI Exploration — Claude

I initially began exploring Rust ownership in a separate Claude session. That session ended before I could develop the topic extensively, so I transferred the relevant discussion and progress into ChatGPT to continue the exploration.

The material from the earlier session is incorporated into this README.

**Original Claude conversation:** https://claude.ai/share/201ba1d8-649e-4d8f-a782-cb5c6228e87b
