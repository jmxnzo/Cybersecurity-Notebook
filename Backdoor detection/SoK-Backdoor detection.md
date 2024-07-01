

We should differentiate between two situations regarding the knowledge of the wanted behaviour of our software project. The strongest results at backdoor detection depend on, how accurate can we define the expected behaviour of our code. 


Looking back in the past years, we can observe a huge, growing gap between the evolvement of backdoors in software projects and the mechanism to detect those. This primarly underlies the reason of the diversity of backdoor implementations. Looking at existing backdoor implementation, we can basically find endless possibilities of how a backdoor can be introduced into software. On the other hand, most backdoors are exactly designed just for the specific software project, by that even existing detection tools could be used by the attacker to minimize the detection of the backdoor.



This paper is aiming to not rely on good fortune of the software ecosystem, rather then systematizing and evaluating the question of existing backdoor detection tools, by categorizing different approach ideas and evaluating their scope of detection. Mainly we focus on the detection of backdoors using different variations of control flow graphs. Also 

Because of the diversity of different programming languages, we mainly focus on the backdoor detection in C. Thus this still covers a lot of diverse software backdoors, e.g.  on embedded devices, user-space binaries and challenge-response protocols. Because most of the approaches focus on a method of decompilation of binaries to an intermediate language the work presented in this paper can be easily used for any other binary programming language. As well the intermediate representation can directly be generated from the source code, if it's publicly available. 

- only based on static analisis -> no dynamic approaches like network activity detection, as well no machine-learning, but still the different techniques of static detection can be used as a datset for machine learning algorithms
## Related work
- missing points in the evaluation of Backdoor Definition Deniability paper and the need for a more detailed evaluation
- difference in details
## Nomenclature  
The definition initially was based on finite state-machines, but it is important to point out, the interchangeability of control flow graphs and finite state machines, as the description of the behavior of a system. When refering to system, Sam L Thomas using it as a term to describe the highest level of abstraction required to model a given backdoor within a platform. Because we shift our focus to application backdoors, the system describes the program under testing in our case. To illustrate the systems behaviour and the two existing perspectives of developer and end-level user(general consumer, security consulting, program analyst) on the behaviour, Sam L Thomas introduces 4 different types of finite-state machines. Each describing a certain foundation of knowledge about the system, to allow arguing about the deniability and the intention of backdoor constructs.
	- DFSM -> developers view
	- AFSM-> real manifestation of the system
	- EFSM-> expected system by end-users
	- RFSM -> reverse-engineering the actual system
Understanding multiple ways of illustrating the behaviour of a program, we can change the finite-state machine to a control-flow graph, which composes the same amount of information as the finite-state machine. So we end up having those categories:
	- DCFG -> developers view
	- ACFG-> real manifestation of the system
	- ECFG-> expected system by end-users
	- RCFG -> reverse-engineering the actual system
Even though it's just a side interest in case of this paper, this allows us to still make use of the examination of intentions and reason about the consequences of deniability, proposed by the approach of Thomas, when using different representations of the system (program) behavior. 
## Definition
>[!definition] Backdoor 
An intentional construct contained within a system that serves to compromise its expected security by facilitating access to otherwise privileged functionality or information. Its implementation is identifiable by its decomposition into four components: input source, trigger, payload, and privileged state, and the intention of that implementation is reflected in its complete or partial (e.g., in the case of bug-based backdoors) presence within the DFSM and AFSM, but not the EFSM of the system containing it.

Observing the diversity of real-world backdoors in the past years and the underlying software diversity, it doesn't seem to be up-to-date to still categorize backdoors a few categories. Further it limits the scope of backdoor detection to these defined categories. Rather we need to start from the general definition of backdoors and look into different ways of creation, than limiting our chances of detecting by searching for hard-coded patterns and relying on known backdoor constructs.

This definition of backdoors uses a really abstract level of what the construct backdoor embodies every time by including all the component parts, that can be found in such constructions and thus doesn't limit our scope of detectable backdoors by categorizing the diverse software backdoors, we are facing today. 
 Looking into approaches of categorizing backdoors in the past years, (like [Wyaposal]) you can notice that defining such categories ends up shifting the towards searching for special static patterns, which only focus on the characteristics itself . In this overview, i'm aiming to start of using the abstract definition of backdoors, but still provide information about implementations of backdoors by specifying deeper, how the different components can look like. This abstract definition acts as the fundament for detecting a wide range of backdoors and further automating the detection process. Additionally serves as a framework to understand the focus and goals of different detection processes and allows us to evaluate missing considerations in different approaches. 

