# Program 04 — 32-bit Procedure Stack Frame

## Purpose
This program demonstrates a stack frame in 32-bit mode, using ESP and EBP and reserving space for two 4-byte local variables.

## Walkthrough
1. `_start` executes `call work`. CALL pushes a 4-byte return address and jumps to `work`.
2. `push ebp` saves the caller's EBP. ESP decreases by 4 bytes.
3. `mov ebp, esp` establishes EBP as the frame pointer.
4. `sub esp, 8` reserves 8 bytes for two 4-byte local variables. ESP decreases by 8 more bytes.
5. `mov dword [ebp - 4], 100` stores 100 in the first local slot.
6. `mov dword [ebp - 8], 200` stores 200 in the second local slot.
7. The next two instructions load the local values into EAX and EBX. They do not change ESP.
8. `mov esp, ebp` releases the local storage.
9. `pop ebp` restores the previous EBP and increases ESP by 4 bytes.
10. `ret` pops the return address and returns to `_start`.
11. `_start` uses the Linux i386 exit system call (`int 0x80`).

## Stack trace
Let S be ESP immediately before `call work`.

| Instruction | Stack effect | ESP |
|---|---|---|
| Before CALL | — | S |
| `call work` | Pushes 4-byte return address | S − 4 |
| `push ebp` | Saves old EBP | S − 8 |
| `mov ebp, esp` | Establishes frame pointer | S − 8 |
| `sub esp, 8` | Reserves local storage | S − 16 |
| Store/load locals | No stack-pointer change | S − 16 |
| `mov esp, ebp` | Releases local storage | S − 8 |
| `pop ebp` | Restores old EBP | S − 4 |
| `ret` | Removes return address | S |

## Key observation
The logic is similar to Program 02, but this is 32-bit code: the return address and saved EBP each occupy 4 bytes, and ESP is the stack pointer. The two local variables use 8 bytes in total.

## Actual test
Assembled using `nasm -f elf32 04.asm -o 04`, linked using `ld -m elf_i386 04.o -o 04`, and executed using `./04`. Observed exit status: **0**. The 32-bit executable ran successfully on the x86_64 Ubuntu host. The program produces no terminal text output.
