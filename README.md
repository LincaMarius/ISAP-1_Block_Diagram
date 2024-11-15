# ISAP-1 Block Diagram
The ISAP-1 computer is the improved version of the SAP-1 computer made by me.

This is the first stage of the design of the ISAP-1 computer and consists of the process of optimizing the functionality of the SAP-1 computer at the block diagram level.

By: Lincă Marius Gheorghe.

Pitești, Argeș, România, Europe.

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) computer, but with minimal changes.


## Version 1
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

## Separation of the Central Processing Unit
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

Acesta este procesorul SAP-1 original.