Abstracting the entire underlying system of the backdoor, we can assume that the origin of every backdoor definitely lies in hidden functionality introduced to the software project. Even if no exclusive program parts are added to the project, there unavoidable has to be introduced some prior unknown functionality to achieve the wanted behavior of the backdoor. 

ToDo: rewrite the hidden functionality part
##### Input source
The input source is a component needed to account for the satisfaction of the trigger condition. To achieve the conditional branching of the trigger itself, the system at least has to compare some user input. Those inputs can be injected at different entry points of the program. So generally every possible source of user input in the program can fulfill this purpose. 



Learning from most of the implemented backdoors in software projects, the most practicable  input sources are authentication handlers and command parsing structures. In both cases of these input sources the normal control flow doesn't differ a lot from the bypass mechanism used for a backdoor, which makes it a suitable location for the entry point of a backdoor. 
Many server applications written in C/C++ utilize central data structures, such as arrays, to store command descriptors and their associated handler function pointers. Researchers have created an analysis module that dynamically scans a server application's memory for pointers linked to previously identified handler functions. When the memory spacing between several identified handler function pointers is consistent, they deduce the existence of a command descriptor table (compare [25, 31]). Following this, they heuristically ascertain the table's boundaries. Once this table is detected, they can search for pointers to unrecognized command handlers, thus uncovering undocumented commands.


##### Trigger
The trigger mechanism is a pivotal component of our abstract model of a backdoor. It describes the location, where the backdoor leaves the common execution paths and follows an exclusive execution path. The trigger and payload components are closely related. It's essential to understand that the trigger marks the initial deviation from the normal execution path, transitioning into the payload phase. Due to this first step of deviation, the trigger presents a significant opportunity to detect the backdoor mechanism. In most cases the trigger functionality is implemented by a static data comparison function. These static data comparisons can be established against different elements of static data, e.g. ASCII-texts, password, hashes, public keys or system time.

[Maybe include payload static data comparison aw]
##### Payload
To reach the final, privileged state of the  backdoor, an intermediate component is required, which describes the transition from the normal system state upon satisfaction of the backdoor trigger to the privileged state. We are going to refer to this component as payload in this work.  The state transitions of the payload phase can be mentally modeled as the solution to puzzle on how to reach the privileged state from successfully satisfying the conditions of a backdoor trigger.


##### Privileged state
When the backdoor is activated, an eventual system state is reached that can be considered the backdoor-activated state. This state represents a state of escalated privileges, privilege abuse or unauthenticated access. We are going to refer to this state as privileged state.





Starting from a top level overview on backdoor detection, there are different properties of the underlying source code, which seem to be typical for a variety of real-world backdoors.  
Wyaposal differentiates between 4  categories of techniques for backdoor detection in his manual, static analysis approach of source code [[Static Detection of Application Backdoors]] :
 - Special credentials backdoor, hidden functionality, unintended network activity and manipulation of security-critical parameters
Including the envolvement of backdoors in the past, these detection techniques don't really suite the picture of static backdoor detection nowadays. The technique of unintended network activity definetely has it's importance, but detecting and disabling unwanted network traffic dynamically has developed a lot over the years. So the static examination would just be a huge overhead.  

Regarding the picture of today there is a need to revise those categories. Focussing on the possibilities of static analysis possibilities, there are three main properties of backdoors, which should be used for the successful detection, including static analysis on source code or on binary level:
- More of an explanation, why the properties rather then a property itself: A backdoor reaches a privileged program point by bypassing authentication functions
- Static data comparison functions, which deeply influence the density of program logic
- Hidden functionality -> "cold edges"
- Localization close to handler and command parsing functionality / Similarity regarding influence of control flow changes [[Stringer-Measuring the Importance of Static Data Comparisons to Detect Backdoors and Undocumented Functionality]]
	-> the localization can still be fulfilled even with low-level knowledge of the expected behaviour
	
-> these two are really close connected to each other, bcs handler follows a static comparison function(decider) to handle the decision of the conditional statements 


From expected behaviour and real-world behaviour to detection  of backdoor


