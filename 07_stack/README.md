# 07_stack — Stack Assembly Programs

This folder contains six NASM assembly programs demonstrating stack operations, procedure calls, stack frames, and the difference between 32-bit and 64-bit stack behavior.

## Test environment

The original `.asm` files were assembled, linked, and executed on the user's Ubuntu machine with:

- NASM 3.01
- GNU ld (GNU Binutils for Ubuntu) 2.46
- Host architecture: `x86_64`

## Actual test results

Each original source file was assembled with NASM, linked with `ld`, and run. All six programs completed with exit status `0`.

| Source | NASM format | Link command | Observed result |
|---|---|---|---|
| `01.asm` | `elf64` | `ld 01.o -o 01` | Exit status 0 |
| `02.asm` | `elf64` | `ld 02.o -o 02` | Exit status 0 |
| `03.asm` | `elf64` | `ld 03.o -o 03` | Exit status 0 |
| `04.asm` | `elf32` | `ld -m elf_i386 04.o -o 04` | Exit status 0 |
| `05.asm` | `elf64` | `ld 05.o -o 05` | Exit status 0 |
| `06.asm` | `elf32` | `ld -m elf_i386 06.o -o 06` | Exit status 0 |

The programs do not print text to the terminal. A successful run is therefore confirmed by the shell's `Exit status: 0` result.

## Stack basics

The stack is a memory area used to hold temporary data, saved registers, and procedure return addresses. It grows toward lower memory addresses on x86: a push moves the stack pointer down, while a pop moves it up.

- In 64-bit mode, `RSP` is the stack pointer. A general-purpose register push or pop changes it by 8 bytes.
- In 32-bit mode, `ESP` is the stack pointer. A general-purpose register push or pop changes it by 4 bytes.
- `CALL` places the return address on the stack. `RET` removes that address and transfers control back to the caller.
- `NOP` does nothing and does not change the stack pointer.

See each numbered folder for the individual program's explanation and stack trace.
