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

The HLT control signal was omitted in the original Block Diagram.

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

### Grouping Control Signals
If we look carefully at the control signals, we notice that they are placed in the order in which they appear in the Block Diagram from left to right and from top to bottom, according to Figure 1.

I want to optimize these control signals by grouping them into three categories depending on how their activation determines an action on the Data Bus as follows:
- Signals that upon activation cause the controlled block to write data to the Bus, marked in red – only one such signal must be active at any time;
- Signals that upon activation cause the controlled block to read data from the Bus, marked in green;
- Signals that upon activation cause the controlled block to change its state but not transfer data to the Bus, marked in black
- Signals that are part of the Control Bus, marked in blue.

Now the structure of the ISAP-1 Computer Central Processing Unit is:

![ Figure 8 ](/Pictures/Figure8.png)

### Control Unit structure
The SAP-1 computer has a Control Unit made using TTL logic gates.

The Control Unit is built from three blocks:
- Instruction Decoder,
- Step Counter,
- Control Matrix.

The instruction decoder has the structure of a classic decoder and activates a single output depending on the instruction code presented at the input. The number of active outputs is equal to the number of instructions present in the Instruction Set.

![ Figure 9 ](/Pictures/Figure9.png)

The SAP-1 computer is based on micro-step control. For this purpose, a Step Counter block is required. The authors of the SAP-1 computer used a Ring Counter to implement the Step Counter.

The control matrix has the role of generating control signals depending on the instruction that is executed in accordance with the current micro-step.

### Binary Display
The simplest output device that can be connected to this Computer is a Binary Display. This device is used in the original construction of the SAP-1 Computer, where it is integrated directly into the structure of this Computer.

My version of the Block Diagram is identical to the original, except that I treated the original Output Register as a standalone block that is connected to the system buses as an Input/Output Device.

![ Figure 10 ](/Pictures/Figure10.png)

The output device consists of a register where 8 bits are written when the I/O control signal is activated and the rising edge of the clock occurs. Each bit from the output of this register is connected to an LED. This is a Binary Display.

### Memory Subsystem
Figure 9 shows the Memory block of the SAP-1 computer.

![ Figure 11 ](/Pictures/Figure11.png)

The Memory has two operating modes, dictated by the position of switch S2.

When S2 is in the Run position, the PGM signal is low and causes the Address Multiplexer to select the Address from the input connected to the Memory Address Register. Also, the CE control signal is connected to the #CE control pin of the RAM.

The Diagram of the Memory Block in Run Mode is as follows

![ Figure 12 ](/Pictures/Figure12.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 13 ](/Pictures/Figure13.png)

Thus, the Memory of the SAP-1 Computer in Run Mode is used as a ROM memory. Control input #CE if high disables the output which is three-state, and if low at the output, the data from the address selected by the Memory Address Register is presented on the Bus.

In this case, the CE control signal has the #CE function for chip activation but also the #OE (Output Enable) function specific to ROM memories.

When switch S2 is in the Program Position, the PGM signal is high and causes the Address Multiplexer to select the address from the input connected to Address Select Switches S1.

The control input #CE is set low, so at the Memory output, the Data from the Address selected by the Address Select Switches S1 are presented on the Bus.

If the S4 (Deposit) switch is pressed, the #W control signal is set to the low value, which causes the Data present at the input pins whose values are set by the switches marked S3 (Data Select Switches) to be written to the Selected Address.

The Block Diagram of the Memory Block in Programming Mode is as follows

![ Figure 14 ](/Pictures/Figure14.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 15 ](/Pictures/Figure15.png)

Since no Data is read from the Bus, so no Data is transferred to the Bus, this can also be ignored.

![ Figure 16 ](/Pictures/Figure16.png)

We can conclude that in programming mode the Memory is functionally separate from the SAP-1 computer.

So, functionally speaking, the Memory is simply a ROM for the SAP-1 computer.

We can synthesize a Block Diagram for the Memory Subsystem of the SAP-1 and ISAP-1 computers

![ Figure 17 ](/Pictures/Figure17.png)

We can see an increased complexity of the Memory Subsystem imposed by the need to modify the contents of the Memory using the Control Panel switches.

