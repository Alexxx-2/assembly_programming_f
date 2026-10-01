# MUL – Arithmetic Operations and EFLAGS

## Program 1 – mul1.asm

### Operation

The program performs:

**25 × 10 = 250**

The result is:

- Decimal: **250**
- Hexadecimal: **0x00FA**

For an 8-bit `MUL`, the result is stored in the 16-bit `AX` register.

### EFLAGS

The result is:

`AX = 0x00FA`

The upper half of the result, `AH`, is zero.

For the unsigned `MUL` instruction, CF and OF indicate whether the upper half of the result is non-zero.

| Flag | Status | Explanation |
|---|---|---|
| CF | Cleared | The upper half of the result is zero, so the multiplication fits within the original operand size. |
| OF | Cleared | The upper half of the result is zero, so there is no unsigned multiplication overflow. |
| SF | Undefined | `MUL` does not define the Sign Flag. |
| ZF | Undefined | `MUL` does not define the Zero Flag. |
| AF | Undefined | `MUL` does not define the Auxiliary Carry Flag. |
| PF | Undefined | `MUL` does not define the Parity Flag. |

Undefined flags should not be classified as set or cleared based on whatever value GDB happens to display.

---

## Program 2 – mul2.asm

### Operation

The program performs:

**3000 × 200 = 600000**

The 32-bit result is:

**0x000927C0**

The result is divided between the registers:

- **DX = 0x0009**
- **AX = 0x27C0**

### EFLAGS

| Flag | Status | Explanation |
|---|---|---|
| CF | Set | The upper half of the multiplication result, DX, is non-zero. |
| OF | Set | The upper half of the result is non-zero, indicating that the result does not fit entirely in the lower 16 bits. |
| SF | Undefined | `MUL` does not define the Sign Flag. |
| ZF | Undefined | `MUL` does not define the Zero Flag. |
| AF | Undefined | `MUL` does not define the Auxiliary Carry Flag. |
| PF | Undefined | `MUL` does not define the Parity Flag. |

---

## Conclusion

MUL differs from ADD and SUB because only CF and OF have defined meanings after an unsigned multiplication. The other arithmetic flags are undefined.
