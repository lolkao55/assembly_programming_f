## Program 1 :'add1.asm'
### Operation Summary
* **Instruction add al,[num2]
* **Input Values:**
*'num1'='120'('01111000b')
'num2'='10'('00001010b')
**Result in AL:** '130'('10000010b')

### GDB EFLAGS Output
* **Active Status Flags:** '[ PF AF SF IF OF ]'

###Flag Analysis
| Flag |Status|Reason|
| :--- | :---: | :--- |
|**SF** (Sign Flag) | **SET (1)** | Bit 7 (MSB) of the result is '1'.In signed 2's complement ,this represents a negative value.|
|**OF** (Overflow Flag) | **SET (1)** | Signed arithmetic overflow occurred since adding 2 positive operands produces a negative result which exceeds the valid 8-bit range. |
|**CF** (Carry  Flag) | **CLEARED (0)** | Unsigned sum is $120 +10=130$.Because $130 \le 255$,there was no carry out of the most significant bit. |
|**ZF** (Zero Flag) | **CLEARED (0)** |The resulting sum is non-zero |
|**AF** (Auxiliary Flag) | **SET(1)** |Adding the lower 4 bits produced a carry out of bit 3 into bit 4 across the nibble |
|**PF** (Zero Flag) | **SET (1)** |The lowest 8 bits contain an even number of set bits that is exactly two '1's bit 7 and bit 1 |

## Program 2 :'add2.asm'
### Operation Summary
* **Instruction** ' add ax,[num2] '
* **Operand Size:** 16_bit Word 
* **Input Values:**
*'num1'='32000'('0111110100000000b')
'num2'='500'('0000000111110100b')
**Result in AL:** '32500'('0111111011110100b')

### GDB EFLAGS Output
* **Active Status Flags:** '[ PF ]'

###Flag Analysis
| Flag |Status|Reason|
| :--- | :---: | :--- |
|**SF** (Sign Flag) | **CLEARED (0)** | Bit 15 (the MSB of `0x7EF4`) is `0`, indicating that the result is positive.|
|**OF** (Overflow Flag) | **CLEARED(0)** | No signed overflow occurred.Adding two positive numbers yielded a valid positive result which fits inside the 16 bit signed range($-32,768$ to $+32,767$). |
|**CF** (Carry  Flag) | **CLEARED (0)** | Unsigned sum is $32500$. Since $32500 \le 65535$, no carry was generated out of the most significant bit (bit 15). |
|**ZF** (Zero Flag) | **CLEARED (0)** |The resulting sum ($32500$) is non-zero. |
|**AF** (Auxiliary Flag) | **CLEARED(0)** |In the lowest 4 bits (`0000b` + `0100b` = `0100b`), no carry occurred across bit 3 into bit 4. |
|**PF** (Zero Flag) | **CLEARED (0)** |Parity is calculated exclusively on the least significant 8 bits (`AL` = `0xF4` = `11110100b`). The count of set bits is 5 (odd), which clears `PF` to 0.|
###Process Termination 
The ZF anf PF flag are set after the XOR operation that clears rhe registers since the value yielded is zero and the number of 1's is zero which is an even number