### SAP-1 computer architecture
The architecture of the ISAP-1 computer up to this point is as follows:

![ Figure 18 ](/Pictures/Figure18.png)

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
- the computer cannot retain the values of some variables because it cannot write to Memory,
- jumps in the program cannot be made to perform repetitive tasks because it cannot be written to the Program Counter,
- the computer does not have a stack, so program subroutines cannot be called,
- there is no input device that allows manual data entry.

### ISAP-1 Computer Optimization by Adding RAM Writing
From Figure 7, Figure 17 and Figure 18 it can be seen that the ISAP-1 Computer has the PM signal that commands the reading of data from memory. There is no control signal that allows writing to the memory.

I propose adding a new control signal that I will call R/W (Read/Write) that will control writing either to RAM memory or to an Input-Output port when the I/O control signal is also active.

The ISAP-1 version 1.1 Central Processing Unit is shown in figure 19.

![ Figure 19 ](/Pictures/Figure19.png)

Now we will have 14 command signals that must be provided by the Control Block.

From figure 19 we can see that we can select the Program Memory through the PM control signal but we do not have a control signal to select the Data Memory.

I introduced a new control signal that I called DM (Data Memory) which is used to control access to the Data Memory for read or write operations.

![ Figure 20 ](/Pictures/Figure20.png)

Now we will have 15 command signals that must be provided by the Control Block.

Following the above changes, the ISAP-1 Computer Address Space is:

![ Figure 21 ](/Pictures/Figure21.png)

Compared to version 1.0 of the ISAP-1 Computer in version 1.2 we have:

| ISAP-1 version | Program Memory | Data Memory | Stack      | Input / Output | Nr. of instructions |
|----------------|----------------|-------------|------------|----------------|---------------------|
|  1.0           |  16 bytes      |      -      |      -     |   1 Device     |          5          |
|  1.2           |  16 bytes      |  16 bytes   |      -     |   16 Devices   |          7          |

Now the architecture of the ISAP-1 Computer is as follows

![ Figure 22 ](/Pictures/Figure22.png)

Improvements made at the Block Diagram level allow us to increase the Instruction Set by adding the STA and IN instructions. Now the OUT instruction can have a parameter to select one of 16 output devices.

The new Instruction Set is:

| Mnemonic | Opcode | Operation                                                                 |
|----------|--------|---------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                            |
| ADD n    | 0001   | Add RAM data to Accumulator                                               |
| SUB n    | 0010   | Substract RAM data from Accumulator                                       |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator       |
| OUT n    | 1110   | Load Accumulator data into Output device                                  |
| HLT      | 1111   | Stop processing                                                           |

## Improved design by adding possibility for Program Counter to be preset
From the Block Diagram of the Central Processing Unit in Figure 20, it can be seen that the Program Counter cannot be loaded with a desired value, thus we do not have the possibility of making conditional or unconditional jumps in the execution of the programs being run.

For this purpose, I modified the Program Counter so that it can be loaded with any value present on the W bus, if the new LP control signal is active and a positive edge of the clock signal appears.

ISAP-1 architecture CPU with loadable Program Counter:

![ Figure 23 ](/Pictures/Figure23.png)

The ability to load numerical values ​​into the Program Counter allows us to extend the Instruction Set of the ISAP-1 Computer by implementing the unconditional jump instruction.

The new Instruction Set is:

| Mnemonic | Opcode | Operation                                                                 |
|----------|--------|---------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                            |
| ADD n    | 0001   | Add RAM data to Accumulator                                               |
| SUB n    | 0010   | Substract RAM data from Accumulator                                       |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address |
| JMP n    | 0100   | Unconditional jump to the given address                                   |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator       |
| OUT n    | 1110   | Load Accumulator data into Output device                                  |
| HLT      | 1111   | Stop processing                                                           |

## Improving system design by adding Flags
To run more advanced programs that require conditional jumps, we need to use Flags that provide us with particularities of the result of the last arithmetic or logical operation performed. These characteristics of the result can be determined by evaluating the values ​​of the Flags.

These Flags can be tested individually or in groups. For the ISAP-1 Computer I will use a Flag selector, so only one condition is tested at a time.

The block diagram of the computer that has the Flags register added is as follows:

