- microprocessor is a clock driven register
	- 8086 data line --> 16 bit
	- 8086 address line --> 20 bit

## features
- 8086 is a 16 bit microprocessor 
- 8086 microprocessor has a 16 bit data line
- 8086 microprocessor has a 20 bit address line
- It generates 16 bit addresses. So, 2<sup>16</sup> = 65536 I/O ports
- it houses 16 bit registers for data storage
- Address and datalines are multiplexed, so less pins and slow data transfers
- requires one phase clock pulse width with 33% duty
- It can perform bit, byte, word, block operations
- It has 2 modes --> min mode and max mode
- supports multiprocessing
- It has a powerful Instruction set

## instruction decoder
It translates the instructions fetched from memory to series of actions that EU can carry out.
## control system
It generates timing and control signals for microprocessors
## arithmetic and logic unit
It performs arithmetic operations

# flag register
1) Conditional flag
	- carry flag
	- parity flag
	- auxiliary flag
	- zero flag
	- sign flag
	- overflow flag
2) Control flag
	- trap flag
	- interrupt flag
	- directional flag

# instruction set
the entire group of instruction supported by the microprocessor
#### format
==instructionName Destination, Source==
- destination can be a register or a memory address pointing to some value
- source can be a register, memory location or immediate operand
	eg: 
			MOV CX, 038AH
			MOV AL, BL
			MOV BX, [0301H]

## classification of instruction set
- data transfer instruction
- arithmetic instruction
- bit manipulation instruction
- program execution transfer instruction
- string instruction
### data transfer instruction
- MOV des, src
	moves the value from source to destination
- PUSH operand
	 push the operand to top the stack
- POP operand
	pops the operand from top stack to AX
- XCHG des, src
	exchanges the data
- IN accumulator, portAddress
	transfers operand from port to accumulator
- OUT portAddress, accumulator
	transfers operand from accumulator to port
- LEA register, src
	used to load operand's address into the register
- LDS des, src
	used to load DS register found in BEU
- LES des, src
	used to load ES register from the memory
- LAHF 
	copies lower byte of the flag register to AH
- SAHF
	copies contents of AH to lower byte of flag register 
- POFF 
	pops the top of stack to flag register

### arithmetic instruction
- ADD des, src
- ADC des, src
	 adds two operands with the carry flag
- SUB des, src
	for subtraction, CF acts as borrow flag
- SBB des, src
- INC src
- DEC src
- NEG src
- CMP des, src
- MUL src
	unsigned multiplication
- IMUL src 
	signed multiplication
- DIV src
- IDIV src
- NOT src

### bit manipulation
- SHR des, count
- ROL des, count
- ROR des, count

### program execution transfer instruction
- CALL des
- RT des
- JMP des
- JXX des
	1) JA 
	2) JAE
	3) JB
	4) JBE
	5) JC
	6) JE
	7) JNC
	8) JNE
	9) JNZ
	10) JPE
	11) JPO
	12) JZ
- LOOP des
### program control instruction
- STC 
	sets CF to 1
- CLC
	clears CF
- CMC
	complements CF
- STD
	sets DF to 1
- CLD
	clears DF

## addressing modes of 8086
- immediate addressing mode
	MOV CL, 12H
- register addressing mode
	MOV AX, BX
- direct-memory addressing mode
	MOV CL, [4321H]
- register-based indirect addressing mode
	MOV CX, [BX]
- register-relative addressing mode
	MOV CL, [BX + 04H]
- base-indexed addressing mode
	MOV CL, [BX + SI]
- relative-base addressing mode
	MOV CL, [BX + DI + 20H]
- implied addressing mode
	STC 

## working modes
### min mode
- a 8286 clock
- a 8282 3 8bits latch for address
- a 8286 2 16bits latch for data 
- a 74138 3:8 decoded
### max mode

| Min mode | Max mode |
| ---- | ---- |
| supports only one processor | supports multiprocessing |
| slow | fast |
| simple | complex |
| MN/<p style="text-decoration:overline">MX</p>==> 1 | MN/<p style="text-decoration:overline">MX</p>==> 0 |
| affordable | pricey |
| used in small systems | used in large systems |

| features | Min | Max |
| ---- | ---- | ---- |
| bus width | 8bits | multiplexed bus |
| address bus width | 20bits | 20bits |
| connection signal | one | many |
| additional support chips | fewer support chips required | multiple support chips required |
| coprocessor chip | not supported | supported |
| max co processor  | 0  | 3 |
