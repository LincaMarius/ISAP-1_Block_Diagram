# ISAP-1 Computer Block Diagram
The ISAP-1 Computer is the improved version of the SAP-1 Computer made by me.

ISAP Computer stands for Improved Simple as Possible Computer

This is the second stage of the design of the ISAP-1 computer and consists of the process of optimizing the functionality of the SAP-1 computer at the block diagram level.

By: Lincă Marius Gheorghe,

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) Computer, but with minimal changes.

## Original Block Diagram
The original Block Diagram of the SAP-1 Computer can be found in the book "Digital Computer Electronics" by Albert Paul Malvino and Jerald A. Brown, on page 141 and is labeled Figure 10-1.

In the following figure, I present a reproduction of the original Block Diagram of the SAP-1 Computer.

![ Figure 7 ](/Pictures/Figure7.png)

## More detailed Block Diagram
I studied the original schematic of the SAP-1 Computer and recreated the Block Diagram to represent the actual functional blocks as closely as possible and I present it in the following figure.

![ Figure 8 ](/Pictures/Figure8.png)

The HLT control signal was omitted in the original Block Diagram.

The programming mode of the SAP-1 Computer described by the authors is as follows: \
a.	Move selector S2 to the PROG position to enter Programming Mode, \
b.	Select with the S1 switches the memory address whose content you want to modify, \
c.	Select with the S3 switches the Data that you want to be written to the memory at the previously set address, \
d.	Press button S4 to write the new value to memory, \
e.	Repeat steps b, c and d until all necessary changes have been made, \
f.	Move selector S2 to the RUN position, to run the program.

In practice, the content of the RAM memory is edited, after which its content is only read by the SAP-1 Computer.

This Computer has no instruction to write data to memory. This is specific to read-only ROMs. So, one ROM can be used for each program.

## Block Diagram where only active high control signals are used
In the Diagram in [Figure 8](/Pictures/Figure8.png) it can be seen that some of the control signals are active high and some are active low. This is due to the fact that the circuit diagram is optimized for the TTL integrated circuits used by the authors of the original design of the SAP-1 Computer.

To simplify and ease the Control Block design process, I propose that in this phase of the design we only use active High control signals. This way, the Timing Diagrams in the chapter where we will study the Instruction Set will be easier to understand.

The Block Diagram where only active high control signals are used, can be seen in the following figure.

![ Figure 9 ](/Pictures/Figure9.png)

## Identification of Computer Components
As we learned in school, a computer can be represented by 3 distinct functional blocks:
- CPU (Central Processing Unit),
- Memory,
- I/O (Inputs / Outputs).

They are interconnected through 3 buses that form the System Bus:
- Data Bus,
- Address Bus,
- Control Bus.

This fact is also presented by the authors in the Book in a simplified form on page 213 in figure 13-1.

A diagram representing a computing system consisting of functional blocks CPU, RAM, I/O and buses is presented in the following figure.

![ Figure 10 ](/Pictures/Figure10.png)

If we check the diagram of the SAP-1 computer we notice that these functional blocks are not grouped, we also cannot identify the three buses on the diagram. We are presented with only the data bus labeled "W Bus".

So, I propose to redraw the Block Diagram of the SAP-1 computer so that we can easily separate these elements: CPU, RAM and I/O, as well as we can easily identify the three buses.

We get the following Block Diagram:

![ Figure 11 ](/Pictures/Figure11.png)

## ISAP-1 Computer version 0.1
Version 0.1 of the ISAP-1 computer is identical in schematic terms to the SAP-1 computer.

The difference will come from the modular approach to computer construction.

### Separation of the Central Processing Unit
I propose separating the component blocks of the Central Processing Unit from the other blocks of the computer. This way we will be able to focus on improving the design of only the Central Processing Unit as an entity independent of the other constructive elements of the ISAP-1 Computer.

Thus, from [Figure 11](/Pictures/Figure11.png) we will remove the following blocks:
- Address Select Switches,
- Program / Run Selector + Deposit,
- Data Select Switches,
- Address MUX,
- 16 x 8 RAM,
- Output Register,
- Binary Display,
- Clock and Reset,
- Power Supply.

The resulting Block Diagram is shown in the following figure:

