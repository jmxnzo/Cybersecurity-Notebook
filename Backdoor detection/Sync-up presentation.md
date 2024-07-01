# Introduction
- a graphical representation of the proliferation and transformation in the past:
	- What can we see?
		- dependencies: 
			- best-case on open-source
			- worst-case on proprietary software or embedded devices in the supply chain of the software project
- reliance on other programs creates the **risk** of having an backdoor inserted into software projects, without even realizing
- ideal world scenario: having a verification process, which ensures backdoor free software
- really limited number of approaches in science and no standardized process of detection -> a lot of work to do, this SoK should be a first step in the right direction

# Idea of structure
- overview: 
	- by using of an existing definition
	- defining detectable attributes of backdoors

# Overview/Definition
- decomposition into 4 elements: input source, trigger, payload, and privileged state
- refer to those components through out the paper


# Attributes of Backdoors
- static data comparison functions, which deeply influence the density of program logic
- hidden functionality -> “cold edges” in CFG
- Localization close to handler and command parsing functionality

# Backdoor detection with a behavioral model
- if we can define the expected behaviour of our software program-> we can use it to detect hidden functionality 
- (Towards Reducing the Attack Surface of Software Backdoors, Felix Schuster) Weasel: only eliminates the trigger, by cutting “cold edges”



# Addressing the Challenge of Undefined behavior
- Stringer-Measuring the Importance of Static Data Comparisons to Detect Backdoors and Undocumented Functionality:
	- focuses on the trigger(static data comparison) and the payload expected to trigger(input source is indirectly determined by input to high scored functions)

- Firmalice-Automatic Detection of Authentication Bypass Vulnerabilities in Binary Firmware: 
	- concentrates on the path from input source(entry point) to the privileged point by backtracing → extract the trigger and find the payload trough constraint solving


# Evaluation
- What are limits and boundaries of those approaches?
- Complications in the detection process: Obfuscation
- discussion for future work