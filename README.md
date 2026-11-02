# Rust-Ownership---Moving-Ownership
Explore what happens when ownership of a value is transferred from one variable to another, and why Rust prevents the original variable from accessing that value afterward.
Checkoff 3
Overview
In this checkoff, you'll use AI as a learning tool to explore a topic related to COMP 211 that we have not covered in depth. You'll then give a 5-7 minute presentation to your peers sharing what you learned, followed by Q&A. You are not expected to become an expert or cover every aspect of your topic. Instead, focus on a few things you found particularly interesting, surprising, or useful, and explain them in a way that your classmates can understand. 
Above all, this assignment is an opportunity to have fun exploring something new! Follow your curiosity, ask questions, and see where your learning takes you!
Components
Your final checkoff consists of four components:
1. In-Person Presentation
You'll give a 5-7 minute presentation, followed by approximately 3 minutes of Q&A, to share what you've learned with your classmates. A suggested outline is provided  in the Presentation Section below.
You must create your own presentation slides. Your slides should not be AI-generated. You should use AI to help you understand your topic, but the organization, explanations, and slides should reflect your own understanding and work.
2. Pre-Recorded Presentation
Before your scheduled in-person checkoff, you must submit a video recording of yourself giving your presentation. The recording should:
Include your complete 5-7 minute presentation.
Use the same slides and cover the same material you plan to present in person.
Be submitted before your scheduled checkoff.
This is an opportunity to practice your presentation, check your timing, and make sure you're prepared to present in person.
3. Public GitHub Repository
Create a public GitHub repository documenting your exploration and what you've learned.
Your repository should include:
README.md: Introduce your topic, explain what you explored, and summarize your most interesting discoveries.
Code examples: Include any code examples or experiments you created while exploring your topic. Provide instructions for running them.
Presentation materials: Include the slides you created for your presentation.
Additional resources: Include any useful references or resources you consulted.
Think of this repository as a small portfolio project that demonstrates your curiosity, initiative, and ability to learn independently.
4. Written Reflection on Your AI Exploration
Submit a short written reflection describing how you used AI to learn about your topic.
Remember, the purpose of this assignment is not simply to produce a presentation. We are particularly interested in your learning process and how you engaged with AI to develop your understanding.
Your reflection should address the following:
How did you approach learning your topic? What were your initial questions, and how did your exploration develop?
What prompts did you use? Share two or three representative prompts from your conversation. Choose prompts that demonstrate how you explored your topic, asked follow-up questions, or worked through something confusing.
How did you engage with AI? Describe how you used AI's responses to guide your learning. Did you ask clarifying questions, request examples, challenge an explanation, or test something yourself?
What would you do differently? Reflect briefly on what worked well and what you might change about how you use AI to learn in the future.
Include a permalink to your AI conversation so your TA can review your exploration.
What Are We Looking For?
A strong AI conversation might show you:
Asking follow-up questions when something wasn't clear.
Requesting examples or alternative explanations.
Connecting new ideas to concepts you've learned in COMP 211.
Testing or verifying information rather than automatically accepting it.
Explaining a concept in your own words and asking AI to check your understanding.
Signing up
Sign-up sheet: [Student] Checkoff 3 Sign-up

Sign up by Wednesday, November 11

Every student in the same slot must have a unique sub-topic