![ Figure 24 ](/Pictures/Figure24.png)

I added the following control signal:
- LF – Load Flags – load the Flags register with the value of the Flags signals present at the output of the Adder/Subtractor or Arithmetic and Logic Units

I have provided 3 Flags for the ISAP-1 computer:
- The Carry Flag – is set if the 8-bit representation capacity of the result of an arithmetic operation is exceeded,
- The Zero Flag – is set if the result of an arithmetic or logical operation is equal to zero,
- The Sign Flag – is set if the result of an arithmetic or logical operation is negative.

The Control Unit will select which Flag to check by commanding a multiplexer that must select one of the three Flags. So, 2 selection signals are needed.

The output of the multiplexer is the signal labeled “FLG” in the block diagram.

If the three Stages directly commanded the Control Matrix from the Control Unit, there would be 7 command inputs, so 2 ^ 7 = 128 combinations must be handled, which increases the number of logic gates needed to implement the Control Matrix.

By using the solution that uses a multiplexer, we have 5 control inputs, so 2 ^ 5 = 32 combinations must be handled, which reduces by 4 times the number of logic gates required to implement the Control Matrix.

To save the Flags states, the LF (load Flags) control signal is provided. If this is active and a rising edge of the clock signal appears, the Flags state presented at the Adder/Subtractor output is loaded into the Flags register.

Now we will have 17 command signals that must be provided by the Control Block.

The presence of Flags allows us to implement conditional jump instructions:
- JC – Jump if the Carry Flag is set
- JNC – Jump if the Carry Flag is not set
- JZ – Jump if the Zero Flag is set
- JNZ – Jump if the Zero Flag is not set
- JS – Jump if the Sign Flag is set
- JNS – Jump if the Sign Flag is not set

Now we can also implement the comparison instruction that will present us through Flags the result of estimating the ratio between two numerical values ​​of interest.

The presence of the CMP instruction allows us to implement other conditional jump instructions:
- JE – jump if equality (A = B)
- JNE – jump if not equality (A != B)
- JG – jump if greater than (A > B)
- JNG – jump if not greater than (A <= B)
- JGE – jump if greater than or equal to (A >= B)
- JNGE – jump if not greater than or equal to (A < B)
- JL – jump if less than (A < B)
- JNL – jump if not less than (A >= B)
- JLE – jump if less than or equal to (A <= B)
- JNLE – jump if not less than or equal to (A > B)

In total we can implement 17 new instructions that use the state of Flags.

Since the ISAP-1 computer can have a maximum of 16 instructions and we already have 8 instructions in use, it is impossible to implement all of these conditional jump instructions.

I decided to implement only the following 3 conditional jump instructions:
- JC – Jump if Carry Flag is set
- JZ – Jump if Zero Flag is set
- JS – Jump if Sign Flag is set

In addition to these three, I will also include the CMP instruction in the ISAP-1 computer's Instruction Set.

The new Instruction Set is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                                |
| ADD n    | 0001   | Add RAM data to Accumulator                                                   |
| SUB n    | 0010   | Substract RAM data from Accumulator                                           |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address     |
| JMP n    | 0100   | Unconditional jump to the given address                                       |
| JC n     | 0101   | Jump if Carry Flag is set to the given address                                |
| JZ n     | 0110   | Jump if Zero Flag is set to the given address                                 |
| JS n     | 0111   | Jump if Sign Flag is set to the given address                                 |
| CMP n    | 1000   | Compares a numeric value in memory with the numeric value in the accumulator  |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator           |
| OUT n    | 1110   | Load Accumulator data into Output device                                      |
| HLT      | 1111   | Stop processing                                                               |

## Improving the system design by adding the Interrupt System
Since we have an Input-Output subsystem, it is necessary to determine the state of an input-output device to know if it can transmit or receive data.

For this purpose, the interruption mechanism or the pooling method can be used.

The interrupt system requires dedicated hardware for this purpose. When an event occurs, the running program is interrupted and a routine is called that handles the interruption, from which the original program is returned.

This system requires the presence of the stack because subroutines are called.

The pooling method consists of querying each input/output device regarding its availability to transmit or receive data. This query must be done cyclically by the main program.

Usually, a register of the input-output device is read where a bit called READY is tested.

