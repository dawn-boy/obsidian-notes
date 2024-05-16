It's a multipurpose, programmable, clock-driven, register-based electronic device that reads in binary data and instructions from main memory and provides result as output. Intel corp launched the first microprocessor.
## 8086 Processor

![[mpc-8086_processor.jpg]]

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
			This part of the processor takes care of fetching the instructions while the EU part of the processor is executing the fetched instruction. 8085 Processor can only fetch or execute at a time, but 8086 can do that simultaneously because of the separate BIU. The BIU also sends out memory addresses to access I/O ports
	- The EU (Execution Unit)
			This part of the processor executes the fetched instructions while the BIU is fetching the next instruction as it happens.
- There are two ALU in each portion of the processor
	- The ALU in the BIU is used for calculating the physical address of the data in memory. [[MPC#formula]]
	- The ALU in the EU is used for performing the execution operations
- The amount of memory that can be accessed depends on the memory bus. The 8086 processor has 20bits memory bus, 2<sup>20</sup> = 1MB. So the Memory size is 1MB
- The 8086 processor has pipe-lining technology. The next instruction is being fetched by BIU as the EU executes the fetched instruction 
### Memory segmentation
Instead of having a raw memory of 1 MB, the memory is divided into four sections for easy access.

![[mpc-memory_segmentation.png]]
- Code segment (CS)
		contains the programs
- Stack segment (SS)
		contains the stack
- Data segment (DS)
		contains a random data
- Extra segment (ES)
		contains a random data
- CS, SS, DS, ES are the starting (base) address of the segment, and IP, SP, SI, DI are their respective offset address. Using the segment address and it's offset address, a data can be located in the section.
#### formula
The ALU in the BIU is used for calculating the physical address using this formula.
$$ PhysicalAddr = SegmentationAddr * 10_H + offsetAddr $$
eg:
$$ PhysicalAddr = CS * 10_H + IP $$
assuming, 
$$ CS = 1000_H, IP = 2345_H $$
$$ PhysicalAddr = 1000_H * 10_H + 2345_H $$
$$ PhysicalAddr = 10000_H + 2345_H $$
$$ PhysicalAddr = 12345_H $$

### The Bus Interface Unit (BIU)
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
- The data is sent back in the data bus (16bits) into the processor's pre-fetch queue. 
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
### The Execution Unit (EU)
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
### instruction set
the entire group of instruction supported by the microprocessor. 8086 has more than 20,000 instruction sets.
#### format
==instructionName Destination, Source==
- destination can be a register or a memory address pointing to some value
- source can be a register, memory location or immediate operand
	eg: 
			MOV CX, 038AH
			MOV AL, BL
			MOV BX, [0301H]

### classification of instruction set
- data transfer instruction
- arithmetic instruction
- bit manipulation instruction
- program execution transfer instruction
- string instruction
- processor control instructions
#### data transfer instruction
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
#### arithmetic instruction
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
#### bit manipulation
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
#### program execution transfer instruction
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
#### string instructions
- CMPS des, src
	compares string bytes or words
- SCAS string
	compares the given string with the byte in AL or the word in AX
- MOVS / MOVB / MOVW
	moves byte or word from one string to another. The src string is in Data segment and the dest string is in Extra segment
- REP (instruction to repeat)
	this is an instruction prefix. repeats until CX becomes 0.
	eg: REP MOV AX, BX
#### processor control instruction
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
### addressing modes of 8086
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
### 8086 pin diagram
![[mpc-8086_pin_diagram.png]]
- GND
- AD0-AD15
	Address/Data bus. These are low order address bus, they are multiplexed with data.
- A16-A19
	high order address bus, these are multiplexed with status signals
- S0-S2
	status pins, these pins are used by 8288 or 74138 modules for generating control signals
	![[mpc-status_sig.png]]
- S3-S6
	status pins used for accessing main memory segments
	![[mpc-status_sig_memory_acces.png]]
### Modes
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
#### minimum mode
In minimum mode, the microprocessor is interfaced with peripherals.
- a 8284 clock
- a 8282 3 8-bits latch for address
- a 8286 2 8-bits transceiver for data 
- a 8286 2 8-bits transceiver for data 
- a 74138 3:8 decoder

![[mpc-8086_processor_min_mode.jpg]]

- The 8086 microprocessor operates in minimum mode when MN/MX' = 1.
- The other components are,
	- 2 - 8286 Transceivers (for data),
	- 3 - 8282 latches (for address),
	- 8284 clock generator
	- 74138 3:8 decoder
	- memory and I/O device
- Out of 20-bits, 16-bits (A<sub>0</sub> to A<sub>15</sub>) or (16 lines) are multiplexed with a data bus. 
- Multiplexing means they will act as address lines during the first T cycle and data lines in the rest of the T cycle.
##### 8282 latch (8-bits) (address)
- The latches are buffered D flipflop. 
- the valid address is separated from the multiplexed address/data bus by using the control signal **ALE (Address Latch Enable)** which is connected to **STB (Strobe)** of 8282
- 3 8282 latches are required because the 8086 processor has 20-bit address bus. So as to support it, 3 8-bit latches makes a total of 24-bit latch.
##### 8286 transceiver (8-bits) (data)
- the valid data is separated from the multiplexed address/data bus using the **DT/R' (Data Transmit/Receive)** and **DEN' (Data Enable)** pins connected to **T (Transmit)** and **OE' (Output Enable)** of 8286 respectively
- 2 8286 transceivers are required as the 8086 processor's data bus is 16-bits long. 2 8-bit transceivers make a 16-bit transceiver.
- DT/R' decides the data flow through the transceiver, that is whether the data is being transmitted from the transceiver or it's receiving the data. 
- DEN' either enables or disables the transceiver altogether.

![[mpc-8286_data_flow.png]]
##### 74138 3:8 decoder (control)
- decides which control signal is to be sent through the control bus
- M/IO' (Memory/IO) decides whether the memory or I/O operation is to be performed. The RD' (Read) and WR' (Write) says whether a read (instruction fetch) or write cycle is currently being performed
- control signals for all the operations are generated by decoding the M/IO', WR', RD' signals from the processor. They are decoded by 74138 3:8 decoder, and the output is sent in the control bus.

![[mpc-8286_control_signals.png]]

##### 8284 clock generator
- used to provide clock signals :)
##### other pins
###### INTR (Interrupt) ,INTA (Interrupt Acknowledge), NMI (Non-Maskable Interrupt)
- INTR and INTA pins are used by external devices. INTR pin is enabled when a device wants to communicate with the processor, and the INTA pin is enabled when the processor is ready to transmit or receiver data to or from that external device.
- if NMI is enabled and there is an interrupt, the processor will finish the current execution of the instruction and only then will it return to the interrupt.
###### HLD (Hold) and HLDA (Hold Acknowledge)
- HLD and HLDA are the pins used by DMA controllers to take over access of the bus, When DMA controllers want's to use the bus, it turns on the HLD pin, and the processor hands over the system bus to the DMA by sending the HLDA signal.
#### maximum mode
In maximum mode, the microprocessor is interfaced with co-processors
### Assembler directives
assembler directives are the commands to the assembler to direct the assembly process. They indicate how the assembler treats an operand, and how the assembler handles the program.

- assume
	assume segment_register:alias
- define byte
	name_of_variable DB initialization_value
- define word
	name_of_variable DW initialization_value
- define double
	name_of_variable DD initialization_value
- define quad word
	name_of_variable DQ initialization_value
- define ten word
	name_of_variable DT initialization_value
- END
	marks the end of assembly language programing
- ENDP
	marks the end of a procedure. In ALP, subroutines or functions are called procedures.
	eg: 
	Procedure greet
	.
	.
	.
	greet ENDP
- ENDS
	marks the end of a segment. 
	eg:
	DATA SEGMENT
	.
	.
	.
	DATA ENDS
- EVEN
### multiprocessor configuration
- multiprocessor means multiple set of processors that executes instructions simultaneously
- three basic multiprocessor configuration,
	- Co-processor configuration
	- Closely coupled configuration
	- Loosely coupled configuration 
#### Co-processor configuration
- A Co-processor is a specially designed circuit on microprocessor chip that can perform the same task very quickly than the main processor
- it reduces the work load on the CPU
- Co-processor shares the same memory, IO system, bus control logic and clock generator
- Co-processor handles specific tasks like mathematical calculations, graphical display on screen, etc.
- eg: the 8086 and 8088 can perform most of the operations but their instruction set is not able to perform complex mathematical operation, so in those cases they require something like the intel 8087 math processor
##### how is the processor and Co-processor connected
- the Co-processor and processor is connected through TEST, RQ/GT and QS<sub>0</sub> and QS<sub>1</sub> signals
- The TEST signal is connected to BUSY pin of Co-processor and remaining three pins are connected to the same pins in Co-processor
- TEST signal returns the status of co-processor's activate. That is, busy or idle.
- the RT/GT is used for bus arbitration
- the Co-processor uses the QS<sub>0</sub> and QS<sub>1</sub> to track the status of the queue of host processor 
#### closely coupled configuration
- closely coupled configuration is similar to Co-processor configuration as both share memory, I/O, system bus, Control Logic and Control Generator with Host processor
- however, the coprocessor and the processor fetches and executes their own instructions. The system bus is also controlled independently by the processor and Co-processor.
#### Loosely coupled configuration
- consists of number of modules of the subprocessor that are connected through a common system bus 
- each module have their own clock generator, memory, I/O devices and are connected to a local bus
- clocks of different modules are of similar frequency but they are asynchronous towards each other
- used in medium to large multiprocessing systems. Each module is capable of being the bus master. There are no direct connection between the modules
- Each share the system bus and communicate through the system bus. Processor in each module can access their private subsystem through their local bus and perform their local data references and instruction fetches independently.
- this results is improved degree of concurrent processing. Good for real time applications.
#### advantages
- having more than one processor increases efficiency 
- each processor have their own local bus to access memory I/O devices. This makes it easy 
### 8051 time counter
8051 has two 16-bit timer/counter registers namely timer 0 and timer 1.
- when used as a timer, the microcontroller is programmed to count internal clock pulse
- when used as a counter, the microcontroller is programmed to count external clock pulse
- maximum count rate is 1/24 of the oscillator frequency.
#### Timer 0 register
- exclusive to Timer 0
	- TH0
	- TL0
- shared by both registers
	- TMOD (Timer mode) register 
	- TCON (Timer control) register 
#### Timer 1 register 
- exclusive to Timer 1
	- TH1
	- TL1
- shared by both registers
	- TMOD (Timer mode) register 
	- TCON (Timer control) register 
#### TMOD register
- 8 bit register
- lower 4 bits
	- 
- upper 4 bits
##### advantages 
- having more than one processor increases efficiency 
- each processor have their own local bus to access memory I/O devices. This makes it easy 
### advanced processors
#### 80186
- based on 8086 with same 20-bit address bus
- 80186 and 80188 is compatible with the code written for 8086 and 8088
- It is intended to be used in embedded systems
- CPU speed is 6MHz to 25MHz
#### 80286
- addresses 16MB of RAM on a 24-bit address bus
- has 1GB of virtual memory
- much more powerful than 8086
- It is the first Intel x86 CPU with built-in memory management
- there are two modes of operations
	- Real mode -> same as 8086
	- Protected mode -> can address a lot more than 64KB.
#### 80386
- addresses 4GB of RAM on a 32-bit address bus
- has 64TB of virtual memory
- **Unix was developed on a 386 system**
#### 80486
- addresses 4GB of RAM 
- has 64TB of virtual memory
- It has Level 1 cache memory and integration of floating point unit and a math co-processor.
#### Pentium
- Twice the cache size of 486
- Named so because numbers cannot be trademarked
- Has a super-scalable design
## 8051 processor
### micro computer
A microcomputer is a complete compute system comprising atleast three major components,
- The microprocessor
- the memory
- the I/O peripheral components
### micro controller
- 16-bit address bus and 8-bit data bus
- 8-bit microcontroller was originally developed by Intel in 1980. It has high-performance CMOS technology. 
- Internal ROM -> 4k bytes,
	internal RAM -> 128 bytes
- four 8-bit I/O ports, Two 16-bit timers. 
- Serial interface communication
- Contains 40 pins
- Its a single chip that contains the microprocessor as well as some often used peripherals. It contains one or more of the following components.
	1) Interrupts
	2) RAM
	3) ROM
	4) timer 0 and timer 1
	5) CPU
	6) oscillators
	7) Bus control(data,address)
	8) I/O ports(0,1,2,3)
	9) serial communication
		- TXN(transmit)
		- RXN(receive)
