---
tags:
  - LiteratureNote
title: Firmalice - Automatic Detection of Authentication Bypass Vulnerabilities in Binary Firmware
author(s): Tom Ganz, Inaam Ashraf, Martin Härterich, Konrad Rieck
year: "2023"
date created: "{{date}}"
link: 
conference: CODASPY 23
---
- instead of searching for concealed functionality in program code -> analysis of how the software has developed and locate clues for malicious activities in its version history(as a collaboration graph)
- approach can not rule out the presence of software backdoors, it provides an alternative detection strategy that complements existing ones
- manifest in: unusual commit messages, code locations or even development times


# Problem setting
- static and dynamic program analysis provides means to detect software bugs and vulnerabilities, but are unlikely to spot backdoor code in commits
- isolation of code functionality, can help to reduce the surface 
-> Backdoor=Anomaly in development process

##### Challenges
- Complex relations: inclusion of multiple commits, properties of code change(colab between developers, changes by same contributors etc.)
- Large variance: fixed rules are not able to capture all possible sources of anomalous properties, statistical regular behavior 
- Semantic reasoning: providing a link between natural language text(commit messages) and code changes



# Methodology

### Collaboration Graphs
- graph G(V,E) composed of nodes V and direct edges E
- the central node type of V are commits
	- adding different node types for branches, files, developers, methods(functions)
- relation between commits: drawing a directed edge from one commit to its successor
- relation between developer and commit: direct edge developer and the commit
![[Pasted image 20240619164340.png]]

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



- **Fan-In**: This is the number of other methods or functions that call a particular method. A high fan-in indicates that many parts of the code rely on this method, suggesting it may be a critical part of the system.
- **Fan-Out**: This is the number of other methods or functions that are called by a particular method. A high fan-out indicates that the method interacts with many other parts of the code, which could imply a high level of complexity or responsibility.

- **Token Count:**
    
    - **Definition:** The total number of tokens (keywords, operators, identifiers, literals, etc.) within the method.
    - **Implication:** Token count can be an indicator of the size and complexity of the method. A high token count might suggest a need for refactoring.
    
- **Cyclomatic Complexity:**
    
    - **Definition:** A quantitative measure of the number of linearly independent paths through a program's source code.
    - **Implication:** This metric helps to understand the complexity of the method. A higher cyclomatic complexity indicates more potential paths through the method, which can lead to higher testing requirements and potential for bugs.



# Embedding the collaboration graph
Sure, let's walk through an example using the provided detailed features for nodes and edges. 

### Example: Embedding a Collaboration Graph Using GVAE

#### Step 1: Building the Collaboration Graph

Imagine a small software project with the following history:

- **Developers**: Alice and Bob
- **Commits**: 
  - Commit 1 by Alice on 2022-01-01
  - Commit 2 by Bob on 2022-01-02
- **Files**: 
  - `file1.py` modified in Commit 1
  - `file2.py` modified in Commit 2
- **Methods**:
  - Method `foo` in `file1.py`
  - Method `bar` in `file2.py`

The collaboration graph is built as follows:
- **Nodes**: Developers (Alice, Bob), Commits (Commit 1, Commit 2), Files (file1.py, file2.py), Methods (foo, bar)
- **Edges**: 
  - Alice -> Commit 1
  - Bob -> Commit 2
  - Commit 1 -> file1.py
  - Commit 2 -> file2.py
  - file1.py -> foo
  - file2.py -> bar

#### Step 2: Defining Node and Edge Features

Enrich these nodes with features:

- **Developer Node Features**:
  - Alice: 
    - {number_of_commits: 1, number_of_projects: 1, number_of_merge_commits: 0, number_of_non_merge_commits: 1, account_age: 2 years, name: "Alice", email: "alice@example.com", location: "NY"}
  - Bob: 
    - {number_of_commits: 1, number_of_projects: 1, number_of_merge_commits: 0, number_of_non_merge_commits: 1, account_age: 1 year, name: "Bob", email: "bob@example.com", location: "CA"}

- **Commit Node Features**:
  - Commit 1: 
    - {message: "Initial commit", timestamp: 1640995200, merge_type: "non-merge", signed: "unsigned", unit_value_of_interfacing_property: 0.1, size_property: 100, complexity_property: 1.5}
  - Commit 2: 
    - {message: "Added new feature", timestamp: 1641081600, merge_type: "non-merge", signed: "signed", unit_value_of_interfacing_property: 0.2, size_property: 200, complexity_property: 2.0}

- **File Node Features**:
  - file1.py: 
    - {file_name: "file1.py", mime_type: "text/x-python", number_of_past_methods: 0, number_of_present_methods: 1, lines_of_code: 50}
  - file2.py: 
    - {file_name: "file2.py", mime_type: "text/x-python", number_of_past_methods: 0, number_of_present_methods: 1, lines_of_code: 100}

- **Method Node Features**:
  - foo: 
    - {parent_file_name: "file1.py", method_name: "foo"}
  - bar: 
    - {parent_file_name: "file2.py", method_name: "bar"}

#### Step 3: Encoding Features into a Vector Space

Convert non-numeric features to numerical vectors:

- **Identifiers**:
  - Alice: 1, Bob: 2, file1.py: 1, file2.py: 2, foo: 1, bar: 2
