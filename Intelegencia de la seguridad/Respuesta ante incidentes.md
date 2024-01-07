- conjunto de pasos que permite detectar, responder y recuperarse de incidentes



## Equipo informàtico de respuesta a incidentes(IRT o CIRT) 
- personal de seguridad
- miembros de los departamentos legal
- recursos humanos 
- relaciones públicas


- CSIRT(computer security incident response team) significa equipo de respuesta a incidentes de seguridad informática.
- CERT (computer emergency response team) significa equipo de respuesta (o preparación) para emergencias informáticas.
- CIRT (cyber incident response team)puede representar al equipo de respuesta a incidentes informáticos o, con menor frecuencia, al equipo de respuesta a incidentes de ciberseguridad.

## Objetivos
• Asegurar que todos los miembros de la organización conocen y aplican un procedimiento rápido y eficaz para actuar ante cualquier incidente.
• Comunicar de forma correcta los incidentes a quien corresponda tanto dentro como fuera de la empresa.
• Registrar los incidentes con sus pruebas y evidencias con objeto de estudiar su origen y evitar que ocurran en un futuro

### Criterios para crear un plan de respuesta
- simple pero preciso
- roles y responsabilidades detalladas
- reunir equipos tecnicos y no tecnicos
- proporcionar una clasificación 
- saber cual la prioridad de la empresa



## 1) Preparación 
- designar un equipo de repuesta a incidentes 
- identificar los activos críticos para priorizar la respuesta
- definir roles y responsabilidades de cada miembro del equipo
## 2) Detección y notificación 
- establecer sistemas de detección
[[SIEM- System incident event management]] 
[[Intrusion Detection System]]
- monitoreo constante
- notificación de incidentes
## 3) Evaluación y clasificación
-  evaluación  inicial: determinar la naturaleza y el alcance del incidente
- clasificación de incidente: 
	- función de su gravedad 
	- impacto en la organización 
	->Utilizar una escala de clasificación de incidentes
## 4) Contención (Eindämmung)
- aislar el incidente y evitar la propagación
- bloque de acceso
## 5) Investigación y análisis:
- recopilación y preservación de evidencia 
- análisis forense: determinar el origin y la causa raíz del incidente
- identificar las vulnerabilidades explotadas(corregirlas)
## 6) Erradicación y recuperación 
- eliminar el malware y las amenazas 
- recuperación de datos: restaurar los sistemas y datos afectados 
## 7) Notificación y comunicación
- notificación a partes interesadas(los afectados, internas y externas), como clientes socios y reguladores 
- comunicación pública: establecer una estrategia de comunicación pública
## 8) Lecciones aprendidas
- revisión exhaustiva y análisis del incidente para identificar lecciones aprendidas
- actualización del plan de respuesta a incidentes
## 9) Mejora continua
- capacitación y entrenamiento(Ausbildung, Training)
- simulacros y ejercicios para probar la efectividad del plan de respuesta
## 10) Documentación y registros
- documentar todas las acciones durante el proceso
- mantener registros detallados para fines de cumplimiento normativo y análisis posterior


# Buenas prácticas
- recopilar datos utilizando herramientas forenses
- inteligencia externa: 
	- busca en la web información sobre MD5 específicos, direcciones IP y dominios que has descubierto durante la investigación
- Copias de seguridad 
- recopilar registros incluen Eventos de Windows, Proxy, Netflow, Antivirus, Firewall, etc


### Malas prácticas
- Pánico
- Apagar los sistemas
- socializar
- usar credenciales de administrator de dominio
- utilización de herramientas no forenses


## Lista de control
- differentes alcances
	- procesos (PRO)
	- tecnología (TEC)
	- personas (PER)

- puntos clave de la lista de control
	- equipo responsable
	- mejora continua 
	- caducidad(Verfall)del plan de gestión 
	- detección del incidente