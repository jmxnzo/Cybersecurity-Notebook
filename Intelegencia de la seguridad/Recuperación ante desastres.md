#### Desastres que las organizaciones pueden planificar
1. **IT Infrastructure Failure:**
    - Application Failure
    - Communication Failure
    - Data Center Disaster
2. **Physical Infrastructure Failure:**
    - Disaster in the Building or Physical Installation
    - Office Disaster
3. **Geographical Scale Failures:**
    - City-wide Disaster
    - Regional Disaster
    - National Disaster
    - Multinational Disaster

## Disaster Recovery Plan
- structured and documented approach that describes how an organization can quickly resume operations after an unplanned incident
- assist an organization in addressing data loss and recovering system functionality
- step-by-step plan(a clear roadmap) consisting of precautions to minimize the effect of a disaster
- before an organizations has to conduct a Business Impact Analysis and a Risk Analysis, which serve RTO and RPO
- Goal: 
	- reduce downtime and minimize financial and reputational damage
	- ensure compliance with all regulatory requirements

### Considerations 
- a DRP should start at the business level and determine which applications are most critical 
- **Recovery Time Objective (RTO):** The RTO goal describes the targeted amount of time a business application can be inactive, usually measured in hours, minutes, or seconds.
    
- **Recovery Point Objective (RPO):** The RPO goal describes the age of files that must be recovered from backup storage to resume normal operations

- In developing a recovery strategy:
	- Budget
	- Insurance coverage
	- Resources - both personnel and physical facilities
	- Management's stance on risks
	- Technology
	- Data
	- Suppliers
	- Compliance requirements

	
### Types of Disaster Recovery Plans
- Disaster Recovery Plans (DRPs) can be tailored specifically to a particular environment. Some specific environmental plans include:

#### Virtualized Disaster Recovery Plan
- provides opportunities to implement the recovery in a more efficient and straightforward manner
- chance to spin up new instances of VMs, providing application recovery along with high availabilty
- testing gets easier as well: validate that RPO and RTO are accomplished
#### Network Disaster Recovery Plan
- gets more complicated with increasing network complexity
- specific to network, such as its performance and network personnel
#### Cloud Disaster Recovery Plan
- backups or replication of data
- can be more expensive in terms of space, time and costs
- administrator has to be aware of the location of virtual and physical servers
- plan as well should address security as a known problem in the cloud
#### Data Center Disaster Recovery Plan
- focuses on the facilities and infrastructure of a data center
- risk assessment is key element
- analyze key components such as building location, power and protection systems, security, and office space (address wide range of potential scenarios)


## Checklist verification of DRP
A DRP checklist should include the following steps:

- Establish the scope or extent of necessary treatment and activity - the scope of recovery.
- Gather relevant network infrastructure documents.
- Identify the most severe threats and vulnerabilities and the most critical assets.
- Review the history of incidents and unplanned outages and how they were handled.
- Identify current disaster recovery strategies.
- Identify the incident response team.
- Have management review and approve the DRP.
- Test the plan.
- Update the plan.
- Implement a DRP audit.

####  Template 
- An organization can start its DRP with a summary of vital action steps and a list of important contacts, making essential information easily accessible.
- The plan should define the roles and responsibilities of disaster recovery team members and outline the criteria for initiating the plan.
-  Subsequently, the plan should specify, in detail, the incident response and recovery activities.


1. **Statement of Intentions and Disaster Recovery Policy:**
   - Clearly articulate the intentions and policies guiding the disaster recovery efforts.

2. **Set Goals:**
   - Define the goals and objectives of the disaster recovery plan.

3. **Authentication Tools, Such as Passwords:**
   - Specify authentication tools, such as password policies.

4. **Risks and Geographical Factors:**
   - Identify risks and geographical factors that could impact recovery efforts.

5. **Tips for Dealing with the Media:**
   - Provide guidance on how to interact with the media during and after a disaster.

6. **Financial and Legal Information and Action Steps:**
   - Include financial and legal information along with actionable steps in case of a disaster.

7. **Plan History:**
   - Maintain a record of the plan's history, documenting changes, updates, and lessons learned from previous incidents.



# Key steps on how to implement a working desaster recovery plan
• Step 1. Main Objectives: 
The first step is to outline the main objectives of a disaster recovery plan in general terms.
• Step 2. Personnel: 
Record your data processing personnel. Include a copy of the organizational chart with the plan.
• Step 3. Application Profile: List applications, indicate if they are essential, and specify if they are fixed assets.
• Step 4. Inventory Profile: List the manufacturer, model, serial number, cost, and ownership status (owned or leased) for each item.
• Step 5. Information Services Backup Procedures: Include information such as "Record receivers are switched to ________ and at ________." And: "Modified items in the following libraries and directories are saved in ____."

• Step 6. Disaster Recovery Procedures:
   - Emergency Response Procedures to document the appropriate emergency response to a fire, natural disaster, or any other activity to protect lives and limit damage.
   - Backup Operations Procedures to ensure that essential data processing tasks can be performed after a disruption.
   - Recovery Action Procedures to facilitate the rapid restoration of a data processing system after a disaster.
• Step 7. DR Plan for the Mobile Site: The plan should include a mobile site configuration plan, a disaster communication plan (including wiring diagrams), and an electrical service diagram.
• Step 8. DR for the Active Site: An alternative active site plan should provide a backup site. The alternative site has a temporary use backup system, which is used while the primary site is being restored.
• Step 9. Restore the Entire System: To return your system to its pre-disaster state, use recovery procedures following a complete system loss in "System Management: Backup and Recovery."
• Step 10. Reconstruction Process: The management team must assess the damage and begin the reconstruction of a new data center.
• Step 11. Testing the Disaster Recovery and Recovery Plan: In proper contingency planning, it is important to regularly test and evaluate the disaster recovery plan.
• Step 12. Disaster Site Reconstruction: This step should include a data center floor plan, current hardware needs and alternatives, as well as data center square footage, power requirements, and security requirements.
• Step 13. Record Changes in the Plan: Keep your disaster recovery plan up to date. Maintain records of changes in configuration, applications, schedules, and backup procedures.

#### Communication plan
- internal communication: 
	- alerts send via email, building location systems, voice messages, or text to mobile devices
- external communication: 
	- even more essential
	- how to inform update key customers and stakeholders about disaster status 
	- how to discuss disaster with media



# Difference between an Incident Management Plan and a DRP

- An Incident Management Plan focuses on protecting confidential data during an event and outlines the scope of actions to be taken during the incident. This includes specifying the functions and responsibilities of the incident response team.
- On the other hand, a DRP focuses on defining recovery objectives and the steps that need to be taken for the organization to return to operational status after an incident occurs.



• UNE 71505 1:2013, UNE 71505 2:2013 y UNE 71505 3:2013.
• Sistema de Gestión de Evidencias Electrónicas (SGEE)
• ISO 27037
• RFC 3227
• UNE 71506:2013.
• Metodología para el análisis forense de las evidencias electrónicas.
• UNE EN ISO/IEC 27037:2016.
• Técnicas de seguridad. Directrices para la identificación, recogida,
adquisición y preservación de evidencias electrónicas (ISO/IEC
27037:2012)
• UNE EN ISO/IEC 27006:2020.
• Técnicas de seguridad. Requisitos para organismos que realizan
auditorías y certificación de sistemas de gestión de seguridad de la
información (ISO/IEC 27006:2015, incluyendo Amd 1:2020)