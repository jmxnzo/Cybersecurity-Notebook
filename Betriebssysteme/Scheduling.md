### Difference Short-Medium-Longterm Scheduling
https://www.geeksforgeeks.org/difference-between-short-term-medium-term-and-long-term-scheduler/


Medium Scheduler regelt nicht wann Prozesse suspended werden, sondern nur das Swapping von suspended Prozessen. 
-> I/=



Beim kooperativen Scheduling ist ein Umschalten des Prozesses prinzipiell immer nur dann möglich, wenn ein Prozess die Kontrolle freiwillig an den Scheduler übergibt. In einer Endlosschleife könnte dies z.B. am Ende jedes Schleifendurchlaufs passieren. Ist dies jedoch nicht explizit vom Programm vorgesehen, dann wird der Prozess für immer die Kontrolle über den Prozessor behalten und ein Wechsel zu einem anderen Prozess ist nicht mehr möglich.  
  
Zum Mehrbenutzerbetrieb: Der Mehrbenutzerbetrieb definiert sich hierüber, dass auf dem System mehrere Benutzer gleichzeitig arbeiten können. Generell ist der Mehrbenutzerbetrieb sowohl bei preemtiven, als auch bei kooperativem Scheduling möglich. Beim kooperativen Scheduling darf allerdings keiner der Benutzer ein Programm starten, dass die Kontrolle nicht mehr abgibt, ansonsten werden die anderen Benutzer für die Laufzeit des entsprechenden Programms aus dem System ausgeschlossen, da ihre Prozesse keine Rechenzeit mehr erhalten.

