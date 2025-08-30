# Section 1 - Bridging from C / C++ to Assembly Language

We start by providing what we're calling "bridging" from C and C++ to assembly language.
We use the knowledge you already have to learn new knowledge - how cool is that!

## Kickstart

In this section, we'll kickstart our exploration of AArch64 assembly
language.

### Registers

At the dawn of time, central processing units (CPUs) could operate upon
memory directly as both were relatively the same speed. CPUs got smaller
and faster, leaving the speed of memory in the dust. At the same time,
memory was getting further and further away.

For (a rather typical) example, the CPU might be on one board, while
the RAM on another, requiring access over a shared bus.

The idea of registers was introduced a very long time ago as a form of
very fast storage that is implemented directly in the CPU. Because the
registers are within the CPU, distance isn't really an issue. Similarly,
because the registers are in the CPU, they operate at the speed of CPU
itself.

There are several important differences between CPU registers and regular
"memory". First of all, the registers don't have addresses, because they
are not considered a part of "memory". Instead, they have specific names
and naming conventions. Registers have only a minimal concept of "data
types", as apart from integer, floating point (single or double
precision) and pointer, every other notion of a "type" is syntactic sugar
provided by your language and its compiler.

ARM processors are [RISC] [^1] processors. The rough idea behind RISC is to make
instructions simpler so as to make room for more registers. AArch64 (what we are
studying) has a lot of registers - 32 integer registers and 32 floating point
registers.

[RISC]: https://en.wikipedia.org/wiki/Reduced_instruction_set_computer
[^1]: Reduced Instruction Set Computer

### Register nomenclature

Register names follow a simple general pattern (with some exceptions): 

`rN` - a letter (`r`) - designating the register's kind ("type"),
followed by a number (`N`) - identifying a specific register of the given
kind.

```admonish example
Register `x2` means a register of type `x` (see below) number `2`.
```
 
Here is an introductory summary of register kinds:

| Letter  |             Kind                     |
| :-----: | ------------------------------------ |
|   `x`   | 64 bit integer or pointer            |
|   `w`   | 32 bit *or smaller* integer          |
|   `d`   | 64 bit (**d**ouble precision) floats |
|   `s`   | 32 bit (**s**ingle precision) floats |
|   ...   |             *other kinds*              |

```admonish info
Some register kinds have been left out.
```

### Integers

| This *declares* an integer (variable in the C language) | This *is* an integer (register in assembly) |
| :-----------------------------------------------------: | :-----------------------------------------: |
|                         `char`                          |                     `wN`                    |
|                         `short`                         |                     `wN`                    |
|                         `int`                           |                     `wN`                    |
|                         `long`                          |                     `xN`                    |

Registers do not have to be declared. They simply **exist**.

```admonish note
There are 32 integer registers; however, only 31 (`x0` - `x30`) are available
for "general use" (and, slightly confusingly, register `x30` has a special use).
```

When you want to perform a 64 bit integer operation you use one of the `x`
registers. For all other integer operations, you use a `w` register and
further specify the size by using different instructions, as you'll see later.

```admonish important
The `wN` register occupies the lower portion of a corresponding `xN` register.
This means that a write to e.g. `w2`, simultaneously overwrites the lower bits
of `x2` and a write to e.g. `x4` completely overwrites `w4`.

|  reg  | 63  | 62  | 61  | ... | 32  | 31  | 30  | ... |  2  |  1  |  0  |
| :---: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| `rN`  |  x  |  x  |  x  |  x  |  x  |  x  |  x  |  x  |  x  |  x  |  x  |
| `wN`  |     |     |     |     |     |  x  |  x  |  x  |  x  |  x  |  x  |
```

#### Pointers

| This *declares* a pointer (in e.g. C) | This *is* a pointer (in assembly) |
| :-----------------------------------: | :-------------------------------: |
|                `char*`                |                `xN`               |
|                `int*`                 |                `xN`               |
|                `float*`               |                `xN`               |
|                `char**`               |                `xN`               |

All pointers are stored in `x` registers. `x` registers are 64 bits long.

```admonish note 
Even though all pointers are stored in 64 bit registers, many operating systems
do not support 64 bit address spaces. This is because keeping track of such a
large address space itself would use a lot of space. Instead, OS's typically
have 48 - 52 bit address spaces. So, while a pointer sits in a 64 bit register,
it is very much possible that not all of the bits are actually used by the pointer.
```

#### Floats

