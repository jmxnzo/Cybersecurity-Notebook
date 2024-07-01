---
tags:
  - LiteratureNote
title: 
author(s): Fabian Buschkowski1 , Georg Land1 , Jan Richter-Brockmann1 , PascalSasdrich1 and Tim Güneysu
year: 
date created: "{{2024}}"
link: 
conference:
---
- tool-assisted, automated Design Space Exploration -> not only efficiency, also security (physical SCAs)
- make a more feasible approach than manually generating hardware implementations -> optimize the development process and enable faster deployment of new crypto
-  the practical realization of these mechanisms(hiding, masking) remains a manual, fragile, and error-prone task, regardless of an expert’s extensive experience in this field


# Common practices Hardware Design
1) Specification: 
		- definition of design goals(constraints area demand, latency etc.)
		- careful consideration of adversary model
2) Functional Design:
		- write HDL code with desired functionality
		- decision taking (top-down, bottom-up approach)
3) Synthesis:
		-  hardware description -> design implementation
 4) Technology Mapping:
		 - map design to target technology (compatibility, efficiency)
5) Place and Route:
		- physical layout is optimized under consideration of timing, power and area factors
6) Verification and Validation:
		- final design is tested against diverse input conditions and the performance is compared to the defined goals 
		-> going back to step 2
7) Deployment



# Nested hardware templates
![[Pasted image 20240618181404.png]]
- fundamental for abstract modeling and performance prediction
- rapid traversal of search space
- extendability and customizability in terms of application-specific algorithm parameters, design-specific configurations
- interface(data transmission) and functionality (data processing)
- hardware security context closely associated-> enables generation of secure designs and performance prediction through additional template media
- allows and promotes cryptoagility and an agile development process in general (instead of static modules) -> dynamic, toll-assisted nature of modern development practices

### Template Settings
1) Algorithm parameter: mainly define the interface and high-level functionality of an instantiated template (immutable and application specific)
2) Template Configurations: are application-independent and mutable under DSE -> they do not affect the external template functionality and interface, but determine how data is processed? (application independent and mutable)
		 -> no impact on the high-level functionality, nor the interface
3) Hardware security context:enables a security-aware design flow, describes the security level of sensitive data processing or control parts within the template (immutable and application specific)



# Design Space Exploration
1) finding designs that meet specific performance requirements
2) selecting designs with optimal performance prediction among all candidates(design space traversal required)




# AES
![[Pasted image 20240618190330.png]]