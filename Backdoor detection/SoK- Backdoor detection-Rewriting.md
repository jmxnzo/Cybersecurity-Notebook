The proliferation of open-source projects has profoundly transformed software development. The ecosystem of software projects is now heavily reliant on various open-source components, presenting a significant opportunity to enhance the ways in which software can be developed. However, these dependencies also introduce unavoidable risks, such as the potential for backdoors that can impact software projects on a large scale.

Ideally, these dependencies should be open-source, providing transparency and allowing the extraction of detailed descriptions of their expected behaviors. These descriptions can then be used to develop backdoor detection mechanisms in a functionality-oriented manner. Implementing an open-source backdoor verification process within repositories could significantly enhance the reliability and security of the code we incorporate from external sources.

Despite these ideals, the current state-of-the-art reveals that many open-source projects still depend on proprietary software components or include proprietary firmware elements within their supply chains. In this systematization, we aim to cover both scenarios: reliance on open-source software as well as dependencies on proprietary software projects.
# Definition
The initial definition was based on finite state machines, but it is important to highlight the interchangeability of control flow graphs (CFGs) and finite state machines (FSMs) in describing the behavior of a system. In this context, Sam L. Thomas uses the term "system" to refer to the highest level of abstraction required to model a given backdoor within a platform. As our focus shifts to application backdoors, "system" describes the program under testing.

To illustrate the system's behavior and the two perspectives of developers and end-level users (including general consumers, security consultants, and program analysts), Sam L. Thomas introduces four types of finite state machines, each representing a different foundational understanding of the system. These types allow for discussions about the deniability and intentions behind backdoor constructs:

