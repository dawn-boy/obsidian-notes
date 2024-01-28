## computer architecture
- it deals with the functional behavior of the system. A set of rules that describe the functionality, management, and implementation of the computers. 
- it refers to the attributes of the computer that is visible to a programmer. These attributes have a direct impact on the logical execution of the program. 
- attributes like,
	- instruction set,
	- number of bits used,
	- I/O mechanism
	- techniques for addressing the memory

- Also commonly known as **Instruction Set Architecture (ISA)**
- ISA defines,
	- instruction formats and opcodes,
	- registers,
	- instruction and data memory,
	- algorithm for controlling the instruction execution
## computer organization
- refers to the operational units and their interconnections 
	eg: instruction set, number of bits used to represent various data type, I/O mechanism, and techniques for addressing memory.
## computer architecture vs computer organization
example: it is an architectural issue whether an instruction will have a multiplication operation and it is an organizational issue whether that multiplication operation will be implemented by successive additions or by some other method. In short, architecture focuses on what, and organization focus on how.
## structure
the way in which the components are inter-related.
4 main structural components
![[coa-top_level_view_cpu.png]]
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
	- input-output (I/O) are referred to as the peripherals
	- when data moves over a long distance, it is called data communication
- control
	- control unit manages a computer's resources 
	- Coordinates the system performances when instructions are given
## CPU vs. Core vs. processor vs. chip
- CPU is the portion of a computer that fetches and executes instructions, it has ALU, registers, control unit and an internal bus
- a core is an individual processing unit on a processor chip. It is equivalent to a single-core processor
- a processor is a physical piece of silicon containing one or more cores. A processor with multiple cores are referred to as a Multicore-processor
- a chip is a single piece of semiconducting material, typically silicon, upon which electronic circuits and logic gates are fabricated. The resulting product is an integrated circuit.
## L1 vs. L2 vs. L3 cache
- each core may have it's own L1 and L2 cache and a processor-level shared L3 cache which all the cores can commonly access.
- L1 is usually the fastest and the smallest cache while L2 is relatively slower and larger when compared to L1. L3 is even slower and a lot larger in comparison to L2.
## instruction logic
these includes the tasks involved in fetching instructions and decoding each of them to determine the instruction operation and the memory location of any operands
## arithmetic and logic unit
Performs operations specified by an instruction 
## load/store logic
Transfers the data to and from main memory via cache
## cache memory 
The fast, temporary storage between CPU and main memory 
***
## The IAS(Institute of Advanced Studies) computer 
- The idea was first published in 1945 by John von neumann for a new computer known as EDVAC (electronic discrete variable computer)
- In 1946, neumann and his colleagues began designing a new stored-program computer and called it the IAS computer.

- The IAS or Von-Neumann architecture is based on the stored program computers concept where the program data and it's memory location is stored on the same memory
- The Von-Neumann or IAS computer works on the following principles,
	1) same memory is used to store both the program and data,
	2) the program is executed in written sequence,
	3) a program can modify itself when the computer executes the program

types,
- Fixed program computer
	- very specific and rigid can't reprogram
- Stored program computer
	- programmed to carry out difference tasks 
#### instruction word
![[coa-word.png]]
a instruction word is 40 bits long.
- the left side is called the left instruction (20bits) and the right side is the right instruction (20bits)
- each side is made up of a opcode (8bits) and an address (12bits)
### IAS system 
![[coa-ias.png]]
- control unit
	the control unit fetches instructions from memory and executes them one at a time.
- main memory
	stores both data and instructions
- arithmetic and logic unit
	capable of operating on binary data and producing outputs
- input-output (I/O)
	devices connected from external environments through ports. I/O are operated by control unit
#### system registers 
- AL/MQ - accumulator register and multiply-quotient register
	it holds the temporary operands and operations of the ALU.
- MBR - memory buffer register
	It contains a word to be stored in memory or in I/O, or receives a word from memory or from I/O.
- PC - program counter
	- contains the address of the next instruction. It's a 16 bit register.
- MAR - memory address register
	- contains the memory address of the instruction that's to be written to or from the MBR.
- IR - instruction register
	- contains the 8bit opcode of instruction that's being executed
- IBR - instruction buffer register
	- holds temporarily the right hand instruction
### working process
- The instructions are obtained from the main memory and is given to the MBR (memory buffer register).
- The MAR (Memory Address register) has the memory address of the instruction that's currently being executed while the PC (Program Counter) holds the memory address of the instruction that's to be executed next. The IR (instruction register) holds the instruction sets that are to be executed right away while the IBR (instruction buffer register) holds the instruction set that are needed soon.
- the CLU (control unit) coordinates all the above components with the help of clock signals, using them to fetch and execute instructions.
- the ALU (arithmetic/logic unit) has AL (accumulator) and MQ (multiplier quotient) that stores in the operand and operators of the current operation
***
## instruction cycle

