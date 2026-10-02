# Multiplication Operations

## Program 1: `mul3.asm`

### 1. Operation Summary
* **Instruction:** `mul dword [num2]`
* **Operand Size:** 32-bit Doubleword
* **Input Values:**
  * `num1` = `100000`(`00000000 00000001 10000110 10100000b`)
  * `num2` = `300000`(`00000000 00000100 10010011 11100000b`)
* **Result Register(s):** 64 bit pair EDX:EAX
***EDX***(Upper 32 bits)
***EAX***(Lower 32 bits)
***Result in memory:***(`dq 30000000000`)
### 2. GDB EFLAGS Output 
* **Active Status Flags:** `[CF IF OF]`

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED(0)** | Bit 7 is 0  therefore it is a non negative number |
| **OF** (Overflow Flag) | **SET(1)** | Bit 11 is 1 whihc shows that the calculated product exceeded the capacity of 32 bit register EAX and spilt into EDX |
| **CF** (Carry Flag) | **SET(1)** | For the `MUL` instruction, the Carry Flag mirrors the Overflow Flag: it is set to 1 when the upper half of the result (`EDX`) contains non-zero bits. |
| **ZF** (Zero Flag) | **CLEARED (0)** |The 64 bit produt (30,000,000)is non-zero .|
| **AF** (Auxiliary Flag) | **CLEARED (0)**  |The multiplier did not leave aborrow or carry across bit 3 into bit 4 in the status latch  |
| **PF** (Parity Flag) | **CLEARED (0)** | Bit 2 is 0,therefore parity is not set  |

### 4. Process Termination
Flags are reset to `[PF ZF IF]` after xor ebx,ebx

# Multiplication Operations


## Program 2: `mul2.asm`

### 1. Operation Summary
* **Instruction:** `mul word [num2]`
* **Operand Size:** 16-bit Word
* **Input Values:**
  * `num1` = `3000`(`00001011 10111000b`)
  * `num2` = `200`(`00000000 11001000b`)
* **Result Register(s):** 32 bit pair DX:AX
***DX***(Upper 16 bits)
***AX***(Lower 16 bits)
***Result in memory:**(`dd 600000`)
### 2. GDB EFLAGS Output 
* **Active Status Flags:** `[CF IF OF]`

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED(0)** | Unsigned multiplication treats all bits as positive magnitude therefore the most significant bits are 0,so no negative sign bit present|
| **OF** (Overflow Flag) | **SET(1)** | Because DX is not zero (DX = 9), the product did not fit inside the primary accumulator AX. The CPU signals that the upper register contains meaningful data by setting both OF and CF to 1 |
| **CF** (Carry Flag) | **SET(1)** |Because DX is not zero (DX = 9), the product did not fit inside the primary accumulator AX. The CPU signals that the upper register contains meaningful data by setting both OF and CF to 1  |
| **ZF** (Zero Flag) | **CLEARED (0)** | The product is not zero so the zero condition is not triggered.|
| **AF** (Auxiliary Flag) | **CLEARED (0)**  | Bit 4 is `0`.The multiplier hardware did not generate or latch a nibble borrow/carry across bit 3 into bit 4  |
| **PF** (Parity Flag) | **CLEARED (0)** | Undefined by hardware specification for `MUL` |

### 4. Process Termination
Flags are reset to `[PF ZF IF]` after xor ebx,ebx