# What to do if we can define the wanted behaviour of our software project?
- case if we want to detect backdoors, injected by other contributors into the own software project or the reliance on other open-source projects

Starting from the point of view, we're we have a complete definition of the behavioral model of our program. This is in the case of open-source software projects, where we can fully extract a behavioral model out of the source code and for own software projects. If the expected behavior can be represented through an abstract structure, like the control flow graph or a finite state machine, then hidden functionality can easily be detected by forming the relative complements of the actual behavior and the expected behavior. This relative complement is nothing less then the hidden functionality.
### Dynamic analysis using control flow graphs (prior knowledge)


#### Behavioral Model extraction:
To record the runtime traces of our program, the Weasel tool uses a dynamic analysis approach, falling back to defined protocols to fulfill  the required interaction with the program under testing. To define the expected behavioral model of certain code parts, they introduced a protocol player, which takes in account a protocol description and is able to compile them to scripts, which are solely build of the atoms PUSH DATA, SEND, RECV and WAIT, and the virtual atoms START RECORDING and STOP RECORDING. The last two are automatically inserted by the
protocol compiler before and after the atoms of interest.
When the protocol processor encounters one of them while
playing the protocol, it activates/deactivates the tracer. By that the Weasel tool allows, that as little noise can be found in the recorded traces. Looking into the example of a program authentication, the prior work which is required to spot hidden functionality, is defining each of the different authentication methods as one protocol run description. These defined protocol run descriptions allow the recording of runtime traces of our expected behavior and by that allow the detection of hidden functionality, which was not included in our defined protocol descriptions, i.e. exclusive execution paths.





The two classes of backdoors are divided into four distinct subparts:

- Authentication validation code
- Specific authentication validation result handling code
- Command parsing code
- Specific command handling code

Each authentication mechanism is designed to determine whether a third party has sufficiently proven its identity to gain legitimate elevation of privilege. Similarly, during command dispatching, different operations are executed based on various commands and their arguments.



In order to behave differently for different inputs, a server application in general needs at one point during runtime to leave
the common execution path and follow an exclusive execution path accordingly.

We begin by capturing runtime traces for various inputs and identifying both common execution paths and those exclusive to specific input groups.
The subsequent stage involves identifying deciders and handlers at either the function or basic block level.
In authentication processes, deciders conduct the actual validation of authentication, while handlers manage the resulting validation outcomes.
For command dispatching processes, deciders are responsible for parsing and dispatching commands, while handlers implement the specific functionalities associated with each command.



#### Localization corresponding with handler and command parsing functionality


The paper [[Towards reducing the attack surface of software backdoors]] illustrates a noval approach to eliminate backdoor, especially aiming for protocol based binaries. The approach follows the idea, that in order to behave differently for special inputs, as in case of a backdoor, the application needs to leave the common execution path at one point and hence follow an exclusive execution path. Looking at the prior definition of a backdoor, this claim is generally true. But finding these common execution path already requires a decent level of how the program behaves, e.g. looking at a protocol we need to know about different authentication methods. These are then defined in different protocol runs. 





# What does Weasel really do?
### The A-WEASEL Algorithm



### The A-WEASEL Algorithm

All tracing, both at the functional and basic block level, in the A-WEASEL algorithm is conducted using gdb. This ensures that the tool can be utilized for any binary running on a platform where gdb can be installed and executed. To automate the tracing process, the protocol player mentioned earlier is employed.

The algorithm starts by determining the set of common functions by identifying the intersection of functions present in all traces. The set of exclusive functions is identified by computing the relative complement of a trace \( T_i \) and the set of common functions. Each exclusive function in the set \( S_{T_i} \) of a protocol run is transformed to facilitate the identification of deciders later on. For each exclusive function, the minimum number of call stack levels is determined, and the signature call stack of each invocation is extracted. Subsequently, top-level invocations of exclusive functions are filtered out by excluding those dominated by other exclusive functions in the call stack.

Next, the remaining filtered sets of exclusive functions are grouped according to shared invocations in the call stack. Each group corresponds to one specific exclusive function and can contain at most one specific invocation from each trace.

The immediate parent function in the common call stack of a group’s exclusive function is necessarily in the set of common functions and is thus added as a decider to the decision tree. For each decider function, the basic block level is dynamically traced using gdb. A-WEASEL is then recursively executed on the sub-traces (sub-CGs) of the decider identified for the group across all applicable traces.

