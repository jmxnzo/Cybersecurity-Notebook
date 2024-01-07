a) Localiza los cinco procesos que más CPU están consumiendo en el
sistema ordenando por cantidad de memoria utilizada en orden inverso.
```Get-Process -Property CPU -Descending | Select-Object - First 5 | Sort-object WS -Descending```


b) Muestra los nombres de los usuarios que están activos en el sistema
y que han iniciado sesión alguna vez.
```get-localuser | Where-Object Enabled| Where-Object LastLogon -gt 0|Select-object Name```

c) Obtén mediante un comando el Fabricante, modelo y número de procesadores lógicos de tu ordenador
```
Get-WmiObject -Class Win32_ComputerSystem | Select-Object
Manufacturer, Model, NumberOfLogicalProcessors
```

d) Obtén el nombre y el número de serie de la BIOS de tu equipo.
```
Get-WmiObject -class win32_bios | Select-Object Name, SerialNumber
```

e) Muestra los 5 últimos eventos del sistema que indiquen un acceso por escritorio remoto
```
Get-WinEvent -LogName Security | Where-Object { $_.Id -eq 1149 -or ($_Id
-eq 4624 -and $_.Message -match "Remote Desktop") } | Select-Object -Last
5
```



### Difference between Get-EventLog and Get-Winevent 
- Get-EventLog works with the classic Windows event logs
- meanwhile Get-WinEvent uses cmdlet , which uses concept of list providers
- performance-wise Get-Event can be faster most of the times using, bc the cmdlet uses the list providers and not the deprecated Win32 API


https://adamtheautomator.com/get-winevent/