Threat Model 1: System-Level Adversary
Der Angreifer hat system-level Privilegien und kann Linux Kernel Modules laden. Er kann daher die Messungen am Kernel anhand des im Paper beschriebenen Tools durchführen und somit genaue Ergebnisse erzielen. 
Threat Model 2: User-Level Adversary
Der Angreifer besitzt nur noch user-level Privilegien und kann somit keine Messungen mehr am Kernel direkt vornehmen und erhält daher ungenauere Messungen, die aus dem user-space entnommen werden.
Threat Model 3: Remote Adversary
Der Angreifer hat keinen direkten, physikalischen Zugang mehr zum Angriffsziel, sondern baut eine remote session zum anzugreifenden Computer auf, die Attack wird also über ein Netzwerk durchgeführt. Für die Messungen wird ein modifizierter UDP Client verwendet der über IPSec direkt mit der TPM in Verbindung tritt und somit die Messungen weiterhin erfolgreich druchführen kann.