If a group consists of only a single invocation from a single trace, the corresponding exclusive function is added as a handler to the decision tree, ending the recursion for that group.

If a decider function is found to be a leaf and does not exhibit any control flow differences, it is transformed into a common handler function.



Static data comparison -> ends in conditional branching and then follows an exclusive execution paths, bcs those of a backdoor wouldn't be included in the traces, they are defined as "cold edges" and cut out (only if we can predefine the different protocol runs, if not it leads to a lot of false positives)


Hidden functionality without any conditional branching for example in command parsing structures , would be scored high because of suspicious code parts and thus be detectable as well

Alpha-Diff-cross version binary code similarity -> after securing the functionality of our code is secured by our defined models, cross version binary code similarity can detect if changes were introduced, which have a big impact on the binary code 

## Detection based on Collaboration Graphs
A noval approach, recently given by Tom Ganz et al. notices the difficulties of searching for concealed functionality in source code or binary analysis and proposes the manifestation of backdoors in unusual commit messages, code location, even development times etc. This orthogonal strategy for detection introduces new heuristics in the field of backdoor detection and takes the detection to a even more abstracted view of software, by just analyzing the collaboration graphs of repositories. 


# Collaboration Graph(node and edge features)
In general every collaboration graph G(V,E) is composed of nodes V and direct edges E. Adding up to the existing representation of Git, were primarily node types of the type commits exist, they introduce the following node types for more comprehensive information: branches, files, developers, methods. To enrich the collaboration graph even more, they add different attributes of nodes and edges: 
### Node attributes
- developer node: statistical information about her behavior(overall number of commits and projects, number of merge and non-merge commits), the account age, name, email, location
- commit node: additional commit information(commit message, timestamp,  merge type, signed or unsigned)
	- code-derived metrics from the DDM model: unit value of interfacing property, the size property and the complexity property
- File node: 
	- Attach name and mime-type
	- numbers of past and present methods 
	- lines of code 
-  Method node:
	- parent file name and method name

### Edge attributes
- commit timestamp to the edges pointing to the descendant file and method nodes
- type of file update (modified, created or deleted)
- fan-in and fan-out degree of the method
- start and end lines 
- token count and cyclomatic complexity (file to method nodes)


So we end up having a really comprehensive structure, composing all the important information of the development process of our software repository. To detect the anomalies, the paper utilizes graph neural networks(GNNs) with convolutional layers. Because of my limited knowledge in the field of machine learning, i'm not going to dive into deep details right here and refer to the original paper, in case you don't want to miss out on that.


GNNs are trying to solve learning tasks on graphs by exploiting therelations of nodes and edges in different proximity. To do so we define convolutional layers, that capture the graph. First we consider a one vector space of dimension d for each node and one of dimension k for each edge. Now each layer of the convolutional network aggregates information from neighboring nodes to update the node representations. The core mechanism of the convolutional layer consists of a message passing algorithm, using 3 learnable differentiable functions. Firstly, the message function generates messages for each node by considering the features of the node itself and its neighboring nodes. Secondly, the aggregation function aggregates the messages received from the neighboring nodes. Finally, the update function updates the node's features based on the aggregated information, ensuring that each node’s representation is enriched with information from its context within the graph.




The GVAE uses the embeddings generated by the GNN to learn a low-dimensional latent representation of the graph. It consists of two main components: the encoder and the decoder. The encoder takes the d-dimensional node vectors and k-dimensional edge vectors produced by the GNN and maps them into a latent space. This latent space is designed to capture the essential characteristics and structure of the graph in a compact form. By doing so, the encoder effectively reduces the dimensionality of the input data while preserving its most important features. The decoder's role is to reconstruct the original graph from the latent representation. This reconstruction ensures that the latent space accurately reflects the original graph's structure and features. During training, the GVAE minimizes the reconstruction loss, which measures how well the decoder can reproduce the input graph from the latent vectors.

The Deep Support Vector Data Description (SVDD) consists of two subphases. First The GVAE is trained on a diverse set of collaboration graphs to learn the optimal embeddings using one-class learning. To enhance anomaly detection, the model can be extended to semi-supervised learning by incorporating a few labeled anomalies. This involves adjusting the objective function to balance the influence of labeled and unlabeled data, guiding the model to better distinguish between normal and anomalous nodes. 

