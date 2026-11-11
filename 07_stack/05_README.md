# Program 05 — 64-bit Stack and Hexadecimal Values

## Purpose
This program demonstrates pushing and popping 64-bit register values, including a large hexadecimal value.

## Walkthrough
1. `mov rax, 0x1122334455667788` loads the 64-bit hexadecimal value into RAX.
2. `mov rbx, 0x1234` loads `0x1234` into RBX.
3. `push rax` stores the 64-bit RAX value on the stack. RSP decreases by 8 bytes.
4. `push rbx` stores RBX above the first value. RSP decreases by another 8 bytes.
5. `nop` has no effect.
6. `pop rbx` retrieves the most recently pushed value, `0x1234`, into RBX. RSP increases by 8 bytes.
7. `pop rax` retrieves `0x1122334455667788` into RAX. RSP increases by another 8 bytes.
8. The exit system call ends the program.

## Stack trace
Let the initial RSP be S.

| Instruction | Result | RSP |
|---|---|---|
| Start | — | S |
| `push rax` | Stores `0x1122334455667788` | S − 8 |
| `push rbx` | Stores `0x1234` at the top | S − 16 |
| `pop rbx` | RBX = `0x1234` | S − 8 |
| `pop rax` | RAX = `0x1122334455667788` | S |

## Key observation
The values are restored to their original registers because the pop order is the reverse of the push order. Each 64-bit push or pop changes RSP by 8 bytes.

## Actual test
Assembled using `nasm -f elf64 05.asm -o 05`, linked using `ld 05.o -o 05`, and executed using `./05`. Observed exit status: **0**. The program produces no terminal text output.