- Internal memory consists of on-chip ROM and on-chip RAM
- 8051 has a separate memory space for programs and data
- The operating frequency is between 24MHz-33MHz
- +5V regulated DC power supply is required to operate
- it has 8-bit ports and a total of 32 I/O lines
- 6-interrupts (2 internal and 2 priority levels)
- low-power idel and power-down modes
- 8051 has 21 special function registers
- 8051 requires an external oscillator circuit that runs at 12MHz-16MHz(XTAL1,XTAL2)
### registers
![[mpc-8051_registers.png]]
1) A (Accumulator) and B
	- A and B are used for all arithmetic and logic instructions
	- 8051 has 34 general purpose registers
	- Significance of A
		- A is used for addition, sub, mul, div, bool, and bit manipulations
		- data transfer between 8051 and memory
1) R0-R7
2) DPTR (data pointer) 
	- Its the 8051's only user-accessible 16-bit (2-byte) register
	- Its meant for pointing at data in the external memory
3) PC (program counter)
	- 16-bit register
	- instructions fetched from memory are held in PC
	- PC do not have an internal address
	- PC starts at 0000h when 8051 initializes and is incremented every time after an instruction is executed
	- PC is always not incremented by 1, some instructions may occupy 2 or 3 bytes, in that case PC will be incremented by 2 or 3.
