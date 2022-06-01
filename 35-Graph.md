# Graphs

![graph](https://techcrunch.com/wp-content/uploads/2020/02/cypher_graph_v2a.png)

A graph is a common data structure that consists of a finite set of nodes (or vertices) and a set of edges connecting them.

A pair (x,y) is referred to as an edge, which communicates that the x vertex connects to the y vertex.

In the examples below, circles represent vertices, while lines represent edges.

Graphs are used to solve real-life problems that involve representation of the problem space as a network. Examples of networks include telephone networks, circuit networks, social networks (like LinkedIn, Facebook etc.).

For example, a single user in Facebook can be represented as a node (vertex) while their connection with others can be represented as an edge between nodes.

Each node can be a structure that contains information like user’s id, name, gender, etc.

svg viewer
Graph showing a Social Network (Nodes as users and Edges show connection)
Types of graphs:
Undirected Graph:
In an undirected graph, nodes are connected by edges that are all bidirectional. For example if an edge connects node 1 and 2, we can traverse from node 1 to node 2, and from node 2 to 1.

Directed Graph
In a directed graph, nodes are connected by directed edges – they only go in one direction. For example, if an edge connects node 1 and 2, but the arrow head points towards 2, we can only traverse from node 1 to node 2 – not in the opposite direction.

svg viewer
Types of Graph Representations:
Adjacency List
To create an Adjacency list, an array of lists is used. The size of the array is equal to the number of nodes.

A single index, array[i] represents the list of nodes adjacent to the ith node.

svg viewer
Graph represented as Adjacency List
svg viewer
Graph represented as Adjacency Matrix
Adjacency Matrix:
An Adjacency Matrix is a 2D array of size V x V where V is the number of nodes in a graph. A slot matrix[i][j] = 1 indicates that there is an edge from node i to node j.

[More References](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/graphs.html)