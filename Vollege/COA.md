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
The main reasons are the difficulty in performing synchronization and arbitration functions at higher data rates and keeping up with current multi-core processors at low bus latency is really challenging for the shared bus interconnection.

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
==note:==
- ==physical address bits --> use main memory size==
- ==line bits --> use total no. of line size in cache==
- ==block bits --> use total no. of blocks size in memory==
- ==offset bits --> use size of one block/line==
- ==tag bits --> use (P.A bits - (line bits + offset bits)) or (log(total mainMem size/total cache size))==

$$P.A= tag\ bits + line\ bits+ block/line\ offset$$
$$P.A = block\ bits+ block/line\ offset$$
## Internal memory
### semiconductor memory
- The most common form of random-access storage for computer main memory employees an array of doughnut shaped ferromagnetic loops referred to as cores
- the basic element of semiconductor memory is memory cell
- properties,
	- they exhibit two stable states, which can represent binary 1 and 0
	- they're capable of being written into, to set the state
	- they're capable of being read from, to sense the state
### memory operation
- A cell has three functional terminals that is capable of carrying an electric signal
- select: select signal is used to select a memory cell for read or write operation
- control: control signals indicates whether the operation to be performed is either read or write
- read/write: this signal is common for both operations. For writing, the terminal provides an electric signal that sets the state. For reading, the terminal is used as an output of the cell's state.
### semiconductor memory types
#### RAM
- it's possible to read and write data into RAM easily and rapidly. Both reading and writing are accomplished through the use of electrical signal.
- Traditional RAM is volatile. A RAM must be provided with a constant power supply, if the power is interrupted, then all the data is lost. So RAM can only be used as a temporary storage.
- traditional forms of RAM are,
	- DRAM
	- SRAM
- newer forms of RAM are non-volatile
- Dynamic RAM
		![[coa-dram.png]]
	- A DRAM is made up of cells that store data as charge on capacitors. The presence or absence of charge in a capacitor is interpreted as binary 1 and 0
	- because capacitors have a natural tendency to discharge, dynamic RAMs require periodic charge refreshing to maintain data storage
	- the term dynamic refers to this tendency of stored charge to leak away even with power continuously applied
	- memory is made of bits of data that are arranged in a two-dimensional grid
	- DRAM will store bits of data in what's called a storage or memory cell, consisting of a capacitor and a transistor
	- the address line is activated when the bit value from this cell is to be read or written. The transistor acts as a switch that is closed (allowing the current to flow) if a voltage is applied to the address line and open(no current flows) if no voltage is present on the address line.
	- write operation
		 for the write operation, a voltage signal is applied to the bit line, a high voltage represents 1, and a low voltage represents 0. A signal is then applied to the address line, allowing a charge to be transferred to the capacitor.
	- read operation
		 for the read operation, when the address line is selected, the transistor turns on and the charge stored on the capacitor is fed out onto the bit line and to a sense amplifier. The sense amplifier compares the capacitor voltage to a reference value and determines if the cell contains a logic 1 or a logic 0. The readout from the cell discharges the capacitor which must be restored to complete the operation since reading from the capacitor drains its charge making it a destructive process.
- Static RAM
	- its a digital device that uses the same logic elements used in the processor
	- in a SRAM, binary values are stored using traditional flip-flop logic gate configurations
	- there are four transistors T1, T2, T3, T4 are cross connected in an arrangement that produces a stable logic state 
	- In logic state 1, C1 is high and C2 is low. T1 and T4 are OFF, T2 and T3 are ON
	- in logic state 0, C1 is low and C2 is high. T1 and T4 are ON, T2 and T3 are OFF
	- both states are stable as long as there is direct current
	- unlike the DRAM, no refresh is needed to retain its data
	- As in the DRAM, the SRAM address line is used to open and close a switch which controls T5 and T6. 
	- for the write operation, the desired bit value is applied to line B whilst its complement is applied to line <span style="text-decoration: overline">B</span>. 
#### ROM
- a read only memory contains a permanent pattern of data that cannot be changed. ROM is non-volatile and no power source is required to maintain the bit values in memory
- while we can read from ROM, its not possible to write anything to it.
##### programmable ROM
- when only small number of ROMs with a particular memory content is needed, a less expensive alternative is PROM. its non-volatile and may be written onto only once.
- for the PROM, writing process is done electrically and may be performed by a supplier or customer at a time later that the original chip fabrication
- special equipment is required for the writing process
###### read mostly memory
read-mostly memory is useful for applications in which read operations are far more frequent that write operations but for which non-volatile storage is required. There are three common forms of read-mostly memory