4) PSW (program status word) or flag registers
	![[mpc-psw.png]]
	- CY (PSW.7)
		carry flag - sets if there's carry after a byte 
	- AC (PSW.6)
		auxiliary carry flag - sets if there's carry after a nibble
	- F0 (PSW.5)
		available to the user for general purpose
	- RS1 (PSW.4)
		register bank selector bit 1
	- RS0 (PSW.3)
		register bank selector bit 0
	- OV (PSW.2)
		overflow flag
	- __ (PSW.1)
		user definable flag
	- P (PSW.0)
		parity flag, sets if there is odd number of 1bits in accumulator
	![[mpc-register_bank.png]]
	example:
	![[mpc-example.png]]
5) stack pointer
	- an 8-bit register
	- it has the address of data item currently on top of the stack
	- stack operations include pushing data on stack and popping data off the stack
	- pushing increments SP before writing the data and popping decrements SP after reading the value
	- stack of 8051 is kept in the internal RAM and SP is set to 07H when 8051 resets
	- eg: MOV SP,#5FH
### internal memory
![[mpc-8051_internal_memory.png]]
- 8051 has a separate memory space for programs and data
- both code and data may be internal, however, they both can expand using external components to a maximum of 64k code and 64k data memory
- on-chip RAM contains a rich arrangement of general purpose storage, bit addressable storage, register banks, and special function registers
- in 8051 the stack resides within the internal RAM rather than the external RAM

