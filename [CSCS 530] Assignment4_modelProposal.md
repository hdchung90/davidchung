# Model Proposal for _'Resilience of the US Interlock Network'_

_Hyuck David Chung_

* Course ID: CMPLXSYS 530
* Course Title: Computer Modeling of Complex Systems
* Term: Winter, 2019

&nbsp; 
### Goal 
*****
Through the proposed model, I hope to understand:
1) the network properties of the interlock network (e.g., the largest cluster size(%), average clustering coefficient, path length, node degree)
2) the resilience of the interlock network (i.e., how much edges should be removed for the giant cluster to collapse)
3) _(if possible)_  the structural changes before / after the financial crisis in the early 2000s.

&nbsp;  
### Justification
****
Previous literature on the US interlock network discuss how corporate practices, such as the golden parachute, diffuse within the network and less attention was paid to the overall structural attributes of the network. However, complex network studies have revealed that the overall network structure has a crucial impact on diffusion among network components. That is, depending on the network type (e.g., the small world network, caveman network, or scale-free network), the average diffusion speed changes dramatically.

Thus, I believe causal inferences through empirical analyses is not sufficient and an ABM approach is required to fully analyze the structure properties of the interlock network. The interlock network can be understood as a complex system, composed of thousands of nodes (corporations) and edges (directors). An ABM approach will help us understand the structural properties of the interlock network.

&nbsp; 

*LS COMMENTS: Solid setup and overview. Well articulated justification.*

### Main Micro-level Processes and Macro-level Dynamics of Interest
****

Albert, Jeong, & Barabasi (2000) has shown that different network structures exhibit different degrees of network resilience. On the one hand, scale-free networks are resilient to random removals (or errors), but possess a great weakness in targeted removals (or attacks on hubs). On the other hand, random networks have a similar degree of resilience to both random and targeted removals.

Following Albert, Jeong, & Barabasi (2000), I will apply the reverse percolation theory by removing edges (directors) from the network (interlock network) and study whether there is a sudden collapse in the largest cluster.

### * Micro-level process:
1. Randomly remove edges (directors) from the network.  
2. Remove edges with specific attributes (female directors) first from the network.

### * Macro-level dynamics:
1. Observe the size change of the largest cluster when edges are randomly removed.
2. Observe the size change of the largest cluster when edges with specific attributes are first removed.

&nbsp; 

*LS COMMENTS: Great baseline setup. This definitely leaves room to consider potentially more complicated and/or highly realistic networks in the future. One thing I was wondering here - will there be a pattern in where female edges occur? This will likely have a big impact on what you find. Also, you might consider making the removal of edges in the 2) process probabilistic instead of deterministic (i.e. make it so that edges with particular attribute have a higher probability of being removed rather than have them all removed first.*

*Another point of clarification - are you thinking about clusters as disconnected components here? Or as "cliques"?*

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
int directorList[directorNum][3] // each column for director ID, female director, ethinicity
int directorMatch[directorNum][2]  // matching the gvkey number to an ordered sequence

int DataNum;   // dyads that connect firms
// data to be included: 1) f_gvkey, 2) t_gvkey, 3) dirID, 4) dirFem, 5) ethinicity
int dataType = 5; 
int bdexInfo[dataNum][dataType];
```

&nbsp; 

*LS COMMENTS: Good.* 

### 3) Action and Interaction 
 
**_Action Sequence_**

1. Randomly select a edge from the directorList[directorNum][1].
2. Remove the edge from the adjacencyMatrix[directorNum][directorNum].
3. Check the largest cluster size when 5%, 10%, 15%, ... , 100% of edges are removed from the network<br>
3-(1) search the giant cluster<br>
3-(2) calcualte the size of the giant cluster<br>
3-(3) record the cluster size at the given period<br>

&nbsp; 

*LS COMMENTS: Good. I suggest looking into existing cluster size calculation algorithms for this if you haven't already.*

### 4) Model Parameters and Initialization

1. Initialize the network setting<br>
 1-(1) construct a network that has nodes with _firmNum_<br>
 1-(2) construct an array to record removed directors<br>
 1-(3) construct an array to record the largest cluster size<br>


2. Import US interlock data<br>
 2-(1) fill in _bdexInfo_<br>
 2-(2) fill in _directorMatch_<br>


3. Build the network<br>
 3-(1) connect nodes using _bdexInfo_<br>

&nbsp; 

*LS COMMENTS: Great to see you are plannning on getting to using real data for this. I would suggest doing an abstract version first to make sure everything is working as expected, and then incorporating the more realistic data.*

### 5) Assessment and Outcome Measures
The outcome measure is the size of the largest cluster size in the network.
8
1. Record the largest cluster size for every 5% of random edges removed
2. Record the largest cluster size for every 5% of edges with female attributes removed
3. Analyze if both removals exhibit a sudden collapse in the size

&nbsp; 

*LS COMMENTS: Solid initial approach. Depending on the network size and density, it might also be interesting to see the number of disconnected components that are produced. Also, how are you defining "collapse" here?*

### 6) Parameter Sweep
The parameter that I would be changing are the number of edges removed from the network.
Ideally, it is best to test for every edge to be removed from the network.
However it might not be possible due to the data size constraints.
According to the complex network literature, many social networks exhibit collapsing behaviors before 30% of the nodes (or edges) are removed. Following the literature, I will first remove at most 30% of the total edges and observe the outcomes.

*LS COMMENTS: Very well-thought out approach for a model that should prove very flexible for future elaborations. If you end up having enough time, you might also consider adding another level of complexity by simulating diffusion processes in the resulting networks. Another direction to consider would be looking at non-random removal wherein, for instance, the likelihood of an edge being removed depends on it being connected to a company that has had other edges dropped. Good start! 19/20*
