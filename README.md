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

[Insert C example here]

#### What I Observed

[Document what happens when two pointers reference
the same allocation and what can go wrong when memory
is freed.]

#### Questions and Follow-ups

[Record questions asked during the AI exploration
and any clarifications.]