Examples of valid sign-up combinations
Example 1
Student 1: Garbage Collection, Generational Garbage Collection
Student 2: Buffer Overflows and Memory Vulnerabilities, Stack Buffer Overflows
Student 3: Compiler Optimizations, Loop Optimizations
Example 2
Student 1: Python Libraries Implemented in C
Student 2: Compiler Optimizations, Loop Optimizations
Student 3: Compiler Optimizations, Vectorization
Assignment Objectives: Why Are We Doing This?
One of the most important skills you can develop as a computer scientist is the ability to learn something new on your own. Technology changes quickly, and throughout your career, you'll encounter unfamiliar programming languages, tools, and concepts. Being able to explore something new, ask good questions, and figure things out independently is an incredibly valuable skill.
In this assignment, you'll choose a topic that interests you, use AI to help you learn about it, and share what you've discovered with your classmates.
What We Want You to Get Out of This Assignment
Learn how to learn with AI. AI can be a powerful learning tool when you use it thoughtfully. Practice asking good questions, following up when something doesn't make sense, requesting examples, and checking your understanding.
Develop your ability to learn independently. Think of this as a small, self-directed project. You'll choose what to explore, decide which questions to ask, and take responsibility for developing your own understanding. These are skills you'll use throughout your career.
Explore something that genuinely interests you. This is an opportunity to investigate an area of computer science that you might not otherwise encounter in class. You might discover a topic you want to learn more about, take additional courses in, or even pursue as a career!
Create something you can share. You'll create a public GitHub repository documenting your exploration and what you've learned. This can become part of your portfolio and demonstrate your curiosity, initiative, and ability to learn independently.
Build experience you can discuss in interviews. Employers value people who can tackle unfamiliar problems and teach themselves new skills. This project gives you a concrete example of how you approached learning something new, what challenges you encountered, and how you worked through them.
Practice communicating technical ideas. You'll share what you've learned with classmates who may be unfamiliar with your topic. Your goal is to make the material interesting and understandable, not to impress your audience with technical complexity.
Topics
Choose from one topic below. If you would like to present on a different topic, please reach out to Professor McMahon.
Data Representation
Applications of Bitwise Operators: Explore how bitwise operations are used to solve real-world problems beyond the applications we've covered in class.
Suggested applications to explore (choose one):
Network IP Addresses: Explore how subnet masks and bitwise AND operations are used to determine which network an IPv4 address belongs to.
Simple Encryption Using XOR: Explore how XOR can be used to encode and decode information, and why simple XOR-based encryption is not secure.
Checksums and CRCs: Explore how bitwise operations are used to detect errors in transmitted or stored data. Focus on a simple example rather than implementing a complex algorithm.
Chess Bitboards: Explore how chess programs use 64-bit integers to represent the positions of pieces on a chessboard and how bitwise operations help manipulate these representations.
Data Compression: Explore how computers reduce the amount of space needed to store or transmit information. 
Suggested techniques to explore (choose one):
Run-length encoding (RLE): A simple lossless technique that compresses repeated values.
Huffman coding: A lossless technique that uses shorter binary codes for frequently occurring symbols.
LZ77: A lossless technique that compresses data by identifying and referencing repeated sequences.

