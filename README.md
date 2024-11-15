# ISAP-1 Block Diagram
The ISAP-1 computer is the improved version of the SAP-1 computer made by me.

ISAP Computer stands for Improved Simple as Possible Computer

This is the first stage of the design of the ISAP-1 computer and consists of the process of optimizing the functionality of the SAP-1 computer at the block diagram level.

By: Lincă Marius Gheorghe.

Pitești, Argeș, România, Europe.

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) computer, but with minimal changes.

## Design improvement by analyzing and modifying the block diagram of the SAP-1 computer

### Original Block Diagram

The original Block Diagram of the SAP-1 computer can be found in the book "Digital Computer Electronics" by Albert Paul Malvino and Jerald A. Brown, on page 141 and is labeled Figure 10-1.

In the following figure, I present a reproduction of the original block diagram of the SAP-1 computer.

![ Figure 1 ](/Pictures/Figure1.png)

### Identification of Computer Components
As we learned in school, a computer can be represented by 3 distinct functional blocks:
- CPU,
- Memory
- I/O.

They are interconnected through 3 buses that form the system bus:
- data bus,
- address bus
- the control bus.

This fact is also presented by the authors in the book in a simplified form on page 213 in figure 13-1.

A diagram representing a computing system consisting of functional blocks CPU, RAM, I/O and buses is presented in the following figure.

![ Figure 2 ](/Pictures/Figure2.png)

If we check the diagram of the SAP-1 computer we notice that these functional blocks are not grouped, we also cannot identify the three buses on the diagram. We are presented with only one bus labeled "W bus".

So, I propose to redraw the Block Diagram of the SAP-1 computer so that we can easily separate these elements: CPU, RAM and I/O, as well as we can easily identify the three buses. We get the following block diagram.

![ Figure 3 ](/Pictures/Figure3.png)

### Block Diagram with control signals active only high
In the diagram in figure 3 it can be seen that some of the control signals are active high and some are active low. This is due to the fact that the circuit diagram is optimized for the TTL integrated circuits used by the authors of the original design of the SAP-1 computer.

To simplify and ease the process of designing the Control Block I propose that in this phase of the design we use only active high control signals. Thus, the time charts will be easier to understand.

The Block Diagram with control signals active only high, can be seen in the following figure.

![ Figure 4 ](/Pictures/Figure4.png)

### Separation of the Central Processing Unit
I propose to separate the component blocks of the Central Processing Unit from the other blocks of the computer.

Thus, from figure 4 we will remove the following blocks and their associated control signals:
- 16 x 8 RAM,
- Output Register
- Binary Display.

The resulting block diagram is shown in the following figure

![ Figure 5 ](/Pictures/Figure5.png)

Now I have renamed the Memory Address Register as the Address Register.

In order to be able to highlight the three buses of the system, we must reverse the positions in the diagram of the Program Counter and the Address Register.

![ Figure 6 ](/Pictures/Figure6.png)

The CE signal was renamed DM = Data Memory Select \
The LM signal was renamed LAR = Load Address Register \
The LO signal has been renamed I/O \

This is the original SAP-1 processor.

### SAP-1 Computer Architecture
The architecture of the SAP-1 computer up to this point is as follows:

![ Figure 7 ](/Pictures/Figure7.png)

We can distinguish the three subsystems of the computer:
- The SAP-1 CPU
- The Memory Subsystem
- Inputs/Outputs Subsystem

They are interconnected through the three buses:
- 4-bit address bus
- 8-bit data bus
- 4-bit commands bus

The available address space for the SAP-1 computer in this structure is:
- 16 Bytes of Program and Data Memory
- 1 Output Devices

The obvious limitation is given by the size of the programs that can be run of only 16 bytes.

The RAM memory is accessed by the SAP-1 computer for reading only. There is no instruction that allows memory to be written, so we can save values ​​in variables.

The system for manual modification of the contents of the RAM memory in the SAP-1 Computer is shown in figure 8

![ Figure 8 ](/Pictures/Figure8.png)

The program cannot change the contents of the memory. The operator can only edit the RAM contents in Programming mode using a series of switches.

So, RAM from the point of view of the available Instruction Set can be viewed as ROM Memory.

The input-output system is very simple and consists of a Binary Display. This is shown in figure 9.

![ Figure 9 ](/Pictures/Figure9.png)

It is noted that it does not have a specific address. It basically displays the information present on the Data Bus if the I/O control signal is active (originally called LO), and when the positive edge of the clock signal is present.