![[mpc-8051_banks.png]]

### pin diagram
![[mpc-8051_pin_diagram.png]]
#### port 0 (9 pins)
- 8-bit bidirectional I/O port
- port 0 pins can be used as high-impedance inputs
- port 0 is also the multiplexed low-order address and data bus while accessing external program and data memory
- when used as output the pin latches are programmed to 0, when used as input the pin latches are programmed to 1
- 32 - 39 pins are used
#### port 1 (9 pins)
- 8-bt bidirectional I/O port
- port 1 has no dual functions
- when used as output the pin latches are programmed to 0, when used as input the pin latches are programmed to 1
- 1 - 9 pins are used
#### port 2 (9 pins)
- 8-bit bidirectional I/O port
- port 2 emits the high-order address byte while accessing external program and data memory
- when used as output the pin latches are programmed to 0, when used as input the pin latches are programmed to 1
- 21 - 28 pins are used
#### port 3 (9 pins)
- 8-bit bidirectional I/O port
- 10 - 17 pins are used 
- the pins are
	1) RXD (P3.0) -> serial input port
	2) TXD (P3.1) -> serial output port
	3) INT0 (P3.2) -> external interrupt
	4) INT1 (P3.3) -> external interrupt
	5) T0 (P3.4) -> timer 0 external input
	6) T1 (P3.5) -> timer 1 external input
	7) WR (P3.6) -> external data memory write strobe
	8) RD (P3.7) -> external data memory read strobe
