## Program 1 :'sub1.asm'
### Operation Summary
* **Instruction sub al,[num2]**
* **Input Values:**
*'num1'='50'('00110010b')
'num2'='80'('01010000b')
**Result in AL:** '226'unsigned,'-30'signed 2's complement('11100010b')

### GDB EFLAGS Output
* **Active Status Flags:** '[ CF PF SF]'

### Flag Analysis ###
| Flag |Status|Reason|
| :--- | :---: | :--- |
|**SF** (Sign Flag) | **SET (1)** | Bit 7 (the MSB of `11100010b`) is `1`. Under signed two's complement , the result represents negative thirty (`-30`).|
|**OF** (Overflow Flag) | **CLEARED (0)** | No signed overflow occurred. Subtracting a positive integer from a positive integer ($+50 - (+80) = -30$) yields a valid signed value within the 8-bit signed range ($-128$ to $+127$). |
|**CF** (Carry  Flag) | **SET (1)** | subtracting a larger unsigned integer (`80`) from a smaller unsigned integer (`50`) requires a borrow past Bit 7. |
|**ZF** (Zero Flag) | **CLEARED (0)** |The result is a non-zero number |
|**AF** (Auxiliary Flag) | **CLEARED(O)** |Evaluated at the low nibble: subtracting the low nibble `0000b` from `0010b` (`2 - 0 = 2`) produces no borrow out of bit 3|
|**PF** (Parity Flag) | **SET (1)** |Evaluated on the lower 8 bits (`11100010b`). The byte contains four `1` bits (bits 7, 6, 5, and 1). |




## Program 2 :'sub2.asm'
### Operation Summary
* **Instruction** ' sub ax,[num2] '
* **Operand Size:** 16_bit Word 
* **Input Values:**
*'num1'='1000'('0000001111101000b')
'num2'='2000'('0000011111010000b')
**Result in AX:** `64536` unsigned, `-1000` signed 2's complement |('1111110000011000b')

### GDB EFLAGS Output
* **Active Status Flags:** '[ CF PF SF ]'

### Flag Analysis ###
| Flag |Status|Reason|
| :--- | :---: | :--- |
|**SF** (Sign Flag) | **SET (1)** | Bit 15  is `1`, indicating that,under two's complement,this indicates a negative number.|
|**OF** (Overflow Flag) | **CLEARED(0)** | No signed overflow occurred.Subtracting a positive integer from a positive integer produces a valid result within the 16-bit signed integer range. |
|**CF** (Carry  Flag) | **SET (1)** |Unsigned borrow condition: subtracting a larger unsigned integer (`2000`) from a smaller unsigned integer (`1000`) requires a borrow beyond Bit 15. |
|**ZF** (Zero Flag) | **CLEARED (0)** |The subtraction result ($-1000$) is non-zero. |
|**AF** (Auxiliary Flag) | **CLEARED(0)** |Evaluated at the low nibble: subtracting `0000b` from `1000b` (`8 - 0 = 8`) generates no borrow across bit 3 into bit 4. |
|**PF** (Parity Flag) | **SET (1)** |Parity is calculated exclusively on the least significant 8 bits (`AL` =  = `00011000b`). The count of set bits is two '1 ' bits which is an even counts.|
###Process Termination 
The ZF anf PF flag are set after the XOR operation that clears the registers since the value yielded is zero and the number of 1's is zero which is an even number