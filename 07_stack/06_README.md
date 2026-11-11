# Program 06 — 32-bit Stack and Hexadecimal Values

## Purpose
This program demonstrates pushing and popping 32-bit register values, including hexadecimal values.

## Walkthrough
1. `mov eax, 0x11223344` loads the 32-bit hexadecimal value into EAX.
2. `mov ebx, 0x1234` loads `0x1234` into EBX.
3. `push eax` stores EAX on the stack. ESP decreases by 4 bytes.
4. `push ebx` stores EBX above the first value. ESP decreases by another 4 bytes.
5. `nop` has no effect.
6. `pop ebx` retrieves the most recently pushed value, `0x1234`, into EBX. ESP increases by 4 bytes.
7. `pop eax` retrieves `0x11223344` into EAX. ESP increases by another 4 bytes.
8. The Linux i386 exit system call ends the program. The exit setup overwrites EAX and EBX after the stack demonstration.

## Stack trace
Let the initial ESP be S.

| Instruction | Result | ESP |
|---|---|---|
| Start | — | S |
| `push eax` | Stores `0x11223344` | S − 4 |
| `push ebx` | Stores `0x1234` at the top | S − 8 |
| `pop ebx` | EBX = `0x1234` | S − 4 |
| `pop eax` | EAX = `0x11223344` | S |

## Key observation
This is the 32-bit counterpart of Program 05. Each push or pop changes ESP by 4 bytes, and the LIFO order restores the original values to their registers.

## Actual test
Assembled using `nasm -f elf32 06.asm -o 06.o`, linked using `ld -m elf_i386 06.o -o 06`, and executed using `./06`. Observed exit status: **0**. The 32-bit executable ran successfully on the x86_64 Ubuntu host. The program produces no terminal text output.
