[[Synchronisation-03.05.23]]
-Semaphore synchronisation kann zu deadlocks führen, wenn z.B. zwei Resourcen gegenseitig auf ihre sinal() calls warten

### verschiedene Arten von deadlocks
■ deadlock (first variant)  
- passive waiting  
- process state: BLOCKED  
■ livelock (second variant)  
- busy waiting (or „lazy“ busy waiting)  
-  arbitrary process state (including RUNNING), but: no progress!  
-> by comparison, deadlocks are the lesser evil  
-  condition can be identified → prerequisite for „resolution“  
-  extremely high system load due to busy waiting



deadlocks sind nur die circulären Zugriffsabhängigkeiten, jedoch nicht das warten von mehreren Prozessen auf einen Prozess