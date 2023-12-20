
Graph Neural Network is a type of Neural Network that directly operates on the graph structure.This is useful because networks are everywhere. Like transportation networks, molecular networks,  social networks and user item networks or web networks. 

![[Pasted image 20230610165209.png]]

GNN take a graph G = (V, E, X) as input. Where V, E, X denote nodes, edges (connections between nodes),  and node attribute. 

GNNs learn features about the graph’s structure and their nodes. GNNs learn a representation vector (embedding) $z_\mathbf{v}$ for each node $\mathbf{v} \in G$, or $Z_G$ for the whole graph G.

This then does:
- **node classification** - Given a graph with partial labeled nodes label the other nodes 
- **graph classification** - Predict the class of an entire graph.  Like type of molecule. 
- **Link Prediction**: predicting the existence of an edge between two arbitrary nodes in a graph. Like potential friends in a network.

PyG is is a library built upon PyTorch to easily write and train Graph Neural Networks (GNNs)



The biggest difference is that we don't have euclidean data. 