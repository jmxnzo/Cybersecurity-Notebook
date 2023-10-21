-  when designing circuits was done by creating the state machine, it often makes sense to describe the state machine for Verilog implementation:
#### Implementation of Final State Machine-Moore Model
```Verilog
module Seqdetector( input x, clk, rst,
output y );
	reg [1:0] state;
	parameter s0=2'b00, s1=2'b01, s2=2'b10, s3=2'b11;
always @(posedge clk)
	if(rst) begin
		state <= s0;
	end
	else begin
		case(state)
			s0 : begin if(x) state <= s1; else state <= s0; end
			s1 : begin if(x) state <= s2; else state <= s0; end
			s2 : begin if(x) state <= s3; else state <= s0; end
			s3 : begin if(x) state <= s3; else state <= s0; end
	endcase
end
	assign y = (state == s3) ? 1'b1 : 1'b0;
endmodule
```



### Assignment 12 2's complement
``` Verilog
module Task1_b(
input x, reset, clk,
output reg y);
 reg state, next_state;
 //create different states as parameter
 parameter s0=1'b0, s1=1'b1;
 always @(posedge clk, posedge reset)
 if (reset) //if reset, than set back to the initial state s0
   state <= s0;
 else
 //else load the next state into state->
 //state gets updated with a blocking assignment, so that the right value can still be calculated for the output y -> y is depending on the present state
   state <= next_state;
always @(state, x) begin
	//first reset the values next_state and y, like initialization
   next_state <= state;
   y <=0;
//switch case statement regarding the different states   
case (state)
s0: if (x) begin next_state <= s1; y <=1'b1; end
s1: begin next_state <= s1; y <= (~x); end
endcase
end
endmodule
```
- [ ] 4 bits signed complement
- [ ] Multiplexer
- [ ] Decoder
- [ ] Encoder
- [ ] Shift modules
- [ ] different counters
- [ ] understand implementation of easy concepts like the above in Verilog
- [ ] **Frequency rate task**


