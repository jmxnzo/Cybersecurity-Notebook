https://www.youtube.com/watch?v=4jdYNO0jhSs
- dual rail logic (like noise cancelling headphones)
- avoid the averaging of different traces(no possible alignment of signals) to filter out the noise and reduce the signal-noise-ratio, by randomizing the power consumption
-> if it's secure random, it's statistically independent of the signal and again it is possible to average it out, so this only reduces the SNR again 
![[Pasted image 20240516123114.png]]


- dual rail logic, using the inverse AES computation to get constant power consumption → manufacturing issues still allow the analysis of the signal (using lots of traces)and thus the make it possible to attack again

→ in case of security and power consumption trade-off this still could be interesting to evaluate