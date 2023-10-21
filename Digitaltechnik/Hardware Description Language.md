**One way to view an HDL is to observe that it describes a relationship between  
signals that are the inputs to a circuit and the signals that are the outputs of the  
circuit.**
HDLs are used in several major steps:  
- Design entry, functional simulation or verification, logic synthesis, timing verification, and fault simulation


### Desigin entry 
- creates an HDL-based description of the functionality that is to be  
implemented in hardware
description forms:  boolean logic equations , truth tables, a netlist of interconnected gates, an abstract behavioral model

### Logic simulation
- displays the behavior of a digital system through the use of a  
computer
-> a simulator interprets the HDL description and either produces readable output, such  as a time-ordered sequence of input and output signal values or displays waveforms of  the signals
-> it predicts how the hardware will behave and as well detects functional errors in a desgin

### Logic synthesis
- is the process of deriving a list of physical components and their  
interconnections (called a netlist )
-> The netlist can be used to fabricate an integrated circuit or to lay out a printed circuit  board with the hardware counterparts of the gates in the list.  
**Hold in mind:** because each logic gate in a circuit has a propagation delay, a signal transition at the  input of a circuit cannot immediately cause a change in the logic value of the output of  a circuit

### Timing verification
- confirms that the fabricated integrated circuit will operate at a  
specified speed.

### Fault simulation
In VLSI(very large scale integration) circuit design, fault simulation compares the behavior of an ideal circuit with  
the behavior of a circuit that contains a process-induced flaw.  
->Fault simulation reveals the difference between the faulty circuit and the fault-free  
circuit.

[[Verilog]]