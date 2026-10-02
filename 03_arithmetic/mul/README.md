# Multiplication Operations

## Program 1: `mul3.asm`

### 1. Operation Summary
* **Instruction:** `mul dword [num2]`
* **Operand Size:** 32-bit Doubleword
* **Input Values:**
  * `num1` = `100000`(`00000000 00000001 10000110 10100000b`)
  * `num2` = `300000`(`300000``00000000 00000100 10010011 11100000b`)
* **Result Register(s):** 64 bit pair EDX:EAX
***EDX***(Upper 32 bits)
***EAX***(Lower 32 bits)
***Result in memory:**(`dq 30000000000`)
### 2. GDB EFLAGS Output 
* **Active Status Flags:** `[CF IF OF]`

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED(0)** | In x86,status of SF is undefined following an unsigned MUL operation |
| **OF** (Overflow Flag) | **SET(1)** | In unsigned multiplication, OF is set to 1 if and only if the upper half of the product register (`EDX`) is non-zero |
| **CF** (Carry Flag) | **SET(1)** | For the `MUL` instruction, the Carry Flag mirrors the Overflow Flag: it is set to 1 when the upper half of the result (`EDX`) contains non-zero bits. |
| **ZF** (Zero Flag) | **CLEARED (0)** | Undefined by hardware specification for `MUL`.|
| **AF** (Auxiliary Flag) | **CLEARED (0)**  |Undefined by hardware specification for `MUL`  |
| **PF** (Parity Flag) | **CLEARED (0)** | Undefined by hardware specification for `MUL` |

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
***Result in memory:**(`dd 60000`)
### 2. GDB EFLAGS Output 
* **Active Status Flags:** `[CF IF OF]`

### 3. Flag Analysis

| Flag | Status | Reason |
| :--- | :---: | :--- |
| **SF** (Sign Flag) | **CLEARED(0)** | In x86,status of SF is undefined following an unsigned MUL operation |
| **OF** (Overflow Flag) | **SET(1)** | In unsigned multiplication, OF is set to 1 if and only if the upper half of the product register (`DX`) is non-zero |
| **CF** (Carry Flag) | **SET(1)** | For the `MUL` instruction, the Carry Flag mirrors the Overflow Flag: it is set to 1 when the upper half of the result (`DX`) contains non-zero bits. |
| **ZF** (Zero Flag) | **CLEARED (0)** | Undefined by hardware specification for `MUL`.|
| **AF** (Auxiliary Flag) | **CLEARED (0)**  | Undefined by hardware specification for `MUL` |
| **PF** (Parity Flag) | **CLEARED (0)** | Undefined by hardware specification for `MUL` |

### 4. Process Termination
Flags are reset to `[PF ZF IF]` after xor ebx,ebx