### addressing modes
1) immediate addressing mode
	- immediate data is specified in the instruction itself
	 eg: MOV A,#65H
2) register addressing mode
	- R0 - R7 registers are used
	eg: MOV A,R3 or MOV R4, A
3) direct addressing mode
	- Although the entire of 128 bytes of RAM can be accessed using direct addressing mode, it is most often used to RAM loc 30 - 7FH
4) register indirect addressing mode
	- In this mode, register is used as a pointer to the data 
	eg: MOV A, @R0
5) indexed addressing mode and on-chip ROM access
	- this mode is widely used for accessing data in program code
	- destination will always be the accumulator (A)
	eg: MOVC A, @A+DPTR
	because the data elements  are stored in program code space of ROM, the instruction is MOVC, C stands for code.
	
## 8051 interrupts

![[mpc-8051_interrupts.png]]
- an interrupt is an external or internal event that interrupts the microprocessor to inform it that a device requires its services.
- a set of program instructions written to service an interrupt is called interrupt service routine.
- 8051 has 6 different sources of interrupts:
	- External: INT0, INT1, power-up reset.
	- Internal: TIMER0, TIMER1, serial port.
#### power-on reset
- the most common type of reset is power-on reset. In this scenario, the RST pin is connected to the power-on reset push button on the circuit.
- Mechanism:
	- after turning the power on, the capacitor charges for several milliseconds through a resistor connected to the ground.
	- the RST pin is driven high during the charging process
	- once the capacitor is fully charged, the power supply voltage stabilizes, the RST pin remains connected to the ground.
#### TMOD register
- Timer 0
	- TR0 (Timer 0 Run Control Bit) 
		starts or stops Timer 0 
	- ET0 (Enable Timer 0 Interrupt Bit):
		enables or disables Timer 0 Interrupts
	- Interrupt Source
		Timer 0 generates an interrupt when it overflows, that is when it reaches its maximum count and then resets back to 0.
	- IT0
		![[mpc-8051_interrupts_it.png]]
		when 0 its set to level-triggering, when 1 its set to edge-triggering
	- IE0
		![[mpc-8051_interrupts_ie.png]]
		when set to 1, that indicates that the microcontroller vectored to the interrupt source and is executing the interrupt service routine.
- Timer 1
	- TR1 (Timer 1 Run Control Bit) 
	- ET1
	- Interrupt source
	- IT1
	- IE1
#### Interrupts and polling
there are two different methods the microcontroller uses to serve a device:
- Interrupts
	- whenever a device needs the microcontroller's service, it requests them by sending an interrupt signal.
	- microcontroller is free to do any work when there is no interrupts.
	
- Polling
	* The microcontroller continuously monitors a device until the pre-determined condition is met, then it proceeds to serve the device.
	* microcontroller cannot perform any other task other than monitoring the status of the device.
#### how are interrupts serviced?
1) 8051 finishes what its currently executing and saves the contents of the program counter on the stack
2) It then jumps to the interrupt vector location corresponding to the interrupt source
3) It then executes the interrupt service routine until it encounters RETI.
4) After finishing it returns back to whence it came from, and by popping the contents of PC from the stack, it starts execution at that address.
#### how interrupts are activated?
- there are two activation levels for external hardware interrupts:
	1) Level Triggered
		- level triggered is the default mode upon RESET of 8051.
	1) Edge Triggered
		- during raising or falling edge.
#### enabling and disabling interrupts
- upon reset, all the interrupts are disabled by default. The interrupts functionality must be enabled by software. 
- A register called IE (interrupt enable) is responsible for enabling or disabling the interrupts.
- upon reset, all IE bits are set to 0.
- if two interrupts are received at the same time, then the device with the highest priority gets the service.
## LCD interfacing
- a 16x2 LCD can display 32 characters in two rows at a time.
- each character is a 5x7 (5 in a row, and 7 in a column) pixel matrix.
#### pin description