The presence of this Status Register for each input-output device in addition to the data one will halve the number of such devices that can be used in the ISAP-1 computer from 16 to a maximum of 8 and complicates the implementation of these devices.

I decided to implement this mechanism differently by introducing a control signal called INT. This is an input signal for the CPU.

Any input-output device can connect to this signal. It is of the open-collector or open-drain type.

Any input-output device can activate the INT signal only if it is accessed by the presence on the address bus of the address established for it.

The INT signal is connected to the Flag selection multiplexer and is treated by the CPU as a Flag.

To allow working with input-output devices that do not act on the INT control signal, I have provided two new instructions for enabling and disabling interrupts. For this purpose, a flip-flop is set or reset whose output is ORed with the INT signal.

![ Figure 25 ](/Pictures/Figure25.png)

Now we will have 19 control signals that must be provided by the Control Block.

The new Instruction Set is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                                |
| ADD n    | 0001   | Add RAM data to Accumulator                                                   |
| SUB n    | 0010   | Substract RAM data from Accumulator                                           |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address     |
| JMP n    | 0100   | Unconditional jump to the given address                                       |
| JC n     | 0101   | Jump if Carry Flag is set to the given address                                |
| JZ n     | 0110   | Jump if Zero Flag is set to the given address                                 |
| JS n     | 0111   | Jump if Sign Flag is set to the given address                                 |
| CMP n    | 1000   | Compares a numeric value in memory with the numeric value in the accumulator  |
| EI       | 1001   | Enable interrupts                                                             |
| DI       | 1010   | Disable interrupts                                                            |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator           |
| OUT n    | 1110   | Load Accumulator data into Output device                                      |
| HLT      | 1111   | Stop processing                                                               |

## Improved system design by adding Stack
I decided to add operations with the Stack of this computer. This way I can implement subroutine calling as the first benefit. The stack also provides the ability to store data temporarily.

I will use a 4-bit register for the stack, since the address is 4 bits. This register must be incrementable as well as decrementable.

For this purpose we can use a counter. It must be able to be incremented but also decremented.

The Block Diagram of the system that has implemented the Stack Pointer is shown in the following figure.

![ Figure 26 ](/Pictures/Figure26.png)

Now we will have 25 command signals that must be provided by the Control Block.

Since the available RAM is only 16 bytes, I decided to have the Stack use a separate address space, so it doesn't reduce the space available for program variables.

Because the Stack does not use the computer's data RAM, but has its own RAM, the direction of growth of the Stack does not matter.

Following the above changes, the ISAP-1 Computer Address Space is:

![ Figure 25 ](/Pictures/Figure25.png)

Compared to version 1.2 of the ISAP-1 Computer in version 1.6 we have:

| ISAP-1 version | Program Memory | Data Memory | Stack      | Input / Output |
|----------------|----------------|-------------|------------|----------------|
|  1.0           |  16 bytes      |   -         |   -        |     1          |
|  1.2           |  16 bytes      |  16 bytes   |   -        |     16         |
|  1.6           |  16 bytes      |  16 bytes   |  16 bytes  |     16         |

New instructions such as: PUSH, POP, CALL, RET, JMP FAR can now be implemented.

The new Instruction Set is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| LDA      | 0000   | Load RAM data into Accumulator                                                |
| ADD      | 0001   | Add RAM data to Accumulator                                                   |
| SUB      | 0010   | Substract RAM data from Accumulator                                           |
| STA      | 0011   | Stores the numeric value from the Accumulator at the given memory address     |
| JMP      | 0100   | Unconditional jump to the given address                                       |
| JC       | 0101   | Jump if Carry Flag is set to the given address                                |
| JZ       | 0110   | Jump if Zero Flag is set to the given address                                 |
| JS       | 0111   | Jump if Sign Flag is set to the given address                                 |
| CMP      | 1000   | Compares a numeric value in memory with the numeric value in the accumulator  |
| EI       | 1001   | Enable interrupts                                                             |
| DI       | 1010   | Disable interrupts                                                            |
| PUSH     | 1011   | Pushes the value stored in Accumulator onto the Stack                         |
| POP      | 1100   | Pop the value stored on the Stack into the Accumulator                        |
| CALL     | ????   | Subroutine call                                                               |
| RET      | ????   | Return from subroutine                                                        |
| JMPF     | ????   | Unconditional far jump                                                        |
| IN       | 1101   | Loads the numeric value given by an input port into the Accumulator           |
| OUT      | 1110   | Load Accumulator data into Output device                                      |
| HLT      | 1111   | Stop processing                                                               |

