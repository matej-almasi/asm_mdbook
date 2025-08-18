# A Gentle Introduction to Assembly Language Programming - mdBook version


## Front Matter

## Table of Contents

### Section 1 - Bridging from C / C++ to Assembly Language

We start by providing what we're calling "bridging" from C and C++ to
assembly language. We use the knowledge you already have to learn new
knowledge - how cool is that!

| Chapter | Markdown | PDF |
| ------- | -------- | --- |
| 0 | [Kickstart](./section_1/kickstart.md) | [Link](./section_1/kickstart.pdf) |
| 1 | [Hello World](./section_1/hello_world/README.md) | [Link](./section_1/hello_world/README.pdf)  |
| 2 | [If Statements](./section_1/if/README.md) | [Link](./section_1/if/README.pdf) |
| 3 | Loops | |
| 3a | [While Loops](./section_1/while/README.md) | [Link](./section_1/while/README.pdf) |
| 3b | [For Loops](./section_1/for/README.md) | [Link](./section_1/for/README.pdf) |
| 3c | [Implementing Continue](./section_1/for/README.md#implementing-a-continue) | [Link](./section_1/for/README.pdf) |
| 3d | [Implementing Break](./section_1/for/README.md#implementing-a-break) |  [Link](./section_1/for/README.pdf) |
| 4 | Interludes | |
| 4a | [Registers](./section_1/regs/README.md) | [Link](./section_1/regs/README.pdf) |
| 4b | [Load and Store](./section_1/regs/ldr.md) | [Link](./section_1/regs/ldr.pdf) |
| 4c | [More About `ldr`](./section_1/regs/ldr2.md) | [Link](./section_1/regs/ldr2.pdf) |
| 4d | [Register Sizes](./section_1/regs/widths.md) | [Link](./section_1/regs/widths.pdf) |
| 4e | [Hexadecimal](./section_1/hex.md) | [Link](./section_1/hex.pdf) |
| 5 | [`switch`](./section_1/jump_tables/README.md) | [Link](./section_1/jump_tables/README.pdf) |
| 6 | Functions | |
| 6a | [Calling and Returning](./section_1/funcs/README.md) | [Link](./section_1/funcs/README.pdf) |
| 6b | [Passing Parameters](./section_1/funcs/README2.md) | [Link](./section_1/funcs/README2.pdf) |
| 6c | [Example of calling some common C runtime functions](./section_1/funcs/README3.md) | [Link](./section_1/funcs/README3.pdf) |
| 7 | [FizzBuzz - a Complete Program](./section_1/fizzbuzz/README.md) | [Link](./section_1/fizzbuzz/README.pdf) |
| 8 | Structs | |
| 8a | [Alignment](./section_1/structs/alignment.md) | [Link](./section_1/structs/alignment.pdf) |
| 8b | [Defining](./section_1/structs/defining.md) | [Link](./section_1/structs/defining.pdf) |
| 8c | [Using](./section_1/structs/using.md) | [Link](./section_1/structs/using.pdf) |
| 8d | [What is "this"](./section_1/structs/this.md) | [Link](./section_1/structs/this.pdf) |
|  9 | [`const`](./section_1/const/README.md) | [Link](./section_1/const/README.pdf) |

### Section 2 - Floating Point

Floating point operations use their own instructions and their own set
of registers. Therefore, floating point operations are covered in their
own section:

| Chapter | Markdown | PDF |
| ------- | -------- | --- |
| 0 | [Chapter Overview](./section_2/float/README.md) | [Link](./section_2/float/README.pdf) |
| 1 | [What Are Floating Point Numbers?](./section_2/float/what.md) | [Link](./section_2/float/what.pdf) |
| 2 | [Registers](./section_2/float/working.md) | [Link](./section_2/float/working.pdf) |
| 3 | [Truncation and Rounding](./section_2/float/rounding.md) | [Link](./section_2/float/rounding.pdf) |
| 4 | [Literals](./section_2/float/literals.md) | [Link](./section_2/float/literals.pdf) |
| 5 | [`fmov`](./section_2/float/fmov.md) | [Link](./section_2/float/fmov.pdf) |
| 6 | [Half Precision Floats](./section_2/float/half.md) | [Link](./section_2/float/half.pdf) |
| 7 | [NEON SIMD Not Yet Written](./not_written_yet.md) | [Link](./not_written_yet.pdf) |

### Section 3 - Bit Manipulation

What would a book about assembly language be without bit bashing?

| Chapter | Markdown | PDF |
| ------- | -------- | --- |
| 1 | Bit Fields | |
| 1a | [Without Bit Fields](./section_3/bitfields/README.md) | [Link](./section_3/bitfields/README.pdf) |
| 1b | [With Bit Fields](./section_3/bitfields/with.md) | [Link](./section_3/bitfields/with.pdf) |
| 1c | [Review of Newly Described Instructions](./section_3/bitfields/review.md) | [Link](./section_3/bitfields/review.pdf) |
| 2 | [Endianness](./section_3/endian/README.md) | [Link](./section_3/endian/README.pdf) |

### Section 4 - More Stuff

In this section, we present miscellaneous material including our "world
famous lecture" on debugging. This lecture has been invited at several
colleges and universities. It is intended for audiences working with
languages like C, C++ and assembly language but some of the lessons
contained therein are applicable to all languages.

| Chapter | Markdown | PDF |
| ------- | -------- | --- |
| 1  | [Apple Silicon](./more/apple_silicon/README.md) | [Link](./more/apple_silicon/README.pdf) |
| 2  | [Apple / Linux Convergence](./macros) | [Link](./macros/README.pdf) |
| 3  | [Variadic Functions](./more/varargs/README.md) | [Link](./more/varargs/README.pdf) |
| 4  | [Under the hood: System Calls](./more/system_calls/README.md) | [Link](./more/system_calls/README.pdf) |
| 5  | [Determining string literal lengths for C functions](./more/strlen_for_c/README.md) | [Link](./more/strlen_for_c/README.pdf) |
| 6  | [Calling Assembly Language From Python](./python/) | [Link](./python/README.pdf) |
| 7  | [Atomic Operations](./more/atomics/README.md) | [Link](./more/atomics/README.pdf) |
| 8  | [Jump Tables](./more/jump_tables/README.md) | [Link](./more/jump_tables/README.pdf) |
| 9  | [argv](./more/argv_example/jess1.S) | ASM CODE |
| 10 | [spin-locks](./more/spin-lock/) | [Link](./more/spin-lock/README.pdf) |
| - | [Debugging Lecture](./debugging/Discourses%20and%20Dialogs%20on%20Debugging.pptx) | PPTX |

## Macro Suite

As indicated immediately above, the macro suite [can be found
here](./macros/).

## Projects

[Here](./projects/README.md) are some project specifications to offer a
challenge to your growing mastery. Here are very brief descriptions
presented in alphabetical order.

* Perhaps before you tackle these, check out the fully described
[FIZZBUZZ](./section_1/fizzbuzz/README.md) program first.

* Then try [this](./projects/first_project/README.md) as your very first
project. With some blank lines and comments it weighs in at 35 lines.

* The [DIRENT](./projects/DIRENT/README.md) project demonstrates how a
complex `struct` can be used in assembly language.

* The [PI](./projects/PI/README.md) project demonstrates floating point
instructions. The program will "throw darts at a target," calculating
an approximation of PI by tracking how many darts "hit the target"
versus the total number of darts "thrown".

* The [SINE](./projects/SINE/README.md) project stresses floating point
math and functions.

* The [SNOW](./projects/snow/README.md) project uses 1970's era tech to
animate a simple particle system. This project demonstrates a reasonable
design process of breaking down complex problems into simpler parts.

* The [WALKIES](./projects/walkies/README.md) presents a cute little
animation demonstrating looping with some pointer dereferencing.

## About The Author

Perry Kivolowitz's career in the Computer Sciences spans just under five
decades. He launched more than 5 companies, mostly relating to hardware,
image processing and visual effects (for motion pictures and
television). Perry received Emmy recognition for his work on the The
Gathering, the pilot episode of Babylon 5. Later he received an Emmy
Award for Engineering along with his colleagues at [SilhouetteFX,
LLC](https://en.wikipedia.org/wiki/SilhouetteFX). SilhouetteFX is used
in almost every significant motion picture for rotoscoping, paint,
tracking, 2D to 3D reconstruction, compositing and more.

In 1996 Perry received an [Academy Award for Scientific and Technical
Achievement](https://en.wikipedia.org/wiki/Academy_Award_for_Technical_Achievement)
for his invention of Shape Driven Warping and Morphing. This is the
technique responsible for many of the famous effects in Forrest Gump,
Titanic and Stargate.

Twenty twenty three marks Perry's 19th year teaching Computer Science at
the college level, ten years at the UW Madison and now 8+ at Carthage
College.

Assembly language is a passion for Perry having worked in the following
ISAs (in chronological order):

* Univac 1100

* Digital Equipment Corporation PDP-11

* Digital Equipment Corporation VAX-11

* Motorola 68000

* ARM beginning with AARCH64

This work is dedicated to my wife Sara and sons Ian and Evan.

### Gratuitous Plugs

Perry has created a library of about 200 programming projects suitable
for CS 1, CS 2, Data Structures, Networking, Operating Systems and
Computer Organization classes. If a publisher of CS text books (or other
CS related content) would be interested in purchasing the library,
please reach out.

Also, check out [Get Off My
L@wn](https://www.amazon.com/Get-Off-My-Zombie-Novel-ebook/dp/B00DQ26J8G),
a Zombie novel for coders.

You read that right... elite programmer Doug Handsman retires to his
wife Ruth Ann's native northern Wisconsin. And then, well, the
apocalypse happens. Bummer.

Rated 4.3 out of 5 with more than 70 reviews, it's a fun read and costs
next to nothing.
