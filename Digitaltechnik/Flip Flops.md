clock jitter= Taktzyklen einer Clock sind nicht identisch und minimal verschoben, somit gilt für zwei Taktzyklen der Clock T1 und T2: T1!=T2

▪ The memory elements used in sequential circuits are called flip-flops.  
▪ A flip-flop is a binary storage device capable of storing one bit of information


Latenzzeit muss dem Latach Zirkel angepasst werden, wie lange dauert es bis der Triggerimpuls wieder am Zustand ankommt?

###### Definition latch:
A latch is **a digital electronic circuit that has two stable states and can store a digital signal**. These two states are known as set and reset state or high or low state as it has two stable states it is also known as bistable multivibrators. It stores the data using the feedback lane


## Latch Verilog 

```
module D_Latch (  
input D, E,  
output reg Q  
);  
always @(E, D)  
if(E)  
Q <= D;  
endmodule
```

really important: use nonblocking assignment, in case of latch implementation


Flip Flop und Latch unterscheiden sich in der graphischen Darstellung nur zwischen dem Dreieck, dass angibt das das Latch edge-triggered ist

positive-edge: es wird auf den Zeitpunkt der Clock geguckt, an dem sie auf 1 umspringt

negative-edge: es wird auf den Zeitpunkt geguckt, an dem die Clock auf 0 zurückspringt, um den sample Wert für den flip flop zu nehmen

D-Flip Flop:
beachte Priorität von Resetwerten in Verilog, ob als erstes Set oder Reset gelesen wird


### Clock simulation in Verilog
```initial  
begin  
clk=1'b0;  
repeat(30)  
#10 clk = ~ clk;  
end
```
bei 30 maliger Wiederholung hat man nur 15 Taktzyklen, da der Code nur die Variable invertiert


### Summary
▪ Flip-flops are powerful storage elements.  
– They can be constructed from gates and latches.  
▪ D flip-flop is simplest and most widely used storage element.  
▪ Multiple flip-flops allow for data storage.  
– The basis of computer memory.  
▪ Combining storage and combinational circuits we can make computing circuits.  
– Sequential circuits

-> Flip flops are used to build static RAM
**Static RAM is fast and expensive, and dynamic RAM is less expensive and slower**. Therefore static RAM is used to create the CPU's speed-sensitive cache, while dynamic RAM forms the larger system RAM space.


