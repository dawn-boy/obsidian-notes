# Module 6
## Disk Structure

### Primary storage
- Temporary storage
- if no current, memory gets erased
### Secondary storage
- Permanent storage
- Current has no effect on the memory retention
#### Hard Disk Structure
![[Operation system-1777306470977.jpeg]]
- Its made up of several platters, each divided into tracks and sectors
###### Platters
- circular coated with magnetic material
- each platter stores data on both surfaces.. both on top and bottom
- The disk arm is what used to read or write data
- Multiple platters stacked on spindle, rotating together at high speed ~7200 RPM
###### Tracks
![[Operation system-1777306658182.jpeg]]
- Each platter surface is divided into concentric circles called tracks
- tracks are identified by track number
- a set of tracks at same radius on different platters is called a cylinder

###### Sectors
- each track is further divided into sector, small arcs where data is actually stored
- each sector typically stores 4kb of data
- combination of track + sector number gives the exact address of data

### Disk Scheduling
- It is the method an OS uses to decide which disk I/O request to process next
- Because moving the disk arm takes time and we want to minimize the total head movement to improve overall system throughput

#### Why needed?
- when many process request data from different parts of disk, we cannot serve them in a random order.. that is inefficient.

### Parameters
1. Seek time: Time to move the disk arm to desired track
2. Rotational Latency: Time to desired sector to rotate
3. Transfer time: Time to actually read/write data
4. Access time: Total of above three times
5. Throughput: No. of I/O requests per unit time

### Common algorithms
- FCFS
- SSTF (Shortest seek time first)
- SCAN(Elevator algorithm)
- C-SCAN (Circular SCAN)
***
# Direct Memory access
- DMA is a technique that allows I/O devices to transfer data directly to and from the main memory without involvement of CPU
- CPU just initiates the transfer then DMA handles the rest

### NEED?
- High CPU overhead
- Slower I/O performance

### Components
- CPU
- DMA Controller (DMAC)
- Memory 
- I/O
- System bus

### DMA Working
- Step 1: CPU Sets up the DMA controller with Source address, Destination address, No. bytes
- 