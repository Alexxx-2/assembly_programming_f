# DIV – Arithmetic Operations and EFLAGS

## Program 1 – div1.asm

### Operation

The program performs:

**100 ÷ 7 = 14 remainder 2**

Therefore:

- Quotient = **14**
- Remainder = **2**
- Quotient in hexadecimal = **0x0E**
- Remainder in hexadecimal = **0x02**

For the 8-bit `DIV` instruction:

- The quotient is stored in `AL`.
- The remainder is stored in `AH`.

### EFLAGS

The x86 architecture does not define the arithmetic status flags after `DIV`.

| Flag | Status |
|---|---|
| CF | Undefined |
| PF | Undefined |
| AF | Undefined |
| ZF | Undefined |
| SF | Undefined |
| OF | Undefined |

Therefore, if GDB displays a particular value for these flags after `DIV`, that value should not be interpreted as definitely set or cleared.

---

## Program 2 – div2.asm

### Operation

The program performs:

**50000 ÷ 300 = 166 remainder 200**

Therefore:

- Quotient = **166**
- Remainder = **200**
- Quotient in hexadecimal = **0x00A6**
- Remainder in hexadecimal = **0x00C8**

### EFLAGS

After `DIV`, the following arithmetic flags are undefined:

| Flag | Status |
|---|---|
| CF | Undefined |
| PF | Undefined |
| AF | Undefined |
| ZF | Undefined |
| SF | Undefined |
| OF | Undefined |

This means that the displayed values of these flags in GDB cannot be reliably used to determine whether they were set or cleared.

---

## Conclusion

DIV is different from ADD and SUB because the arithmetic status flags are undefined after the instruction. The important outputs for these programs are the quotient and remainder.