![[mpc-lcd_pin_desc.png]]

- The pin can be categorized into 
	1) Power (1,2,3)
		- pin 1 is ground
		- pin 2 is vcc
		- pin 3 is used to set contrast between the foreground and the background. It makes the text darker.
	1) Control (4,5,6)
		- pin 4 is used to select the registers where control instructions like clear LCD or shift cursor are stored
		- pin 5 is used to read from or write to the lcd
		- pin 6 is considered to be a clock and data is given to the microcontroller when there is a transition in the pin
	1) Data (7-14)
		- you can use the first 4 data pins if you decide to save the rest for interfacing the lcd with other devices. If not, it is wiser to use all 8 pins for a faster transfer rate.
	1) Backlight (15,16)
		- pin 15 is connected to vcc 
		- pin 16 is connected to ground
		- always connect using a resistor as we don't want to damage the led. Except for the times we want to.

## matrix keypad
- a 4x4 matrix keypad has 16 switches.
- keypads are organized in rows and columns. When a key is pressed it makes contact with a row and a column and hence its location is identified. Otherwise, there is no connection.
#### schematic of a 4x4 keypad

![[mpc-keypad.png]]

- there are a total of 16 switches that are strategically placed such that when pressed it would short its row and column, thus making an closed path. All other paths would be open.
#### principle of operation
- all the rows are connected to V<sub>DD</sub>. So, if we read, all the rows will produce 1111.
- connect column 1 to ground and all other columns to V<sub>DD</sub>
- so if SW1 is pressed, row 1 will be grounded and all other rows will be at 5V. So the output will read 0111
- Note that this can only work to identify the button presses on column 1. If we need to find the button presses at column 2. Column 2 should be connected to ground while all other columns should be connected to V<sub>DD</sub> 
- Now, apply the pattern 0111 to the columns and detect for button presses on column 1. 

## Memory interfacing of 8051

![[mpc-8051_block_diag.png]]
### address bus 

![[1. Bandit_1.png]]
- 8051 has a 16-bit address bus for accessing RAM/ROM memory
### Data bus
- used to transfer opcodes and and data
- 8051 has a 8-bit data bus
### Memory map table 
- EPROM chip name -> 27 (size)
- RAM chip name -> 62 (size)
#### ROM
| Address lines         | Memory size           | IC Name |
| --------------------- | --------------------- | ------- |
| A9 - A0 (10)          | 2<sup>10</sup> = ~1k  | 27 8    |
| A10 - A0 (11)         | 2<sup>11</sup> = ~2k  | 27 16   |
| A11 - A0 (12)         | 2<sup>12</sup> = ~4k  | 27 32   |
| A12 - A0 (13)         | 2<sup>13</sup> = ~8k  | 27 64   |
| A13 - A0 (14)         | 2<sup>14</sup> = ~16k | 27 128  |
| A14 - A0 (15)         | 2<sup>15</sup> = ~32k | 27 256  |
| A15 - A0 (16)<br><br> | 2<sup>16</sup> = ~64k | 27 512  |
#### RAM
| Address lines         | Memory size           | IC Name |
| --------------------- | --------------------- | ------- |
| A9 - A0 (10)          | 2<sup>10</sup> = ~1k  | 62 8    |
| A10 - A0 (11)         | 2<sup>11</sup> = ~2k  | 62 16   |
| A11 - A0 (12)         | 2<sup>12</sup> = ~4k  | 62 32   |
| A12 - A0 (13)         | 2<sup>13</sup> = ~8k  | 62 64   |
| A13 - A0 (14)         | 2<sup>14</sup> = ~16k | 62 128  |
| A14 - A0 (15)         | 2<sup>15</sup> = ~32k | 62 256  |
| A15 - A0 (16)<br><br> | 2<sup>16</sup> = ~64k | 62 512  |
### problems
- Total number of address lines available in 8051 is 16.
1. If a system has a 16kb memory space made of 2 8kb memory chips, then
	- number of address lines required is 13 (A12 - A0) (~8kb single chip)
	- number of chip select lines required is 2 (cause there are only 2 chips)
	- size of decoder to be used is 1:2 Decoder
