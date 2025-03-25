# ISAP-1 Block Diagram
The ISAP-1 Computer is the improved version of the SAP-1 Computer made by me.

ISAP Computer stands for Improved Simple as Possible Computer

This is the first stage of the design of the ISAP-1 Computer and consists of the process of optimizing the functionality of the SAP-1 computer at the Block Diagram level.

By: Lincă Marius Gheorghe,

Pitești, Argeș, Romania, Europe.

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) Computer, but with minimal changes.

## ISAP-1 version 1

The original Block Diagram of the SAP-1 Computer can be found in the book "Digital Computer Electronics" by Albert Paul Malvino and Jerald A. Brown, on page 141 and is labeled Figure 10-1.

In the following figure, I present a reproduction of the original Block Diagram of the SAP-1 Computer.

![ Figure 1 ](/Pictures/Figure1.png)

### More detailed Block Diagram
I studied the original schematic of the SAP-1 Computer and recreated the Block Diagram to represent the actual functional blocks as closely as possible and I present it in the following figure.

![ Figure 2 ](/Pictures/Figure2.png)

The programming mode of the SAP-1 Computer described by the authors is as follows: \
a.	Move selector S2 to the PROG position to enter Programming Mode, \
b.	Select with the S1 switches the memory address whose content you want to modify, \
c.	Select with the S3 switches the Data that you want to be written to the memory at the previously set address, \
d.	Press button S4 to write the new value to memory, \
e.	Repeat steps b, c and d until all necessary changes have been made, \
f.	Move selector S2 to the RUN position, to run the program.

In practice, the content of the RAM memory is edited, after which its content is only read by the Computer.

This Computer has no instruction to write data to memory. This is specific to read-only ROMs. So, one ROM can be used for each program.

### Block Diagram where only active high control signals are used
In the Diagram in figure 2 it can be seen that some of the control signals are active high and some are active low. This is due to the fact that the circuit diagram is optimized for the TTL integrated circuits used by the authors of the original design of the SAP-1 Computer.

To simplify and ease the Control Block design process, I propose that in this phase of the design we only use active High control signals. This way, the Timing Diagrams in the chapter where we will study the Instruction Set will be easier to understand.

The Block Diagram where only active high control signals are used, can be seen in the following figure.

![ Figure 3 ](/Pictures/Figure3.png)

### Identification of Computer Components
As we learned in school, a computer can be represented by 3 distinct functional blocks:
- CPU,
- Memory
- I/O.

They are interconnected through 3 buses that form the System Bus:
- Data Bus,
- Address Bus
- Control Bus.

This fact is also presented by the authors in the Book in a simplified form on page 213 in figure 13-1.

A diagram representing a computing system consisting of functional blocks CPU, RAM, I/O and buses is presented in the following figure.

![ Figure 4 ](/Pictures/Figure4.png)

If we check the diagram of the SAP-1 computer we notice that these functional blocks are not grouped, we also cannot identify the three buses on the diagram. We are presented with only the data bus labeled "W bus".

So, I propose to redraw the Block Diagram of the SAP-1 computer so that we can easily separate these elements: CPU, RAM and I/O, as well as we can easily identify the three buses. We get the following block diagram.

![ Figure 5 ](/Pictures/Figure5.png)

### Separation of the Central Processing Unit
I propose separating the component blocks of the Central Processing Unit from the other blocks of the computer. This way we will be able to focus on improving the design of only the Central Processing Unit as an entity independent of the other constructive elements of the SAP-1 Computer.

Thus, from Figure 5 we will remove the following blocks and their associated control signals:
- Address Select Switches,
- Program / Run Selector + Deposit,
- Data Select Switches,
- Address MUX,
- 16 x 8 RAM,
- Output Register,
- Binary Display,
- Clock and Reset,
- Power Supply.

The resulting Block Diagram is shown in the following figure

![ Figure 6 ](/Pictures/Figure6.png)

## ISAP-1 Architecture CPU version 1
In order to highlight the three system buses, we must invert the positions of the Program Counter and the Memory Address Register in the diagram.

Now I have renamed the Memory Address Register as the Address Register

![ Figure 7 ](/Pictures/Figure7.png)

The CE signal was renamed PM = Program Memory select \
The LM signal was renamed LAR = Load Address Register \
The LO signal was renamed I/O = Input/Output Device select

