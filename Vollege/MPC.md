# Microprocessor
It's a multipurpose, programmable, clock-driven, register-based electronic device that reads in binary data and instructions from main memory and provides result as output. Intel corp launched the first microprocessor.
## 8086 Processor

![[8086_processor.jpg]]

- It's a 16bit processor meaning it is capable of operating at 16bits of data in a single operation or in a single second.
- It has 20-bit address bus, that is 2<sup>20</sup> = 1MB per cycle or second or operation.
- 8086 processor has 16-bit I/O address, hence it can access 2<sup>16</sup> = 65536 ports at a time. 
- It has 14 16-bit registers for storage needs.
- 8086 processor operates in two different modes,
	- Minimum mode
	- Maximum mode
- Address and datalines are multiplexed, so less pins and slow data transfers
- requires one phase clock pulse width with 33% duty
- It can perform bit, byte, word, block operations
- supports multiprocessing
- It has a powerful Instruction set
- The architecture itself is divided into 2 units,
	- The BIU (Bus Interface Unit)
			This part of the processor takes care of fetching the instructions while the EU part of the processor is executing the fetched instruction. 8085 Processor can only fetch or execute at a time, but 8086 can do that simultaneously because of the separate BIU . The BIU also sends out memory addresses to access I/O ports
	- The EU (Execution Unit)
			This part of the processor executes the fetched instructions while the BIU is fetching the next instruction as it happens.
- There are two ALU in each portion of the processor
	- The ALU in the BIU is used for calculating the physical address of the data in memory. [[MPC#formula]]
	- The ALU in the EU is used for performing the execution operations
- The amount of memory that can be accessed depends on the memory bus. The 8086 processor has 20bits memory bus, 2<sup>20</sup> = 1MB. So the Memory size is 1MB
- The 8086 processor has pipe-lining technology. The next instruction is being fetched by BIU as the EU executes the fetched instruction 
## Memory segmentation
Instead of having a raw memory of 1 MB, the memory is divided into four sections for easy access.

![[memory_segmentation.png]]
- Code segment (CS)
		contains the programs
- Stack segment (SS)
		contains the stack
- Data segment (DS)
		contains a random data
- Extra segment (ES)
		contains a random data
- CS, SS, DS, ES are the starting (base) address of the segment, and IP, SP, SI, DI are their respective offset address. Using the segment address and it's offset address, a data can be located in the section.
### formula
The ALU in the BIU is used for calculating the physical address using this formula.
$$ PhysicalAddr = SegmentationAddr * 10_H + offsetAddr $$
eg:
$$ PhysicalAddr = CS * 10_H + IP $$
assuming, 
$$ CS = 1000_H, IP = 2345_H $$
$$ PhysicalAddr = 1000_H * 10_H + 2345_H $$
$$ PhysicalAddr = 10000_H + 2345_H $$
$$ PhysicalAddr = 12345_H $$

## The Bus Interface Unit (BIU)
- Main components are,
	- pre-fetch instruction queue
	- segment registers
	- instruction pointer

- Most important function,
	1) fetch the next instruction,
	2) calculate the physical address
	3) manages the pre-fetch queue (6 byte)
- The BIU has a few segment registers,
	- CS
	- SS
	- DS
	- ES
	- IP (Instruction Pointer)
	The CS, SS, DS, ES segment registers contains the starting address of the main memory's four section segments and a common IP is used to store the offset address that points at the next instruction. The IP gets updated frequently. With the help of segment registers and the instruction pointer, an instruction can be located in the main memory.

The ALU chip in the BIU calculates the physical address of the next instruction in the main memory 
- A read signal is sent over the control bus stating that an instruction is needed to be fetched,
- The physical address is sent through the address bus, 
- The data is sent back in the data bus (16bits) into the processor'r pre-fetch queue. 
- The fetched data is not going to be executed immediately as there's already another instruction that's being executed. This process of fetching instructions in advance is known as pre-fetching.
- As the EU executes the instructions one by one from the pre-fetch queue, more instructions are added to the queue by BIU.
- The BIU only refills the pre-fetch queue when 2 bytes are empty. 2 bytes = 16 bits and 8086 is a 16-bit processor, so it's efficient this way.
- But pipe-lining fails momentarily when there is a branch as the program jumps a few instructions and the in-between instructions are of no use, so they must be discarded. But after they are discarded, pipe-lining continues as usual.

==Note:==
1) ==Instructions can vary anywhere from 1 byte - 6 bytes, this is why the pre-fetch queue is 6 bytes as it can hold even the largest possible instruction.
2) ==There is an opcode for every instructions.
3) ==eg: MOV BL, CL has some opcode like 0010100
4) ==BUT, MOV BL, 25H has opcode only for the MOV BL, part as the next part is a number, and since that number parameter can have infinite variations, it's not reasonable (impossible, yet) to assign an opcode for every iterations.
5) ==So, MOV BL, 25H have an opcode for the MOV BL part and an operand for the 25H part.==
## The Execution Unit (EU)
- the main components are, 
	- instruction decoder
	- control system or control unit
	- ALU
	- general purpose registers
	- flag registers
	- pointer and index registers