Memory and Memory Management
Garbage Collection: Explore how programming languages automatically manage memory and how garbage collection compares with manual memory management in C.
Suggested approaches to explore (choose one):
Reference Counting (Python): Explore how Python's CPython implementation tracks references to objects and reclaims memory when their reference counts reach zero.
Mark-and-Sweep Garbage Collection (Java or JavaScript): Explore how a garbage collector identifies objects that are still reachable and reclaims memory occupied by unreachable objects.
Generational Garbage Collection (Java): Explore why garbage collectors often treat newer and older objects differently to improve efficiency.
Concurrent Garbage Collection (Go): Explore how garbage collection can run alongside a program to reduce pauses.
Cyclic Garbage Collection (Python): Explore why reference counting alone cannot reclaim certain groups of objects that reference one another, and how Python handles these cycles.
Rust Ownership: Explore how Rust's ownership system manages memory without requiring a garbage collector. Compare Rust's approach with manual memory management in C, including how ownership helps prevent common memory errors.
Suggested concepts to explore (choose one):
Ownership and Automatic Memory Cleanup: Explore how Rust automatically releases memory when its owner goes out of scope, and compare this with using malloc and free in C.
Moving Ownership: Explore what happens when ownership of a value is transferred from one variable to another, and why Rust prevents the original variable from accessing that value afterward.
Preventing Double-Free Errors: Explore how Rust's ownership rules help prevent multiple attempts to free the same memory.
Preventing Use-After-Free Errors: Explore how Rust prevents programs from accessing memory after its owner has been destroyed.
Ownership and Function Calls: Explore what happens when values are passed to functions in Rust, including when ownership is transferred and when values are copied.
Ownership vs. Garbage Collection: Explore how Rust manages memory without a garbage collector and compare its approach with garbage-collected languages such as Python or Java.
Security 
Buffer Overflows and Memory Vulnerabilities: Explore how memory errors in programs can create security vulnerabilities and how programmers defend against them. Investigate why languages like C are particularly susceptible to certain memory vulnerabilities, and choose one type of vulnerability to explore in detail.
Suggested vulnerabilities to explore (choose one):
Stack Buffer Overflows: Investigate what happens when a program writes beyond the boundaries of a local array and how this can corrupt nearby memory.
Integer Overflows and Memory Safety: Investigate how integer overflow can lead to incorrect memory allocation sizes and potentially cause buffer overflows.
Uninitialized Memory: Explore the risks of reading memory before it has been initialized, including how programs might accidentally expose sensitive information.
Performance and Optimization
Compiler Optimizations: Explore how compilers transform programs to improve performance without changing their intended behavior. Investigate different compiler optimization levels (such as -O0, -O1, -O2, and -O3) and experiment with how they affect the performance of C programs. Choose at least one specific compiler optimization technique to investigate.
Suggested optimization techniques to explore (choose two):
Dead Code Elimination: Investigate how compilers identify and remove code that cannot affect a program's observable behavior.
Loop Optimizations: Explore how compilers transform loops to reduce execution time, such as through loop unrolling.
Function Inlining: Investigate how compilers can replace a function call with the function's code to reduce overhead.
OR Suggested optimization techniques to explore (choose one):
Common Subexpression Elimination: Explore how compilers avoid repeating calculations when the same expression is used multiple times.
Vectorization: Investigate how compilers can use SIMD instructions to perform the same operation on multiple values simultaneously.
Performance Benchmarking: C vs. Python: Explore how to benchmark programs to measure and compare their performance. Learn how to design reliable benchmarks, measure execution time, and interpret results. Apply what you've learned by benchmarking equivalent programs written in C and Python. You may choose which programs to compare.
Suggested programs to benchmark (choose one, or come up with your own):
Matrix Multiplication: Compare the performance of multiplying matrices of different sizes.
Finding Prime Numbers: Compare how long it takes to find prime numbers up to a given limit.
Sorting Arrays: Implement the same sorting algorithm in both languages and compare execution times.
String Processing: Compare how long it takes to search or process large amounts of text.
Searching Arrays: Compare the performance of searching through increasingly large arrays.
Summing Numbers: Compare how long it takes to sum a large sequence of integers.
Things to investigate:
How can you measure the execution time of a program?
What tools can you use to benchmark C and Python programs?
Why is it important to run a benchmark multiple times?
What factors can influence benchmark results?
How can you ensure that you're making a fair comparison?
How should you interpret and report your results?
Python Libraries Implemented in C: Explore how libraries like NumPy achieve high performance by implementing computationally intensive operations in C. Investigate how Python programs can call functions written in C and why this approach can improve performance.
Things to explore:
Calling C from Python: Write a simple function in C and learn how to call it from Python using a tool such as ctypes.
Compiling C for Use in Python: Explore how C code can be compiled into a shared library that Python can load and use.
How NumPy Works: Investigate how NumPy uses compiled implementations of operations to efficiently process large arrays.
Performance Comparison: Compare the performance of a computation implemented using a Python loop with an equivalent computation performed using NumPy.
Why Use C Extensions? Explore why Python programmers sometimes implement performance-critical operations in C rather than Python.
Operating Systems
Operating System Scheduling: Explore how operating systems decide which processes get to use the CPU when multiple processes are ready to run. Investigate how scheduling algorithms balance competing goals, such as fairness, responsiveness, and efficiency. Choose one scheduling algorithm to explore in detail and demonstrate how it works using an example or simulation.
Suggested scheduling algorithms to explore (choose one):
First-Come, First-Served (FCFS)
Shortest Job First (SJF)
Round-Robin Scheduling
Priority Scheduling
Multilevel Feedback Queue (MLFQ)
Linux's CPU Scheduler
Using AI Effectively to Explore Your Topic
For this assignment, you'll use AI to explore a topic that is new to you. The goal isn't just to collect information for your presentation, it's to use AI to help you develop a deeper understanding of your topic.
Think of AI as a tutor you can have a conversation with. You don't need to understand everything immediately, and you shouldn't feel limited to asking one question and accepting the first response.
Best Practices for Learning with AI
1. Start with what you already know.
Tell AI about your background so it can explain concepts at an appropriate level.
For example:
I'm a student taking a systems programming course. I know C, pointers, and basic memory management, but I haven't learned assembly. Can you explain how compiler optimizations work at my level?
2. Ask clarifying questions when you don't understand something.
If an explanation is confusing, don't just move on! Ask AI to explain it differently, break it into smaller steps, or clarify unfamiliar terminology.
For example:
I don't understand what you mean by dead code elimination. Can you explain it more simply?
You mentioned that the compiler can optimize away a variable. What does that mean?
3. Ask for examples.
Examples can make abstract concepts much easier to understand. You can request code examples, diagrams, analogies, or comparisons.
For example:
Can you show me a short C program that demonstrates this concept?
Can you walk me through that example step by step?
4. Connect new concepts to things you already know.
Relating unfamiliar ideas to concepts you've learned in COMP 211 can help you build understanding.
For example:
How does this relate to pointers and memory allocation in C?
Is this similar to anything we've learned about the stack and heap?
5. Ask follow-up questions that go deeper.
Once you understand the basics, explore why something works, when it's useful, or what happens in different situations.
For example:
Why would a programmer choose this approach over another?
What are the trade-offs?
What happens if we change this part of the program?
6. Ask AI to check your understanding.
One of the best ways to learn is to try explaining a concept yourself and get feedback.
For example:
Here's how I understand this concept: [your explanation]. Is that correct? What am I missing?
Can you give me a short question to test whether I understand this?
7. Don't assume AI is always correct.
AI can make mistakes, provide misleading explanations, or confidently present incorrect information. If something seems surprising or doesn't match what you've learned, investigate further.
For example:
Are there situations where this explanation wouldn't be correct?
Can you provide a source where I can verify this information?
Can you show me a C program I can run to test this claim?
8. Ask AI to help you explain what you've learned to others.
Remember that your classmates may not know anything about your topic. Practice explaining concepts in accessible language.
For example:
How would you explain this concept to someone who knows C but has never studied compiler optimizations?
Can you suggest an analogy that would help my classmates understand this?
What Does a Good AI Conversation Look Like?
A productive AI conversation is more than a series of unrelated questions. Your questions should build on what you're learning.
For example, a conversation about compiler optimizations might develop like this:
What are compiler optimizations?
Can you show me a simple example in C?
I don't understand why the compiler can remove that calculation. Can you explain?
How can I experiment with optimization levels using GCC?
I tried compiling my program with -O0 and -O2, but I didn't notice a difference in execution time. Why might that be?
Let me try explaining what I learned. Can you tell me if my understanding is correct?
Presentation
Presentation Skills
A good presentation helps your audience understand and stay engaged with your topic. As you prepare, keep the following in mind:
Introduce yourself and your topic. Briefly explain what you'll be discussing and why it's interesting.
Speak to your audience, not your slides. Use slides or notes to guide your presentation, but avoid reading directly from them.
Explain concepts in your own words. Don't assume your classmates already know the terminology. Use examples or analogies to make unfamiliar ideas easier to understand.
Speak clearly and at a comfortable pace. Give your classmates time to process new information, especially when introducing technical concepts.
Keep your slides simple. Avoid overcrowding slides with text. Use diagrams, examples, or code snippets when they help explain an idea.
Practice and manage your time. Rehearse your presentation to make sure it fits within the allotted 5-7 minutes.
Remember, you are not expected to be an expert or a professional public speaker! The goal is to share something interesting you've learned in a way your classmates can understand.
Suggested Presentation Outline (5-7 Minutes)
You have the freedom to organize your presentation however you'd like, but here is a suggested structure to help you get started. You don't need to cover everything you learned about your topic. Instead, focus on the ideas you found most interesting and think your classmates would enjoy learning about.
1. Introduction (~1 minute)
Introduce your topic and give your audience a reason to be interested in it.
What topic did you explore?
Why did you choose this topic?
Consider starting with a surprising fact, an interesting question, or a real-world application to capture your audience's attention.
2. Background and Key Concepts (~1 minute)
Provide enough background information for your classmates to understand the rest of your presentation.
What is your topic, and how does it work at a high level?
Are there any important terms or concepts your audience needs to understand?
What problem does this technology or concept solve? Why does it exist?
3. Interesting Discoveries (~3-4 minutes)
This should be the main part of your presentation! Share some of the most interesting things you discovered while exploring your topic.
Choose 2-3 interesting ideas, concepts, or discoveries to explain in more detail.
Use concrete examples to help your classmates understand what you're explaining.
Consider including:
A short code example or demonstration.
A diagram or visualization.
A comparison between two approaches or technologies.
A surprising behavior or result.
An interesting real-world application.
You don't need to cover every aspect of your topic. It's better to explain a few ideas clearly than to rush through too much information.
4. Takeaways and Reflection (~1 minute)
Wrap up by reflecting on what you learned.
What was the most interesting or surprising thing you discovered?
Did anything challenge an assumption you had before exploring the topic?
What questions do you still have?
Is there anything you'd like to learn more about?
End with one key takeaway you'd like your classmates to remember.
Audience Participation
Learning from your classmates is an important part of this checkoff! Everyone is expected to participate both as a presenter and as an audience member.
As a Presenter:
Ask your audience at least one question during your presentation.
Your question could ask classmates to
Make a prediction
Interpret an example

As an Audience Member:
After each presentation, you must ask the presenter at least one question about their topic.
Your question can ask for clarification, explore something you found interesting, or build on an idea from the presentation.
You are not expected to be an expert on the topic! The purpose is to be curious, engage with what your classmates learned, and encourage further discussion.
There are no expectations that your questions be particularly advanced or technical. Asking a thoughtful question about something you don't understand is just as valuable as asking a question that explores the topic in greater depth.
