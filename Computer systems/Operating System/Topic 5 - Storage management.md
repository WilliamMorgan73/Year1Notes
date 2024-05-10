# Disk performance parameters
- Seek time
	- Moving head to target track
- Rotational delay or rotational latency
		- Waiting for targets sector to rotate under head
	- rpm (Revolutions per minute)
- $Access \; time = Seek \; time + Latency$

# Disk scheduling
OS is responsible for using hardware efficiently - for the disk drives, this means having a fast access time
- Access time has two major components
	- Seek time is the time for the disk arm to move the heads to the cylinder containing the desired sector
	- Rotational latency is the additional time waiting for the disk to rotate the desired sector to the disk head

Minimise seek time: $Seek \; time \approx Seek \; distance$
Disk bandwidth is the total number of bytes transferred, divided by the total time between the first request for service and the completion of the last transfer

OS maintains queue of requests, per disk or device
Idle disk can immediately work on I/O request, busy disk means work must queue
- Optimization algorithms only make sense when a queue exists

Several algorithms exist to schedule the servicing of disk I/O requests

We illustrate scheduling algorithms with a request queue

## FCFS scheduling
$$queue =98,183,37,122,14,124,65,67$$
Head starts at $53$

![[FCFS disk schedule graph.png]]

## SSTF scheduling
Shortest seek time first selects the request with the minimum seek time from the current head position
SSTF scheduling is a form of SJF scheduling; may cause starvation of some requests

Total head movements of $236$ cylinders
![[Pasted image 20240305135017.png]]

# SCAN / Elevator scheduling
The disk arm starts at one end of the disk, and moves toward the other end, servicing requests until it gets to the other end of the disk, where the head movement is reversed and servicing continues

Total head movement of $236$ cylinders

![[Pasted image 20240305135224.png]]

## C-Scan scheduling
Provides a more uniform wait time than SCAN
The head moves from one end of the disk to the other, servicing requests as it goes

- When it reaches the other end, however, it immediately returns to the beginning of the disk, without servicing any requests on the return trip

Treats the cylinders as a circular list that wraps around from the last cylinder to the first one

![[Pasted image 20240305135603.png]]

## LOOK scheduling
LOOK, a version of SCAN, C-LOOK a version of C-SCAN
ARM only goes as far as the last request in each direction, then reverses direction immediately, without first going all the way to the end of the disk


### C-LOOK scheduling

![[Pasted image 20240305140157.png]]

## Selecting a Disk-scheduling Algorithm
SSTF is a common and has a natural appeal

SCAN and C-SCAN perform better for systems that place a heavy load on the disk
- Less starvation

Performance depends on the number and types of requests
Requests for disk service can be influenced by the file-allocation method
- And metadata layout

The disk-scheduling algorithm should be written as a separate module of the OS, allowing it to be replaced with a different algorithm if necessary

Either SSTF or LOOK is a reasonable choice for the default algorithm

# Storage array
Can just attach disks, or arrays of disks
Storage Array has controller(s), provides features to attached host(s)
- Ports to connect hosts to array
- Memory, controlling software
- RAID, hot spares, hot swap
- Shared storage
	- More efficiently

## Storage area network
Common in large storage environments
Multiple hosts attached to multiple storage arrays - flexible

![[Pasted image 20240305141530.png]]

## Network-attached storage
Network attached storage (NAS) is storage made available over a network rather than over a local connection (such as a bus)
- Remotely attaching to a file systems

NFS and CIFS are common protocols
Implemented via remote procedure calls (RPCs) between host and storage over typically TCP or UDP
on IP network

iSCSI protocol uses IP network to carry the SCSI protocol
- Remotely attaching to devices (blocks)

![[Pasted image 20240305142130.png]]

# RAID
RAID - Redundant Array of Inexpensive Disks

- Multiple Disk drives provides reliability via redundancy
- RAID is arranged into SIX different levels
- RAID schemes improve performance and improve the reliability of the storage system by storing redundant data
	- Mirroring or shadowing keeps duplicates of each disk
	- Block interleaved party uses much less redundancy
- Data striping
	- Bit-level striping/block level striping

## Raid levels
![[Pasted image 20240305142608.png]]

### RAID 0 - Non-redundant striping
Involves striping data across multiple disks without parity of mirroring
#### Advantages 
- Improved performance (Allows for parallel read and write)
#### Disadvantages
- No data redundancy or fault tolerance, if one drive fails all data is lost

### RAID 1 - Mirrored disks
Mirrors data across two or more drives. Each piece of data is duplicated on all disks 
#### Advantages
- Redundancy and fault tolerance - If one drive fails data is not lost
- Increased read speed - Can read in parallel
#### Disadvantages
- Higher cost due to need for additional drive
- Slower write times as must write to all drives

### RAID 2 - memory-style error-correcting codes.
Uses bit-level striping and adds error-correcting code (Hamming code) for data integrity.
#### Advantages
- High data integrity through error correction.
#### Disadvantages
- Rarely used due to advances in error correction techniques

### RAID 3 - bit-interleaved parity
Stripes data at the bit level and uses a dedicated parity disk to store parity information
#### Advantages
- Good read performance
- Suitable for applications with large sequential data access
#### Disadvantages
-  Write performance can be impacted due to need to update parity information
- All parity data on single disk

### RAID 4 - block-interleaved parity.
Similar to RAID 3, uses block level striping and a dedicated parity disk
#### Advantages
- Improved write performance compared to RAID 3
#### Disadvantages
- Potential for a "parity bottleneck" during heavy write operations
- All parity data on single disk

### RAID 5 - block-interleaved distributed parity
Stripes data at the block level and distributes parity information across all disks in the array
#### Advantages
- Balanced read and write performance
- Good fault tolerance as parity is spread
#### Disadvantages
- Slower write performance compared to RAID 0

### RAID 6 - RAID 6: P + Q redundancy.
Used block level striping but with dual parity for increased fault tolerance
#### Advantages
- Can withstand the failure of two drives without data loss
#### Disadvantages
- Slower write performance compared to raid 5
- Increased cost due to additional parity disk