# computer architecture
refers to those attributes that have direct impact on the logical execution of a program.
### ISA (instruction set architecture)
defines the instruction formats, instruction opcodes, registers, instructions and data memory
### computer organization
refers to the operational units and their interconnections that realize the architectural specification.
eg: instruction set, number of bits used to represent various data type, I/O mechanism, and techniques for addressing memory.
## computer architecture vs computer organization
example: it is an architectural issue whether an instruction will have a multiplication operation and it is an organizational issue whether that multiplication operation will be implemented by successive additions or by some other method.
***
## structure
the way in which the components are inter-related.
4 main structural components
- CPU
	controls the operation of the computer and performs it's data processing functions
	- registers - provides storage internal to the CPU.
	- ALU - performs the computer's data processing functions.
	- internal bus - provides a pathway for data communication internally
	- control unit - controls the operation of the CPU and thus the whole system.
		- sequencing logic
		- control registers and decoders
		- control memory
- Main memory
- I/O
	- Anything connected to system from the outside 
	- moves data between computer and it's external environment
- system interconnection
	Communication by the means of system bus
## function
the operation of each individual components in the structure.
- data processing
- data storage
	- Long term
	- short term
- data movement
	- a system consist of devices that serve as sources or destinations of data, when data are received from or delivered to a device that is directly connected to the computer, the process is known as input-output and the device is called as a peripheral.
	- when data moves over a long distance,it is called data communication
- control
	- control unit manages a computer's resources and orchestrates it's performance
	- Coordinates the system registers when instructions are given
## CPU vs. Core vs. processor vs. chip
- CPU is the portion of a computer that fetches and executes instructions, it has ALU, registers, control unit and an internal bus
- a core is an individual processing unit on a processor chip. It is equivalent to a single-core processor
- a processor is a physical piece of silicon containing one or more cores. A processor with multiple cores are referred to as a Multicore-processor
- a chip is a single piece of semiconducting material, typically silicon, upon which electronic circuits and logic gates are fabricated. The resulting product is an integrated circuit.
## L1 vs. L2 vs. L3 cache
- each core may have it's own L1 and L2 cache and a processor-level shared L3 cache
- L1 is usually the fastest and the smallest cache while L2 is relatively slower and larger when compared to L1. L3 is even slower and a lot larger in comparison to L2.
## instruction logic
It deals with fetching instructions and decoding each of them to determine the instruction operation and the memory location of any operands
## arithmetic and logic unit
Performs operations given by an instruction 
## load/store logic
Transfers the data to and from main memory via cache
## cache memory 
The fast, temporary storage between CPU and main memory 
***
# The IAS computer 
## (institute of advanced studies)
- The IAS computer implemented a fundamental design approach known as stored-program concept.
- The idea was first published in 1945 by John von neumann for a new computer known as EDVAC (electronic discrete variable computer)
- In 1946, neumann and his colleagues began designing a new stored-program computer and called it the IAS computer.

- Fixed program computer
	- very specific and rigid can't reprogram
- Stored program computer
	- programmed to carry out difference tasks 
## instruction word
![[word.png]]
a instruction word is 40 bits long.
- the left side is called the left instruction (20bits) and the right side is the right instruction (20bits)
- each side is made up of a opcode (8bits) and an address (12bits)
### IAS system 
![[ias.png]]
- control unit
	the control unit fetches instructions from memory and executes them one at a time.
##### system registers 
- AL/MQ - accumulator and multiplier quotient
	- holds the temporary operands and operations of the ALU 
- MBR - memory buffer register
	- contains a word to be stored in memory or in I/O
	- receives a word from memory or from I/O
- PC - program counter
	- contains the address of the next instruction 
	- 16 bit 
- MAR - memory address register
	- contains the memory address of the instruction that's is to be written to or from the MBR.
- IR - instruction register
	- contains the 8bit opcode of instruction that's being executed
- IBR - instruction buffer register
	- holds temporarily the right hand instruction
### working process
- The instructions are obtained from the main memory and is given to the MBR (memory buffer register).
- The PC (program counter) has the memory address of the instruction that's currently being executed while the MAR (memory address register) holds the memory address of the instruction that's to be executed next. The IR (instruction register) holds the instruction sets that are to be executed right away while the IBR (instruction buffer register) holds the instruction set that are needed soon.
- the CLU (control unit) coordinates all the above components with the help of clock signals, using them to import and execute instructions.
- the ALU (arithmetic/logic unit) has AL (accumulator) and MQ (multiplier quotient) that stores in the operand and operators of the current operation
***
## instruction cycle
the process of fetching the instructions from the memory and decoding them for it's execution. The control unit takes care of these actions and stores the necessary contents in it's appropriate locations.

- start
	- fetch the next instruction
	- decode the fetched instruction
	- execute that instruction
