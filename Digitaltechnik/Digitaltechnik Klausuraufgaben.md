
### Combinational circuits
- spotting hazards when a single bit change occurs -> Karnaugh Map zeichnen und anschließend Analysieren, ob eine Disjunktion zwischen verschiedenen True values fehlt
- logical circuit Designen, der bestimmte Operation ausführt als combinational circuit
	1) construct truth table
	2) simplify the function using karnaugh map in the sum-of-products form
	3) draw the logic diagram
		- this might include only using NOR or NAND gates, so take look at universal gates
- draw logic diagram of a described circuit and also be able to provide Verilog code




### Sequential circuits
- the distinction between mealy and moore circuits/state machine and be able to design a state diagram/machine
- D-flip flops and other flip flops types, learn the truth tables
- binary state encoding (different encoding schemes in general)
- be able to use a karnaugh map to specify the different input/output signals, to allow the type-specific flip flop use, by looking at the combinational equations done by the Karnaugh Map
- draw logic diagrams of the flip flops inputs circuits

- fill in verilog code of a given module and table about the behaviour of a module
- Additionally, We want to build a divide-by-586 frequency divider using several copies of
this counter. The circuit should produce a periodic output signal (clk_out) whose frequen-
cy is 586 times slower than its input clock (clk) frequency. Complete the following code
to perform this operation. ?????


- know how to minimize a state diagram



### extra concepts of last lectures