#### instruction decoder
translates instructions fetched from memory
#### control system
generates timing and control signals to perform the internal operations
#### ALU
- ADD
- SUBTRACT
- AND
- OR
- INCREMENT
- DECREMENT
- COMPLEMENT
- SHIFT 
#### flag registers
8086 has 16-bit flag register. It contains 9 active flags. 
- There are two types of flags in 8086,
	- Conditional flags
		- CARRY FLAG
				This flag is set when there's a carry out of MSB in case of addition or subtraction (CF acts as BORROW FLAG)
		- PARITY FLAG
				This flag is set when the lower byte of the result contains even number of 1's. For odd number of 1's, it's flag is set to 0
		- AUXILIARY FLAG
				this is set if there's a carry from the lowest nibble
		- ZERO FLAG
				this flag is set if the result is 0
		- SIGN FLAG
				this flag is set if the result is negative
		- OVERFLOW FLAG
				this flag is set if overflow occurs
	- Control flags
		- TRAP FLAG
				If this flag is set, the processor enters the single step execution mode by generating internal interrupts 
		- INTERRUPT FLAG
				causes the 8086 to recognize external mask interrupts. Clearing this IF flag disables these interrupts.
		- DIRECTION FLAG
				this is used by string manipulation instructions. If set to 0, The string is processed from the lowest address to the highest address (i.e Auto-incrementing mode) Or else the string is processed from highest address to lowest address (i.e Auto-decrementing mode)

- It has one grand purpose, to execute the given instructions!
- the instructions that are fetched and stored in the pre-fetch queue will one by one enter the control section where those instructions are decoded. The entering instructions will be in opcodes (binary) it has to be decoded to interpret the meaning of those binary numbers
- The EU has **General Purpose Registers (GPRs)**,
	- AX - AH, AL
	- BX - BH, BL
	- CX - CH, CL
	- DX - DH, DL
- pointer (16-bit)
	- SP (Stack pointer)
	- BP (Base pointer)
- index registers (16-bit)
	- SI (Source index)
	- DI (Data index)
- The EU has some flag registers that gives some status about the current result

***
# instruction set
the entire group of instruction supported by the microprocessor. 8086 has more than 20,000 instruction sets.
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
- processor control instructions
### data transfer instruction
The instruction used to transfer data from source to destination.
- MOV des, src
	moves the value from source to destination
- PUSH operand
	 push the operand to top of the stack
- POP operand
	pops the operand from top stack to AX
- XCHG des, src
	exchanges the data within des and src. (It cannot exchange data directly with memory locations, need to pass registers(i.e AX, BX, etc) as the operands)
- IN accumulator, portAddress
	transfers operand from port to accumulator
- OUT portAddress, accumulator
	transfers operand from accumulator to port
- LEA register, src
	used to load operand's address into the given register
- LDS des, src
	used to load DS register from the memory
- LES des, src
	used to load ES register from the memory
- LAHF 
	copies lower byte of the flag register to AH
- SAHF
	copies contents of AH to lower byte of flag register 
- PUSHF
	pushes flag register to top of the stack
- POPF
	pops the stack top to flag register

### arithmetic instruction
- ADD des, src
	adds byte to byte, or word to word
- ADC des, src
	 adds two operands with the carry flag
- SUB des, src
	subtracts byte from byte, or word from word
- SBB des, src
	for subtraction, CF acts as borrow flag
- INC src
	increments byte or word by 1
- DEC src
	decrements byte or word by 1
- NEG src
	creates 2's complement of the given number, meaning it changes the sign of the given number.
- CMP des, src
	compares given word or byte
- MUL src
	unsigned multiplication
- IMUL src 
	signed multiplication
- DIV src
	signed division
- IDIV src
	unsigned division
- CBW
	converts byte in AL to word in AX
- CWD
	converts word in AX to double word in DX: AX
### bit manipulation
These instruction are used at the bit level
- NOT src
	complements each bit of src and produces 1's complement
- AND des, src
- OR des, src
- XOR des, src
- SHL des, count
	shifts bits of byte or word to left by count. Puts 0 in LSBs. MSB is shifted to CF.
- SHR des, count
	shifts bits of byte or word to right by count. Puts 0 in MSBs. LSBs is shifted to CF.
- ROL des, count
	rotates bits of byte or word to left by count
- ROR des, count
	rotates bits of byte or word to right by count
### program execution transfer instruction
these instructions cause change in the sequence of execution of instruction.
- CALL des
	used to call a sub-routine or a function
- RET 
	return the control from procedure to the calling program. Every call instruction should have a RET.
- JMP des
	used for unconditional jump from one place to another