![[coa-instruction_cycle.png]]

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
	- 0 - 11 bits  --> operand address
	- 12 - 14 bits --> opcode
	- 15 bit       --> addressing mode 
### instruction execution
- the instruction is send to the MBR (memory buffer register) inside the ALU (arithmetic and logical unit) for execution 

this cycle is repeated until the system comes to a halt or a shutdown.
***
## interconnection structure
Computer is a network of modules. The collection of paths connecting various modules is called the interconnection structure.
- processor
- memory 
- I/O module
#### processor
![[coa-cpu.png]]
- it reads in instructions or data and writes out the data after processing
- uses control signal to control the overall operation of the system
- receives the interrupt signals from the I/O module
#### memory
![[coa-memory.png]]
- it has N-words of equal length
- each word has a unique memory address
- a word of data can be written to or read from the memory
- read or write operations are indicated by a read or write signal
#### I/O module
![[coa-io.png]]
- I/O functions are similar to memory's
- this module can control more than one external device
- each interface to an external device is called a port and each of them is given a unique address
- external devices has an external data path for it's input and output communications
- I/O module can send interrupt signals to the processor.
### layouts supported by interconnection structure
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

![[coa-bus_interconnection_scheme.png]]

a bus that connects major computer components is called system bus. A system bus may typically contain about 50 - 100s of separate lines and each line is assigned a specific function. On any bus the lines can be classified into three functional groups, data-lines, address-lines, control-lines. (in addition to all this, there might also be power distribution lines that supply power to the attached modules)
### data line
- provides a path for moving data among the system modules, these lines are collectively called as data bus
- data bus has 32, 64, 128, or even more separate lines and each line can only carry one signal at a time
- the number of lines determine how much bits can be transmitted at a time, while the width of the lines determine the overall performance. 
- eg: if the bit is 32 bit wide and the instruction is 64 bit long, then the processor needs to access the memory twice each cycle.
### address line
- used to designate the source and the destination of the data travelling in the data bus
- width of the address lines determine the maximum capacity of the memory
- These lines are also used to address the I/O ports
- eg: if the processor wants to read some (8,16,32)-bits of data from the memory, then the processor puts the memory address of that data in the address line
### control lines
- controls the access and use of data and address lines, because the data and address lines are shared by all components, there must be a means of controlling their use.
- timing information
	indicates the validity of data and the address information
- command signal
	specifies the operations to be executed
- the signals that control lines send are
	1) memory write
			causes data on the bus to be written into the addressed location
	2) memory read
			causes data from the addressed location to be placed on the bus
	3) I/O write
			causes data on the bus to be output to the addressed I/O port
	4) I/O read
			causes data on the addressed I/O port to be placed on the bus
	5) transfer ACK
			indicates that data have been accepted from or placed on the bus
	6) bus request
			indicates that a module needs to gain control of the bus
	7) bus grant
			indicates that the requesting module has been granted control of the bus
	8) interrupt request
			indicates that an interrupt is pending
	9) interrupt grant
			indicates that the pending interrupt has been recognized
	10) clock
			used to synchronize operations
	11) reset
			initializes all modules
***
## point to point interface
the shared bus architecture was the standard approach to interconnection between processor and other components for decades, but present computers are switching to point-to-point interconnection. 
The main reasons are the difficulty in performing synchronization and arbitration functions at higher data rates adn keeping up with current multi-core processors at low bus latency is really challenging for the shared bus interconnection.

![[coa-multi_core_config_QPI.png]]

- point-to-point interconnect has lower latency, higher data rate and more scalability.
- Intel's point-to-point approach is the **QuickPath Interconnect (QPI)**, which was introduced in 2008.
- QPI's advantages are,
	1) multiple direct connections 
			multiple components within the system enjoy direct connection to other components, this eliminates the need for arbitration
	2) layered protocol architecture 
			as found in networking models (OSI, TCP/IP models,etc), these processor-level interconnects use a layered protocol
	3) Packetized data transfer
			data are not sent as raw bit stream. Rather, they are sent as a sequence of data packets, each of which includes control headers and error control codes.
- QPI's componenets are,
	1) QPI links
			it forms a switching fabric that enables a data to move throughout the network
	2) I/O hub (IOH)
			it acts as a switch, it directs traffic to and from I/O devices
### QPI layers

![[coa-qpi_layers.png]]

4) protocol layer
	the highest layer contains a set of rules for exchanging the packets between devices. A packet is an integral number of flits.