![ Figure 12 ](/Pictures/Figure12.png)

In order to highlight the three system buses, we must invert the positions of the Program Counter and the Memory Address Register in the diagram.

Now I have renamed the Memory Address Register as the Address Register

![ Figure 13 ](/Pictures/Figure13.png)

The CE signal was renamed PM = Program Memory select \
The LM signal was renamed LAR = Load Address Register \
The LO signal was renamed I/O = Input/Output Device select

### Grouping Control Signals
If we look carefully at the control signals, we notice that they are placed in the order in which they appear in the Block Diagram from left to right and from top to bottom, according to [Figure 7](/Pictures/Figure7.png)

I want to optimize these control signals by grouping them into three categories depending on how their activation determines an action on the Data Bus as follows:
- Signals that when activated cause the commanded block to write data to the Data Bus are marked in RED – only one such signal must be active at any given time;
- Signals that when activated cause the commanded block to read data from the Data Bus are marked in GREEN;
- Signals that when activated cause the commanded block to change its state but not transfer data to the Data Bus are marked in BLACK;
- Signals that are part of the Command Bus are marked in BLUE.

Now the structure of the ISAP-1 Computer Central Processing Unit is:

![ Figure 14 ](/Pictures/Figure14.png)

### Control Unit structure
The SAP-1 computer has a Control Unit made using logic gates.

The Control Unit is built from three blocks:
- Instruction Decoder,
- Step Counter,
- Control Matrix.

The Instruction Decoder has the structure of a classic decoder and activates a single output depending on the instruction code presented at the input. The number of active outputs is equal to the number of instructions present in the Instruction Set.

![ Figure 15 ](/Pictures/Figure15.png)

The SAP-1 computer is based on micro-step control. For this purpose, a Step Counter block is required. The authors of the SAP-1 computer used a Ring Counter to implement the Step Counter.

The Control Matrix has the role of generating control signals depending on the instruction that is executed in accordance with the current micro-step.

### Binary Display
The simplest output device that can be connected to this Computer is a Binary Display. This device is used in the original construction of the SAP-1 Computer, where it is integrated directly into the structure of this Computer.

My version of the Block Diagram is identical to the original, except that I treated the original Output Register as a standalone block that is connected to the system buses as an Input/Output Device.

![ Figure 16 ](/Pictures/Figure16.png)

The output device consists of a register where 8 bits are written when the I/O control signal is activated and the rising edge of the clock occurs. Each bit from the output of this register is connected to an LED. This is a Binary Display.

### Memory Subsystem
[Figure 17](/Pictures/Figure17.png) shows the Memory block of the SAP-1 computer.

![ Figure 17 ](/Pictures/Figure17.png)

The Memory has two operating modes, dictated by the position of switch S2.

When S2 is in the "Run" position, the PGM signal is low and causes the Address Multiplexer to select the Address from the input connected to the Memory Address Register. Also, the CE control signal is connected to the #CE control pin of the RAM.

The Diagram of the Memory Block in Run Mode is as follows

![ Figure 18 ](/Pictures/Figure18.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 19 ](/Pictures/Figure19.png)

Thus, the Memory of the SAP-1 Computer in Run Mode is used as a ROM memory. Control input #CE if high disables the output which is three-state, and if low at the output, the data from the address selected by the Memory Address Register is presented on the Bus.

In this case, the CE control signal has the #CE function for chip activation but also the #OE (Output Enable) function specific to ROM memories.

When switch S2 is in the "Program" Position, the PGM signal is high and causes the Address Multiplexer to select the address from the input connected to Address Select Switches S1.

The control input #CE is set low, so at the Memory output, the Data from the Address selected by the Address Select Switches S1 are presented on the Bus.

If the S4 (Deposit) switch is pressed, the #W control signal is set to the low value, which causes the Data present at the input pins whose values are set by the switches marked S3 (Data Select Switches) to be written to the Selected Address.

The Block Diagram of the Memory Block in Programming Mode is as follows

![ Figure 20 ](/Pictures/Figure20.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 21 ](/Pictures/Figure21.png)

Since no Data is read from the Bus, so no Data is transferred to the Bus, this can also be ignored.

![ Figure 22 ](/Pictures/Figure22.png)