There are 32 additional registers for floating point values, ranging from
half precision[^2] through single precision to double precision floats
and beyond.

```admonish question
What is beyond double?

[Vector registers] (a special kind of register we haven't
mentioned yet) can support multiple values in a single "very large" register.

[Vector registers]: https://www.corsix.org/content/whirlwind-tour-aarch64-vector-instructions
```

[^2]: If you've never heard of *half floats*, don't worry. After this course
you will likely never hear of them again.

### Instructions

Remember what RISC means? *Reduced Instruction Set*? Well, that was *then*.
This is **now**. AArch64 has an *enormous* instruction set - hundreds of
instructions, each potentially with many variations.

*You will be responsible for mastering every one.*

... just kidding - you won't be responsible for too too many. Relatively few,
actually. Even so, you will be able to write sophisticated programs.

```admonish important
**EVERY** AArch64 instruction is **4** bytes wide. Everything the CPU needs
to know about what the instruction is and what variation it might be, plus what
data it will use, will be found in those 4 bytes.
```

You might immediately wonder: *How* could you load a big **big** number into
a register, if the whole instruction is exactly and always 4 bytes long?

*Be patient, campers.*

```admonish info
We can draw a distinction between the RISC nature of ARM and the [CISC] [^3]
nature of Intel or AMD processors. The x86 and x64 ISA has variable length
instructions ranging from 1 to **15** bytes in length! Complex indeed!
```

Every instruction is specified by a ***mnemonic*** consisting of some letters
which the *assembler* converts into numeric ***op-codes***.

Most (but not all) AArch64 instructions have three ***operands***. These
are read in the following way:

```
    op    ra, rb, rc
    │     │   │   └─ operand 3
    │     │   │
    │     │   └───── operand 2
    │     │      
    │     └───────── operand 1
    │          
    └── the instruction mnemonic
```

and mean the following:

```asm
    ra = rb op rc
```

```admonish example
A subtraction operation that subtracts `x1` from `x2` and stores the result
in `x0`:
 
    sub    x0, x2, x1

which means:

    x0 = x2 - x1
```

```admonish example
An example of a two operand instruction is:

    mov    x0, x1

This means *copy* the 64 bit contents of `x1` into the 64 bit register `x0`.
Or, in other words:

    x0 = x1

```

[CISC]: https://en.wikipedia.org/wiki/Complex_instruction_set_computer
[^3]: Complex Instruction Set Computers

### Mixing Register Types

With a few exceptions, different register types cannot be part of the same
instruction. For example, adding a 64 bit register to a 32 bit register
cannot be done.

```admonish example
Given:

    mov    w0, 10       // copy a 32 bit literal 10 in w0

You cannot do this:

    add    x1, w0, x1   // attempts to add w0 and x1 - BAD

But you can do this:

    add    x1, x0, x1   // This is fine
```

Putting a smaller-than-64-bit value into an integer register zeros out the
higher order bits (ignoring the sign bit - will be explained later).

### Two Instructions for Dealing with Memory

With minimal exception, the AArch64 ISA permits operations to be performed only
on data in registers. Two obvious instruction families are those for transferring
data from RAM to register(s) and those for transferring data from register(s)
to RAM.

Both loading and storing instructions must specify:

* The registers involved
* The address in RAM involved (always held in an `x` register)

Loading has the general form of:

```asm
    ldr    rN, [xM]
```

Which means:

"Load the value located at address `xM` and place it to register `rN`."

```admonish example
The following assembly:

    mov x1, #0x4f0c  // set x1 to hold a literal value 0x4f0c
    ldr x0, [x1]     // load whatever is stored at address 0x4f0c to register x0

would load whatever value is stored at address 0x4f0c.
```

This is analogous to the following C-like code:

```c
    // main.c
    some_type* ptr = some_address;
    some_type var;

    var = *ptr;
```

Storing has the general form of:

```asm
   str   rn, [xm]
```

This is like:

```c
   // main.c
   some_type* ptr = some_address;
   some_type var;

   *ptr = var;
```

```admonish caution
The analogies are not exact, but close.
```

Pairs of registers can also be stored and loaded with the [`stp` and `ldp`] op-codes.

```admonish note
Post- and pre- increment and decrement of the pointer involved are also supported.
```

[`stp` and `ldp`]: https://developer.arm.com/documentation/102374/0102/Loads-and-stores---load-pair-and-store-pair



```admonish success
Now You Are Ready to Proceed!

Have fun!
```