- cycle till halt
### instruction fetch
- instruction cycle stores the memory address of next instruction in PC (program counter)
- the content of the PC (program counter) is assigned to the MAR (memory address register) in the 1st clock cycle.
- In the next clock cycle, the instruction is read from the memory and is stored in the IR (instruction register) and the PC (program counter) is incremented by a value of 1 to point at the memory address of the next instruction.
### instruction decode
- This is the second phase of the cycle.
- The CU (control unit) decodes the instruction once it is loaded into the IR (instruction register)
- the decoding process is based on the opcode bits of the instruction
	-  0 - 11 bits --> Addressing mode
	- 12 - 14 bits --> opcodes 
	- 15 bit --> operand
### instruction execution
- the instruction is send to the MBR (memory buffer register) inside the ALU (arithmetic and logical unit) for execution 

this cycle is repeated until the system comes to a halt or a shutdown.
***
## interconnection structure
- processor
- memory 
- I/O module
#### processor
- it reads in instructions or data and writes out the data after processing
- uses control signal to control the overall operation of the system
- receives the interrupt signals from the I/O module
#### memory
- it has N-words of equal length
- each word has a unique memory address
- a word of data can be written to or read from the memory
- read or write is indicated by a read or write signal
#### I/O module
- I/O functions are similar to memory's
- this module can control more than one external device
- each interface to an external device is called a port and each of them is given a unique address
- external devices has an external data path for it's input and output communications
- I/O module can send interrupt signals
### supported layouts
- memory --> processor
	processor reads from the memory
- processor --> memory
	processor writes to the memory
- I/O --> processor
	processor reads from the I/O device
- processor --> I/O
	processor writes to the I/O device
- I/O <--> memory
	the I/O module is allowed to exchange data directly with memory without the help of a processor, this is called **DMA (direct memory access)**
## bus interconnection
- the bus is the communication pathway connecting two or more devices. It is a shared transmission medium
- multiple devices are connected to the bus but only one can access it at a time
- bus is made up of multiple transmission line where each line is capable of transmitting one binary signal (1,0)
- eg: 8bits of data would be transmitted over 8 lines

### data line
- provides a path for moving data among the system modules, these lines are collectively called as system bus
- data bus has 32, 64, 128, or even more separate lines
- each line can only carry one signal at a time
- the number of lines determine how much bits can be transmitted at a time, while the width of the lines determine the overall performance (bottlenecking the flow.)
- eg: if the bit is 32 bit wide and the instruction is 64 bit long, then the processor needs to access the memory twice each cycle.
### address line
- used to designate the source and the destination of the data travelling in the data bus
- width of the address lines determine the maximum capacity of the memory
- generally used to address the I/O ports
### control lines
- controls the access and use of data and address lines
- monitors all the system modules by sending them the timing information
- timing information
	indicates the validity of data and the address information
- command signal
	specifies the operations to be executed
***
## point to point interface
- p2p has lower latency, higher data rate and more stability than the system bus
- eg: QPI (quick path interconnect)
- data is transmitted over packets instead of bits as like in convention buses
## bus arbitration
- multiple devices like CPU, memory, I/O controllers are connected to a common communication pathway called bus. They need to have access to the bus in order to transfer any data between them.
- bus arbitration is a process of resolving any conflicts that may arise when multiple devices attempt to take over control of the bus at the same time. This might lead to data corruption and instability if not handled properly.
- it's also a process by which the next device becomes the bus master by a transfer of ownership
- methods,
	- centralized
		a single device called the bus controller is responsible for managing the bus access
	- decentralized
		each device is give a priority level and the device with the highest priority level is allowed access to the bus
	- distributed arbitration
		each device competes for control by sending a request signal and they wait till the grant signal is received
- the controller that has the access to the bus is called the **bus master**
- the selection of a bus master needs to accounted for by various needs of the device and the **bus arbiter** decides who gets to be the bus master
### bus master
- a device that initiates the data transfer on the bus
- there can be more than one bus master like the CPU or DMA
- they share the bus access by first completing their transfers and giving up control for the next device
- two approaches to bus arbitration,
	- centralized bus arbitration
		single bus arbitration anoints the chosen one. 
	- distributed bus arbitration
		all devices participates in the selection of bus master
## methods of controlled bus arbitration
- daisy chain
	- simple and cheaper method where all bus master use same line for requesting the bus 
	- bus grant signal serially propagates through each bus master until it encounters the first one that requested access to the bus, at this point the master blocks the propagation of the bus grant signal, so that the other devices can't get access to the bus.
	advantages:
	- doesn't favor a single device
	- it is simple
	disadvantages:
	- adding more bus masters are difficult as it requires including more address lines
	- if one device fails, the whole system stops working.
- fixed priority or independent request method
	- each master has a separate pair of bus request and bus grant lines and each each pair has a priority assigned to it.
	- built-in priority decodes with controller
## QPI (quick path interconnect)
### QPI links
forms a link for data to move throughout the net
### QPI layers
- protocol layer
	it has rules for how the packets should travel
- routing layer
	it gives framework for directing the packets
- link layerj
	responsible for reliable transmission and flow control. A unit of transfer is 80 bit FLIT (flow control unit)
- physical layer
	contains the actual wires, cables, circuitry and the logic that supports features required for transmission. Carries 20 bits at a time called PHIT (physical unit).
	It has 84 individual links and each path has 20 links. A pair of 2 links makes a path. Additionally, it has a clock link.