3) routing layer
	provides the framework for directing the packets
2) link layer
	responsible for reliable transmission and flow control. Link layer's unit of transfer is an 80-bit Flit(Flow Control Unit)
1) physical layer
	consists of actual wires that carry the signals. The unit of transfer is Phit(Physical Unit)
	![[coa-qpi_physical_layer.png]]
	- the QPI port consist of 84 individual links. Each data path has a pair of wire that transmits 1-bit at a time. The pair is referred to as a lane.
	- There are 20 data lanes, and a clock lane in each direction.
	- the lanes in each direction are grouped by four, each group consists of 5 lanes
	- QPI is capable of transmitting 20-bits parallely in each direction, that's why a Phit is 20-bits
## bus arbitration
- multiple devices like CPU, memory, I/O controllers are connected to a common communication pathway called bus. They need to have access to the bus in order to transfer any data between them.
- bus arbitration is a process of resolving any conflicts that may arise when multiple devices attempt to take over control of the bus at the same time. This might lead to data corruption and instability if not handled properly. To prevent all this mess, bus arbitration mechanism is used to ensure that only one device has access to the bus at any given time.
- it's also a process by which the next device becomes the bus master by a transfer of ownership
- methods,
	- centralized
		a single device called the bus controller is responsible for managing the bus access
	- decentralized
		each device is give a priority level and the device with the highest priority level is allowed access to the bus
	- distributed arbitration
		each device competes for control by sending a request signal and they wait till the grant signal is received
#### bus master
- the device that has the access to the bus or that initiates the data transfer on the bus is called the **bus master**
- the selection of a bus master needs to accounted for by various needs of the device and the **bus arbiter** decides who gets to be the bus master
- there can be more than one bus master like the CPU or DMA
- they share the bus access by first completing their transfers and giving up control for the next device
- two approaches to bus arbitration,
	- centralized bus arbitration
		single bus arbiter anoints the chosen one. 
	- distributed bus arbitration
		all devices participates in the selection of bus master. Each device is assigned a 4-bit identification number. The priority of the device will be determined by the generated ID.
### methods of centralized bus arbitration

==note:
BGT --> bus grant signal
BRQ --> bus request signal==

1) daisy chain mode
	![[coa-daisy_chain.png]]
	- simple and cheaper method where all bus master use the same line for making bus requests
	- bus grant signal serially propagates through each bus master until it encounters the first one that requested access to the bus, at this point the master blocks the propagation of the bus grant signal, so that the other devices can't get access to the bus.
	- disadvantages,
		- the value of priority assigned to a device depends it's position relative to that of the master bus
		- There is a propagation delay
		- if one device fails, the whole system stops working
2) polling or rotating priority mode
	![[coa-rotating_priority.png]]
	- the controller is used to generate the address of the master
	- number of address lines required depends on the number of masters connected in the system.
	- The controller generates a sequence of address, and when the requesting master sees it's address, it activates the busy line and begins to use the bus
	- advantages,
		- doesn't favor a single device
		- it is simple
	- disadvantages,
		- if one device fails then the whole system stops working
		- add more bus master is difficult as it increases the number of address lines 
3) fixed priority or independent request method
	![[coa-fixed_priority.png]]
	- each master has a separate pair of bus request and bus grant lines and each each pair has a priority assigned to it.
	- the built-in priority decoder within the controller selects the device with the highest priority request and acknowledges it's bus request signal with a bus grant signal.
	- advantages,
			this method generates a fast response
	- disadvatages,
			hardware cost is high as more number of control lines are required.
***
## computer memory systems
1) location
	- internal - processor registers, cache, main memory, etc
	- external - usb, cd, hard disk, ssd, etc
2) capacity
	- number of words - used to express internal memory
	- number of bytes - used to express external memory
3) unit of transfer
	- word
	- block
4) access method
	- sequential 
		memory is organized into a sequence of data called record. It must be accessed in a linear sequence manner.
	- direct
		involves shared write and read
	- random
		any location can be selected in random and can directly accessed or stored.
	- associative
5) performance
	- access time (latency)
	- cycle time
	- transfer rate
6) physical type
	- semiconductors
	- magnetic
	- optical
	- magneto-optical
7) physical characteristics
	- volatile 
	- non-volatile
	- erasable
	- non-erasable
8) organization
	- memory modules
#### memory hierarchy
arranging different kinds of storage device based on their size, cost, and access speeds, and also in the role they play in application processing.

### cache memory
![[coa-cache_memory.png]]
- it's a small, really fast memory that stores copies of data from frequently used main memory locations. 
- the most important use of cache memory is to reduce the average time to access data from the main memory
#### main memory and cache structure
![[coa-main_mem_and_cache_structure.png]]
##### basic terms
- block
	the minimum unit of transfer between cache and main memory. It's also the physical location in main memory or cache.
