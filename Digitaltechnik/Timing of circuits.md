

# Combinational circuits
- propagation delay = sum(propagation delays of most critical path)
- contamination delay= sum (contamination delays of shortest path)



# Sequential circuits
- propagation delay= amount of time that elapses from the time the clock changes to the time the Q output has changed
	- differentiate between 
		- a low-to-high change in Q: t_plh
		- a high-to-low change in Q: t_phl
- inputs must be stable for a certain amount of time before active clock edge: setup time t_su
- must be stable for a certain amount of time after active clock edge: hold time t_h
-> the clock period has to be long enough for all signals to settle 
![[Pasted image 20230728191321.png]]

![[Pasted image 20230728191334.png]]