Once the GVAE is trained, it generates accurate embeddings into latent space for new collaboration graphs. The weights of the trained AE are then used to initialize the weights W of a neural network phii. These embeddings are used for anomaly detection through the Deep Support Vector Data Description (Deep SVDD) method.  A center \(c\) is defined in the latent space as the mean of the embeddings obtained from the AE. The anomaly scores are then calculated by measuring the distance between each node’s embedding and the center \(c\). Nodes with embeddings that are far from the center are flagged as anomalies.




# What to do if we can <u>not</u> define the wanted behaviour of our software project? 
- this is the case if our software project relies on some third-party project, which is not open-source or embedded firmware, which is used in the supply chain
- similarity to binary reversing
- Goal: creating the control flow graph of the binary

In case our software depends on some third-party, which keeps the source code to themselves, it gets really hard to even define a model of expected behaviour, because there is close to no chance to identify all special cases of the software behaviour. Thus we need to focus on ideas, which will facilitate the manual static analysis of the provided binaries, to ensure that our software doesn't include any backdoors introduced by the dependency. 

Starting from only having the binary, it simplifies the process afterwards a lot if we decompile the binary code to an intermediate language. Like in the Springer paper, we can make use of our already advanced manual static analisis tools and use the intermediate language Ghidra IL as a bases to fulfill our further analisis.

Now we are going to take a look at two different approaches.

#### Bypassing authentication functions to a privileged point 
The first one is concentrating on the more general property of backdoors. Even though we cannot define the entire behaviour of the binary under analysis, we can still extract different privileged points in the application, which our software project depends on. In the Firmalice paper is based on the assumption that all paths leading from an entry point of the software to a privileged operation must validate some input that the attacker cannot derive from the binary itself or from prior communication to the binary. Keeping that assumption in mind, we can create a PDG out of a CFG and tracing back each authentication slice leading to a privileged point.
![[Pasted image 20240610115405.png]]

##### 1) Creating the program-level CFG 
- We start to create a CFG of context-sensitivity 2 by starting from each of the entry points of the binary and recursively explore both directions of every conditional branch, using forced execution. As well a Symbolic execution module is used to support computed and indirect jumps(including jump tables)
- The different contexts are illustrated as nodes and control flow transfers as edges.

##### 2) Creating Programm dependency graph
The program dependency graph(PDG), we are aiming for, consists of a CDG and a DDP. A CDG represents, for each statement X (generally, a binary instruction, but in our case, an IR statement), which other statements Y determine whether X is executed. While the DDG shows how instructions correlate with each other with respect to the production and consumption of data.

##### 3) Backward Slicing
Now starting from a given privileged program point going backwards, we can produce every statement on which that point depends. We end up creating each authentication slice respectively.

##### 4) Symbolic execution engine
Now we can run a symbolic execution engine on each authentication slice. The symbolic state in this case would store the values contained in memory(e.g. variables), registers, status open-files etc. It keeps track of the different constraints on these values in a set of path constraints. As well the set of path constraints includes output routines as constraint. For example any data D, that is exposed in an output routine, is added as a constraint D\==C to the constraint set. Adding this constraint has an effect on concretising existing symbolic variables (for example, if a symbolic
variable E previously existed with a constraint E == D,
then the constraint D == C also implies E == C). This ensures that any loss of secrecy of variables (e.g., leaking a password hash) is detectable within this approach.

##### 5) Constraint Resolving
After collecting the sets of path constraints, the last step comprise the concretizing of the inputs. A properly-authenticated path contains inputs that
concretize to a large set of values (because the underlying
passwords that they are compared against are unknown, and
thus, unconstrained). If we achieve to concretize the input into a limited set of values, it signifies that an attacker can determine an input that allows them to authenticate. 
## Static data comparison functions
In other approaches like Stringer- Measuring the Importance of static data comparison functions, the focus is directly shifted to the static data comparison function itself. Again beginning with our CFG in Ghidra IL, we follow along the question, which functions contain a relatively high density of decision logic that depends on successful return of static data comparison functions. The end goal in mind, is to construct a function-level CFG based on static data comparisons, which can then be used for further transformation and scoring of the density of decision logic.