## Extending the Instruction Set
The original format of the SAP-1 computer instructions is:

| 4 bits instruction code   | 4 bits operand (memory address)          |
|---------------------------|------------------------------------------|

This implies that a maximum of 2^4 = 16 instructions can be implemented.

From the table above we can see that we need to implement 19 instructions but we only have 16 possible encodings.

Thus the CALL, RET and JMPF instructions cannot be implemented

Since there are instructions that have parameters and instructions that do not require parameters, I will group the instructions without parameters into a separate set of instructions.

This instruction set will have a prefix. I chose the value 1111 binary, 0xF in hexadecimal for this prefix.

| Extended instruction prefix 4 bits (0xF) | Extended instruction 4 bits (0xF)        |
|------------------------------------------|------------------------------------------|

This will leave us with 15 instructions that have parameters and we will be able to implement 16 instructions that do not have parameters.

The ISAP-1 computer will have an Instruction Set consisting of 31 instructions: 15 instructions with parameters and 16 instructions without parameters.

To modify the optimal control signals if we have to execute an extended instruction the Control Block must receive all 8 bits stored in the Instruction Register. This causes the block diagram of the Central Processing Unit of the ISAP-1 computer to be modified as follows:

![ Figure 26 ](/Pictures/Figure26.png)

Compared to version 1.6 of the ISAP-1 Computer in version 1.7 we have:

| ISAP-1 version | Program Memory | Data Memory | Stack      | Input / Output | Nr. of instructions |
|----------------|----------------|-------------|------------|----------------|---------------------|
|  1.0           |  16 bytes      |   -         |   -        |     1          |     5               |
|  1.2           |  16 bytes      |  16 bytes   |   -        |     16         |     7               |
|  1.5           |  16 bytes      |  16 bytes   |   -        |     16         |     14              |
|  1.6           |  16 bytes      |  16 bytes   |  16 bytes  |     16         |     16              |
|  1.7           |  16 bytes      |  16 bytes   |  16 bytes  |     16         |     19              |

The new Instruction Set of the ISAP-1 computer is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                                |
| ADD n    | 0001   | Add RAM data to Accumulator                                                   |
| SUB n    | 0010   | Substract RAM data from Accumulator                                           |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address     |
| JMP n    | 0100   | Unconditional jump to the given address                                       |
| JC n     | 0101   | Jump if Carry Flag is set to the given address                                |
| JZ n     | 0110   | Jump if Zero Flag is set to the given address                                 |
| JS n     | 0111   | Jump if Sign Flag is set to the given address                                 |
| CMP n    | 1000   | Compares a numeric value in memory with the numeric value in the accumulator  |
| CALL n   | 1001   | Subroutine call                                                               |
| JMPF n   | 1010   | Unconditional far jump                                                        |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator           |
| OUT n    | 1110   | Load Accumulator data into Output device                                      |
| EXTENDED | 1111   | Prefix for instructions without parameters                                    |

The new Extended Instruction Set of the ISAP-1 computer is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| PUSH     | 0000   | Pushes the value stored in Accumulator onto the Stack                         |
| POP      | 0001   | Pop the value stored on the Stack into the Accumulator                        |
| RET      | 0010   | Return from subroutine                                                        |
| EI       | 1101   | Enable interrupts                                                             |
| DI       | 1110   | Disable interrupts                                                            |
| HLT      | 1111   | Stop processing                                                               |

## Improving system design by reducing the number of control signals
As can be seen from Figure 26, 5 control signals are used for reading and writing data from memory and input-output ports in version 1.7 of the ISAP-1 Central Processing Unit.

These are: PM, R/W, DM, I/O, SM. With their help we can access: Program Memory, Data Memory, Stack and Input-Output Ports.

