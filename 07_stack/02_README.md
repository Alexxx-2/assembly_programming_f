# Program 02 — 64-bit Procedure Stack Frame

## Purpose
This program demonstrates a procedure call, saving the old frame pointer, reserving local stack space, accessing local variables, and restoring the stack frame before returning.

## Walkthrough
1. `_start` executes `call work`. CALL pushes the address of the instruction after the call onto the stack, then transfers control to `work`.
2. `push rbp` saves the caller's RBP value on the stack. RSP decreases by 8 bytes.
3. `mov rbp, rsp` makes RBP the reference point for this procedure's stack frame.
4. `sub rsp, 16` reserves 16 bytes for local data. RSP decreases by 16 more bytes.
5. `mov qword [rbp - 8], 100` stores 100 in the first 8-byte local slot.
6. `mov qword [rbp - 16], 200` stores 200 in the second 8-byte local slot.
7. The two `mov` instructions load those local values into RAX and RBX. These loads do not change RSP.
8. `mov rsp, rbp` releases the 16 bytes reserved for local variables by restoring RSP to the saved frame position.
9. `pop rbp` restores the caller's RBP and increases RSP by 8 bytes.
10. `ret` takes the saved return address from the stack and returns to `_start`.
11. `_start` performs the exit system call.

## Stack trace
Let S be RSP immediately before `call work`.

| Instruction | Stack effect | RSP |
|---|---|---|
| Before CALL | — | S |
| `call work` | Pushes 8-byte return address | S − 8 |
| `push rbp` | Saves old RBP | S − 16 |
| `mov rbp, rsp` | Establishes frame pointer | S − 16 |
| `sub rsp, 16` | Reserves local storage | S − 32 |
| Store/load locals | No stack-pointer change | S − 32 |
| `mov rsp, rbp` | Releases local storage | S − 16 |
| `pop rbp` | Restores old RBP | S − 8 |
| `ret` | Removes return address | S |

## Key observation
RBP provides stable offsets for local variables while RSP moves to reserve space. The procedure restores RSP and RBP before `ret`, so the caller's stack position is recovered.

## Actual test
Assembled using `nasm -f elf64 02.asm -o 02.o`, linked using `ld 02.o -o 02`, and executed using `./02`. Observed exit status: **0**. The program produces no terminal text output.