-> handler or parsing functionality are scored the highest
#### Identification of static data comparison functions
1) Argument references (pointer or direct reference to read-only memory or the initialized data section)
2) Function Arity(comparison function should at least take two arguments)
3) Branching properties(result of a call to a data comparison function should influence a branching condition) 
4) Local call frequency(processing routines generally utilize the same static comparison function multiple times)
5) Data properties (in section_data or section_rodata, no format strings, no unusual white-space use)



##### Function-level CFG
 Using the heuristics for scoring gives us, the opportunity to detect static data comparison functions in binaries, even if the developers of proprietary software stripped the binary and no symbolic search is possible. After extracting each static comparison function, we can use the CFG of GIL instructions for the scoring each basic block respectively.
 
 We first construct sets of static data sequences at each basic block within the CFG, this is achieved by labeling each branching basic block and mapping it to the computed static data sequence set. To determine the static data sequence set, we iterate over the predecessors of the basic block and add the static data comparison to the current static sequence data set, if the basic block follows on a true conditional branch. Independently of the branching, we form the union of the (updated) data sequence set of the currently scanned predecessor and the already found data sequence sets by other predecessors of the basic blocks.
 
 The static data sequence set of a branching block is computed by adding the branching condition to the    The none branching basic blocks are mapped to the union of their predecessor basic blocks.
 
 ((Graphical representation))
In the second step we can run trough each branching basic block and score each of them, based on different heuristics:
1) a mapping of static data to the number of times the element of static data s occurs within the sequences within the set of static data sequences ->
![[Screenshot from 2024-05-27 20-34-45.png]]
		-> identifies the reachability of a given block depending on the
	
2) the functionality of a basic block computes to the number of lifted (BIL) instructions w(b) (scaling factor)![[Screenshot from 2024-05-27 20-19-42.png]]
3) 
	- scaling factor:
	![[Screenshot from 2024-05-27 20-17-30.png]]
	inverse number of incident edges 
![[Screenshot from 2024-05-27 20-32-22.png]]
---> function score is the sum of all block level scores, so we can determine where decision logic is largely influenced by static data


Those static data sequence sets allow us to determine the "guards" of functionality and bypassing the problem of scoring static data comparison functions in early stages within the CFG with an significantly higher score.


### Algorithm for scoring importance of code




# Combining both of them


# Detection using Collaboration graphs











# Problems to face 
## Results
In the evaluation part we are primarily focusing on two leading questions. How do the different approaches take in account the different components of our abstract backdoor definition? Which categories or types of payloads of payloads are detectable by these approaches? 
This allows us to find missing considerations in approaches regarding the abstract definition of a backdoor and point out the efficiency and scope of each approach. Furthermore we are interest into the complement of not-detectable payload constructions, which creates a summary of we to aim for in future work.
 Deciders and handlers are automatically detected in the CFG by Weasel, which allows us to eliminate exclusive functionality, which was not used in the different protocol runs. By that we can disable the trigger, but only if it exist as an explicit transition leaving the common execution path at a decider function. Even if the following payload parts include non-explicit changes, the explicit trigger will be detected by the Weasel tool. The Weasel tool doesn't consider different possibilities of input sources, because the protocol player is only concentrating on the standard input routine.  As well the tool doesn't define any form of privileged state in the program under testing. Nonetheless this doesn't really influence the detection possibilities of the approach, because independently of which input source and privileged state deciders and handlers branching of the common execution path can be detected.  Threrefore the Weasel tool strongly relies on a comprehensive definition of a behavioral model using the protocol run descriptions. By knowing the expected CFG, we can cut overhead functionality without reasoning about the input source and privileged state and still deactivate trigger to the backdoor.

The Stringer approach should be seen as a helping tool for binary analyst and can not fully detect or even disable any backdoor. It just uses the scoring of functions consisting of a high density of logic based on a returning conditional branch. These functions can also be normal authentication handlers or command parsing routines inside of our project. But by scoring potentially suspicious code parts high, Stringer leverages the ability for a binary analyst to shift their focus directly into interesting program parts. As the trigger and payload parts often are build using static data comparison function, we can say that the Stringer approach similarly to Weasel concentrates on spotting the trigger and payload phase in a backdoor without regarding input sources and privileged states. Taking the privileged state into account when scoring the functions, would be a good feature to add to the Stringer tool. The missing components can then be determined by the analyst manually post-analysis after finding suspicious static data comparisons