### steps to draw that diagram

![[mpc-8051_mem_interfacing.png]]
1.  8051 will have the following pins
	- AD<sub>7</sub> - AD<sub>0</sub> 
	- ALE (address latch enable)
	- A<sub>15</sub> - A<sub>8</sub> 
	- <span style="text-decoration:overline">PSEN</span>
	- <span style="text-decoration:overline">RD</span>
	- <span style="text-decoration:overline">WR</span>
2. an 8kb ROM will have the following inputs
	- A<sub>12</sub> - A<sub>0</sub> 
	- O<sub>7</sub> - O<sub>0</sub>
	- <span style="text-decoration:overline">OE</span> from <span style="text-decoration:overline">PSEN</span>
	- <span style="text-decoration:overline">CS</span> from the decoder
3. an 8kb rom will have the following inputs
	- A<sub>12</sub> - A<sub>0</sub> 
	- IO<sub>7</sub> - IO<sub>0</sub>
	- <span style="text-decoration:overline">OE</span> from <span style="text-decoration:overline">RD</span>
	- <span style="text-decoration:overline">WE</span> from <span style="text-decoration:overline">WR</span>
	- <span style="text-decoration:overline">CS</span> from the decoder
4. a decoder that takes in 
	- A<sub>13</sub> - A<sub>14</sub> 

## 8255 PPI (Programmable Peripheral Interface)
- I/O port chip used for interfacing I/O devices with the microprocessor
- it is a programmable device
- It has 3 ports 
	- Port A
	- Port B
	- Port C 
		Port C has two independent 4-bits port 
### pin diagram 

![[mpc-8255_pin_diag.png]]

- <span style="text-decoration:overline">CS</span> - Data transfer occurs from 8085 when signal is low
- D<sub>0</sub> - D<sub>7</sub> - These are 8-bit bi-directional data bus connected to 8085
- PA<sub>0</sub> - PA<sub>7</sub> - it is a 8-bit bi-directional I/O pins used to send and receive data to and from peripherals
- PB<sub>1</sub> - same as PA
- PC<sub>0</sub> - PC<sub>7</sub>  - 8-bit bidirectional I/O pins
- A<sub>0</sub> - A<sub>1</sub> is used to select the ports

| A<sub>1</sub> | A<sub>0</sub> | port             |
| ------------- | ------------- | ---------------- |
| 0             | 0             | port A           |
| 0             | 1             | port B           |
| 1             | 0             | port C           |
| 1             | 1             | control register |
### block diagram of 8255

![[mpc-8255_block_diag.png]]

- Data bus 
	- 8-bit bidirectional data bus
- read and write logic
	- gets input from the control bus and address bus of the cpu
	- control signals are RD and WR
	- address signals are A0, A1, and CS
	- 8255 operations are enabled or disabled by CS
- Group A and Group B control
	- gets signal from the CPU and sends the command to individual command blocks
	- group A controls port A and port C upper
	- group B control port B and port C lower

- Port A
	- 8 bit buffer I/O latch
	- can be programmed by mode 0, mode 1, mode 2
- Port B
	- 8 bit buffer I/O latch
	- can be programmed by mode 0 and mode 1
- Port C
	- 8 bit buffer unlatched. Has input and output latches
	- programmed by bit set / reset operations. Only work in mode 0.
	- can be used as 
		- simple I/O
		- handshake signals
		- status signals
### Modes of operations in 8255
- 8255 can operate in 2 modes
	1. I/O mode
		I/O mode is further divided into
		- Basic I/O (mode 0)
		- Strobe I/O (mode 1)
		- Bi - conditional bus (mode 2)
	1. BSR mode

- mode 0
	- in this mode, port A, B, C are just used individually. A simple mode.
	- outputs are latched and inputs are buffered
	- no handshake capability
- mode 1
	- in this mode, inputs and outputs are transferred by hand shaking signals
- mode 2 
	- allows for bidirectional data transfer using handshakes
	- this feature is only possible in group A
	- port A works as a bidirectional port
	- upper port C is used for the handshakes