### Binary Display
The simplest output device that can be connected to this Computer is a Binary Display. This device is used in the original construction of the SAP-1 Computer, where it is integrated directly into the structure of this Computer.

My version of the Block Diagram is identical to the original, except that I treated the original Output Register as a standalone block that is connected to the system buses as an Input/Output Device.

![ Figure 8 ](/Pictures/Figure8.png)

The output device consists of a register where 8 bits are written when the I/O control signal is activated and the rising edge of the clock occurs. Each bit from the output of this register is connected to an LED. This is a Binary Display.

### Memory Subsystem
Figure 9 shows the Memory block of the SAP-1 computer.

![ Figure 9 ](/Pictures/Figure9.png)

The Memory has two operating modes, dictated by the position of switch S2.

When S2 is in the Run position, the PGM signal is low and causes the Address Multiplexer to select the Address from the input connected to the Memory Address Register. Also, the CE control signal is connected to the #CE control pin of the RAM.

The Diagram of the Memory Block in Run Mode is as follows

![ Figure 10 ](/Pictures/Figure10.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 11 ](/Pictures/Figure11.png)

Thus, the Memory of the SAP-1 Computer in Run Mode is used as a ROM memory. Control input #CE if high disables the output which is three-state, and if low at the output, the data from the address selected by the Memory Address Register is presented on the Bus.

In this case, the CE control signal has the #CE function for chip activation but also the #OE (Output Enable) function specific to ROM memories.

When switch S2 is in the Program Position, the PGM signal is high and causes the Address Multiplexer to select the address from the input connected to Address Select Switches S1.

The control input #CE is set low, so at the Memory output, the Data from the Address selected by the Address Select Switches S1 are presented on the Bus.

If the S4 (Deposit) switch is pressed, the #W control signal is set to the low value, which causes the Data present at the input pins whose values are set by the switches marked S3 (Data Select Switches) to be written to the Selected Address.

The Block Diagram of the Memory Block in Programming Mode is as follows

![ Figure 12 ](/Pictures/Figure12.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 13 ](/Pictures/Figure13.png)

Since no Data is read from the Bus, so no Data is transferred to the Bus, this can also be ignored.

![ Figure 14 ](/Pictures/Figure14.png)

We can conclude that in programming mode the Memory is functionally separate from the SAP-1 computer.

So, functionally speaking, the Memory is simply a ROM for the SAP-1 computer.

We can synthesize a Block Diagram for the Memory Subsystem of the SAP-1 and ISAP-1 computers

![ Figure 15 ](/Pictures/Figure15.png)

We can see an increased complexity of the Memory Subsystem imposed by the need to modify the contents of the Memory using the Control Panel switches.

### SAP-1 computer architecture
The architecture of the ISAP-1 computer up to this point is as follows:

![ Figure 16 ](/Pictures/Figure16.png)

We can distinguish the three subsystems of the computer:
- The SAP-1 CPU
- The Memory Subsystem
- Outputs Subsystem

They are interconnected through the three buses:
- 4-bit Address Bus
- 8-bit Data Bus
- 5-bit Control Bus

The available address space for the SAP-1 computer in this structure is:
- 16 bytes of Program Memory
- 1 Output Devices

From the analysis carried out so far we can draw the following conclusions:
- the Size of Programs that can be run is only 16 bytes,
- the computer cannot retain the values of some variables because it cannot write to Memory,
- jumps in the program cannot be made to perform repetitive tasks because it cannot be written to the Program Counter,
- the computer does not have a stack, so program subroutines cannot be called,
- there is no input device that allows manual data entry.

### ISAP-1 Computer Optimization by Adding RAM Writing
From Figure 7, Figure 15 and Figure 16 it can be seen that the ISAP-1 Computer has the PM signal that commands the reading of data from memory. There is no control signal that allows writing to the memory.

I propose adding a new control signal that I will call R/W (Read/Write) that will control writing either to RAM memory or to an Input-Output port when the I/O control signal is also active.

The ISAP-1 version 1.1 Central Processing Unit is shown in figure 17.

![ Figure 17 ](/Pictures/Figure17.png)

Now we will have 13 command signals that must be provided by the Control Block.

From figure 17 we can see that we can select the Program Memory through the PM control signal but we do not have a control signal to select the Data Memory.

I introduced a new control signal that I called DM (Data Memory) which is used to control access to the Data Memory for read or write operations.

Now we will have 14 command signals that must be provided by the Control Block.

