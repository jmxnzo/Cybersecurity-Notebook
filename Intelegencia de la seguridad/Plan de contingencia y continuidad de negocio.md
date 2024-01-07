- se compone de 6 fases
- prevenir, protegerse y reaccionar ante incidentes de seguridad
- la recuperación es la capacidad de la compañía para dominar la situación y poner en práctica todas las medidas y protocoles (recovery most important ability, use IMC metrics and measures to ensure continuity)
- doesn't need to encompass all departments or services, bcs different services vary in their needs

## Fase 0. Determinación del alcance.
- Que elementos van a ser el foco de la mejora de la continuidad de nuestra empresa??
	- implicado el personal, los activo de información, los sistemas informáticos, otros servicios y procesos
	- sistemas y procesos de mayor(those that would have the most significant impact on our organization in the event of a loss)
- Dos tipos:
	• El enfoque por activo.
	• El enfoque por proceso.
	-->If we want to create a Bussiness Continuity Plan for Information Technology, more likely to focuss on a process-centric approach
## Fase 1. Análisis de la organización.
- la obtención, elaboración y comprensión de las circunstancias, tecnologías, procesos y recursos de nuestra organización
- Reuniones con los usuarios finales del proceso:
	- las dependencias de proveedores
	- el personal implicado
	- las aplicaciones que se utilicen 
	- datos sobre las necesidades temporales de cada aplicación

### Análisis del impacto
- Business Impact Analysis
	- Conduct a Business Impact Analysis (BIA) based on the information we have gathered
	- temporal and resource requirements of the processes within the scope and, along with Risk Analysis, defines the initiatives to be implemented to recover processes in contingency situations
	- Contingency situations can take various forms, such as natural disasters, cyber-attacks, equipment failures, or other incidents that might disrupt the regular course of business activities.
### BIA: Business Impact Analysis
- **Recovery Time Objective (RTO):** The time it takes to recover a business process after a disruption. It helps define the acceptable downtime for a process.
    
- **Human and Technological Resources Involved:** Identification and assessment of the human and technological resources required for the continuity of the process.
    
- **Maximum Tolerable Downtime (MTD):** The maximum amount of time a process can be disrupted before it causes significant harm to the organization. It sets a limit on how long a process can be down.
    
- **Revised Operating Level (ROL):** The minimum service levels that need to be maintained during the recovery process to meet business requirements.
    
- **Dependencies on Internal Processes or External Suppliers:** Identification and analysis of dependencies on other internal processes or external suppliers that may affect the continuity of the process.
    
- **Dependency on Data Timeliness (Recovery Point Objective - RPO):** Determination of the acceptable amount of data loss in case of a disruption. It sets the point in time to which data must be recovered to ensure continuity.

### Análisis de riesgo
- end-goal of risk analysis
	- What threats could be realized, affecting the processes within the scope,
	- With what probability,
	- What impact they would have on these processes, and
	- What assets of those involved in critical business processes (for example, those with an MTD of less than 24 hours) are at risk.
- Guide:
1. Identify the threats
2. Assess probability and impact
3. Calculate the product of the probability and impact for each threat 
- other methodologies:
	- some take into account variables such as the value of assets, their vulnerabilities
	- best to establish ranges of impact associated with temporal values so that we can relate MTD/RTO to the impact times of a threat

## Fase 2. Determinación de la estrategia de continuidad.
- different assets to protect, thus we need  to determine the most appropriate recovery strategy(or multiple regarding some assets) for each
	- **Personnel:** Based on critical staff identified in the BIA, we must evaluate different options to mitigate their absence.
	- **Locations:** Situations where there is no available workplace must be assessed.
	- **Technology:** For various technologies involved in assets supporting the process, potential operational alternatives or complementary measures should be evaluated.
	- **Information:** All aspects related to the availability and safeguarding of information related to critical processes must be considered.
	- **Suppliers:** It is essential to ensure that critical suppliers have response times aligned with the needs of our company and that we are not exposed to them transferring their possible contingencies.
- strategies should be implemented in a subsequent phase and **we must assess the cost and feasibility of their implementation, maintenance, required resources, etc**

## Fase 3. Respuesta a la contingencia.
1. implementation of the initiatives identified in the prev. phase: 
	- documentation phase of contingency response

2. a phase of classification and prioritization of measures based on the affected process and its criticality
#### Plan de Crisis
- central element in crisis management
- aiming to prevent us from taking bad decision, when a crisis occurs
#### Planes Operativos de recuperación de entornos
- may cover one or more independent environments and contain specific information about the environment to which they apply
- After the activation of different Operational Environment Recovery Plans, each affected infrastructure will begin its recovery process, relying on the ultimate element in the execution of the continuity strategy: technical work procedures.

#### Technical work procedures
- all documentation that describes how we should perform the necessary tasks for the management and recovery of an application, system, infrastructure, or environment
-  Documents that contain a wealth of environment-specific information: IP addresses, program versions, detailed command lists, routing tables, database backup recovery, application startup procedures, etc.



## Fase 4. Prueba, mantenimiento y revisión.
- The purpose of TIC Continuity Plan is to manage unforeseen crisis situations, so:
- it is imperative to keep it updated at all times and regularly verify its validity

#### While testing
- we should run tests on the environments defined in the scope, with different levels of complexity and elaboration, need to be conducted(at least once a year)
	- Technical staff involved in the test
	- Application user involved in the test;
	- External personnel involved in the test: clients, suppliers, etc;
	- Description of the test to be performed;
	- Description of the expected result after the test execution;
	- Time and date of execution;
	- It should be noted that whenever the test may involve a service outage, whether executed successfully or not, it must be scheduled during a low-impact timeframe.
- create a report for unexpected outcomes, exceeded estimated times, poor communication with staff, unavailability of suppliers, etc. Any incident that occurred should be analyzed for the implementation of necessary corrective measures.
#### Plan de mantenimiento
- The purpose is to keep all documentation updated whenever a significant change occurs in the organization
- ensure that documentation we need to use in a crisis situation accurately reflects information:
		- Technical infrastructure,
		- Personnel,
		- External suppliers, and
		- Third parties that need to be considered in a contingency situation.
### Plan de pruebas
- The objective is to outline the various types of contingency tests that need to be conducted.
- This allows:
  - Ensuring that the information in the plan stays updated.
  - Ensuring that, in a contingency situation, the organization can recover within the established timeframes, a crucial aspect that can determine the organization's continuity.
  - Increasing the cohesion of the personnel involved in a potential contingency.
  - Improving user knowledge regarding continuity tests.
  - Boosting users' confidence in the organization.
## Fase 5. Concienciación.
- We must carry out tasks that increase the awareness of personnel regarding continuity.
- This should be done for both personnel involved in business processes and IT personnel.
- We should design an awareness process that includes a description of the elements we use in continuity (business impact analysis, crisis plan, recovery strategies, etc.).
- The target audience in this case should include both technical and business personnel

[[Recuperación ante desastres]]