I propose grouping these signals so that we can control the 4 address spaces with only 2 control signals by using binary encoding. I have called these control signals CS0 (Chip Select 0) and CS1 (Chip Select 1).

Since Program Memory is read-only I propose to also use write access to this address space and use it to implement a display memory. So I can read code from Program Memory and write data to Display Memory.

The binary encoding of the Memory addressing mode is presented in the following table.

| CS0 | CS1 | R/W | Operation                |
|-----|-----|-----|--------------------------|
|  0  |  0  |  0  | read from Program Memory |
|  0  |  0  |  1  | write to Display Memory  |
|  0  |  1  |  0  | read from Data Memory    |
|  0  |  1  |  1  | write to Data Memory     |
|  1  |  0  |  0  | read from Stack Memory   |
|  1  |  0  |  1  | write to Stack Memory    |
|  1  |  1  |  0  | read from I/O Port       |
|  1  |  1  |  1  | write to I/O Port        |

Control of each type of memory is done by using an external decoder

![ Figure 27 ](/Pictures/Figure27.png)

Now we will have 23 command signals that must be provided by the Control Block compared to 25 in the previous version.

Following the above changes, the ISAP-1 Computer Address Space is:

![ Figure 28 ](/Pictures/Figure28.png)

Now the architecture of the ISAP-1 Computer is as follows

![ Figure 29 ](/Pictures/Figure29.png)

## Improved system design by loading the lower Nibble and upper Nibble of the Accumulator register separately
If we want to load an immediate numerical value into the Accumulator, due to the format of the ISAP-1 Computer instruction we find that it can have values ​​between 0000 binary and 1111 binary, which corresponds to a minimum value of 0 and a maximum value of 15.

To run programs that allow immediate values to be loaded into the 8-bit Accumulator Register, since the Load Accumulator Immediate (LAI) instruction allows 4-bit values equivalent to a nibble, I decided to implement two separate instructions.

- LIL Instruction – Load immediate value into the lower Nibble of the Accumulator
- LIH Instruction - Load immediate value into the upper Nibble of the Accumulator

The block diagram of the Central Processing Unit which has the Accumulator register with separate charging signals for each nibble is shown in the following figure

![ Figure 30 ](/Pictures/Figure30.png)

The LA control signal is replaced by two new control signals
- LAL – load register Accumulator Lower Nibble
- LAH – load register Accumulator Upper Nibble.

The new Instruction Set of the ISAP-1 computer is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| LDA n    | 0000   | Load RAM data into Accumulator                                                |
| ADD n    | 0001   | Add RAM data to Accumulator                                                   |
| SUB n    | 0010   | Substract RAM data from Accumulator                                           |
| STA n    | 0011   | Stores the numeric value from the Accumulator at the given memory address     |
| JMP n    | 0100   | Unconditional jump to the given address                                       |
| JC n     | 0101   | Jump if Carry Flag is set to the given address                                |
| JZ n     | 0110   | Jump if Zero Flag is set to the given address                                 |
| JS n     | 0111   | Jump if Sign Flag is set to the given address                                 |
| CMP n    | 1000   | Compares a numeric value in memory with the numeric value in the accumulator  |
| CALL n   | 1001   | Subroutine call                                                               |
| JMPF n   | 1010   | Unconditional far jump                                                        |
| LAL n    | 1011   | Load immediate value into the lower Nibble of the Accumulator                 |
| LAH      | 1100   | Load immediate value into the upper Nibble of the Accumulator                 |
| IN n     | 1101   | Loads the numeric value given by an input port into the Accumulator           |
| OUT n    | 1110   | Load Accumulator data into Output device                                      |
| EXTENDED | 1111   | Prefix for instructions without parameters                                    |

The Extended Instruction Set of the ISAP-1 computer is:

| Mnemonic | Opcode | Operation                                                                     |
|----------|--------|-------------------------------------------------------------------------------|
| PUSH     | 0000   | Pushes the value stored in Accumulator onto the Stack                         |
| POP      | 0001   | Pop the value stored on the Stack into the Accumulator                        |
| RET      | 0010   | Return from subroutine                                                        |
| EI       | 1101   | Enable interrupts                                                             |
| DI       | 1110   | Disable interrupts                                                            |
| HLT      | 1111   | Stop processing                                                               |