- **Natural Text**:
  - "Initial commit" -> [0.1, 0.2, ..., 0.1]
  - "Added new feature" -> [0.3, 0.1, ..., 0.2]
- **Time Information**:
  - Commit 1: 1640995200 -> (day_of_week: 6, month: 1, day_feature: 1, time_feature: 0.5)
  - Commit 2: 1641081600 -> (day_of_week: 0, month: 1, day_feature: 2, time_feature: 0.6)

#### Step 4: Graph Neural Networks (GNNs)

1. **Message Function (\( \phi \))**: Generates messages using node and edge features.
   - Example: From Alice to Commit 1, the message includes Alice's features and initial commit features.
2. **Aggregation Function (\( \rho \))**: Aggregates messages from neighbors.
   - Example: For Commit 1, aggregate messages from Alice.
3. **Update Function (\( \gamma \))**: Updates node features based on aggregated messages.
   - Example: Update Commit 1's features using aggregated information from Alice.

#### Step 5: Graph-Variational Autoencoder (GVAE)

1. **Encoder**: 
   - Uses GNN to process graph and node features.
   - Transforms processed features into a latent space (low-dimensional representation).
   - Example: Commit 1 encoded to latent vector [0.25, 0.45, ..., 0.35].

2. **Decoder**:
   - Takes latent representation and attempts to reconstruct original graph.
   - Ensures latent space accurately reflects structure and features of original graph.

#### Step 6: Training the GVAE

- **Dataset Preparation**: Collect multiple collaboration graphs, each enriched with node and edge features.
- **Training**:
  - **Reconstruction Loss**: Minimize loss between original and reconstructed graphs to ensure latent space retains important information.
  - **Kullback-Leibler (KL) Divergence**: Ensure latent space follows Gaussian distribution, preventing overfitting and maintaining smoothness.
- **Optimization**: Use gradient descent to minimize combined loss function (reconstruction loss + KL divergence).



Der G Der collaboration graph kommt als input in den GVAE und der encoder embedded diesen collaboration graph in unser graph neural network GNN, anhand der 3 Funktionen zum berechnen der vector spaces der nodes und edges. GVAE ist Instrument um das GNN zu erzeugen

Convolutional level:
- embodies the 3 aggregation functions
- d dimensional vector of each node
- k dimensional vector for each edge
Der GVAE kann dann mit verschiedenen Daten trainiert werden und erzeugt somit die richtigen embeddings, Diese embeddings erlauben es uns nun die Distanzen zum center zu bestimmen und dadurch Anomalien zu detecten.

- **Kollaborationsgraph als Eingabe**:
    
    - Der Kollaborationsgraph, der Informationen über Entwickler, Commits, Dateien und Methoden enthält, wird als Eingabe in den GVAE gegeben.
- **Graph Neural Network (GNN)**:
    
    - **Convolutional Layer**: Das GNN verwendet Convolutional Layer, die die drei Aggregationsfunktionen embody (Nachrichtenfunktion, Aggregationsfunktion und Aktualisierungsfunktion).
    - **d-dimensionaler Vektor**: Jeder Knoten im Graphen wird durch einen d-dimensionalen Vektor repräsentiert, der die Eigenschaften des Knotens erfasst.
    - **k-dimensionaler Vektor**: Jede Kante im Graphen wird durch einen k-dimensionalen Vektor repräsentiert, der die Beziehung zwischen den Knoten erfasst.
- **GVAE (Graph Variational Autoencoder)**:
    
    - **Encoder**: Der Encoder des GVAE nimmt den Kollaborationsgraphen und bettet ihn in einen latenten Raum ein, indem er die d-dimensionalen Vektoren der Knoten und die k-dimensionalen Vektoren der Kanten verwendet.
    - **Decoder**: Der Decoder des GVAE rekonstruiert den Graphen aus dem latenten Raum, um sicherzustellen, dass die Einbettungen die wesentlichen Informationen des ursprünglichen Graphen erfassen.
- **Training des GVAE**:
    
    - Der GVAE wird mit verschiedenen Kollaborationsgraphen trainiert, um die richtigen Einbettungen zu lernen, die die Struktur und die Merkmale des Graphen erfassen.
    - Das Training minimiert die Rekonstruktionsverlust und die Kullback-Leibler-Divergenz, um sicherzustellen, dass der latente Raum genau und gut reguliert ist.
- **Erzeugen von Einbettungen**:
    
    - Nach dem Training kann der GVAE verwendet werden, um Einbettungen für neue Kollaborationsgraphen zu erzeugen.
    - Diese Einbettungen sind die d-dimensionalen Vektoren für die Knoten im Graphen.
- **Anomalieerkennung mit Deep SVDD**:
    
    - **Initialisierung**: Ein Autoencoder (AE) wird auf den vom GVAE erzeugten Einbettungen trainiert und die Gewichte des AE werden verwendet, um die Gewichte WWW eines neuronalen Netzwerks ϕ\phiϕ zu initialisieren.
    - **Zentrum ccc**: Ein Zentrum ccc im latenten Raum wird als Mittelwert der Einbettungen gesetzt.
    - **Anomalieerkennung**: Die Anomaliewerte werden basierend auf den Abständen der Einbettungen vom Zentrum ccc berechnet. Knoten mit großen Abständen werden als Anomalien betrachtet.