# SUB – Arithmetic Operations and EFLAGS

## Program 1 – sub1.asm

### Operation

The program performs:

**50 - 80 = -30**

The 8-bit two's-complement representation of -30 is:

- Decimal: **-30**
- Hexadecimal: **0xE2**
- Binary: **11100010**

### EFLAGS

GDB displayed:

`EFLAGS = 0x287 [ CF PF SF IF ]`

| Flag | Status | Explanation |
|---|---|---|
| CF | Set | 50 is smaller than 80 when treated as unsigned values, so the subtraction requires a borrow. |
| PF | Set | The result `0xE2` contains four 1-bits, which gives even parity. |
| AF | Cleared | There is no borrow from bit 4 during the subtraction of the lower nibbles. |
| ZF | Cleared | The result is -30, not zero. |
| SF | Set | The most significant bit of `0xE2` is 1, indicating a negative two's-complement result. |
| OF | Cleared | The result -30 is within the signed 8-bit range of -128 to 127, so there is no signed overflow. |

The `IF` flag shown by GDB is unrelated to the arithmetic operation.

---

## Program 2 – sub2.asm

### Operation

The program performs:

**1000 - 2000 = -1000**

The 16-bit two's-complement representation is:

**0xFC18**

### EFLAGS

| Flag | Status | Explanation |
|---|---|---|
| CF | Set | 1000 is smaller than 2000 as unsigned values, so a borrow is required. |
| PF | Set | The low byte `0x18` contains two 1-bits, giving even parity. |
| AF | Cleared | There is no borrow from bit 4 during the subtraction of the lower nibbles. |
| ZF | Cleared | The result is -1000, not zero. |
| SF | Set | The most significant bit of `0xFC18` is 1, indicating a negative result. |
| OF | Cleared | -1000 is within the signed 16-bit range of -32768 to 32767, so there is no signed overflow. |

---

## Conclusion

SUB demonstrates the difference between the Carry Flag and Overflow Flag. CF indicates an unsigned borrow, while OF indicates signed arithmetic overflow.