- **DFSM (Developer's Finite State Machine)**: Represents the developer's view.
- **AFSM (Actual Finite State Machine)**: Represents the real manifestation of the system.
- **EFSM (Expected Finite State Machine)**: Represents the system as expected by end-users.
- **RFSM (Reverse-engineered Finite State Machine)**: Represents the system as reverse-engineered by analysts.

Understanding multiple ways to illustrate a program's behavior allows us to interchange FSMs with CFGs, which convey the same amount of information. Thus, the categories become:

- **DCFG (Developer's Control Flow Graph)**: Represents the developer's view.
- **ACFG (Actual Control Flow Graph)**: Represents the real manifestation of the system.
- **ECFG (Expected Control Flow Graph)**: Represents the system as expected by end-users.
- **RCFG (Reverse-engineered Control Flow Graph)**: Represents the system as reverse-engineered by analysts.

Although this is a side interest in the context of this paper, it allows us to utilize Thomas's examination of intentions and reason about the consequences of deniability when using different representations of system (program) behavior.

>[!definition] Backdoor 
An intentional construct contained within a system that serves to compromise its expected security by facilitating access to otherwise privileged functionality or information. Its implementation is identifiable by its decomposition into four components: input source, trigger, payload, and privileged state, and the intention of that implementation is reflected in its complete or partial (e.g., in the case of bug-based backdoors) presence within the DFSM and AFSM, but not the EFSM of the system containing it.

Given the diverse nature of real-world backdoors observed in recent years, coupled with the underlying software diversity, it is no longer sufficient to categorize backdoors into a limited number of predefined categories. This approach restricts the scope of backdoor detection to these defined categories. Instead, it is essential to start from a general definition of backdoors and explore various methods of their creation, rather than constraining our detection capabilities by searching for hard-coded patterns and relying on known backdoor constructs. Examining previous approaches to categorizing backdoors, such as those by Wyaposal, reveals that defining such categories often leads to a focus on identifying specific static patterns, which concentrates solely on the characteristics themselves

 This comprehensive definition of backdoors given by Sam L. Thomas et al. operates at a highly abstract level, encapsulating all potential components found in such constructs. Consequently, it broadens the scope of detectable backdoors, avoiding the limitations imposed by categorizing the diverse software backdoors encountered today. Thus it serves as a foundation for detecting a wide range of backdoors and further automating the detection process. Additionally, it functions as a framework to understand the focus and objectives of different detection processes, allowing us to identify any gaps in various approaches.
  In this overview, I aim to utilize the abstract definition of backdoors as a starting point, while also providing detailed information about the implementation of backdoors by specifying how different components can manifest. 

By abstracting the entire underlying system of the backdoor, we can infer that the origin of every backdoor invariably lies in hidden functionality introduced into the software project. Even if no exclusive program parts are added to the project, some previously unknown functionality must be introduced to achieve the intended behavior of the backdoor.


##### Input source
The input source is a critical component required to satisfy the trigger condition. To achieve the conditional branching of the trigger, the system must at least compare some user input. These inputs can be injected at various entry points of the program. Therefore, any potential source of user input within the program can serve this purpose.
##### Trigger 
The trigger mechanism is a pivotal component of our abstract model of a backdoor. It describes the location, where the backdoor leaves the common execution paths and follows an exclusive execution path. In most cases the trigger functionality is implemented by a static data comparison function. These static data comparisons can be established against different elements of static data, e.g. ASCII-texts, password, hashes, public keys or system time.



##### Payload
To reach the final, privileged state of the  backdoor, an intermediate component is required, which describes the transition from the normal system state upon satisfaction of the backdoor trigger to the privileged state. We are going to refer to this component as payload in this work.  The state transitions of the payload phase can be mentally modeled as the solution to puzzle on how to reach the privileged state from successfully satisfying the conditions of a backdoor trigger.


To further define how explicit transitions can be composed, we delve deeper into the general concept of exclusive execution paths. In our case, these paths can be found in the transitions and states included in the trigger and payload phases of the backdoor. It is useful to distinguish between three different classes of exclusive execution paths:

- **C1:** Through exclusive function invocations
- **C2:** Through exclusive paths inside commonly invoked functions (i.e., exclusive basic blocks)
- **C3:** Without exclusive program parts, but through an exclusive execution order of common functions and basic blocks
- 
##### Privileged state
When the backdoor is activated, an eventual system state is reached that can be considered the backdoor-activated state. This state represents a state of escalated privileges, privilege abuse or unauthenticated access. We are going to refer to this state as privileged state.


# What to do if we can define the wanted behaviour of our software project?
The first part of this work will be about the backdoor detection process in open-source software projects. This category is rather defined about the amount of information on our program to test, then on the actual code access of others. Thus this as well includes the backdoor detection process in own software projects or software project, where the source code is accessible and information about the development process, e.g. collaboration graphs exist.
The first approach A-Weasel focuses on the detection of a backdoor relying on a behavioral model of the software itself. Regarding the point where we have a comprehensive definition of the behavioral model of our program, this applies to open-source software projects where we can fully extract a behavioral model from the source code, as well as to our own software projects. If the expected behavior can be represented through an abstract structure, such as a control flow graph or a finite state machine, then hidden functionality can be easily detected by forming the relative complements of the actual behavior and the expected behavior. This relative complement is essentially the hidden functionality.


#### Behavioral Model Extraction
The Weasel approach defines the behavioral model of a binary by relying on protocol run descriptions, which specify the entire behavior of the program. To capture runtime traces of the protocol runs, the Weasel tool utilizes a dynamic analysis approach, defaulting to predefined protocols to ensure the necessary interaction with the program under test. A protocol player is employed to establish the expected behavioral models for specific segments of code. This protocol player interprets protocol descriptions and compiles them into scripts composed exclusively of the atomic operations PUSH DATA, SEND, RECV, and WAIT, as well as the virtual operations START RECORDING and STOP RECORDING. The protocol compiler automatically inserts the latter two operations before and after the relevant atoms to control the tracer's activation and deactivation, thereby minimizing noise in the recorded traces.

For instance, in the context of program authentication, preliminary work essential for identifying hidden functionalities involves defining each authentication method as a separate protocol run description. These detailed protocol run descriptions facilitate the recording of runtime traces representing expected behaviors, which in turn enables the detection of hidden functionalities that deviate from these descriptions, such as exclusive execution paths.

#### Backdoor Classification

Backdoors are classified into four distinct subcategories:

- Authentication validation code
- Specific authentication validation result handling code
- Command parsing code
- Specific command handling code

The approach is based on the assumption that during execution, a server application must diverge from the common execution path and pursue an exclusive execution path to respond differently to varied inputs. This method specifically aims to secure authentication handling and command parsing routines in programs, as backdoors are often located near these routines.

Weasel addresses this by creating a combined decision tree consisting of deciders and top-level handlers. The goal is to detect "cold" edges—edges in the decision tree that are not recorded in any basic block trace for the defined protocol runs. By disabling these "cold" edges, hidden functionality can be effectively canceled out, ensuring that only the program parts of the authentication or command parsing routines used in the defined protocol runs are included.


This approach results in a combined decision tree of deciders and handlers that includes all recorded protocol run traces, as well as a representation of all the "cold" edges in the control flow. The deciders and handlers are scored using simple heuristics to assess the suspicion level of certain handler functionalities. This allows us to prioritize deeper examination of the more suspicious program parts. Although this tool provides a good starting point for automating backdoor detection, it still relies on manual analysis in the final stage. 
Nonetheless the combined decision tree can only cover cases of exclusive execution flow of C1 or a combination of C1 and C2, because the identification of exclusive handlers fails. If there are no functions that are exclusive to a certain subset of all traces, no handlers can be identified (and as a consequence, no deciders as well). To cope with this problem Weasel uses Differential Return Value Comparison. Functions with the same return value in both traces, but different return values between different protocol runs, are treated as handlers by A-WEASEL. 
As well the paper introduces a really interesting analysis module "Function Pointer Table identifier". Because many applications written in C/C++  store command descriptors including pointers to handler functions in central data structures such as arrays. They proposed a analysis module that scans memory of binaries at runtime for pointers to previously identified handler functions. If the in-memory distance between several identified pointers to handlers is equal size, we assume that a table of command descriptors was found. Last step is to heuristically determine beginning and start of the table. In this case when missing a handler in the computation of the combined decision tree, we can still fall back to the table structure and include missing headers.
## Addressing the Challenge of Undefined Software Behavior

In situations where our software project depends on a third-party component that is not open-source or involves embedded firmware in the supply chain—it becomes challenging to define the desired behavior of our software. Therefore, we must focus on approaches that facilitate the manual static analysis of the provided binaries to ensure our software does not contain any backdoors introduced by these dependencies. This scenario is analogous to binary reversing, based on the creation of a control flow graph (CFG) of the binary.

Starting with only the binary, decompiling the binary code to an intermediate language simplifies the subsequent analysis. As discussed in the Springer paper, we can utilize advanced manual static analysis tools. Given the popularity of open-source binary analysis frameworks today, we employ the intermediate language Ghidra IL as a foundation for our further analysis. We will now examine two different approaches.


## Stringer Measuring
In other approaches like Stringer- Measuring the Importance of static data comparison functions, the focus is directly shifted to the static data comparison function itself. Again beginning with the Control Flow Graph (CFG) in Ghidra Intermediate Language (IL), we aim to identify functions that contain a high density of decision logic dependent on the successful return of static data comparison functions. Our ultimate goal is to construct a function-level CFG based on static data comparisons, which can then be used for further transformation and scoring of the density of decision logic.


## Identification of Static Data Comparison Functions

The identification of static data comparison functions involves utilizing several heuristics. Firstly, we consider argument references, which often involve pointers or direct references to read-only memory or the initialized data section. Secondly, we examine the function arity, noting that a comparison function typically takes at least two arguments. Thirdly, we assess the branching properties, ensuring that the result of a call to a data comparison function influences a branching condition. Additionally, we analyze local call frequency, observing that processing routines generally use the same static comparison function multiple times. Lastly, we inspect data properties, identifying that these functions are usually located in the `section_data` or `section_rodata`, do not employ format strings, and avoid unusual whitespace usage.

### Construction of Function-Level CFG (CFG)

Using proposed heuristics based on static data  comparison function properties provides us with the opportunity to detect them in binaries, even if the developers of proprietary software have stripped the binary and no symbolic search is possible. After extracting each static comparison function, we can use the CFG of Ghidra Intermediate Language (GIL) instructions to score each basic block accordingly.

We first construct sets of static data sequences at each basic block within the CFG. This is achieved by labeling each branching basic block and mapping it to the computed static data sequence set. To determine the static data sequence set, we iterate over the predecessors of the basic block and add the static data comparison to the current static sequence data set if the basic block follows a true conditional branch. Independently of the branching, we form the union of the (updated) data sequence set of the currently scanned predecessor and the already identified data sequence sets by other predecessors of the basic blocks.

The static data sequence set of a branching block is computed by adding the branching condition to the set. The non-branching basic blocks are mapped to the union of their predecessor basic blocks.







##### Firmalice
The approach primarily concentrates on detecting backdoors in firmware, yet its principles provide a solid foundation for a broader scope of detection. Despite our inability to define the entire behavior of the binary under analysis, we can still identify various privileged points within the application on which our software project depends. According to the Firmalice paper, the assumption is that all paths leading from an entry point of the software to a privileged operation must validate some input that the attacker cannot derive from the binary itself or from prior communication with the binary. With this assumption in mind, we can create a Program Dependence Graph (PDG) from a CFG and trace back each authentication slice leading to a privileged point.


##### 1) Creating the Control Flow Graph (CFG)

To create a CFG with context-sensitivity 2, we begin at each entry point of the binary and recursively explore both directions of every conditional branch using forced execution. A symbolic execution module is employed to support computed and indirect jumps, including jump tables. The different contexts are represented as nodes, and control flow transfers are depicted as edges.

##### 2) Creating the Program Dependency Graph (PDG)

The PDG we aim to construct consists of a Control Dependency Graph (CDG) and a Data Dependency Graph (DDG). The CDG represents, for each statement XXX (generally, a binary instruction, but in our case, an intermediate representation (IR) statement), the statements YYY that determine whether XXX is executed. The DDG illustrates how instructions correlate with each other concerning the production and consumption of data.

##### 3) Backward Slicing

Starting from a given privileged program point and tracing backwards, we can produce every statement on which that point depends, thus creating each authentication slice accordingly.

##### 4) Symbolic execution engine
Now we can run a symbolic execution engine on each authentication slice. The symbolic state in this case would store the values contained in memory(e.g. variables), registers, status open-files etc. It keeps track of the different constraints on these values in a set of path constraints. As well the set of path constraints includes output routines as constraint. For example any data D, that is exposed in an output routine, is added as a constraint D\==C to the constraint set. Adding this constraint has an effect on concretising existing symbolic variables (for example, if a symbolic
variable E previously existed with a constraint E == D,
then the constraint D == C also implies E == C). This ensures that any loss of secrecy of variables (e.g., leaking a password hash) is detectable within this approach.

##### 5) Constraint Resolving

After collecting the sets of path constraints, the final step involves concretizing the inputs. A properly authenticated path contains inputs that concretize to a large set of values (because the underlying passwords they are compared against are unknown and thus unconstrained). If we manage to concretize the input into a limited set of values, it indicates that an attacker can determine an input that allows them to authenticate.


# Collaboration Graphs
Tom Ganz et al. recently proposed a novel approach to backdoor detection based on anomaly detection in collaboration graphs. This method is complementary to existing detection techniques based on binary analysis and provides an additional layer of security. The primary source of information required for this approach is the collaboration graph of the repository under examination.

In general, every collaboration graph \(G(V, E)\) is composed of nodes \(V\) and direct edges \(E\). To extend the existing representation in Git, which primarily consists of commit node types, additional node types such as branches, files, developers, and methods have been introduced for more comprehensive information. To further enrich the collaboration graph, different attributes of nodes and edges have been incorporated.

### Node Attributes
For developer nodes, statistical information about their behavior (including the overall number of commits and projects, number of merge and non-merge commits), account age, name, email, and location is recorded. Commit nodes contain additional commit information such as commit messages, timestamps, merge types, and whether they are signed or unsigned. They also include code-derived metrics from the DDM model, such as the unit value of interfacing property, size property, and complexity property. File nodes are characterized by attributes like name, MIME type, numbers of past and present methods, and lines of code. Method nodes include the parent file name and method name.

### Edge Attributes
Edge attributes include commit timestamps for edges pointing to descendant file and method nodes, types of file updates (modified, created, or deleted), fan-in and fan-out degrees of methods, start and end lines, token count, and cyclomatic complexity (from file to method nodes).

This comprehensive structure encapsulates all significant information about the development process of a software repository. To detect anomalies, the study employs Graph Neural Networks (GNNs) with convolutional layers. GNNs address learning tasks on graphs by exploiting the relations of nodes and edges in different proximities. Convolutional layers are defined to capture the graph. Each node is considered within a one-dimensional vector space of dimension \(d\), and each edge within a dimension \(k\). Each layer of the convolutional network aggregates information from neighboring nodes to update the node representations. The core mechanism of the convolutional layer consists of a message-passing algorithm, utilizing three learnable differentiable functions: the message function, the aggregation function, and the update function. The message function generates messages for each node by considering the features of the node itself and its neighboring nodes. The aggregation function compiles the messages received from the neighboring nodes. Finally, the update function refines the node's features based on the aggregated information, ensuring that each node’s representation is enriched with context from within the graph.

The Graph Variational Autoencoder (GVAE) leverages the embeddings generated by the GNN to learn a low-dimensional latent representation of the graph. It consists of two primary components: the encoder and the decoder. The encoder transforms the \(d\)-dimensional node vectors and \(k\)-dimensional edge vectors produced by the GNN into a latent space, capturing the essential characteristics and structure of the graph in a compact form. This process effectively reduces the dimensionality of the input data while preserving its most critical features. The decoder's role is to reconstruct the original graph from the latent representation, ensuring that the latent space accurately reflects the original graph's structure and features. During training, the GVAE minimizes the reconstruction loss, which measures how effectively the decoder can reproduce the input graph from the latent vectors.

The Deep Support Vector Data Description (SVDD) method consists of two subphases. First, the GVAE is trained on a diverse set of collaboration graphs to learn optimal embeddings using one-class learning. To enhance anomaly detection, the model can be extended to semi-supervised learning by incorporating a few labeled anomalies. This involves adjusting the objective function to balance the influence of labeled and unlabeled data, guiding the model to better distinguish between normal and anomalous nodes.

Once the GVAE is trained, it generates accurate embeddings into the latent space for new collaboration graphs. The weights of the trained Autoencoder (AE) are then used to initialize the weights \(W\) of a neural network \(\phi\). These embeddings are used for anomaly detection through the Deep Support Vector Data Description (Deep SVDD) method. A center \(c\) is defined in the latent space as the mean of the embeddings obtained from the AE. Anomaly scores are calculated by measuring the distance between each node’s embedding and the center \(c\). Nodes with embeddings that deviate significantly from the center are flagged as anomalies.


