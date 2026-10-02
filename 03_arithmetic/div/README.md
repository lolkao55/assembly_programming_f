# 03_arithmetic: Division Operations

## Program 1: `div1.asm` (8-bit Division)

### 1. Operation Summary
* **Instruction:** `div bl`
* **Operand Size:** 8-bit Byte Divisor (`db` / `BL`)
* **Input Values:**
  * **Dividend (in AX):** `100` ( `00000000 01100100b`)
  * **Divisor (in BL):** `7` (`00000111b`)
* **Mathematical Operation:** $100 \div 7 = 14$ remainder $2$
* **Result Register(s):** Split inside `AX`
  * **AL** (Quotient): `14` (`0x0E` | `00001110b`)
  * **AH** (Remainder): `2` (`0x02` | `00000010b`)

### 2. GDB EFLAGS Output

* **Active Status Flags:** `[ AF IF ]` *

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED (0)** | The high bit of the quotient is 0|
| **OF** (Overflow Flag) | **CLEARED (0)** |  The quotient (14) fits within the 8-bit destination register AL (capacity $0$–$255$) without exceeding register limits |
| **CF** (Carry Flag) | **CLEARED (0)** |  bit 0 is 0. The unsigned division completed without requiring a borrow out of the upper bit of AX (since dividend $100 < 256$, fitting inside 8 bits) |
| **ZF** (Zero Flag) | **CLEARED (0)** |Bit 6 is 0. Neither the quotient (14) nor the remainder (2) produced a zero value. |
| **AF** (Auxiliary Flag) | **SET(1)** |Since CPU runs shift and subtract cycles,subtracting 7 requires borrowing across bit 3 into bit 4   |
| **PF** (Parity Flag) | **CLEARED (0)** |The number of 1's in the quotient are three making it odd. |

## Program 2: `div2.asm` (16-bit Division)

### 1. Operation Summary
* **Instruction:** `div bx`
* **Input Values:**
  * **Dividend (in DX:AX):** `DX`=`0` 
  `AX`(Low word)=`50000`
  * **Divisor (in BX):** `300` 
* **Mathematical Operation:** $50000 \div 300 = 166$ remainder $200$
* **Result Register(s):** 
  * **AX** (Quotient): `166` (`00000000 10100110b`)
  * **DX** (Remainder): `200` (`00000000 11001000b`)

### 2. GDB EFLAGS Output

* **Active Status Flags:** `[AF IF ]` *

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED (0)** | Most Significant Bit of quotient is 0|
| **OF** (Overflow Flag) | **CLEARED (0)** |  The quotient (166) fits within the 16-bit destination register AX (capacity $0$–$65535$) without exceeding register limits |
| **CF** (Carry Flag) | **CLEARED (0)** |  bit 0 is 0. The unsigned division completed without requiring a borrow out of the upper bit of DX:AX  |
| **ZF** (Zero Flag) | **CLEARED (0)** |Bit 6 is 0. Neither the quotient (166) nor the remainder (200) produced a zero value. |
| **AF** (Auxiliary Flag) | **SET(1)** | $50000 \div 300$, the iterative shift-and-subtract hardware cycles isolating the remainder (`200` / `0x00C8`) generating a borrow across the low nibble boundary (out of bit 3 into bit 4).  |
| **PF** (Parity Flag) | **CLEARED (0)** |The number of 1's were odd. |