The Firmalice does take the considerations of input source and privileged state into account and focuses on the bypass of authentication through defining an entry point of the program and different privileged states. By constraint resolving the different, found authentication slices are examined further to determine the input values for trigger and payload. In this case it is really important that the trigger and payload are fully explicit, because otherways they would not be traceable and not included in the CFG. Thus the limitation right here is, that there are no non-explicit elements contained in the backdoor.
Even if Firmalice does consider the input source and piriveleged state it limits the approach in a certain way. Privileged states, which might be reachable and interesting for a backdoor, really need to be defined in the security policy of the Firmalice tool. This complication is additionally revealed in the notion of payload states. The Firmalice tool doesn't consider any difference between trigger and payload. So when a payload state is entered it might leave a program in a pre-privileged state, which won't be caught by the security policy. If not backdoors leading to these program  points of certain privliges can not be detected by the tool. The same does count for input sources. The entry points defined in security policies are more of a limitation then a good example of following the definition. Determining the right entry points as the input source of the backdoor, ends up for the same amount of work then manually detecting the backdoor right away. In conclusion even taking the two components into account, ends up violating the detection of backdoors. So it is really important to not overdefine different components of the backdoor and keep an abstract level of specification for extending the detection to a broader scope.


Starting with 
Coming back to the categories of payloads we defined earlier and evaluating the scope of different detection methods. Looking into payloads which get triggered by an explicit transition, so they are already existing parts of a binary file, they are already a few proposed detection methods, that have certain abilities to detect or disable backdoor triggers right away. The Weasel Tool, proposed by Felix Schuster recursively determines different deciders and handlers in the CFG of our program. After recording all the traces, it does the comparison based on signature call stacks. If a explicit trigger is introduced into some authentication or command parsing routine, the tool will detect the backdoor by running different analysis modules. Primarily it succeeds if the trigger is implemented a exclusive function invocations, because the deciders can be extracted on functional level. Even if it comes to non-explicit payload parts after using the explicit trigger, the tool serves the chance to disable the backdoor functionality, by cutting the "cold" edges of the control flow and implicitly deactivating non-explicit states or transitions.  But through added detection functionality like Differential return Value analysis or the C structure determination, it also server a great starting point for detecting triggers combining classes C2 and C3.  

For the Stringer tool it provides important new heuristics to scoring functions, which might hide functionality. Still this tool doesn't allow to automatically detect backdoors and serves as a helping hand for program analyst to search at the right spots. If it comes to fully explicit trigger and payload, the Stringer tool has it's potential in alarming the analyst about suspicious functionality. Because the explicit trigger most of the times exists as some form of static data comparison function, the Stringer tool will detect the trigger and allow the analyst for further examination. If it comes to non-explicit states and transitions, which are exploited in the backdoor construct, the Stringer tool has really low chance to detect those, just because these transitions and states won't be found in the CFG and by that are ignored in scoring the logical density of functions.


Similarly the Firmalice tool only detects fully explicit triggers and payloads. Because the CFG is created as part of static analysis and then backtraced starting from the privileged point, if reduces the ability of detection to only explicit states and transitions as non-explicit can't be found in the CFG. Summing up, it cristalizes, that the abilities of static and dynamic automated binary analyses rely on the explicit code constructions of backdoor constructs. On the other hand, there are no existing detection tools and approaches to detect the exploitation of non-explicit states and transitions during a backdoor. This underlines, the huge gap between attackers and detection abilities in this field of science and creates the need of noval detection methods. 
We analyzed deeper the orthogonal approach of Detection using collaboration graphs, which creates a huge possibility to detect anomalous code commits into software repositories right away. Changing the heuristics of detection away from static and dynamic binary analysis to some more abstract view on the problem, allows us to circumvent the gap of our detection abilities and create new challenges for the attackers in the build process of backdoors. Still this approach can not rule out the presence of software backdoors, it provides an alternative detection strategy, that complements existing ones. Choosing a lot of different detection methods and combining them, just like in existing field of virus detection, increases the chances of detecting the injection of a backdoor into our software projects. Using orthogonal and broader approaches of detection can be seen as the key of backdoor detection and the only solution to face the diversity of our software ecosystem today.