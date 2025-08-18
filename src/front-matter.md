# Front Matter

## For Whom Is This Book Intended?

As mentioned, if you are already familiar with C (or languages descended
from C, such as C++ or Rust), this book begins with what you already know.

Later chapters dive more deeply into the corners and recesses of the
[ARM V8 ISA] [^1] and are suitable for those wishing to master the rich
instruction set of the 64 bit ARM processors.

[ARM V8 ISA]: https://en.wikipedia.org/wiki/AArch64

## Can This Book Be Used In Courses Covering Assembly Language?

Yes, absolutely!

## Calling Convention Used In This Book

Assembly language programming is quite closely dependent upon the
underlying hardware architecture. The host operating environment plays
an outsized role in determining how assembly language programs are
constructed. A "calling convention" refers to how functions are called
and how parameters are passed.

Originally, this book taught only the ARM Linux conventions. However,
over time, we developed a suite of macros that make it much easier to
write code for use either on MacOS or on Linux. You can take a look at
them, other utility macros and their documentation [here](./section-4/README.md).

```admonish info
You can find additional information about Apple Silicon assembly language
programming in [chapter 4.1](./section-4/apple-silicon.md).
```

You'll notice that we make use of the C-runtime (CRT) directly rather than
make OS system calls. So, for instance, if we want to call `write()`,
we call `write` from the assembly language.

This version of the system call `write` is a wrapper function built into
the C-runtime which handles the lower level details of performing
a system call. See [chapter 4.4](./section-4/system-calls.md) on what
actually happens inside these wrapper functions.

The benefit of using the CRT wrappers is that differences between various
distributions and specific system architectures are masked. Therefore, when you
use the wrappers rather than the direct method of making system calls, your code
will be more portable.

## A Lot of Names

As commendable as the ARM designs are, ARM's naming conventions for
their Intellectual Properties are horrid. In this book, AArch64 and ARM
V8 are taken to be synonyms for the 64 bit ARM ISA[^1].

It is very difficult to find documentation at the ARM site because they
have *so many versions*, so many names for the same thing and so much
documentation in general. It really can be maddening.

Within the text we will provide germane links as appropriate.

[Here](https://developer.arm.com/documentation/ddi0602/latest)
is a link to "a" main instruction set page.

## What you need to work with assembly language on Linux/MacOS

Getting the tools for assembly language development is quite straightforward -
perhaps you already have them. Using `apt` from the Linux terminal, say:

```sh
sudo apt update
sudo apt install build-essential gdb
```

On the Macintosh type:

```sh
xcode-select --install
```

and follow directions. Note that `gdb` is replaced by `lldb` with just enough
differences to make you cry.

Then you'll need your favorite editor. We ourselves use `vi` for quick
edits and Visual Studio Code for any heavy lifting.

## How to build assembly code

We use `gcc`, the C "compiler". `g++` and `clang` can also be used.

But wait! What sense does that make... using a "compiler" to "compile" assembly
code!?

Well, to answer that, one must understand that the word "compiler" refers
to only one step in a build sequence. What we talk about as being the
"compiler" is actually an umbrella that includes:

* The **preprocessor** that acts on any `#` preprocessor commands (like
  `#include`). These commands are not part of C or C++. Rather, they
  are commands to the preprocessor.

```admonish note
  `gcc` will invoke the C preprocessor if your assembly
  language file ends in `.S` - capital S. It may or may not be invoked
  if your file ends in a lower case `s` or any other file extension -
  depending on your system.
```

* The *actual* **compiler**, whose job it is turn high level languages
  such as C and C++ into assembly language.

* The **assembler**, which turns assembly language into machine code which
  is not quite ready for execution.

* And finally, the **linker**, which combines potentially many intermediate
  machine code files (called object files), potentially many library
  files (statically linked `.dll`s on Windows and `.a` files on Linux). The
  linker is the last step in this chain.

[Here](https://youtu.be/Iv3psS4n9j8) is a video explaining this process.

We use `gcc` and `g++` directly because, being umbrellas, they automate
the above steps and automatically link with the CRT.

Suppose you've implemented `main()` in a C file (`main.c`) and want to
make use of an assembly language file you have written (`asm.S`). This can
be achieved in several ways.

### All at once

```sh
gcc main.c asm.S
```

That's all you need for a minimal build. The resulting program will be
written to `a.out`. All the intermediate object files (in this case, `main.o`
and `asm.o`) that are generated will be automatically removed, before you can
inspect them.

### Modularly

```sh
gcc -c main.c
gcc -c asm.S
gcc main.o asm.o
```

Used this way, `.o` files are left on disk.

## If there are no C or C++ modules used

Now, let's suppose `main()` is implemented in assembly language and `main.S` is
self-contained. Then simply:

```sh
gcc main.S
```

will be enough to create the resulting binary.

Often, you will want to include debug info (consumed by debuggers like `gdb` or
`lldb`) for later debugging of your binary. To include the debug info, pass `-g`
to the invocation of `gcc`.

```sh
gcc -g main.S
```

Without the `-g` command line option, the debugger could have difficulty to
debug your program.

### The C Preprocessor

To repeat, if you want `gcc` to run your code through the C
pre-processor (for handing `#include`s for example), name your assembly
language source code files with a capital S. So, on Linux:

```sh
gcc main.s
```

Will not go through the C preprocessor but

```sh
gcc main.S
```

will.

### Programs called by the "compiler"

To drive home the point that the "compiler" is an umbrella, using `gcc` to
"compile" a program causes the following to be called on Ubuntu running
on ARM:

```sh
/usr/bin/cpp
/usr/lib/gcc/aarch64-linux-gnu/11/cc1
/usr/bin/as
/usr/lib/gcc/aarch64-linux-gnu/11/collect2 // which internally calls...
/usr/bin/ld
```

`cpp` is the C preprocessor - it is a general tool that is used by other
languages as well (C++, for example).

`cc1` is the actual *compiler* (i.e. the program that translates from a higher
language to assembly code).

`as` is the assembler.

`ld` is the linker.

You can see why we default to using the umbrella command in this book.

[^1]: [Instruction Set Architecture](https://en.wikipedia.org/wiki/Instruction_set_architecture)