## 8254 timer
- it has 3 independent 16-bit down counters and these counters can be programmed in 6 modes.
- The counting types can be set to either BCD or binary system.
- It has a powerful command called "READ BACK COMMAND" which allows the user to check the count value, programmed mode, current mode, and the current status of the counter.
- The operating frequency of 8254 timer is upto 10MHz.
### pin diagram 

![[mpc-8254_pin_diag.png]]

### block diagram

![[mpc-8254_block_diag.png]]

- each counter contains 
	1. clock input that provides the basic operating frequency
	2. a gate input that enables or disables the counter.
		when any value is loaded onto the counter, the value is decremented by 1, until it becomes 0.
	3. an output to get the output value of the counter.
### the working
- After the power-up, 8254 is initially undefined. It has no mode, no count value, and all the outputs of the counters are undefined.
- Each counter should be programmed before it can be used and this programming is done by setting bits in the control word of 8254 and by setting an initial value of the counter.
#### control word
![[mpc-8254_control_word.png]]

- a counter is selected by setting SC<sub>1</sub> and SC<sub>0</sub> values

| SC1 | SC0 | selection                        |
| --- | --- | -------------------------------- |
| 0   | 0   | C0                               |
| 0   | 1   | C1                               |
| 1   | 0   | C2                               |
| 1   | 1   | read the status and reports back |
- the values of RW<sub>1</sub> and RW<sub>0</sub> are used to define the read and write operations

| RW1 | RW0 | selection                                     |
| --- | --- | --------------------------------------------- |
| 0   | 0   | counter latch command                         |
| 0   | 1   | read/write lower byte                         |
| 1   | 0   | read/write higher byte                        |
| 1   | 1   | read/write lower byte followed by higher byte |
- the values of M<sub>2</sub>, M<sub>1</sub>, M<sub>0</sub> are used to decide the operating modes of 8254

| M2  | M1  | M0  | selection |
| --- | --- | --- | --------- |
| 0   | 0   | 0   | mode 0    |
| 0   | 0   | 1   | mode 1    |
| 0   | 1   | 0   | mode 2    |
| 0   | 1   | 1   | mode 3    |
| 1   | 0   | 0   | mode 4    |
| 1   | 0   | 1   | mode 5    |
 - The 0 bit is used to decided whether 8254 should act as a binary counter or BCD counter

### operating modes of 8254
1. Interrupt on terminal count (MODE 0)
	- mode 0 is used for event counting
	- Initially mode 0 will output low until the counting reaches 0, the count is decremented by 1 at each clock cycle.  Once the count reaches 0, the output goes high and remains high until a new word control is written
2. Hardware retrigger-able one shot (MODE 1)
	- Initially the output will be high, it will go low when it encounters a clock pulse that follows a trigger and then it will remain low until the counter reaches 0.
3. Rate generator (MODE 2)
	- mode 2 is used as frequency divider
	- initially the output is low. When the counting is enabled, it goes high and this process is repeated periodically.
4. Square wave generator (MODE 3)
	- mode 3 is used to generate square waves
	- counting is enabled when GATE is 1 and disabled when GATE is 0. 
5. Soft triggered strobe (MODE 4)
	- counting is enabled when GATE is 1 and disabled when GATE is 0. 
	 - initially the output is high and becomes low when value of count is at last stage. Count is reloaded again for the next clock pulse.
6. Hardware triggered strobe (MODE 5)
	- initially the output will be high. 
	- the counting is triggered by a rising edge of GATE
	- when the count reaches 0, the output becomes low for one clock pulse and is high again
	- after writing the new control word and the initial count, the counter will not be loaded until there's a clock pulse after one trigger

### read operations of 8254
- simple read operation
- counter latch command
- read-back command

1.  Simple read operation
	- the counter is selected using A1, A0 inputs.
	- the clock input of the selected counter must be controlled in order to properly read the value from the counter. Otherwise, the count may be in progress during the read operation, thus giving an undefined result.
2. counter latch command
	- if the counter latched and the sometime later it is latched again before the count is read, then the second latch command is ignored
	- and the count read will output the count value of the first latch command.
3. read-back command
	- this command is used when more than one counter should be read at a time.

- status register - shows the state of the output pin