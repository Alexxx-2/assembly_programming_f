# ADD – Arithmetic Operations and EFLAGS

## Program 1 – add1.asm

### Operation

The program performs:

**120 + 10 = 130**

The result is:

- Decimal: **130**
- Hexadecimal: **0x82**
- Binary: **10000010**

### EFLAGS

| Flag | Status | Explanation |
|---|---|---|
| CF | Cleared | There is no unsigned carry out of the 8-bit result because 130 fits within the range 0–255. |
| PF | Set | The result `0x82` contains two 1-bits. Since the number of 1-bits is even, PF is set. |
| AF | Set | A carry occurs from the lower 4 bits to the upper 4 bits during the addition. |
| ZF | Cleared | The result is 130, so it is not zero. |
| SF | Set | The most significant bit of the 8-bit result `0x82` is 1. |
| OF | Set | For signed 8-bit arithmetic, 120 + 10 = 130, which is greater than the maximum signed value of 127. |

GDB displayed:

`EFLAGS = 0x996 [ PF AF SF IF OF ]`

The `IF` flag is not considered part of the arithmetic result because it is the Interrupt Flag and is unrelated to the ADD operation.

---

## Program 2 – add2.asm

### Operation

The program performs:

**32000 + 500 = 32500**

The result is:

- Decimal: **32500**
- Hexadecimal: **0x7EF4**

### EFLAGS

| Flag | Status | Explanation |
|---|---|---|
| CF | Cleared | 32500 fits within the unsigned 16-bit range of 0–65535, so there is no carry out. |
| PF | Cleared | The low byte is `0xF4`, which contains five 1-bits. This is odd parity, so PF is cleared. |
| AF | Cleared | There is no carry from bit 3 to bit 4. |
| ZF | Cleared | The result is 32500, not zero. |
| SF | Cleared | The most significant bit of `0x7EF4` is 0. |
| OF | Cleared | 32500 is within the signed 16-bit range of -32768 to 32767, so there is no signed overflow. |

GDB displayed:

`EFLAGS = 0x202 [ IF ]`

The `IF` flag is unrelated to the arithmetic operation.

---

## Conclusion

The ADD examples show how the arithmetic result determines the status of the different EFLAGS. Carry and overflow represent different conditions: CF concerns unsigned carry, while OF concerns signed overflow.
