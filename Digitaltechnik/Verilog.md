
## Gatelevel
-die wirklichen Gates werden durch input und output Beschreibungen anhand von wire beschrieben und so die Schaltungen beschrieben

## Dataflow level
Dataflow modeling of combinational logic uses several operators that act on binary operands to produce a binary result

## Behavorial level

```
module Adder_Subtractor  
	#(parameter n=8)  
	( input M, [n-1:0] X, [n-1:0] Y,  
	output Cout, [n-1:0] SUM);  
	assign {Cout, SUM}= M? (X-Y):(X+Y);  
endmodule
```

_Procedural assignments_ are used for updating register data types and memory data types.

The expression in a blocking procedural assignment is evaluated and assigned when the statement is encountered. 

### Procedural Modeling  
▪ Each signal in the sensitivity list can be separated by comma @(a, b), or by the  
keyword or: @(a or b)  
▪ The target output of a procedural assignment statement must be of the reg data type.  
▪ Contrary to the wire data type, whereby the target output of an assignment may be  
continuously updated, a reg data type retains its value until a new value is assigned.

![[Pasted image 20230515125202.png]]
![[Pasted image 20230515125150.png]]