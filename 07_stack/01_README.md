# Program 01 — Basic 64-bit PUSH and POP

## Purpose
This program demonstrates how values are placed on and removed from the 64-bit stack using `push` and `pop`.

## Walkthrough
1. `mov rax, 100` places 100 in RAX.
2. `mov rbx, 200` places 200 in RBX.
3. `push rax` places 100 on the stack. RSP decreases by 8 bytes.
4. `push rbx` places 200 above the previous stack item. RSP decreases by another 8 bytes.
5. `nop` has no effect.
6. `pop rcx` removes the most recently pushed value, 200, into RCX. RSP increases by 8 bytes.
7. `pop rdx` removes 100 into RDX. RSP increases by another 8 bytes.
8. The exit system call ends the program.

## Stack trace
Let the initial RSP be S.

| Instruction | Result | RSP |
|---|---|---|
| Start | — | S |
| `push rax` | Stack top = 100 | S − 8 |
| `push rbx` | Stack top = 200; 100 remains below | S − 16 |
| `pop rcx` | RCX = 200 | S − 8 |
| `pop rdx` | RDX = 100 | S |

## Key observation
The stack follows Last In, First Out (LIFO): the last value pushed (200) is the first value popped. The two pops restore RSP to its original value.

## Actual test
Assembled using `nasm -f elf64 01.asm -o 01.o`, linked using `ld 01.o -o 01`, and executed using `./01`. Observed exit status: **0**. The program produces no terminal text output.