- frame
	to distinguish between the data transferred and the chunk of physical memory, the term 'frame' is used
- line
	a portion of cache memory capable of holding one block. A line also includes control information.
- tag
	a portion of cache line that is used for addressing purposes. A cache line may also include other control bits.

##### main memory structure
- main memory consists of up to 2<sup>n</sup> addressable words, with each word having a unique n-bit address. 	$$ 4\ bits\ a\ word \implies 2^4 = 16\ words  $$
- For mapping purposes, the main memory is considered to consist of a fixed-length blocks of K words each.
	that is,
$$M = \frac{2^n}{K}$$
$$MainMemory\ blocks = \frac{total\ no.\ of\ words\ in\ MainMemory}{words\ in\ a\ single\ block\ in\ MainMemory} $$
$$4\ bits\ a\ word ,\ 2\ words \ a\ block \implies M= \frac{2^4}{2} = \frac{16}{2} = 8\ blocks\ in\ MainMemory$$
##### cache structure
- the cache consists of m lines and each line consist of K words and a tag. Each line also includes control bits, such as a bit to indicate whether the line has been modified since being loaded into the cache. 
- the length of a line not including tag and control bits is the line size.
$$ line\ size\ in \ Cache=a\ block\ in\ MainMemory$$
- since there are more blocks in main memory than lines in cache, an individual line cannot be uniquely and permanently dedicated to an individual block, which is why each line has a tag that identifies which particular block is currently being stored
- a tag is usually a portion of the main memory address

##### cache read operation
![[coa-cache_read_op.png]]

- the processor generates the read address of the word to be read, if the word is present in cache then that's called cache hit. Or else, it's called cache miss
- if cache miss occurs, then the block containing the word must be loaded onto cache and the word must be delivered to processor.
##### cache organization
![[coa-cache_org.png]]
- the cache is connected to the processor through control, data, and address lines, and the data and address lines are connected to the system bus through data and address buffers. Using system bus, the processor can access the main memory.
- the tag field of the CPU read address is compared with the tag of the cache line, if they match then it is a catch hit, in that case the address and data buffers are disabled and the communication is only between cache and the process.
- in case of a cache miss, the desired memory address is loaded into the address bus and the data is returned to data buffer which is then sent to both cache and the processor.
#### elements of cache
##### virtual memory 
virtual memory is a memory management technique that is used by modern operating systems to provide more amount of memory (RAM) than that is physically available in the system. This is achieved by a combination of RAM and disk space. 
##### memory management unit (MMU)
when virtual memory addresses are used, a hardware memory management unit is required to translate every virtual memory address into a physical memory address.
##### types of cache
###### logical cache
![[coa-logical_cache.png]]
a logical cache, also known as virtual cache, stores data using virtual addresses. The processor accesses the cache without going through the MMU
- advantage,
	cache access speed is faster in logical cache because a cache can respond before a MMU can perform any operations.
- disadvantage,
	the same virtual address in different application might refer to different physical locations
###### physical cache
![[coa-physical_cache.png]]
a physical cache stores data using physical addresses of the main memory.
##### cache size
![[coa-levels_of_cache.png]]
the size of the cache is pretty small. Processors have different levels of cache such as L1, L2 and L3

#### mapping function
because there are few cache lines than there are main memory blocks, an algorithm is required for mapping the needed blocks. A mapping function describes how the cache should be organized.

there are three techniques,
- direct mapping
- associative mapping
- set associative mapping

###### units
$$1\ kilobyte = 2^{10}\ bytes$$
$$1\ megabyte= 2^{20}\ bytes$$
$$1\ gigabyte= 2^{30}\ bytes$$
###### formula
$$total\ blocks\ in\ MainMemory = \frac{total\ words\ in\ MainMemory}{words\ in\ each\ block}$$
$$total\ bits\ in \ a\ word = log_2(total\ words\ in\ MainMemory) = log_2(2^n)$$
$$tag\ bits = Physical\ address\ bits - (line\ bits
 +offset\ bits)$$
$$tag\ bits = log_2(\frac{total\ main\ memory\ size}{total\ cache\ size})$$ 
$$tag\ directory\ size = no.\ of\ lines\ in\ cache * tag\ bits$$
==note:
- ==physical address bits --> use main memory size==
- ==line bits --> use total no. of line size in cache==
- ==block bits --> use total no. of blocks size in memory==
- ==offset bits --> use size of one block/line==
- ==tag bits --> use (P.A bits - (line bits + offset bits)) or (log(total mainMem size/total cache size))==