1) EPROM
	 optically erasable programmable read only memory is read and written electrically as with PROM. However, before a write operation, all the storage cells must be erased to the same initial state by exposure of packaged chip to ultraviolet. Erasure is performed by shining an intense ultraviolet light through a window that is kept in the memory chip for that purpose. Erasure process can be performed repeatedly and each erasure takes about 20 minutes. EPROM is expensive than PROM but has the advantage of being updated
1) EEPROM
	a type of non-volatile ROM that enables individual bytes of data to be erased and reprogrammed. It uses electric signals to erase and program the contents rather than UV signals. This is a read-mostly memory that can be written to at any time without clean wiping prior to writing. EEPROM is more expensive than EPROM and is less dense supporting fewer bits per chip.
1) Flash memory
	a type of non-volatile memory that erases data in units called blocks and rewrites data at byte level. its the intermediate between EPROM and EEPROM in both cost and functionality
	Like EEPROM it uses electrical erasing technology resulting in a much faster erasure rate than EPROM. And like EPROM, flash memory uses only only transistor per bit resulting in a higher density than EEPROM
### chip logic
![[coa-chip_logic.png]]
an organization in which the physical arrangement of cells in array is same as the logical arrangement of words in memory. 
- 4 bits are read or written at a time, logically memory array is organized as four square arrays of 2048 by 2048 elements
### hamming code error detection
its a network technique designed by R. W. hamming for damage and error detection during data transmission between multiple network channels. Its the one of the most effective ways to detect single-data bit errors in original data at the receiver's end. Its not only used for error detection but also for correcting errors in data bit
## External devices
- External devices provides a means for exchanging data between the external environment and the computer. 
- an external device attaches to the computer by a link to an I/O module. The link is used to exchange control, status and data between the I/O module and external devices. The external device that is connected to an I/O module is often referred to as a peripheral device
- its broadly classified into three categories,
	1) Human readable: suitable for communicating with the computer user
		 eg: video display terminals
	2) Machine readable: suitable for communicating with equipment
		 eg: magnetic disk and tape systems, sensors and actuators
	3) communication: suitable for communicating with remote devices
		 eg: exchange data with remote device
### block diagram
![[coa-external_dev_block_diagram.png]]


- The interface to the I/O module is in the form of control, data, and status signals
- the Control signals determine the function that the device will perform,
	1) send data to I/O module (INPUT or READ)
	2) accept data from I/O module (OUTPUT or WRITE)
	3) report status
- data are in the form of set of bits to be send to or received from I/O module
- status signals indicate the state of devices (READY or NOT-READY)
#### control logic
 control logic associated with the device controls the device's operation in response to direction from the I/O module 
#### transducer
it converts data from electricals to other forms of energy during the output. It also converts from other forms of energy to electric whilst input.
#### buffer
A buffer is associated with the transducer. It temporarily holds data that's being transferred between the I/O module and external environment. A common buffer size is about 8 - 16 bits long for serial devices whereas block-oriented devices such as disk drive controllers have much larger buffers.
### I/O module
The major functions of an I/O module 
- Control and timing
	 - At any time, the processor may communicate with one or more external devices depending on the program's need for I/O 
	 - the internal resources such as main memory and the system bus, is shared among a number of activities including data I/O
	 - so the I/O function requires a control and timing requirement to co-ordinate the flow of traffic between internal resources and external devices. 
	 - The control of the transfer of data from an external device to the processor includes the following steps
		 1. the processor request the I/O module to check the status of the attached device
		 2. the I/O module returns the device status
		 3. if the device is operational and ready to transmit, the processor requests the transfer of data by means of a command to the I/O module
		 4. I/O module obtains the data from the external device 
		 5. the data is transferred to the processor form the I/O module.
- processor communication
	- To communicate with the processor and with the external device, the following steps are required
		1) command decoding
			 -  The I/O module accepts commands from the processor
			 -  it sends it as signals to the control bus.
			     commands like: READ SECTOR, WRITE SECTOR, SEEK track_number, SCAN record_ID
		2) data
			 data is exchanged between the processor and the I/O module over the data bus
		3) status reporting
			 because peripherals are so slow, its important to know their status using the I/O module. Common status signals are BUSY and READY.
		4) address recognition
			 just as each word of memory has an address, so does each I/O devices. Thus, an I/O module must recognize one unique address for each peripheral it controls, then I/O module must be able to perform device communication. The communication involves commands, status information and data.
