# Model Proposal for _[Resilience of the US Interlock Network]_

_Hyuck David Chung_

* Course ID: CMPLXSYS 530
* Course Title: Computer Modeling of Complex Systems
* Term: Winter, 2019

&nbsp; 
### Goal 
*****
Through the proposed model, I hope to understand:
1) the network properties of the interlock network (e.g., the largest cluster size(%), average clustering coefficient, path length, node degree) 2) the resilience of the interlock network (i.e., how much edges should be removed for the giant cluster to be collapsed), and _(if possible)_ 3) the structural changes before / after the financial crisis in the early 2000s.

&nbsp;  
### Justification
****
Previous literature on the US interlock network discuss how corporate practices such as the golden parachute diffuse within the network and less attention was paid to the overall structural attributes of the network. However, complex network studies have revealed that the overall network structure has a crucial impact on diffusion among network components. That is, depending on the network type (e.g., the small world network, caveman network, or scale-free network), the average diffusion speed changes dramatically.
Thus, causal inferences through empirical analyses is not sufficient; I believe an ABM approach is required to fully analyze the structure properties of the interlock network. The interlock network can be understood as a complex system, composed of thousands of nodes (corporations) and edges (directors). An ABM approach will help us understand the structural properties of the interlock network.

&nbsp; 
### Main Micro-level Processes and Macro-level Dynamics of Interest
****

Albert, Jeong, & Barabasi (2000) has shown that different network structures exhibit different degree of network resilience. On the one hand, scale-free networks are resilient to random removals (or errors), but possess a great weakness in targeted removals (or attacks on hubs). On the other hand, random networks have a similar degree of resilience to both random and targeted removals.

Following Albert, Jeong, & Barabasi (2000), I will apply the reverse percolation theory by removing edges (directors) from the network (interlock network) and study whether there is a sudden collapse in the largest cluster.

# * Micro-level process:
1. Randomly remove edges (directors) from the network.  
2. Remove edges with specific attributes (female directors) first from the network.

# * Macro-level dynamics:
1. Observe the size change of the largest cluster when edges are randomly removed.
2. Observe the size change of the largest cluster when edges with specific attributes are first removed.

&nbsp; 
## Model Outline
****
&nbsp; 
### 1) Environment
The environment in the model is the interlock network where nodes (US corporations) are connected with edges (directors).

```python
int firmNum;   // the number of firms in the given year
int adjacencyMatrix[firmNum][firmNum];   // the network structure where the value is equal to 1 if two nodes are connected, 0 if not.
```

&nbsp; 
### 2) Agents
The agents in the model is edges (directors) that connect nodes and form the interlock network.

```python
int directorNum;  // the number of directors
int directorMatch[directorNum][3] // each columns for director ID, female director, ethinicity

int DataNum;   // dyads that connect firms
// data to be included: 1) f_gvkey, 2) t_gvkey, 3) dirID, 4) dirFem, 5) ethinicity
int dataType = 5; 
int bdexInfo[dataNum][dataType];
```

&nbsp; 
### 3) Action and Interaction 
 
**_Interaction Topology_**

_Description of the topology of who interacts with whom in the system. Perfectly mixed? Spatial proximity? Along a network? CA neighborhood?_
 
**_Action Sequence_**

_What does an agent, cell, etc. do on a given turn? Provide a step-by-step description of what happens on a given turn for each part of your model_

1. Step 1
2. Step 2
3. Etc...

&nbsp; 
### 4) Model Parameters and Initialization

_Describe and list any global parameters you will be applying in your model._

_Describe how your model will be initialized_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

&nbsp; 

### 5) Assessment and Outcome Measures

_What quantitative metrics and/or qualitative features will you use to assess your model outcomes?_

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_
