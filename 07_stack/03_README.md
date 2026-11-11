# Program 03 — CALL and RET

## Purpose
This program demonstrates how CALL and RET use the stack to support a simple procedure.

## Walkthrough
1. `mov rax, 10` puts 10 in RAX.
2. `call calculate` pushes the return address onto the stack and jumps to `calculate`. In 64-bit mode, the return address occupies 8 bytes, so RSP decreases by 8.
3. `add rax, 5` adds 5 to RAX. RAX becomes 15. This instruction does not change RSP.
4. `ret` pops the return address from the stack and continues at `after_call`. RSP increases by 8 and returns to its original value.
5. The `nop` at `after_call` has no effect. At this point, RAX contains 15, as the source comment indicates.
6. The exit system call ends the program. It reuses RAX to hold the syscall number, so RAX is overwritten after the calculation.

## Stack trace
Let S be RSP immediately before CALL.

| Instruction | Stack effect | RSP |
|---|---|---|
| Before CALL | — | S |
| `call calculate` | Pushes return address | S − 8 |
| `add rax, 5` | No stack change | S − 8 |
| `ret` | Pops return address | S |

## Key observation
CALL automatically saves where execution must resume. RET retrieves that address. The stack is used for control flow even though this procedure does not explicitly push any data register.

## Actual test
Assembled using `nasm -f elf64 03.asm -o 03.o`, linked using `ld 03.o -o 03`, and executed using `./03`. Observed exit status: **0**. The program produces no terminal text output.