- device communication
- data buffering
- error detection
#### block diagram
![[coa-io_modules_block_diagram.png]]
- the module connects to the rest of the computer through a set of signal lines. The data transferred to and from the module are buffered in one or more data registers.
- there are status registers that provide the current status information. A status register may also function as a control register to accept detailed control information from the processor. 
- The logic within the module interacts with the processor via a set of control lines. The processor uses the control lines to issue commands to the I/O module. Each I/O module has a unique address. 
- the I/O module contains logic specific to the interface with each device that it controls.
==An I/O module that takes on most of the detailed processing burden, presenting a high-level interface to the processor, is usually referred to as an I/O channel or I/O processor.==
### I/O operation techniques
#### programmed I/O
- data is read in one word into memory
- for each word that is read in, the processor must remain in status checking cycle until it determines that the word i s available in the I/O module's data register
- the main disadvantage of this technique is that its time consuming process that keeps the processor busy needlessly.
- since the processor has to wait a long time for the external device to be ready for either reception or transmission of data and also it has to repeatedly interrogate the status of the external device, the performance of the entire system is severely degraded.

In simple words, once the CPU checks for the status of the external device through the I/O module, it waits if the external device is BUSY. 
#### Interrupt I/O
this technique is more efficient than programmed I/O because it eliminates the needless waiting time period. However interrupt I/O still consumes a lot of processor time because every word from memory to I/O module or from I/O module to memory still has to go through the processor.
- the device issues an interrupt signal to the processor
- the processor finishes execution of the current instruction before responding to the interrupt
- the processor tests for an interrupt, if there is one, then it sends back an acknowledgment signal to the device that issued the interrupt
- the acknowledgment allows the device to remove its interrupt signal
- The processor now needs to prepare to transfer control to the interrupt routine
- the minimum information required to resume its current tasks are,
	1. the status of the processor, which is copied to a the Program Status Word (PSW)
	2. the location of the next instruction to be executed, which is copied to the Program Counter (PC)
- these are pushed to the system control stack
- the processor now loads the program counter with the entry location address

in simple words, the processor checks the status of the external device but does not wait if its busy, the processor carries on with its task. When the external device is READY, the processor stores its current data process in a stack, goes to the I/O module and performs the required operation and comes back to the stack to pick it up from where it left.
#### Direct memory access (DMA)
The DMA module transfers the entire block of data, one word at a time directly to or from the memory without going through the processor at all. When the transfer is complete, the DMA module sends an interrupt signal to the processor. Thus the processor is involved only at the beginning and at the end of the transfer.
- DMA is an additional module on the system bus
- its capable of mimicking the processor, taking control over the processor.
- The DMA module must use the bus only when the CPU doesn't need it or it must force the processor to suspend operation temporarily. This technique is called cycle stealing.
the DMA mechanism can be configured in a variety of ways,
1) Single bus, detached DMA: 
![[coa-single_bus_DMA.png]]
	All the modules share the same system bus, the DMA module acting as a surrogate processor. 

2) Single bus, integrated DMA-I/O: 
![[coa-single_bus_int_DMA.png]]
	 the number of bus cycles can be cut substantially by integrating the DMA and I/O functions. This means that there is a path between the I/O module and the DMA which doesn't include the system bus.

3) I/O bus: 
![[coa-io_bus.png]]
- this reduces the I/O interfaces in the DMA module to one.
- the system bus that the DMA uses with the processor and memory is only there to exchange data.
### I/O commands
to execute an I/O related instruction, 
- the processor issues an address specifying the particular I/O module and external device
- the processor issues an I/O command
there are four types of I/O commands that an I/O module may receive when it is addressed by the processor,
1) Control
	 used to activate a peripheral and tell it what to do
2) Test
	 used to test various status conditions associated with an I/O module and its peripherals
3) Read
	 causes the I/O module to obtain an item of data from the peripheral and place it in the internal buffer
4) Write
	causes the I/O module to take an item of data from the data bus and transmit it to the peripheral.
### I/O structure
1) memory mapped I/O
	 - there is a single address space for memory locations and I/O devices. 
	 - The processor treats the status and data registers of I/O modules as memory locations. 
	 - The processor uses the same machine instructions to access both memory and I/O devices
		for example: with 10 address lines, 2<sup>10</sup> = 1024 memory locations and I/O addresses can be contained in any combination
2) Isolated I/O
	- the address space for I/O is isolated from that of the memory's. So, with 10 address lines, there could now be 1024 memory locations and 1024 I/O addresses.
	- the I/O ports are accessible only by special I/O commands, which activate the I/O command lines on the bus.