We can conclude that in programming mode the Memory is functionally separate from the SAP-1 computer.

So, functionally speaking, the Memory is simply a ROM for the SAP-1 computer.

We can synthesize a Block Diagram for the Memory Subsystem of the SAP-1 and ISAP-1 computers

![ Figure 23 ](/Pictures/Figure23.png)

We can see an increased complexity of the Memory Subsystem imposed by the need to modify the contents of the Memory using the Control Panel switches.

### Reset Circuit
The Reset circuit has the role of bringing the computer back to its initial state. Internally, the Central Processing Unit initializes the functional blocks so that they can begin stable execution of any program.

The block diagram of the reset circuit is shown in the following figure

![ Figure 24 ](/Pictures/Figure24.png)

The circuit consists of a switch marked S5 with two positions followed by a debouncing circuit consisting of an RS flip-flop in the case of the SAP-1 computer.

## Clock generator circuit
The clock signal is responsible for ensuring synchronous operation of the computer, so that any action takes place at a precise moment in time. Through synchronization, data transfer in the system occurs in a controlled manner.

The SAP-1 computer has two operating modes:
- Manual – in this mode the clock signal is generated by pressing a button and the program execution advances step by step,
- Automatic – in this mode the clock signal is generated continuously and the program execution is continuous.

For the Automatic mode, the clock signal is generated by an oscillator made with an astable. Its output reaches a T-type flip-flop. The T-type flip-flop divides the input frequency by 2 but we also obtain a signal duty cycle of 50%.

To generate the clock signal in step-by-step mode, we have a two-position switch marked S6 in the diagram followed by an RS-type flip-flop which acts as a debouncing circuit.

The switch marked S7 in the schematic is used to select the operating mode. This is followed by an RS type flip-flop which acts as a debouncing circuit.

Depending on the chosen operating mode, one of the two clock signals is selected using a multiplexer.

The output of the multiplexer is taken by the buffer. Its role is to ensure the necessary fanout as the clock signal reaches all the components of the computer.

![ Figure 20 ](/Pictures/Figure20.png)

## SAP-1 computer architecture
The architecture of the ISAP-1 computer up to this point is as follows:

![ Figure 21 ](/Pictures/Figure21.png)

We can distinguish the three subsystems of the computer:
- The ISAP-1 CPU
- The Memory Subsystem
- Inputs/Outputs Subsystem

They are interconnected through the three buses:
- 4-bit Address Bus
- 8-bit Data Bus
- 5-bit Control Bus

The available address space for the SAP-1 computer in this structure is:
- 16 bytes of Program Memory
- 1 Output Devices

The original instruction set of the SAP-1 computer is:

| Mnemonic | Opcode | Operation                                  |
|----------|--------|--------------------------------------------|
| LDA      | 0000   | Load RAM data into Accumulator             |
| ADD      | 0001   | Add RAM data to Accumulator                |
| SUB      | 0010   | Substract RAM data from Accumulator        |
| OUT      | 1110   | Load Accumulator data into Output Register |
| HLT      | 1111   | Stop processing                            |

From the analysis carried out so far we can draw the following conclusions:
- the Size of Programs that can be run is only 16 bytes,
- the Computer cannot retain the values of some variables because it cannot write to Memory,
- jumps in the program cannot be made to perform repetitive tasks because it cannot be written to the Program Counter,
- the Computer does not have a Stack, so program subroutines cannot be called,
- there is no input device that allows manual data entry.

## ISAP-1 Computer version 0.1
For version 0.1 we need to implement the FETCH portion of an instruction execution. This is equivalent to implementing the NOP instruction.

The starting point is the timing diagram of the NOP instruction shown in the following figure.

![ Figure 1 ](https://github.com/LincaMarius/ISAP-1_Instruction_Set/blob/main/Pictures/Figure1.png)

The functional blocks that participate in the execution of the NOP instruction are:
- Program Counter
- Address Register
- RAM – can be ignored because we are not decoding the instructions
- Instruction Register

These alone are not enough to ensure the execution of the NOP instruction. The remaining functional blocks that are required can be determined from the following figure:

![ Figure 21 ](/Pictures/Figure21.png)

We will also need the following circuits:
- Clock
- Reset

From the structure of the Central Processing Unit shown in the following figure