- JXX des
	used for conditional jump, follows some conditional statement or the flags
	1) JA 
		jump if above
	2) JAE
		jump if above or equal
	3) JB
		jump if below
	4) JBE
		jump if below or equal
	5) JC
		jump if carry
	6) JE
		jump if equal
	7) JNC
		jump if not carry 
	8) JNE
		jump if not equal
	9) JNZ
		jump if not zero
	10) JPE
		jump if parity even
	11) JPO
		jump if parity odd
	12) JZ
		jump if zero
- LOOP des
	this is a looping instruction, the number of times to loop is placed in the CX register, with each iteration, the CX register is decremented and ZF is checked whether to loop again or not

### string instructions
- CMPS des, src
	compares string bytes or words
- SCAS string
	compares the given string with the byte in AL or the word in AX
- MOVS / MOVB / MOVW
	moves byte or word from one string to another. The src string is in Data segment and the dest string is in Extra segment
- REP (instruction to repeat)
	this is an instruction prefix. repeats until CX becomes 0.
	eg: REP MOV AX, BX
- 
### processor control instruction
these instructions control the processor itself.
- STC 
	sets CF to 1
- CLC
	clears CF to 0
- CMC
	complements CF
- STD
	sets DF to 1. So, string bytes are accessed from higher memory address to the lower memory address
- CLD
	clears DF to 0. So, string bytes are accessed from lower memory address to the higher memory address

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

***
## Modes
#### difference
| Min mode | Max mode |
| ---- | ---- |
| supports only one processor | supports multiprocessing |
| slow | fast |
| simple | complex |
| MN/<p style="text-decoration:overline">MX</p>==> 1 | MN/<p style="text-decoration:overline">MX</p>==> 0 |
| affordable | pricey |
| used in small systems | used in large systems |
#### features comparison
| features | Min | Max |
| ---- | ---- | ---- |
| bus width | 8bits | multiplexed bus |
| address bus width | 20bits | 20bits |
| connection signal | one | many |
| additional support chips | fewer support chips required | multiple support chips required |
| coprocessor chip | not supported | supported |
| max co processor | 0 | 3 |
#### high active and low active signals
- high active signals are those that enables the pin when 1 is transmitted
	eg: ALE
- low active signals are those that enables the pin when 0 is transmitted.
	eg: DEN'
### minimum mode
In minimum mode, the microprocessor is interfaced with peripherals.
- a 8284 clock
- a 8282 3 8-bits latch for address
- a 8286 2 8-bits latch for data 
- a 74138 3:8 decoder

![[8086_processor_min_mode.jpg]]

- The 8086 microprocessor operates in minimum mode when MN/MX' = 1.
- The other components are,
	- 2 - 8286 Transceivers (for data),
	- 3 - 8282 latches (for address),
	- 8284 clock generator
	- 74138 3:8 decoder
	- memory and I/O device
- Out of 20-bits, 16-bits (A<sub>0</sub> to A<sub>15</sub>) or (16 lines) are multiplexed with a data bus. 
- Multiplexing means they will act as address lines during the first T cycle and data lines in the rest of the T cycle.
## 8282 latch (8-bits) (address)
- The latches are buffered D flipflop. 
- the valid address is separated from the multiplexed address/data bus by using the control signal **ALE (Address Latch Enable)** which is connected to **STB (Strobe)** of 8282
- 3 8282 latches are required because the 8086 processor has 20-bit address bus. So as to support it, 3 8-bit latches makes a total of 24-bit latch.
## 8286 transceiver (8-bits) (data)
- the valid data is separated from the multiplexed address/data bus using the **DT/R' (Data Transmit/Receive)** and **DEN' (Data Enable)** pins connected to **T (Transmit)** and **OE' (Output Enable)** of 8286 respectively
- 2 8285 transceivers are required as the 8086 processor's data bus is 16-bits long. 2 8-bit transceivers make a 16-bit transceiver.
- DT/R' decides the data flow through the transceiver, that is whether the data is being transmitted from the transceiver or it's receiving the data. 
- DEN' either enables or disables the transceiver altogether.

![[8286_data_flow.png]]
## 74138 3:8 decoder (control)
- decides which control signal is to be sent through the control bus
- M/IO' (Memory/IO) decides whether the memory or I/O operation is to be performed. The RD' (Read) and WR' (Write) says whether a read (instruction fetch) or write cycle is currently being performed
- control signals for all the operations are generated by decoding the M/IO', WR', RD' signals from the processor. They are decoded by 74138 3:8 decoder, and the output is sent in the control bus.

![[8286_control_signals.png]]

## 8284 clock generator
- used to provide clock signals :)
## other pins
- when INTR (Interrupt) is enabled then that means there is an interrupt to 8086 from other devices for their service
- when INTA (Interrupt Acknowledge) is enabled that means the 8086 is ready to provide service for them
- bus request is made by other devices using HOLD pin and the processor acknowledges them by HLDA (Hold Acknowledge) pin

### maximum mode
In maximum mode, the microprocessor is interfaced with co-processors