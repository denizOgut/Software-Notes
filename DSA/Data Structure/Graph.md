
# Graph

## The Problem

 A data structure is primarily used to store and retrieve data efficiently. All linear data structures store data **sequentially**, like arrays, linked lists, stacks, and queues. On the other hand, tree data structures, like binary trees and heaps, store data **hierarchically**. 

When designing solutions to complex problems, we often need some way to model the **relationship** between multiple data items. While a tree can model parent-child relationships, it cannot model many-to-many relationships.

### Travel booking problem

For example, we are looking to create a travel booking website that will show flight connections between cities. To accomplish this, we need to tackle two specific problems

![[Pasted image 20251128171015.png]]

Storing this data in a tree is impossible as there could be cycles, and a tree, by definition, is acyclic. One way to model this data is to store these connections in multiple lists, where each list has two nodes representing the two cities, and the link between them represents the flight connection

![[Pasted image 20251128171029.png]]

#### Finding maximum number of flights for a given budget

Consider that we also have airfare for travel between each city, and we want to extend our offering and provide the user with the maximum number of flights they can take for a given amount of money from a source city. The destination doesn't matter; we only want to provide the user with the **maximum** number of flights they can take.

![[Pasted image 20251128171111.png]]

## The Solution

A graph is a non-linear data structure comprising one or more nodes connected via links called edges. Each connection between nodes represents the relationship between the nodes. A graph data structure stores and manipulates many-to-many relationships between data.

![[Pasted image 20251128171153.png]]

Each edge in the graph can hold data, often called the edge's weight. Depending on what the graph represents, the weight could be anything.

### Travel booking problem

we can use a graph to model the airfare data for our travel booking website. Each node could be a city, and we could add edges between cities with direct flights. Further to our example, we can assign weight to these edges, representing the airfare between the respective cities

![[Pasted image 20251128171501.png]]

A graph representation of cities and airfare is much more intuitive and easy to understand. Adding new cities or new flight connections is also quite simple, as we only need to add a node and connect it to nodes that can be reached via direct flights.

### Finding minimum hops between cities

To find the minimum number of hops between two cities, we can start from the source city and trace all paths leading to the destination city while counting hops

### Finding optimal number of fights for a given budget

To solve this query, we need to add airfare as a weight to the edges of our graph and trace all paths from the source city while counting the hops and adding airfare along the way. The point where we exhaust our money is when we return and trace a different path. This way, we will have a list of all the paths we can take from the source city for the given money and the number of hops needed for each path.

## Graph Terminologies

### Vertex

A node in a graph is also called a vertex. The node primarily holds the data and the references to all the adjacent nodes.

![[Pasted image 20251128171906.png]]

### Edge

An edge in a graph is the link connecting any two nodes. An edge can either be directed or undirected. A directed edge represents a one-way connection between two nodes. It can be traversed only in one direction and not vice versa. An undirected edge, on the other hand, represents a two-way connection between two nodes that can be traversed in both directions. A graph can have both directed and undirected edges.

![[Pasted image 20251128171948.png]]

### Degree

The degree of a vertex is the number of edges that are incident to the vertex.

![[Pasted image 20251128172015.png]]

#### Indegree and outdegree

The indegree and outdegree are most commonly used for graphs with all directed edges. The in-degree is the total number of incoming edges incident on a vertex, while the outdegree is the total number of outgoing edges from a vertex.

![[Pasted image 20251128172236.png]]

### Path

A path in a graph is a sequence of edges that joins a sequence of distinct vertices. **==In simpler terms, a path is a way to reach a destination node from a source node by following a sequence of edges, where all edges and vertices crossed by those edges are distinct.==**

![[Pasted image 20251128172321.png]]

## Types of Graphs

A graph is a fairly advanced data structure used to model complex relationships. Its logical representation may seem like a simple network of nodes and edges, but the underlying data it represents gives this structure meaning

### Undirected graph

An undirected graph is where all the edges in the graph are undirected. Undirected graphs represent relationships between data items that hold both ways, like the distance between cities, the social connection between people, etc.

![[Pasted image 20251128173204.png]]

### Directed graph

A directed (graph, also called a **digraph**) is one where all edges in the graph are directed (unidirectional) edges. Directed graphs arise naturally, modeling interdependent data. For example, modeling a project schedule where some tasks can only be started when other tasks are completed. In this case, an outward edge from a node means that this task must be completed before the task represented by the node where this edge terminates.

![[Pasted image 20251128173234.png]]

### Weighted graph

A weighted graph is a graph in which the edges are assigned a numerical value called weight. Depending on the graph's representation, the weight quantifies the connection/relationship between two nodes, such as distance, cost, time, etc.

![[Pasted image 20251128173256.png]]

### Connected and disconnected graph

A connected graph is a graph where there is a path between any two vertices. This means that any vertex in the graph can be reached from any other vertex. A disconnected graph, on the other hand, is a graph with at least one pair of vertices with no path connecting them.

![[Pasted image 20251128173515.png]]

### Cyclic graph

A cycle in a graph is defined as a path that begins and ends at the same vertex without crossing any vertex twice. A cyclic graph is a graph that has at least one cycle.

![[Pasted image 20251128173543.png]]

### Directed acyclic graph

A directed acyclic graph (DAG) is a graph that does not have cycles. It can represent hierarchical relationships while still providing the flexibility of a graph. A DAG arises naturally when modeling interrelated hierarchical data like database schemas or UML diagrams or representing scientific and biological data relationships like evolution, family trees, scheduling, etc.

**==A DAG may look like a tree at first glance, but it is NOT a tree. Unlike trees, a node in a DAG can have multiple parents.==**

![[Pasted image 20251128173614.png]]

### Bipartite graph

A bipartite graph is a special type where the vertices can be separated into two disjoint sets. All the edges in the graph connect a vertex in one set to a vertex in another. There is no edge between vertices of the same set. Bipartite graphs are very common and arise naturally when modeling relationships that match data from two sets

![[Pasted image 20251128173634.png]]

# Adjacency Matrix Representation

## Structure of an Adjacency Matrix

![[Pasted image 20251129115817.png]]

If we look at the graph as a set of edges connecting different nodes, the easiest way to implement it in memory is to store all its edges. If we map the relationship of one node with **all** other nodes in a matrix, we can store the graph as a matrix.

However, to do so, we need some way to identify each node uniquely. The easiest and recommended way to do that is to **enumerate** all nodes in the graph. We assign unique values between 0 and N-1 to all nodes, where N is the total number of nodes.

![[Pasted image 20251129115905.png]]

We can then create an NxN matrix to store relationships between all those nodes. This matrix is called the **adjacency matrix**, ==which is a boolean matrix in its simplest form.== For any given pair of nodes, say `i, j` it stores `true` in the cell `i, j` if there is an edge between them or `false` otherwise.

![[Pasted image 20251129115951.png]]

An adjacency matrix is usually used to implement an undirected, unweighted graph, **==meaning it cannot store edge weights and direction.==**

## Implementation of Adjacency Matrix

To create a graph data structure, we need data items and the relationship between them. We need the total number of nodes and a list of edges to implement an adjacency matrix. This information is usually available as data from the problem statement or the use case.

==To implement the graph, we create a function that takes the total number of nodes and a list of edges as input. We then create a boolean `NxN` matrix where `N` is the total number of nodes, and it is initialized with all false values. We then iterate over the list of edges and the cell `i, j` to true if there is an edge between node numbers `i` and `j`.==

```java
public boolean[][] createGraph(int nodes, int[][] edges) {
    // Create adjacency matrix
    boolean[][] adj = new boolean[nodes][nodes];

    for (int i = 0; i < adj.length; i++) {
        for (int j = 0; j < adj[i].length; j++) {
            adj[i][j] = false;
        }
    }

    for (int[] edge : edges) {
        // Update cells both ways for undirected graphs
        adj[edge[0]][edge[1]] = true;
        adj[edge[1]][edge[0]] = true;
    }

    return adj;
}
```

## Enhanced Implementation Techniques

An adjacency matrix is an easy and effective way to implement a graph in memory. However, it is not the best way to do it. Some graphs cannot be implemented using the basic boolean matrix implementation.

> Adjacency matrix implementation cannot store:
> 
> - Weighted edges
> - Data value at nodes

![[Pasted image 20251129121242.png]]

An adjacency matrix only stores the relationship between nodes and nothing about the node. Also, it only stores the **existence** of an edge between two nodes, so it cannot store any additional edge data, such as weights 

### Store weighted edges

To implement a weighted graph, we can modify the adjacency matrix to hold numerical values instead of boolean `true` and `false`. We initialize the matrix with a **sentinel value** (a value that can never be a valid weight value). We store the weight in the cell `i, j` if there is a weighted edge between nodes enumerated `i` and `j`. This way, we can assert the existence of an edge between nodes if the cell holds any value other than the sentinel value and the value is the weight of the edge itself.

![[Pasted image 20251129121419.png]]

The implementation is only very slightly different from the boolean adjacency matrix. We create a function that takes the total number of nodes and a list of edges as input. We then create a numerical `NxN` matrix where `N` is the total number of nodes, and it is initialized with all sentinel values. We then iterate over the list of edges and set the cell `i, j` to the weight of the edge between the node numbers `i` and `j`.

```java
/*
 * Function to create graph
 * nodes: The number of nodes in the graph
 * edges[in]: A list of edges. An edge is a list storing
 * the two nodes it connects.
 *
 * returns: Adjacency matrix
 */
public int[][] createGraph(int nodes, int[][] edges) {
    // Create adjacency matrix, sentinel is -1
    int[][] adj = new int[nodes][nodes];

    for (int i = 0; i < adj.length; i++) {
        for (int j = 0; j < adj[i].length; j++) {
            adj[i][j] = -1;
        }
    }

    for (int[] edge : edges) {
        // Update cells both ways for undirected graphs
        adj[edge[0]][edge[1]] = edge[2];
        adj[edge[1]][edge[0]] = edge[2];
    }

    return adj;
}
```

### Store Data at Nodes

To implement a graph that also holds some data at the node, we need to create another array to hold that data. Since the nodes of the graphs are enumerated from 0 to N-1, we can create a single array of size N and use the enumeration of a node as its index in the array to store data. We can also define a custom datatype if the data to be stored is complex.

![[Pasted image 20251129122108.png]]

The implementation uses an array to store the node data for each node. Since the nodes are enumerated from 0 to N-1, the data at an index `i` in the array is the data for the node `i`. When creating the graph, we take this array as an additional input along with the list of edges. We then create a numerical `NxN` matrix where `N` is the total number of nodes, and it is initialized with all sentinel values. We then iterate over the list of edges and set the cell `i, j` to the weight of the edge between the node numbers `i` and `j`.

```java
/*
 * Function to create graph
 * nodes[in]: A list node data
 * edges[in]: A list of weighted edges. An edge is a list storing
 * the nodes it connects and weight respectively
 *
 * returns: Adjacency matrix
 */
public int[][] createGraph(int[] nodes, int[][] edges) {
    // Create adjacency matrix, sentinel is -1
    int[][] adj = new int[nodes.length][nodes.length];

    for (int i = 0; i < adj.length; i++) {
        for (int j = 0; j < adj[i].length; j++) {
            adj[i][j] = -1;
        }
    }

    for (int[] edge : edges) {
        // Update cells both ways for undirected graphs
        adj[edge[0]][edge[1]] = edge[2];
        adj[edge[1]][edge[0]] = edge[2];
    }

    return adj;
}
```

# Adjacency List Representation

## Structure of Adjacency List

![[Pasted image 20251129115817.png]]

Instead of looking at the graph as a set of edges connecting the nodes, if we look at the graph as a set of nodes connected, we can implement the graph from the point of view of nodes. For every node, we can store all the nodes directly connected to it by an edge in a list, also called the **adjacency list**. This way, the entire graph can be implemented as a list of adjacency lists.

However, just like the adjacency matrix implementation, we need to **enumerate** all nodes in the graph to identify each node uniquely. We assign unique values between 0 and N-1 to all nodes, where N is the total number of nodes.


![[Pasted image 20251129115905.png]]

We can then create a two-dimensional list with the outer list of size N, where N is the number of nodes. The item `i` in the list is the adjacency list for the ith node in the graph.

![[Pasted image 20251129134010.png]]

### Representation in memory

Unlike the adjacency matrix implementation, where the size of the matrix is known at the time of creation, in the adjacency list implementation, only the size of the outer list is known. The adjacency list grows when we create the graph, so it is implemented as either a dynamic array or a linked list. The outer list can be dynamic if nodes must be added or removed from the graph. For this reason, the structure of memory depends very much on its implementation.

In most graph implementations, however, dynamic arrays are used instead of linked lists as they provide random access in the adjacency list and benefit from the locality of reference.

![[Pasted image 20251129134233.png]]

## Implementation of Adjacency List

To create a graph data structure, we need data items and the relationship between them. Just like the adjacency matrix implementation, we need the total number of nodes and a list of edges to implement an adjacency list. This information is usually available as data from the problem statement or the use case.

To implement the graph, we create a function that takes the total number of nodes and a list of edges as input. Each edge in the list has two values, the source node and destination nodes respectively. We then create a two-dimensional dynamic list, where each list stores all the neighbors of a node. We then iterate over the list of edges and add the nodes as neighbors in their respective adjacency lists.

```java
public List<List<Integer>> createGraph(int nodes, int[][] edges) {
    // Create adjacency list
    List<List<Integer>> adjList = new ArrayList<List<Integer>>();

    for (int i = 0; i < nodes; i++) {
        adjList.add(new ArrayList<Integer>());
    }

    for (int[] edge : edges) {
        // Add nodeB (edge[1]) to adjacency list of nodeA (edge[0])
        adjList.get(edge[0]).add(edge[1]);

        // Add nodeA (edge[0]) to adjacency list of nodeB (edge[1])
        adjList.get(edge[1]).add(edge[0]);
    }

    return adjList;
}
```

## Enhanced Implementation Techniques

Adjacency list implementation cannot store:

- Weighted edges
- Data value at nodes

![[Pasted image 20251129121242.png]]

The basic implementation of an adjacency list only stores the relationship between nodes and nothing about the node. Also, it only stores the **existence** of an edge between two nodes, so it cannot store any additional edge data, such as weights.

### Store weighted edges

We can modify the adjacency list to store a pair of values instead of a single value to implement a weighted graph. We can then choose the first value in the pair to represent the weight of the edge, while the other could be the destination node for this edge. There are other ways we can store weights as well but this is the simplest way to do it.

The implementation is slightly different from the basic implementation of the adjacency list. We create a function that takes the total number of nodes and a list of edges as input. Each edge in the list is represented by three values: source node, destination node, and weight, respectively. We then create a two-dimensional dynamic list, where each internal list stores the destination node and the edge weight respectively. We then iterate over the list of edges and add edge weight and neighbor nodes in their respective adjacency lists.

```java
/*
 * Function to create graph
 * nodes: The number of nodes in the graph
 * edges[in]: A list of edges. An edge is a list storing
 * the two nodes it connects and the weight.
 *
 * returns: Adjacency list
 */
public List<List<List<Integer>>> createGraph(int nodes, int[][] edges) {
    // Create adjacency list
    List<List<List<Integer>>> adjList = new ArrayList<List<List<Integer>>>();

    for (int i = 0; i < nodes; i++) {
        adjList.add(new ArrayList<List<Integer>>());
    }

    for (int[] edge : edges) {
        // Add nodeB (edge[1]) and edge weight (edge[2])
        // to adjacency list of nodeA (edge[0])
        List<Integer> pair1 = new ArrayList<Integer>();
        pair1.add(edge[1]);
        pair1.add(edge[2]);
        adjList.get(edge[0]).add(pair1);

        // Add nodeA (edge[0]) and edge weight (edge[2])
        // to adjacency list of nodeB (edge[1])
        List<Integer> pair2 = new ArrayList<Integer>();
        pair2.add(edge[0]);
        pair2.add(edge[2]);
        adjList.get(edge[1]).add(pair2);
    }

    return adjList;
}
```

### Store data at nodes

To implement a graph that also holds some data at the node, we can create another array to hold that data. Since the nodes of the graphs are enumerated from 0 to N-1, we can create a single array of size N and use the enumeration of a node as its index in the array to store data.

Since, unlike the adjacency matrix implementation, the data of the edges stays with the node in the adjacency list implementation, another way of implementing a graph with data at nodes is to create a new data type for the node. This new datatype can encapsulate the node data along with the adjacency lists, and the graph can then be represented as an array of these nodes.

![[Pasted image 20251129144718.png]]

```java
class Node

{
    public int data;

    public List<List<int>> adj;

    Node(int data)

    {
        this.data = data;
        this.adj = new ArrayList<List<int>>();
    }
};
```

The graph can then be implemented as an array of such nodes where the index `i` represents the node enumerated `i` in the logical representation of the graph. This is a better way of implementing graphs with node data, as it allows for extending the node data with more data if needed.

![[Pasted image 20251129144755.png]]

The implementation uses an array to store all the node objects together. Since the nodes are enumerated from 0 to N-1, the data at an index `i` in the array is the node `i`. When creating the graph, we take the array containing the node data as an additional input, along with the list of edges. We then create a dynamic list to hold the new node datatype and iterate over the array containing the node data to create and initialize graph nodes with the respective data. We then iterate over the list of edges and add neighbors and edge weights to the adjacency list of the source and destination nodes.

```java
/*
 * Function to create graph
 * nodeData: A list of node data
 * edges[in]: A list of edges. An edge is a list storing
 * the two nodes it connects and the weight.
 *
 * returns: graph as array of nodes
 */
public List<Node> createGraph(int[] nodeData, int[][] edges) {
    // Create adjacency list
    List<Node> nodes = new ArrayList<Node>();

    // Fill in the node data
    for (int i = 0; i < nodeData.length; i++) {
        nodes.add(new Node(nodeData[i]));
    }

    for (int[] edge : edges) {
        // Add nodeB (edge[1]) and edge weight (edge[2])
        // to adjacency list of nodeA (edge[0])
        List<Integer> pair1 = new ArrayList<Integer>();
        pair1.add(edge[1]);
        pair1.add(edge[2]);
        nodes.get(edge[0]).adj.add(pair1);

        // Add nodeA (edge[0]) and edge weight (edge[2])
        // to adjacency list of nodeB (edge[1])
        List<Integer> pair2 = new ArrayList<Integer>();
        pair2.add(edge[0]);
        pair2.add(edge[2]);
        nodes.get(edge[1]).adj.add(pair2);
    }

    return nodes;
}
```

## Example Clone Adjacency List

Given the **adjacency list** of a directed graph, write a function to clone this list and return a new list.

```JAVA
import java.util.*;

class Solution {
    public List<List<Integer>> cloneAdjacencyList(
        List<List<Integer>> adjList
    ) {
        int n = adjList.size();

        // Create a new adjacency list for the cloned adjList
        List<List<Integer>> clonedList = new ArrayList<>();

        // Copy each node's neighbours from the original adjList to the
        // cloned adjList
        for (int i = 0; i < n; i++) {
            clonedList.add(new ArrayList<Integer>());

            // Iterate over the neighbours of node i in the original
            // adjList
            for (int j = 0; j < adjList.get(i).size(); j++) {
                // Add the neighbour to the cloned adjList
                clonedList.get(i).add(adjList.get(i).get(j));
            }
        }

        // Return the cloned adjList
        return clonedList;
    }
}
```

## Example  Adjacency List to Adjacency Matrix

Given the **adjacency list** of a directed graph, write a function to convert it to an adjacency matrix.

```JAVA
import java.util.*;

class Solution {
    public int[][] adjacencyListToAdjacencyMatrix(
        List<List<Integer>> adjList
    ) {
        int n = adjList.size();
        // Initialize adjacency matrix with 0s
        int[][] adjMatrix = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < adjList.get(i).size(); j++) {
                int neighbour = adjList.get(i).get(j);
                // Mark the corresponding cell in the matrix as 1
                adjMatrix[i][neighbour] = 1;
            }
        }

        return adjMatrix;
    }
}
```

## Example Adjacency Matrix to Adjacency List

Given the **adjacency matrix** of a directed graph, write a function to convert it to an adjacency list.

```JAVA
import java.util.*;

class Solution {
    public List<List<Integer>> adjacencyMatrixToAdjacencyList(
        int[][] adjMatrix
    ) {
        int n = adjMatrix.length;
        List<List<Integer>> adjList = new ArrayList<>();

        // Traverse the adjacency matrix
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
            for (int j = 0; j < n; j++) {
                // If an edge exists between nodes i and j
                if (adjMatrix[i][j] == 1) {
                    // Add node j to the adjacency list of node i
                    adjList.get(i).add(j);
                }
            }
        }

        return adjList;
    }
}
```

# Traversing a Graph

## Depth First Traversal

Unlike linear data structures, we cannot traverse all nodes in a graph using simple loops. The depth-first traversal is a fundamental traversal algorithm for graph data structures that uses depth-first search to visit all nodes connected to a node. The depth-first search is a **recursive** algorithm that starts from a node and explores one complete branch at a time.

![[Pasted image 20251130121851.png]]

The depth-first traversal algorithm utilises the depth-first search algorithm to traverse all nodes connected to a given node. The depth-first search algorithm is quite straightforward as it fully explores one branch before backtracking to other branches. It can be considered a generalisation of the three tree traversal algorithms (preorder, inorder and postorder traversal).

The simple recursive equation given below summarizes the depth-first search algorithm from a source node.

![[Pasted image 20251130121915.png]]

Only applying depth-first search from any one node in the graph may not be enough, as it may not cover all the nodes of the graph if the graph is disconnected.

![[Pasted image 20251130121947.png]]

And so, the depth-first traversal algorithm performs depth-first search from every unvisited node until all nodes are visited. This way, all the nodes in the graph are traversed, even in disconnected graphs.

![[Pasted image 20251130122004.png]]

To traverse all the nodes in the graph, we initialize a `visited` set and iterate over all the nodes of the graph. For any node that is not in the `visited` set, we call the depth-first search function on it. The depth-first search function takes as input the current node and the reference to the `visited` set. For languages that do not support passing data by reference, the `visited` set can be created in the global scope to share the same copy between recursive function calls.

As we enter a node, we add the node to the `visited` set to make sure they are not revisited if there are cycles. We then iterate over all the neighbors of the node and recursively call the depth-first search on the unvisited nodes, which in turn recursively performs the same operation. The algorithm backtracks from a node when there are no unvisited neighbors left.

This way, at the end of the top-level call to the depth-first search function, all the nodes connected to the top-level node are visited and added to the `visited` set. We then continue our iteration over the graph nodes in the calling function and repeat the same process for the remaining unvisited nodes. At the end of all iterations, all the nodes of the graph will be visited and added to the `visited` set, completing the depth-first traversal.

**dfs(node, [ref] graph, [ref] visited)**

- **Step 1:** Add `node` to `visited` set
- **Step 2:** Iterate over all the neighbours of `node` in a variable `neighbour` and do the following
    - **Step 2.1:** If `neighbour` is not in `visited` set call `dfs(neighbour, graph, visited)`

**depthFirstTraversal([ref] graph)**

- **Step 1:** Create a `visited` set
- **Step 2:** Iterate over all the nodes in the graph in a variable `node` and do the following
    - **Step 2.1:** If `node` not in `visited` set call `dfs(node, graph, visited)`


### Implementation

Consider that we have a graph of size **N**, where the nodes are enumerated from **0** to **N-1**, and we are given the adjacency list of the graph as a two-dimensional list of integers `graph`, where the value is the enumeration of the neighbor node. 

Given below is the implementation of the depth-first traversal algorithm. We create a recursive `dfs` function that takes as input the current node, a reference to the adjacency list `graph` and a reference to the `visited` set. For languages where passing by reference is not supported, we create the variables in the enclosing scope to make the same copy available in recursive calls.

We create the visited set in the calling function, `depthFirstTraversal`, and iterate over all the nodes in the graph, calling `dfs` on all the unvisited nodes

```java
import java.util.*;

class Solution {
    public void dfs(
        List<List<Integer>> graph,
        int node,
        Set<Integer> visited,
        List<Integer> result
    ) {
        // Mark the current node as visited in the graph to avoid
        // visiting it again
        visited.add(node);

        // Add the current node to the result list
        result.add(node);

        // Traverse all the neighbours of the current node
        for (int neighbour : graph.get(node)) {
            // If the neighbour is not visited, recursively call the DFS
            // function on the neighbour
            if (!visited.contains(neighbour)) {
                dfs(graph, neighbour, visited, result);
            }
        }
    }

    public List<Integer> depthFirstTraversal(List<List<Integer>> graph) {
        // Number of nodes in the graph
        int N = graph.size();

        // If the graph is empty, return an empty result
        if (N == 0) {
            return new ArrayList<>();
        }

        // Initialize a list to store the result of the DFS which will
        // contain the nodes visited during the DFS traversal
        List<Integer> result = new ArrayList<>();

        // Initialize visited set
        Set<Integer> visited = new HashSet<>();

        // Traverse all nodes in the graph
        for (int node = 0; node < N; node++) {
            // If the node is already visited, continue to the next node
            if (visited.contains(node)) {
                continue;
            }

            // Perform DFS on this new node to visit all the nodes
            // connected to it.
            dfs(graph, node, visited, result);
        }

        return result;
    }
}
```

## Breadth First Traversal

 The breadth-first traversal is another fundamental graph traversal algorithm that uses breadth-first search to explore all nodes at a fixed distance (depth) before moving to nodes at the next greater distance (depth). It can be visualized as moving outwards from the center of concentric circles, covering one full circle at a time.

![[Pasted image 20251130122437.png]]

Just like depth-first search is the generalization of preorder, inorder, and postorder traversals, breadth-first search is the generalization of level traversal. The only difference between the level order traversal of a tree and the breadth-first search of a graph is that we maintain map to keep track of nodes that are already scheduled to visit, as graphs can have cycles.

The breadth-first traversal algorithm utilises the breadth-first search algorithm to traverse all nodes connected to a given node. The breadth-first search is a simple two-step algorithm in which we maintain a `queue` of nodes to visit and a `visited` set to keep track of nodes **scheduled** for a visit. It can be considered a generalization of the level order traversal algorithm for trees.

![[Pasted image 20251130122506.png]]

Only applying breadth-first search from any one node in the graph may not be enough, as it may not cover all the nodes of the graph if the graph is disconnected.

![[Pasted image 20251130122525.png]]

And so, the breadth-first traversal algorithm performs breadth-first search from every unvisited node until all nodes are visited. This way, all the nodes in the graph are traversed, even in disconnected graphs.

![[Pasted image 20251130122603.png]]

To traverse all the nodes in the graph, we initialize a `visited` set and iterate over all the nodes of the graph. For any node that is not in the `visited` set, we call the breadth-first search function on it. The breadth-first search function takes as input the current node and the reference to the `visited` set. For languages that do not support passing data by reference, the `visited` set can be created in the global scope to share the same copy between function calls.

The breadth-first search function initializes a local `queue` to schedule visits to nodes.

![[Pasted image 20251130122750.png]]

We start by adding the source node (passed as input) to the `queue` and iterate while the `queue` is not empty.

![[Pasted image 20251130122759.png]]

In each iteration, we pop a node from the front of the queue, which is equivalent to visiting it. We then use the `visited` set to find all its neighbours that are **not** scheduled for a visit and push them to the `queue`. Once we add a neighbour to the queue, we also add it to the `visited` set so that we don't add it to the `queue` again from another path.

Since we add all the neighbours of a node to the `queue` **before** visiting them and the queue follows a FIFO (first in, first out order), it is guaranteed that we visit all neighbours of a node before visiting any other node.

This process is repeated until the `queue` is empty, which means that all nodes reachable from the top-level source node have been traversed and added to the `visited` set.

![[Pasted image 20251130122820.png]]

We then continue our iteration over the graph nodes in the calling function and repeat the same process for the remaining unvisited nodes. At the end of all iterations, all the nodes of the graph will be visited and added to the `visited` set, completing the breadth-first traversal.

**Algorithm**

**bfs(node, [ref] graph, [ref] visited)**

- **Step 1:** Create a `queue` and add the `node` to it.
- **Step 2:** Add `node` to the `visited` set
- **Step 3:** Iterate while `queue` is not empty and do the following:
    - **Step 3.1:** Pop a node from the front of the `queue` in the variable `node`
    - **Step 3.2:** Iterate over all the neighbors of `node` in a variable `neighbour` and do the following:
        - **Step 3.2.1:** If `neighbour` is not in `visited` set, add `neighbour` to the `queue` and `visited` set

**breadthFirstTraversal([ref] graph)**

- **Step 1:** Create a `visited` set
- **Step 2:** Iterate over all the nodes in the graph in a variable `node` and do the following
    - **Step 2.1:** If `node` not in `visited` set call `bfs(node, graph, visited)`


### Implementation

Consider that we have a graph of size **N**, where the nodes are enumerated from **0** to **N-1**, and we are given the adjacency list of the graph as a two-dimensional list of integers `graph`, where the value is the enumeration of the neighbor node.

Given below is the implementation of the breadth-first traversal algorithm. We create a `bfs` function that takes as input the current node, a reference to the adjacency list `graph` and a reference to the `visited` set. For languages where passing by reference is not supported, we create the variables in the enclosing scope. The bfs function creates a local variable `queue` every time it is called to schedule the nodes to visit.

We create the `visited` set in the calling function `breadthFirstTraversal`, and iterate over all the nodes in the graph, calling `bfs` on all the unvisited nodes.

```java
import java.util.*;

class Solution {
    public void bfs(
        List<List<Integer>> graph,
        int source,
        Set<Integer> visited,
        List<Integer> result
    ) {
        // Create a queue to perform breadth-first search
        Queue<Integer> queue = new LinkedList<>();

        // Add the source node to the queue
        queue.add(source);

        // Mark the source node as visited
        visited.add(source);

        // Perform BFS
        while (!queue.isEmpty()) {
            // Get the front node from the queue
            int node = queue.poll();

            // Add the current node to the result
            result.add(node);

            // Visit all the neighbours of the current node
            for (int neighbour : graph.get(node)) {
                // If the neighbour is not visited, add it to the queue
                if (!visited.contains(neighbour)) {
                    // Add the neighbour to the queue
                    queue.add(neighbour);

                    // Mark the neighbour node as visited
                    visited.add(neighbour);
                }
            }
        }
    }

    public List<Integer> breadthFirstTraversal(
        List<List<Integer>> graph
    ) {
        // Number of nodes in the graph
        int N = graph.size();

        // If the graph is empty, return an empty result
        if (N == 0) {
            return new ArrayList<>();
        }

        // Initialize a list to store the result of the BFS which will
        // contain the nodes visited during the BFS traversal
        List<Integer> result = new ArrayList<>();

        // Initialize visited set
        Set<Integer> visited = new HashSet<>();

        // Traverse all nodes in the graph
        for (int node = 0; node < N; node++) {
            // If the node is already visited, continue to the next node
            if (visited.contains(node)) {
                continue;
            }

            // Perform BFS on this new node to visit all the nodes
            // connected to it.
            bfs(graph, node, visited, result);
        }

        return result;
    }
}
```

#  Traversing a Grid

A graph is a set of nodes connected by edges, while a grid is a two-dimensional matrix of values that is often encountered in many software development and mathematical problems. Many grid-based problems can be solved effectively by modelling the grid as a graph.

![[Pasted image 20251130125745.png]]

Consider we have a two-dimensional matrix (grid) where every cell has some value and one can move from any cell to all its adjacent cells (typically in the four cardinal directions: up, down, left, and right).

![[Pasted image 20251130130201.png]]

This grid can be modelled as a graph where every cell represents a node that is connected to all other nodes in all the allowed directions. The value in the cell may represent the data associated with the node or some **sentinel** value that carries some special meaning (e.g., indicating obstacles, boundaries, etc). The unique identifier in the resulting graph is the coordinate (row, col) pair for the corresponding cell in the grid.

![[Pasted image 20251130130216.png]]

### Traversal in a Grid

A grid modelled as a graph can be used as a graph without creating any adjacency list or matrix. This is because every node in the modelled graph is identified using its coordinate in the grid. Since every node is connected to adjacent nodes in all cardinal directions, we can easily calculate the coordinates of all the neighbors for any node.

![[Pasted image 20251130130250.png]]

Once a grid is modelled as a graph, all graph algorithms, including the depth-first and breadth-first traversal, can be applied to it. In the lesson, we will learn more about how to implement depth-first and breadth-first traversal on a grid. However, all graph algorithms that we learn later in the course can also be applied to it in the same way.

## Depth First Traversal on a Grid

The depth-first algorithm on a grid is the same as for any other graph. We start from a node and recursively traverse all the unvisited neighbour nodes until no unvisited node remains in any paths originating at the start node. To fully traverse disconnected graphs, however, we need to iterate over all the nodes and run depth-first search from any unvisited node.

Depth-first search on a grid uses coordinates (row, col) to uniquely identify a node and **compute** the identifiers (coordinates) of adjacent nodes, instead of reading them from an adjacency list. In this explanation, we will use the term **cell** and **node** interchangeably, as every node is uniquely identified by the coordinates (row, col) of its cell in the grid.

![[Pasted image 20251130130511.png]]

To understand depth-first search on a grid, let's consider a grid where a value of 1 indicates that the cell should be explored, while a value of 0 indicates it should not be explored. We can model this grid as a graph that has a mix of nodes, where some can be visited while others cannot. Since some cells also have 0 values, the resulting graph can potentially be disconnected, meaning there may not be a path between every pair of nodes. Therefore, we may need to run a depth-first search multiple times from different nodes.

![[Pasted image 20251130130528.png]]

We start by creating a two-dimensional `visited` array of the same size as the grid and initialise it with false.

![[Pasted image 20251130130540.png]]

We then iterate in the `visited` array and in each iteration, check if the current cell (node) is marked `false` and the grid has value 1 at that coordinate. If the condition holds `true`, we start depth-first search from that cell by passing its coordinate (row, col) and references to the `grid` and `visited` array to the recursive depth-first search function. If not, it means the node is either already visited or cannot be visited.

![[Pasted image 20251130130552.png]]

We pass `grid` and `visited` array as references to ensure that every recursive stack frame shares the same copy of this data. For languages that do not support passing data by reference, we can create them in the enclosing scope to make them global for recursive function calls.

As we enter a node, we mark it visited in the `visited` array using its coordinates (row, col). We then compute the coordinates of all its neighboring nodes, iterate over those coordinates and in each iteration, check if the coordinate is within the bounds of the grid, not marked visited in the `visited` array, and has a value of 1. If the condition holds true, we visit it by recursively calling depth-first search and passing the computed coordinates(row, col) this time.

![[Pasted image 20251130130607.png]]

The recursive call will stop and backtrack when all reachable neighbours of a node are marked visited. This way, at the end of the top-level call to the depth-first search function, all nodes that can be reached from the first node will be marked visited. We then continue iteration in the `visited` array and repeat the process for all the nodes that have a value of 1 and have not yet been marked as visited. This way, at the end of all iterations, all nodes that can be visited will be visited.

The algorithm below summarises the depth-first search on such a grid.

> **Algorithm**
> 
> **dfs(row, col, [ref] grid, [ref] visited)**
> 
> - **Step 1:** Set `visited[row][col]` to `true`
> - **Step 2:** Compute coordinates in all four (up, right, bottom, top) in `(newRow, newCol)` and for each, do the following:
>     - **Step 2.1:** If `(newRow, newCol)` is within the bounds of `grid` and `grid[newRow][newCol]` is `1` and `visited[newRow][newCol]` is `false`, do the following
>         - **Step 2.1.1:** Call `dfs(newRow, newCol, grid, visited)`
> 
> **callingFunction([ref] grid)**
> 
> - **Step 1:** Create a `visited` array of the same size as `grid` and initialize it to `false`
> - **Step 2:** Iterate in `grid` using `row` and `col` and do the following for each cell:
>     - **Step 2.1:** If `grid[row][col]` is `1` and `visited[row][col]` is `false`, call `dfs(row, col, grid, visited)`


### Implementation

To implement depth-first search on a grid, we create a recursive function `dfs`, that takes as arguments: the reference to the `visited` array and the coordinates (row, col) of a cell to identify a node uniquely. We create the `visited` array in the calling function to pass it by reference to `dfs`. For languages that don't support passing data by reference, we create it in the enclosing scope.

We create and use a temporary array `dir` to easily compute the coordinates of all potential neighbours.

```java
import java.util.*;

class Solution {
    public boolean isValidCell(int[][] grid, int row, int col) {
        // Check if a cell is valid and belongs to a region of 1's, also
        // check that the cell is not water
        return (
            row >= 0 &&
            row < grid.length &&
            col >= 0 &&
            col < grid[0].length &&
            grid[row][col] == 1
        );
    }

    public void dfs(
        int[][] grid,
        int row,
        int col,
        boolean[][] visited,
        List<List<Integer>> result
    ) {
        // Mark the current cell as visited
        visited[row][col] = true;

        // Add the current cell to the result
        result.add(List.of(row, col));

        // Define the possible movements: up, right, down, left
        int[][] directions = {
            {-1, 0}, // up
            {0, 1},  // right
            {1, 0},  // down
            {0, -1}  // left
        };

        for (int[] dir : directions) {
            int newRow = row + dir[0];
            int newCol = col + dir[1];

            // If the neighbour is not visited, recursively call the DFS
            // function on the neighbour
            if (
                isValidCell(grid, newRow, newCol) &&
                !visited[newRow][newCol]
            ) {
                dfs(grid, newRow, newCol, visited, result);
            }
        }
    }

    public List<List<Integer>> depthFirstTraversalOnAGrid(int[][] grid) {
        int rows = grid.length;

        // If the grid is empty, return an empty result
        if (rows == 0) {
            return new ArrayList<>();
        }

        int cols = grid[0].length;

        // Initialize a list to store the result of the DFS
        // which will contain the coordinates of the cells visited
        // during the DFS traversal
        List<List<Integer>> result = new ArrayList<>();

        // Initialize visited array
        boolean[][] visited = new boolean[rows][cols];

        // Traverse each cell of the grid
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                // If the cells is not visitable or is already visited,
                // continue to the next cell
                if (grid[row][col] == 0 || visited[row][col]) {
                    continue;
                }

                // Perform DFS on this new cell to visit all the cells
                // connected to it.
                dfs(grid, row, col, visited, result);
            }
        }

        return result;
    }
}
```
## Breadth First Traversal on a Grid

The breadth-first algorithm on a grid is the same as for any other graph. We start from a node and all its unvisited neighbours to a queue to schedule their visit later. We then pick the node at the front of the queue and repeat the process until the queue is empty. However, to fully traverse disconnected graphs, we need to iterate over all the nodes and run breadth-first search from any unvisited node.

Breadth-first search on a grid uses coordinates (row, col) to uniquely identify a node and **compute** the identifiers (coordinates) of adjacent nodes, instead of reading them from an adjacency list. In this explanation, we will use the term **cell** and **node** interchangeably, as every node is uniquely identified by the coordinates (row, col) of its cell in the grid.

![[Pasted image 20251130130511.png]]

To understand breadth-first search on a grid, let's consider a grid where a value of 1 indicates that the cell should be explored, while a value of 0 indicates it should not be explored. We can model this grid as a graph that has a mix of nodes, where some can be visited while others cannot. Since some cells also have 0 values, the resulting graph can potentially be disconnected, meaning there may not be a path between every pair of nodes. Therefore, we may need to run a breadth-first search multiple times from different nodes.

![[Pasted image 20251130130528.png]]

![[Pasted image 20251130130540.png]]

We also create `queue` top hold pair of integers (coordinates of a node).

![[Pasted image 20251130130833.png]]

We then iterate in the `visited` array and in each iteration, check if the current cell (node) is marked `false` and the grid has a value 1 at that coordinate. If the condition holds `true`, we start breadth-first search from that cell by adding its coordinates (row, col) to the `queue`. If not, it means the node is either already visited or cannot be visited.

![[Pasted image 20251130130848.png]]

To start the breadth-first search, we iterate until `queue` is empty and in each iteration, extract the pair at the front of the `queue`. The pair denotes the coordinate of the current node, and we mark it as visited in the `visited` array. We then compute the coordinates of all its neighbouring nodes, iterate over those coordinates and in each iteration, check if the coordinate is within the bounds of the grid and has a value of 1. If it is within bounds, not marked as visited, and has a value of 1, we add the coordinate to the `queue` and continue to the next iteration.

![[Pasted image 20251130130607.png]]

This way we traverse the `grid` in breadth-frst order, starting from the start node. At the end of all iterations, all nodes reachable from the first node will have been visited. We then continue iteration in the `visited` array and repeat the process for all the nodes that have a value of 1 and have not yet been marked as visited. This way, at the end of all iterations, all nodes that can be visited will be visited.

The algorithm below summarises the breadth-first search on such a grid.

> **Algorithm**
> 
> **bfs(row, col, [ref] grid, [ref] visited)**
> 
> - **Step 1:** Create a queue `q` to hold coordinates
> - **Step 2:** Add the pair `(row, col)` to `q`
> - **Step 3:** Iterate while `q` is not empty and do the following:
>     - **Step 3.1:** Pop the coordinate at the front of `q` as `(currentRow, currentCol)`
>     - **Step 3.2:** Set `visited[currentRow][currentCol]` to `true`
>     - **Step 3.3:** Compute coordinates in all four (up, right, bottom, top) in `(newRow, newCol)` and for each, do the following:
>         - **Step 3.3.1:** If `(newRow, newCol)` is within the bounds of `grid` and `grid[newRow][newCol]` is `1` and `visited[newRow][newCol]` is `false`, do the following:
>             - **Step 3.3.1.1:** Add `(newRow, newCol)` to `q`
>             - **Step 3.3.1.2:** Set `visited[newRow][newCol]` to `true`
> 
> **callingFunction([ref] grid)**
> 
> - **Step 1:** Create a `visited` array of the same size as `grid` and initialize it to `false`
> - **Step 2:** Iterate in `grid` using `row` and `col` and do the following for each cell:
>     - **Step 2.1:** If `grid[row][col]` is `1` and `visited[row][col]` is `false`, call `bfs(row, col, grid, visited)`


### Implementation

To implement breadth-first search on a grid, we create a function `bfs`, that takes as arguments: the reference to the `visited` array and the coordinates (row, col) of a cell to identify a node uniquely. We create the `visited` array in the calling function to pass it by reference to `bfs`. For languages that don't support passing data by reference, we create it in the enclosing scope.

We create and use a temporary array `dir` to easily compute the coordinates of all potential neighbours.

```java
import java.util.*;

class Solution {
    public boolean isValidCell(int[][] grid, int row, int col) {
        // Check if a cell is valid and belongs to a region of 1's, also
        // check that the cell is not water
        return (
            row >= 0 &&
            row < grid.length &&
            col >= 0 &&
            col < grid[0].length &&
            grid[row][col] == 1
        );
    }

    public void bfs(
        int[][] grid,
        int row,
        int col,
        boolean[][] visited,
        List<List<Integer>> result
    ) {
        // Create a queue to perform breadth-first search
        Queue<int[]> queue = new LinkedList<>();

        // Add the current cell to the queue
        queue.add(new int[] { row, col });

        // Mark the current cell as visited
        visited[row][col] = true;

        // Define the possible movements: up, right, down, left
        int[][] directions = {
            {-1, 0}, // up
            {0, 1},  // right
            {1, 0},  // down
            {0, -1}  // left
        };

        // Perform BFS
        while (!queue.isEmpty()) {
            // Get the front cell from the queue
            int[] current = queue.poll();
            row = current[0];
            col = current[1];

            // Add the current cell to the result
            result.add(List.of(row, col));

            // Explore all possible movements
            for (int[] dir : directions) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];

                // If the neighbour is not visited, add it to the queue
                if (
                    isValidCell(grid, newRow, newCol) &&
                    !visited[newRow][newCol]
                ) {
                    // Add the new cell to the queue
                    queue.add(new int[] { newRow, newCol });

                    // Mark the new cell as visited
                    visited[newRow][newCol] = true;
                }
            }
        }
    }

    public List<List<Integer>> breadthFirstTraversalOnAGrid(
        int[][] grid
    ) {
        int rows = grid.length;

        // Check if the grid is empty
        if (rows == 0) {
            return new ArrayList<>();
        }

        int cols = grid[0].length;

        // Initialize a vector to store the result of the BFS
        // which will contain the coordinates of the cells visited
        // during the BFS traversal
        List<List<Integer>> result = new ArrayList<>();

        // Initialize visited array
        boolean[][] visited = new boolean[rows][cols];

        // Traverse each cell of the grid
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                // If the cells is not visitable or is already visited,
                // continue to the next cell
                if (grid[row][col] == 0 || visited[row][col]) {
                    continue;
                }

                // Perform BFS on this new cell to visit all the cells
                // connected to it.
                bfs(grid, row, col, visited, result);
            }
        }

        return result;
    }
}
```

# Cycle Detection

## Cycle Detection in an Undirected Graph

Graphs are composed of nodes connected via edges and are not restricted by any specific topology. Unlike a tree, which is a specialized graph as it is acyclic, a general graph can have cycles. A cycle in a graph is a path that starts and ends at the same node, has no repeated edges, and has at least three nodes. In this lesson, we will look at cycles in undirected graphs and learn the algorithm that can be used to detect such cycles.

![[Pasted image 20251206125415.png]]

### Algorithm

Detecting a cycle in an undirected graph is quite simple. We can piggyback on any traversal algorithm, like depth-first or breadth-first traversal, while keeping track of visited nodes. If we ever revisit a node during traversal, it means a cycle exists in the graph. We will learn more about the proof of correctness later in the lesson. In this explanation, we will use depth-first traversal to detect a cycle, as it is a simpler, more concise implementation.

We begin by creating a `visited` set to keep track of the nodes that have been visited. We then iterate through the list of nodes and for each node, check if it is already visited. If it is visited, we ignore it and proceed to the next node; otherwise, we perform a depth-first traversal from the node to detect if it is part of any cycle using a cycle detection function.

The reason we iterate through all the nodes is that the graph may be disconnected, and therefore, a depth-first traversal from a node may not visit all the nodes in the graph.

![[Pasted image 20251206125513.png]]

The cycle detection function is a slightly modified depth-first traversal algorithm that exits as soon as it detects a cycle. It accepts the identifier of the current node, the identifier of the parent node and the `visited` set as arguments, where the `visited` set is passed by reference. We pass the parent node to filter out the parent node from the neighbours, as undirected edges can be traversed both ways. Since the first node where the depth-first traversal starts does not have a parent, we pass a sentinel value that will never be a node identifier as the parent.

We pass the `visited` set by reference so that all recursive function calls share the same copy of the `visited` set. For languages that do not support passing data by reference, the visited set can be created in the enclosing scope to make it global for all function calls. The function returns a boolean value indicating the existence of a cycle.

![[Pasted image 20251206125623.png]]

As we enter a node, we add it to the `visited` set. We then iterate through all the neighbours of the node and in each iteration, check if the neighbour is already added to the `visited` set. If yes, it means the neighbour has already been visited, which means there is a cycle in the graph, and we return `true` to the parent node

![[Pasted image 20251206125648.png]]

Otherwise, we recursively call the cycle detection function (dfs) on the neighbour. If the recursive call to any neighbour returns `true`, we return the `true` value to the parent node without checking any other neighbour, as we have already confirmed the presence of a cycle. The parent node does the same, and the recursive calls all unwind to the top-level.

![[Pasted image 20251206125706.png]]

On the other hand, if no call to the cycle detection function returns a `true` value, all the iterations finish. In this case, we return `false` to the parent at the end of all iterations, indicating this node is not a part of any cycle.

This way, when the top-level call to the cycle detection function (dfs) ends in the calling function, the caller gets a boolean value indicating if a cycle containing the source node exists in the graph. If it does, we return `true` to the caller, ending the algorithm; otherwise, we continue the iteration and repeat the process for the next unvisited node. If at the end of all iterations, we don't get a `true` value even once, we return `false`, confirming there is no cycle in the graph.

The steps given below summarize the cycle detection algorithm in an undirected graph.

> **Algorithm**
> 
> **hasCycle(node, parent, [ref] graph, [ref] visited)**
> 
> - **Step 1:** Add `node` to `visited`
> - **Step 2:** Iterate in all the neighbours of `node` in `neighbour` and do the following:
>     - **Step 2.1:** If `neighbour` is not in `visited`
>         - **Step 2.1.1:** Call `hasCycle(neighbour, node, graph, visited)` and if its return value is `true`, return `true` to the parent
>     - **Step 2.2:** If `neighbour` is not `parent`, return `true` to the parent
> - **Step 3:** Return `false`
> 
> **callingFunction([ref] graph)**
> 
> - **Step 1:** Create a `visited` set
> - **Step 2:** Iterate in all the nodes of the graph using `node` and do the following:
>     - **Step 2.1:** If `node` is not in `visited`, call `hasCycle(node, -1, graph, visited)` and return `true` if it returns `true`
> - **Step 3:** Return `false`

### Implementation

```java
import java.util.*;

class Solution {
    public boolean hasCycle(List<List<Integer>> graph, int node, int parent, Set<Integer> visited) {
        visited.add(node);

        for (int neighbour : graph.get(node)) {
            if (!visited.contains(neighbour)) {
                if (hasCycle(graph, neighbour, node, visited)) {
                    return true;
                }
            } else if (neighbour != parent) {
                return true;
            }
        }

        return false;
    }

    public boolean detectCycleInUndirectedGraph(List<List<Integer>> graph) {
        Set<Integer> visited = new HashSet<>();

        for (int node = 0; node < graph.size(); node++) {
            if (!visited.contains(node)) {
                if (hasCycle(graph, node, -1, visited)) {
                    return true;
                }
            }
        }

        return false;
    }
}

```

## Cycle Detection in a Directed Graph

A directed graph is one where all edges can only be traversed in one direction. Similar to an undirected graph, a cycle in a directed graph is a path that starts and ends at the same node, has no repeated edges, and has at least three nodes. Unlike undirected graphs, revisiting an already visited node is not sufficient to confirm the existence of a cycle. In this lesson, we will look at cycles in directed graphs and learn the algorithm that can be used to detect such cycles.

![[Pasted image 20251206130317.png]]

### Algorithm

Detecting a cycle in a directed graph is very similar to that in an undirected graph, but there are some notable differences. In an undirected graph, revisiting a previously visited node while traversing the graph is sufficient to confirm the existence of a cycle. However, in a directed graph, the revisited node must be part of the currently traced path from the source node. If the revisited node is not in the currently traced path, we can ignore it and continue with the traversal. We will learn more about the proof of correctness later in the course.

![[Pasted image 20251206130334.png]]
Unlike cycle detection in an undirected graph, where any traversal algorithm can be used, for a directed graph, we can only use depth-first traversal, which keeps track of all nodes in the currently traced path in the function call stack. 

We begin by creating two sets `visited` and `nodesInPath` to keep track of the nodes that have been visited and the nodes in the currently traced path from the source, respectively. We then iterate through the list of nodes and for each node, check if it is already visited. If it is visited, we ignore it and proceed to the next node; otherwise, we perform a depth-first search from the node to detect if it is part of any cycle using a cycle detection function.

The reason we iterate through all the nodes is that a directed graph may not be fully connected. Depending on the node we we start the traversal, we may only be able to cover a part of the graph.

![[Pasted image 20251206130429.png]]

The cycle detection function is a slightly modified depth-first traversal algorithm that exits as soon as it detects a cycle. It accepts the identifier of the current node, the `visited` set and the `nodesInPath` set as arguments, where both sets are passed by reference.

We pass both sets by reference so that all recursive function calls share the same copy of the sets. For languages that do not support passing data by reference, the sets can be created in the enclosing scope to make them global for all function calls. The function returns a boolean value indicating the existence of a cycle.

As we enter a node, we add it to both the `visited` and `nodesInPath` set to mark it as visited and record it as being the currently traced path from the source, respectively.

![[Pasted image 20251206130443.png]]

We then iterate through all the neighbors of the node and in each iteration, check if the neighbor is already added to the `nodesInPath` set. If yes, it means there is a cycle in the graph, and we return `true` to the parent node. Otherwise, we check if the neighbor is already added to the `visited` set. If so, it means it was already visited via another path, and we can skip it.

![[Pasted image 20251206130458.png]]

If none of these conditions hold, we recursively call the cycle detection function (dfs) on the neighbour. If the recursive call to any neighbour returns `true`, we return the `true` value to the parent node without checking any other neighbour, as we have already confirmed the presence of a cycle. All iterations finish if a `true` value is not returned in any iteration. In this case, we remove the current node from `nodesInPath` set and return `false` to the parent, indicating this node is not a part of any cycle.

This way, when the top-level call to the cycle detection function (dfs) ends in the calling function, the caller gets a boolean value indicating if a cycle containing the source node exists in the graph. If it does, we return `true` to the caller, ending the algorithm; otherwise, we continue the iteration and repeat the process for the next unvisited node. If at the end of all iterations, we don't get a `true` value even once, we return `false`, confirming there is no cycle in the graph.

The steps given below summarize the cycle detection algorithm in a directed graph.

> **Algorithm**
> 
> **hasCycle(node, [ref] graph, [ref] nodesInPath, [ref] visited)**
> 
> - **Step 1:** Add `node` to `visited`
> - **Step 2:** Add `node` to `nodesInPath`
> - **Step 3:** Iterate in all the neighbours of `node` in `neighbour` and do the following:
>     - **Step 3.1:** If `neighbour` is not in `visited`
>         - **Step 3.1.1:** Call `hasCycle(neighbour, node, graph, nodesInPath, visited)` and if its return value is `true`, return `true` to the parent
>     - **Step 3.2:** If `neighbour` is in `nodesInPath`, return `true` to the parent
> - **Step 4:** Remove `node` from `nodesInPath`
> - **Step 5:** Return `false`
> 
> **callingFunction([ref] graph)**
> 
> - **Step 1:** Create a `visited` set
> - **Step 2:** Create a `nodesInPath` set
> - **Step 3:** Iterate in all the nodes of the graph using `node` and do the following:
>     - **Step 2.1:** If `node` is not in `visited`, call `hasCycle(node, graph, nodesInPath, visited)` and return `true` if it returns `true`
> - **Step 3:** Return `false`


```java
import java.util.*;

class Solution {
    public boolean hasCycle(List<List<Integer>> graph, int node, Set<Integer> visited, Set<Integer> nodesInPath) {
        visited.add(node);
        nodesInPath.add(node);

        for (int neighbour : graph.get(node)) {
            if (!visited.contains(neighbour)) {
                if (hasCycle(graph, neighbour, visited, nodesInPath)) {
                    return true;
                }
            } else if (nodesInPath.contains(neighbour)) {
                return true;
            }
        }

        nodesInPath.remove(node);
        return false;
    }

    public boolean detectCycleInDirectedGraph(List<List<Integer>> graph) {
        Set<Integer> visited = new HashSet<>();
        Set<Integer> nodesInPath = new HashSet<>();

        for (int node = 0; node < graph.size(); node++) {
            if (!visited.contains(node)) {
                if (hasCycle(graph, node, visited, nodesInPath)) {
                    return true;
                }
            }
        }

        return false;
    }
}
```

# Topological Sort

A graph can be used to model various problems involving relationships between entities and solve them efficiently. Often, when modelling problems using a graph, we end up with a directed graph that does not contain any cycles (a directed acyclic graph). Since these graphs are directed and don't have any cycles, we can define a linear ordering of their nodes such that each node appears before all the other nodes connected to it directly or indirectly via out-edges. Such an ordering is called the topological sort or topological ordering of the graph.

![[Pasted image 20251206133251.png]]

## Topological Sort Algorithm

The topological sort algorithm sorts the nodes of a graph in a topological order. For the algorithm to work, the graph should be a directed acyclic graph, as no topological order exists for a cyclic graph. Moreover, there can be many topological orders for a directed acyclic graph, and all of them can be correct. In this lesson, we will learn about the depth-first search-based algorithm used to find a topological order.

![[Pasted image 20251206133529.png]]

The topological sort algorithm is really simple to understand as it is only a series of depth-first searches. Every depth-first search discovers a section of the topological order of the entire graph. These individual sections are stitched together to get the topological order of the whole graph. We will learn more about the proof of correctness of the algorithm later in the lesson.

This topological sort algorithm only works for directed **acyclic** graphs and returns a topological order of nodes. There can be many correct topological orders for a graph and this graph only returns one of those.

We start by creating a `visited` set to perform depth-first search in the graph and a `result` list that will store the nodes of the graph in topological order.

We iterate through the list of nodes and, for each unvisited node, perform a depth-first search from it to visit all nodes reachable from it. We add a node to the `visited` set as we enter it and append it to the `result` list just before exiting. Once the depth-first search from a node ends, we continue the iterations to repeat the process for all the remaining unvisited nodes.

This way, at the end of the traversal, all nodes will be added to the `visited` set, and the `result` list will have the **reverse** topological order of the nodes. We finally reverse the `result` list to get the topological order of nodes in the graph. We will learn more about the proof of correctness of this algorithm later in the lesson.

The steps given below summarize the topological sort algorithm for a graph.

> **Algorithm**
> 
> **dfs(node, [ref] graph, [ref] visited, [ref] result)**
> 
> - **Step 1:** Add `node` to `visited` set
> - **Step 2:** Iterate over all the neighbours of `node` in a variable `neighbour` and do the following
>     - **Step 2.1:** If `neighbour` not in `visited` set call `dfs(neighbour, graph, visited, result)`
> - **Step 3:** Add `node` to `result` list
> 
> **topologicalSort([ref] graph)**
> 
> - **Step 1:** Create a `visited` set
> - **Step 2:** Create a `visitedresult` list
> - **Step 3:** Iterate over all the nodes in the graph in a variable `node` and do the following
>     - **Step 3.1:** If `node` not in `visited` set call `dfs(node, graph, visited, result)`
> - **Step 4:** Reverse the `result` list
> - **Step 5:** Return `result`

```java
import java.util.*;

class Solution {
    public void dfs(List<List<Integer>> graph, int node, Set<Integer> visited, List<Integer> result) {
        visited.add(node);
        for (int neighbour : graph.get(node)) {
            if (!visited.contains(neighbour)) {
                dfs(graph, neighbour, visited, result);
            }
        }
        result.add(node);
    }

    public List<Integer> topologicalSort(List<List<Integer>> graph) {
        int N = graph.size();
        if (N == 0) return new ArrayList<>();

        Set<Integer> visited = new HashSet<>();
        List<Integer> result = new ArrayList<>();

        for (int node = 0; node < N; node++) {
            if (!visited.contains(node)) {
                dfs(graph, node, visited, result);
            }
        }

        Collections.reverse(result);
        return result;
    }
}
```

# Single Source Shortest Path

The single source shortest path problem is the most common problem that can be modeled as a graph.

where all the edges have the same weight, a node at depth from the source will be at a greater distance, and it is easy to see how the breadth-first search from the source node can give the shortest path to all other nodes.

The breadth-first search visits the nodes in the order of their depth from the source. This is because, in BFS, we add all neighbors at depth `D` to the queue before adding neighbors at depth `D+1`, and the FIFO order of the queue guarantees that the front of the queue always has the smallest depth of any unvisited node.

We can start the breadth-first search from the source node and keep track of the depth as we traverse. The first time we visit a node, we are guaranteed to arrive at it through the shortest path, so we assign it a distance equal to the current depth. Since we keep track of visited nodes, we will not update the distance if we arrive at it at subsequent times.

Now, let's consider a real-world scenario in which the graph edges have different weights, with the weight of an edge representing the distance between two nodes. For such graphs, nodes at greater depths can have a smaller distance (sum of weights) from the source

The graph above is a very simplified representation of the situation. The road networks can be much more complicated, and the area considered may also span cities.

To efficiently solve the single-source shortest path problem from graphs with different edge weights, we need a special algorithm that visits nodes in the order of distance instead of their depth.

## Dijkstra's Algorithm

Dijkstra's algorithm is a single-source shortest path finding algorithm that can solve this problem for graphs ==with **non-negative** edge weights.== It is a generalized form of breadth-first search, using the same idea but generalizing the order of visiting nodes. The breadth-first search algorithm determines the order of nodes to visit based on their **depth** from the source node, whereas Dijkstra's algorithm does the same based on the **distance** from the source node.

The depth of a node is the minimum number of edges between itself and the source, whereas the distance is the minimum sum of edge weights between itself and the source. For an unweighted graph or a graph where all edge weights are the same, depth and distance mean the same thing and as we will see later, Dijkstra's algorithm will visit them in the same order as the breadth-first search

![[Pasted image 20251213110211.png]]

### Algorithm

To generalise the BFS algorithm into Dijkstra's algorithm, we use a **sorted set**, which is a binary search tree-based data structure, instead of a regular queue to always maintain a sorted list of nodes to visit. Instead of just the nodes, we add a pair consisting of the node and its currently known minimum distance from the source to the set, allowing us to access the pair with the minimum distance value easily.

To keep track of the shortest distance, we create a `distance` map and initialize it with 0 for the source node and `infinite` for all other nodes.

![[Pasted image 20251213110240.png]]We then create a sorted set `set` of distance, node pairs, and add all the distance node pairs from the `distance` map to the `set`. The set is first sorted by the first item in the pair, which is the currently known distance from the source node, and then by the node identifier itself. Since the `set` is sorted this way, the node with the shortest distance from the source is always at the beginning of the `set`.

![[Pasted image 20251213110253.png]]

We then iterate until the `set` is empty and, in each iteration, extract the distance node pair from the beginning of the `set`. The distance value for the extracted node `node` is its shortest distance from the source node, as we will see shortly in the proof of correctness.

We then iterate over all the neighbours of the extracted node `node` in a variable `neighbour` and calculate their distance from the source via `node` as `distance[node] + weight(node, neighbour)`. If the newly calculated distance for `neighbour` is smaller than the stored value in the `distance` map, we update the `distance` map and `set`.

Since `set` is always sorted, the distance node pair with the smallest distance makes its way to the beginning of the `set` after the update.

![[Pasted image 20251213110310.png]]

We repeat these steps until `set` is empty. Since we obtain the shortest distance of a node in each iteration, by the end of all iterations, we will have the shortest distance for all nodes in the `distance` map.

- Step 1: Create a map `distance` and initialize it with `infinite` for every node and 0 for the source node.
- Step 2: Create a sorted set `set` to hold a pair of (distance, node) and add all the (distance, node) pairs from the `distance` map to it.
- Step 3: Iterate until the `set` is empty and do the following:
    - Step 3.1: Get the (distance, node) pair with the smallest distance from the front of the `set`. The distance value of this `node` is its shortest distance from the source.
    - Step 3.2: For all neighbours of this node, calculate their distance via the extracted node as `distance[node]` + `edge weight` to the neighbour. If this value is less than `distance[neighbour]`, then update the `distance` map and corresponding (distance, node) pair in `set` with the new value.

We can see how BFS can now be considered a particular case of Dijkstra's algorithm, where all edges' weights are the same. In that case, a node's distance from the source becomes the same as its depth, and Dijkstra's algorithm follows the BFS order.

### Implementation

Although Dijkstra's algorithm is relatively straightforward, its implementation in its original form requires in-place updates in a sorted set to update distance values. The standard libraries in most programming languages do not provide this functionality in their implementations, so we need to use a binary search tree-based data structure to search, delete, and then insert to perform an update. This is not the most efficient way to implement Dijkstra's algorithm.

```java
import java.util.*;

// Comparator class for the priority queue to create a min-heap based on weight
class CompareMinHeap implements Comparator<List<Integer>> {
    @Override
    public int compare(List<Integer> a, List<Integer> b) {
        return Integer.compare(a.get(0), b.get(0));
    }
}

class Solution {
    public int[] dijikstrasAlgorithm(
        List<List<List<Integer>>> graph,
        int source
    ) {
        int N = graph.size();

        if (N == 0) {
            return new int[0];
        }

        int[] distance = new int[N];
        Arrays.fill(distance, Integer.MAX_VALUE);

        PriorityQueue<List<Integer>> pq =
            new PriorityQueue<>(new CompareMinHeap());

        distance[source] = 0;
        pq.add(List.of(0, source));

        while (!pq.isEmpty()) {
            int node = pq.poll().get(1);

            for (List<Integer> edge : graph.get(node)) {
                int neighbour = edge.get(0);
                int weight = edge.get(1);

                if (distance[node] != Integer.MAX_VALUE &&
                    distance[node] + weight < distance[neighbour]) {

                    distance[neighbour] = distance[node] + weight;
                    pq.add(List.of(distance[neighbour], neighbour));
                }
            }
        }

        for (int i = 0; i < distance.length; i++) {
            if (distance[i] == Integer.MAX_VALUE) {
                distance[i] = -1;
            }
        }

        return distance;
    }
}
```

## Negative Weight Edges

 many problems modeled as graphs may also have negative edge weights. To better understand these cases, let's look at a few real-world examples of such problems and how we can compute the single source shortest path for them.
Note that most problems modeled as graphs with negative edges are often directed graphs.

### Shortest path with Dijkastra's Algorithm

 To understand why Dijkstra's algorithm fails on graphs with negative edges, let's consider the graph above, modelling the stages of a chemical reaction and compute the shortest path from the source using Dijkstra's algorithm. In Dijkstra's algorithm, we start from the source and visit nodes in the increasing order of their distance from the source, and once we extract a node from the sorted set, we assign its distance value as the shortest distance to that node.

Since we only update distance values for nodes that are **in** the sorted set, if we reach a node that has already been extracted from the sorted set via a path that initially seemed longer but is overall smaller due to a large negative weight, we can no longer update its distance in the distance map. In graphs with negative-weight edges, the distance value for a node can decrease **later** in the iteration due to a negative weight in a path that seemed bigger initially. Consider the example below where Dikastr's algorithm finds the incorrect shortest path.

![[Pasted image 20251213112022.png]]

## Bellman-Ford Algorithm

The Bellman-Ford algorithm is a single-source shortest path-finding algorithm that can solve this problem for graphs with negative edge weights. **==Dijkastra's algorithm fails on graphs with negative edge weights because it assumes the first time we reach a node will always be via the shortest path.==** This assumption is valid for graphs with non-negative edge weights but not for those with negative edge weights. The Bellman-Ford algorithm overcomes this by calculating the shortest path for each node incrementally over multiple iterations and considering every path from the source to that node.

![[Pasted image 20251213112351.png]]

### Algorithm

The Bellman-Ford algorithm finds the shortest distance from the source to all nodes by starting from a base condition and relaxing the distance values of all nodes until it is no longer possible.

We start by creating a `distance` map to store the currently known shortest distance of a node and initialize it to `infinite` for each node and 0 for the source node, which acts as the base condition for the algorithm.  We then iterate through all the edges of the graph and, for each edge, check if it reduces the distance value of its destination node. For example, for an edge from node `u` to node `v` having a weight `w`, we check if `distance[u] + w < distance[v]` and update the `distance` map if the new distance is less than what was stored. This process is called **relaxing the edge** from the node `u` to node `v`.

![[Pasted image 20251213112410.png]]

After relaxing all the graph's edges, the `distance` map may have been modified for a few nodes. Consider that the node `u` is adjacent to nodes `a`, `b` and `c` while node `v` had nodes `x`, `y` and `z` as adjacent nodes. The distance value of nodes `a`, `b` and `c` may have been reduced, which could reduce the distance for the node `u`. Similarly, since the distance of the node `v` might have been reduced, which could reduce the distance value of the nodes `x`, `y`, and `z`.

![[Pasted image 20251213112429.png]]

So, some edges in the graph must be relaxed again to propagate the updates in the previous iteration to adjacent nodes. Since it is difficult to keep track of all the nodes that might be affected by a previous relaxation, we relax all the edges in the graph. This may result in the same situation again and hence, the process has to be repeated until the `distance` map is no longer updated, which can be a stopping condition for the algorithm.

However, if a graph has negative weight cycles, the iterations to relax the distances will repeat indefinitely, and we will never reach the stopping condition. This is because the distance values for some nodes in the cycle will be updated in each iteration.

![[Pasted image 20251213112443.png]]

The Bellman-Ford algorithm provides a stopping condition to detect a negative weight cycle in the graph. It is guaranteed to find the shortest path between the source and all nodes after **N-1** repetitions, where **N** is the number of nodes in the graph. If the number of repetitions exceeds this, we have a negative weight cycle, and Bellman-Ford can terminate. We will learn the proof of correctness for this later in the course.

> **Algorithm**
> 
> - Step 1: Create a `distance` map and initialize it to 0 for the source node and `infinite` for all other nodes.
> - Step 2: Iterate `N-1` times where `N` is the number of nodes and, in each iteration, do the following:
>     - Step 2.1: Iterate over all the edges (u, v) in the graph and do the following:
>         - Step 2.1.1: Update `distance[v]` if `distance[u]` + weight of edge from `u` to `v` < `distance[v]`
>     - Step 2.2: To check for negative weight cycle, iterate over all the edges (u, v) in the graph once and do the following:
>         - Step 2.2.1: If `distance[u]` + weight of edge from `u` to `v` < distance[v], terminate as graph has negative weight cycle
> - Step 3: The distance map now has the shortest distance of all nodes from the source.

### Implementation

```JAVA
import java.util.*;

class Solution {
    public int[] belmanFordAlgorithm(
        List<List<List<Integer>>> graph,
        int source
    ) {
        int N = graph.size();

        if (N == 0) {
            return new int[0];
        }

        int[] distance = new int[N];
        Arrays.fill(distance, Integer.MAX_VALUE);

        distance[source] = 0;

        for (int i = 0; i < N - 1; i++) {
            for (int node = 0; node < N; node++) {
                for (List<Integer> edge : graph.get(node)) {
                    int neighbour = edge.get(0);
                    int weight = edge.get(1);

                    if (distance[node] != Integer.MAX_VALUE &&
                        distance[node] + weight < distance[neighbour]) {
                        distance[neighbour] = distance[node] + weight;
                    }
                }
            }
        }

        for (int node = 0; node < N; node++) {
            for (List<Integer> edge : graph.get(node)) {
                int neighbour = edge.get(0);
                int weight = edge.get(1);

                if (distance[node] != Integer.MAX_VALUE &&
                    distance[node] + weight < distance[neighbour]) {
                    Arrays.fill(distance, -1);
                    return distance;
                }
            }
        }

        for (int i = 0; i < distance.length; i++) {
            if (distance[i] == Integer.MAX_VALUE) {
                distance[i] = -1;
            }
        }

        return distance;
    }
}
```

# All-pair Shortest Path Problem

The all-pair shortest path problem is the natural extension of the single source shortest path problem and is also a very common problem that can be modeled as a graph.

## Shortest Path With Dijkastra's Algorithm

Dijkastra's algorithm to find the shortest path from a single source node to all the other nodes in the graph. Running the algorithm for each node as the source will give us the shortest path between all pairs of nodes. Since we run Dijkastra's algorithm **N** times where **N** is the number of nodes and **E** is the number of edges in the graph, the time complexity would be **O (N*E*logN)**. In the worst case, if the graph is a complete graph, the number of edges E ~ N^2 and and so time complexity will be O(N^3 * logN).

![[Pasted image 20251214112027.png]]

While this is one effective way to solve the all-pair shortest path problem, it would not work for graphs with negative weight edges.

## Shortest Path with Bellman-Ford Algorithm

We can use the Bellman-Ford algorithm to find the shortest path from a source node to all the other nodes in a graph with negative edge weights. Running the algorithm for each node as the source will give us the shortest path between all pairs of nodes. Since we run the Bellman-Ford algorithm **N** times where **N** is the number of nodes and **E** is the number of edges in the graph, the time complexity would be **O (N*N*E)**.

![[Pasted image 20251214112122.png]]

Running the Bellman-Ford algorithm multiple times may seem an effective solution, but in the worst case (complete graphs), a graph can have N*(N-1), where N is the number of nodes. This results in the worst-case time complexity of **O (N*N*N*N) = O(N^4)**.

## Floyd-Warshall Algorithm

The Floyd-Warshall algorithm efficiently solves the all-pairs shortest path problem for directed and undirected graphs. It can work with negative edges, but cannot detect negative weight cycles like Bellman-Ford.

### Algorithm

The idea behind the Floyd-Warshall algorithm is quite simple. Consider two nodes, `s`, and `t`, in the graph representing the source and destination nodes, respectively. The shortest path between these nodes can have 0 more intermediate nodes. For each such pair of nodes in the graph, the Floyd-Warshall algorithm iterates over all the nodes in the graph and for each node, checks if it exists as an intermediate node in the shortest path between the pair.

![[Pasted image 20251214112529.png]]

We create a two-dimensional distance map where `distance[s][t]` stores the **current** shortest path between the nodes `s` and `t`. We initialize the map with 0 for the same pair of nodes (where `s` and `t` are the same), the weight of the edge if an edge connects the pair and `infinite` for all the other pairs. This is our base case, where the `distance` map stores the shortest distance between all pairs of nodes if there are 0 intermediate nodes.

Now, we iterate over the list of nodes in the graph, where in the `ith` iteration we consider all nodes from 0 to `i` as intermediate nodes for all pairs of nodes in the graph. In each iteration, we check for every pair of nodes `s` and `t`, if adding the node `i` as an intermediary node reduces the **currently** known shortest distance between them. We do this by checking if `distance[s][i] + distance[i][t] < distance[s][t]`. If the distance is reduced, we update the `distance` map for the node pair `s` and `t`  to the smaller value, signifying that the **currently** known shortest path has the node `i` in it; otherwise, we move to the next pair.

Once we have checked this for all the pairs in the graph, we can move to the next node, `i+1`, and repeat the same process. Once we finish checking all the nodes, it is guaranteed that the `distance` map will have the shortest path between all pairs of nodes in the graph. We will learn the proof of correctness for this later in the course.

> **Algorithm**
> 
> - **Step 1**: Create a 2D `distance` map and initialize it with 0 for the same node pair, edge weights for node pairs with edges between them, and `infinite` for all other node pairs.
> - **Step 2**: Iterate over all the nodes using the variable `i` representing the intermediate node:
>     - **Step 2.1**: Iterate over all the nodes using the variable `s` representing the source node:
>         - **Step 2.1.1**: Iterate over all the nodes using the variable `t` representing the target node
>             - **Step 2.1.1.1**: if `distance[s][i] + distance[i][t]` < `distance[s][t]` update `distance[s][t]` with this new minimum value
> - **Step 3**: The `distance` map now has the shortest distance between all the pairs of nodes


### Implementation

Consider that we have a graph of size **N**, where the nodes are enumerated from **0** to **N-1**, and we are given the adjacency list `adj` of the graph as a two-dimensional list of pairs where the first value of the pair is the enumeration of the neighbouring node, and the second value is the weight of the edge. Since nodes can be identified by their enumeration, which runs from **0** to **N-1** instead of creating a `distance` map, we can create a `distance` array and use the node enumerations as indices to store and retrieve values from it.

Implementing the Floyd-Warshall algorithm is simple, as it only involves three nested iterations. We create a 2D `distance` array and initialize it to 0 for the same node pairs, edge weights for nodes that have edges between them, and infinite for all other nodes. We then iterate over all nodes in the graph in a loop that selects the intermediate node to check. We create a nested loop inside the outer loop to compute all possible pairs in the graph and check if the intermediate node can be added to that pair.

```java
import java.util.*;

class Solution {
    public int[][] floydWarshallAlgorithm(
        List<List<List<Integer>>> graph
    ) {
        int N = graph.size();
        int[][] distance = new int[N][N];

        for (int node = 0; node < N; node++) {
            for (int neighbour = 0; neighbour < N; neighbour++) {
                distance[node][neighbour] = -1;
            }

            distance[node][node] = 0;

            for (List<Integer> edge : graph.get(node)) {
                int neighbour = edge.get(0);
                int weight = edge.get(1);
                distance[node][neighbour] = weight;
            }
        }

        for (int k = 0; k < N; k++) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    if (distance[i][k] != -1 && distance[k][j] != -1) {
                        if (distance[i][j] == -1 ||
                            distance[i][j] >
                            distance[i][k] + distance[k][j]) {
                            distance[i][j] =
                                distance[i][k] + distance[k][j];
                        }
                    }
                }
            }
        }

        return distance;
    }
}
```

# Max-flow Min-cut Theorem

The max flow problem is another common class of problems that can be modeled as a graph. The goal is to find the maximum flow through a flow network, a directed graph in which each edge has a capacity and receives flow. The amount of flow in the edge is capped by its capacity. The flow network has two special nodes, the source and the sink, where the flow starts and terminates. For all nodes except the source and the sink, there is a **conservation of flow**, which means the amount of flow going into a node should be the same as the flow coming out of it. The following example shows a simple flow network with the source and sink nodes and the capacity of edges.

![[Pasted image 20251214112737.png]]

The goal of the maximum flow problem is to find the maximum flow that can go through the network from the source node to the sink node.

## Residual graph

In a flow network with some flow f from the source to the sink node, the capacity of all edges with flow is reduced. The remaining capacity of such edges is called their residual capacity. A graph representing the flow network with the residual capacity of its edges is called a residual graph.

A residual graph also has reverse edges between nodes with some flow in them, and the residual capacity of these reverse edges is the total flow in the forward edge. We will learn later why these reverse edges are so crucial when we learn how to find the maximum flow in a flow network.

![[Pasted image 20251214112824.png]]

## Augmenting path

In a flow network with some flow `f` from the source to the sink node; an augmenting path is a simple path from the source node to the sink node in the residual graph. The maximum flow that can be augmented through an augmenting path is the minimum residual capacity of all its edges. And so, if we augment flow `fp` through an augmenting path, the total flow in the network becomes `f + fp`.

![[Pasted image 20251214112845.png]]

## Cut

A cut of the flow network denoted by `cut(S, T)`, partitions the graph's nodes into two disjoint sets, `S`, and `T`, such that the set `S` contains the source node and the set `T` contains the sink node.

![[Pasted image 20251214112916.png]]

![[Pasted image 20251214112925.png]]

### Capacity of a cut

The capacity of a cut `capacity(S, T)` is the sum of the capacity of all edges from nodes in the set `S` to nodes is set `T` in the `cut(S, T)` of a flow network.

## Ford-Fulkerson Method

The Ford-Fulkerson method uses the max-flow min-cut theorem to solve the maximum flow problem for flow networks. It is called a method because some parts of its protocol do not specify implementation. A method is a more general algorithm where individual steps can be implemented differently. For the Ford-Fulkerson method to work, a graph should have at least one source and sink node, where the maximum flow must be calculated from the source to the sink

### Algorithm

The Ford-Fulkerson method starts by initialising a variable `maxFlow` to 0 and repeatedly tries to find an augmenting path in the residual graph. If an augmenting path is found, it gets the minimum capacity of the edges in the augmenting path in a variable `pathFlow` and adds it to `maxFlow`. It then simulates the flow (`pathFlow`) through the augmenting path in the residual graph to generate a new residual graph for the next iteration. This process is repeated until an augmenting path can no longer be found, at which point the value in `maxFlow` denotes the maximum possible flow in the graph.

We start the method by initializing a variable `maxFlow` which keeps track of the maximum flow in the graph. Then, we initialize the first residual graph `residualGraph` and set the capacity of all edges equal to the capacity of the edges in the input graph.

![[Pasted image 20251214113545.png]]

We then start from the source node and try to find a path to the sink node where all the edges have non-zero residual capacity (augmenting path). Ford Fulerkson's method does not specify the algorithm for finding the path. We will use a depth-first search to illustrate this example.

It is important to note that multiple augmenting paths could be present in the graph, but a depth-first search will choose the first one it finds.

![[Pasted image 20251214113601.png]]

Consider that we chose the augmenting path `1` from the example. Once we choose a path, we find the maximum flow that can pass through it, which is the minimum of the residual capacities of its edges in a variable `pathFlow`.

Once we find the maximum flow possible through the augmenting path (`pathFlow`), we simulate the flow by reducing `pathFlow` from the residual capacity of all edges in the augmenting path, and add it to `maxFlow`.

We also add **reverse edges** along the augmenting path with the same capacity as the simulated flow (`pathFlow`) in the `residualGraph`. These reverse edges can be used in an augmenting path in some later iteration and allow for reorienting the flow in the graph. Simulating flow in a reverse edge means reducing the same flow from the real edge between the corresponding nodes. We will learn more about reverse edges and why they are crucial later in this course.

Once we have added reverse edges, we get a new residual graph that can be used for the next iteration.

In the next iteration, once again, we try to find an augmenting path in the `residualGraph`. We perform a depth-first search to find paths from the source to the sink with some residual capacity; this time, also exploring paths via the reverse edges. Note that just like before, there may be other augmenting paths, but we chose any one of them.

Once we find an augmenting path in the residual graph, we again find the maximum flow that can pass through it, which is the minimum of the residual capacities of its edges and store it in the variable `pathFlow`.

We then simulate the flow by reducing `pathFlow` from the residual capacity of all edges in the augmenting path, and add it to `maxFlow`.

We also add **reverse edges** along the augmenting path with the same capacity as the simulated flow (`pathFlow`) in the `residualGraph`.

Once we have added reverse edges, we get a new residual graph that can be used for the next iteration.

We repeat the same steps to find an augmenting path in `residualGraph` and simulate flow in it until an augmented path can no longer be found. When an augmenting path can no longer be found, the value of `maxFlow` will be the maximum possible flow in the graph.

The steps below summarize the Ford-Fulkerson's method using a residual graph implemented as an adjacency matrix.

> **Algorithm**
> 
> **dfs([ref] residualGraph, [re] visited, [ref] path, node, sink)**
> 
> - **Step 1:** Add `node` to `visited` set
> - **Step 2:** Append `node` to `path`
> - **Step 3:** if `node` is `sink` return `true`
> - **Step 4:** Iterate over all the neighbours of `node` in a variable `neighbour` and do the following
>     - **Step 4.1:** If `neighbour` not in `visited` and `residualGraph[node][neighbour]` > 0 do the following:
>         - **Step 4.1.1:** If the call to `dfs(residualGraph, visited, path, neighbour, sink)` returns `true`, return `true`
> - **Step 5:** Pop the `node` from the end of `path`
> - **Step 6:** Return `false`
> 
> **fordFulkersonMethod([ref] graph, source, sink)**
> 
> - **Step 1:** Create a two-dimensional array `residualGraph` to hold the adjacency matrix of the residual graph
> - **Step 2:** Initialize `residualGraph` with the weights between nodes in `graph`
> - **Step 3:** Initialize a variable `maxFlow` to 0
> - **Step 4:** Iterate while call to `dfs(residualGraph, visited, path, source, sink)` returns true:
>     - **Step 4.1:** Initilize a variable `pathFlow` to `infinite`
>     - **Step 4.2:** Iterate in `path` taking two items at a time in variables `u` and `v` and for each do the following:
>         - **Step 4.2.1:** Set `pathFlow` to `min(pathFlow, residualGraph[u][v])`
>     - **Step 4.3:** Iterate in `path` taking two items at a time in variables `u` and `v` and for each do the following:
>         - **Step 4.3.1:** Reduce `pathFlow` from `residualGraph[u][v]`
>         - **Step 4.3.2:** Add `pathFlow` to `residualGraph[v][u]`
>     - **Step 4.4:** Add `pathFlow` to `maxFlow`
> - **Step 5:** Return `maxFlow`


### Implementation

onsider that we have a graph of **N** nodes, where the nodes are enumerated from **0** to **N-1**, and we are given the adjacency list of the graph as a two-dimensional list of pairs `graph`, where the first item in the pair is the enumeration of the neighbouring node and the second item is the weight (capacity) of the edge.

We implement the residual graph as an adjacency matrix by creating a two-dimensional array `residualGraph` and initialize it by setting the capacity of edges between nodes to the same as the input `graph`.

The reason we store it as an adjacency matrix and not a list is that it simplifies the addition of forward and reverse edges and manipulating weights.

We create a `dfs` function that finds an augmenting path in the `residualGraph` and returns a boolean `true` or `false` and is call it repeatedly until it returns `false`. In each iteration, we pass it an empty `visited` set and an empty `path` list, and it tries to find an augmenting path in the `residualGraph`.

If it finds a path, the nodes in the path are added in the correct order to the `path` , list which is then used to find the maximum possible flow that can be simulated through it in `pathFlow`.

The `residualGraph` is then updated by simulating `pathFlow` through it, `pathFlow` is added to `maxFlow` and all variables (`pathFlow`, `visited`, `path`) are reset for the next iteration. At the end of all iterations, we get the maximum flow in `maxFlow`.

```java
import java.util.*;

class Solution {
    public boolean dfs(
        int[][] residualGraph,
        Set<Integer> visited,
        List<Integer> path,
        int node,
        int sink
    ) {
        visited.add(node);
        path.add(node);

        if (node == sink) {
            return true;
        }

        for (int neighbour = 0;
             neighbour < residualGraph.length;
             neighbour++) {

            if (!visited.contains(neighbour) &&
                residualGraph[node][neighbour] > 0) {

                if (dfs(residualGraph, visited, path, neighbour, sink)) {
                    return true;
                }
            }
        }

        path.remove(path.size() - 1);
        return false;
    }

    public int maximumFlow(
        List<List<List<Integer>>> graph,
        int source,
        int sink
    ) {
        int N = graph.size();

        if (N == 0) {
            return 0;
        }

        int[][] residualGraph = new int[N][N];
        for (int node = 0; node < N; node++) {
            for (List<Integer> edge : graph.get(node)) {
                int neighbour = edge.get(0);
                int capacity = edge.get(1);
                residualGraph[node][neighbour] = capacity;
            }
        }

        int maxFlow = 0;

        while (true) {
            Set<Integer> visited = new HashSet<>();
            List<Integer> path = new ArrayList<>();

            if (!dfs(residualGraph, visited, path, source, sink)) {
                break;
            }

            int pathFlow = Integer.MAX_VALUE;
            for (int i = 0; i < path.size() - 1; i++) {
                int u = path.get(i);
                int v = path.get(i + 1);
                pathFlow = Math.min(pathFlow, residualGraph[u][v]);
            }

            for (int i = 0; i < path.size() - 1; i++) {
                int u = path.get(i);
                int v = path.get(i + 1);
                residualGraph[u][v] -= pathFlow;
                residualGraph[v][u] += pathFlow;
            }

            maxFlow += pathFlow;
        }

        return maxFlow;
    }
}

```

# Maximum Bipartite Matching Problem

 bipartite graph is a graph whose nodes can be divided into two disjoint sets, L and R, so all edges connect nodes from one set to another. Bipartite graphs arise naturally when we try to model relationships between two different classes of objects, and their structured nature allows us to model many real-life problems using them. They are most commonly used in optimization problems where we want to maximize fixed resource usage among some users.
![[Pasted image 20251214123726.png]]

## Matching in bipartite graphs

Consider a bipartite graph where nodes are divided into disjoint sets, L and R connected by some edges. A matching in the graph is defined as a subset of edges such that all nodes have **at most** one edge incident on them. Conversely, matching is a subset of edges where no two edges share the same node. A matching in the bipartite graph can leave some nodes with no edges incident on them, but it cannot have more than one edge incident on any node.

Naturally, a bipartite graph can have multiple matching. The number of edges in the matching is also called the cardinality of the matching. Consider a bipartite graph below and all its matching.

A maximum matching in a bipartite graph is a matching with a maximum number of edges. Meaning it is the matching with the maximum cardinality. A bipartite graph can have multiple maximum matchings since there can be multiple matchings with the same cardinality.

The maximum bipartite matching problem can be solved by converting it into a maximum flow problem. To solve the problem, we create the corresponding flow network for the bipartite graph and run an algorithm to find the maximum flow in the flow network. The maximum flow in the flow network is the maximum matching of the bipartite graph. We will prove this later in the course.

Consider a bipartite graph with nodes separated in two disjoint sets, `L` and `R`, with some edges connecting nodes in these sets.

## Algorithm

The first step in solving the maximum bipartite matching problem is to create the corresponding flow network of the bipartite graph. We define a corresponding flow network for the graph by adding a source and sink node, where the source has a directed edge towards all nodes in the set `L`, edges between nodes in the sets `L` and `R` are converted to directed edges, and all nodes in the set `R` have a directed edge towards the sink. All edges in the flow network are set to have a capacity of 1 unit.

![[Pasted image 20251214123821.png]]
he next step is to find the maximum flow in the flow network as that will also be the maximum matching of the bipartite graph. We can find the maximum flow using any algorithm; however, in this lesson, we will use the Ford-Fulkerson method that we learnt earlier in the course.

The Ford-Fulkerson method is already explained in an earlier lesson and so we don't repeat it in this section.

The steps below summarize the algorithm to find the maximum bipartite matching using the Ford-Fulkerson method.

> **Algorithm**
> 
> **dfs([ref] residualGraph, [re] visited, [ref] path, node, sink)**
> 
> - **Step 1:** Add `node` to `visited` set
> - **Step 2:** Append `node` to `path`
> - **Step 3:** if `node` is `sink` return `true`
> - **Step 4:** Iterate over all the neighbours of `node` in a variable `neighbour` and do the following
>     - **Step 4.1:** If `neighbour` not in `visited` and `residualGraph[node][neighbour]` > 0 do the following:
>         - **Step 4.1.1:** If the call to `dfs(residualGraph, visited, path, neighbour, sink)` returns `true`, return `true`
> - **Step 5:** Pop the `node` from the end of `path`
> - **Step 6:** Return `false`
> 
> **fordFulkersonMethod([ref] graph, source, sink)**
> 
> - **Step 1:** Create a two-dimensional array `residualGraph` to hold the adjacency matrix of the residual graph
> - **Step 2:** Initialize `residualGraph` with the weights between nodes in `graph`
> - **Step 3:** Initialize a variable `maxFlow` to 0
> - **Step 4:** Iterate while call to `dfs(residualGraph, visited, path, source, sink)` returns true:
>     - **Step 4.1:** Initilize a variable `pathFlow` to `infinite`
>     - **Step 4.2:** Iterate in `path` taking two items at a time in variables `u` and `v` and for each do the following:
>         - **Step 4.2.1:** Set `pathFlow` to `min(pathFlow, residualGraph[u][v])`
>     - **Step 4.3:** Iterate in `path` taking two items at a time in variables `u` and `v` and for each do the following:
>         - **Step 4.3.1:** Reduce `pathFlow` from `residualGraph[u][v]`
>         - **Step 4.3.2:** Add `pathFlow` to `residualGraph[v][u]`
>     - **Step 4.4:** Add `pathFlow` to `maxFlow`
> - **Step 5:** Return `maxFlow`
> 
> **maximumBipartiteMatching([ref] graph, [ref] left, [ref] right)**
> 
> - **Step 1:** Create a two-dimensional list of pairs `flowGraph` with the same size as `graph`
> - **Step 2:** Iterate in `graph` using a variable `node` and do the following:
>     - **Step 2.1:** Iterate in `graph[node]` using a variable `neighbur` and do the following:
>         - **Step 2.1.1:** Append a pair `(neighbour, 1)` to `flowGraph[node]`
> - **Step 3:** Set a variable `source` to the size `flowGraph` and append an empty list of pairs at the end of `flowGraph`
> - **Step 4:** Iterate in the list `left` using a variable `node` and do the following:
>     - **Step 4.1:** Append a pair `(node, 1)` to `flowGraph[source]`
> - **Step 5:** Set a variable `sink` to the size `flowGraph` and append an empty list of piars at the end of `flowGraph`
> - **Step 6:** Iterate in the list `right` using a variable `node` and do the following:
>     - **Step 6.1:** Append a pair `(sink, 1)` to `flowGraph[node]`
> - **Step 7:** Set a variable `maxMatching` as the return value of call to `fordFulkersonMethod([ref] flowGraph, source, sink)`
> - **Step 8:** Return `maxMatching`

## Implementation

Consider that we have a bipartite graph of **N** nodes, where the nodes are enumerated from **0** to **N-1**, and we are given the adjacency list of the graph as a two-dimensional list `graph`. We are also given two lists, `left` and `right`, containing the nodes in the left and right disjoint sets.

We create the corresponding `flowGraph` as a two-dimensional list of pairs where the first item in the pair is the enumeration of the neighbouring node, and the second item is the weight (capacity) of the edge. We then copy all the edges from `graph` in `flowGraph` with a capacity 1. We also create a `source` and a `sink` node in the `flowGraph` and connect them to the respective nodes in the `left` and `right` sets.

We then run the Ford-Fulkerson method on the `flowGraph` to find the maximum flow from the `source` node to the `sink` node and return the result as the maximum matching.

```java
import java.util.*;

class Solution {

    boolean dfs(
        int[][] residualGraph,
        Set<Integer> visited,
        List<Integer> path,
        int node,
        int sink
    ) {
        // Mark the current node as visited in the graph to avoid
        // visiting it again
        visited.add(node);

        // Add the current node to the path
        path.add(node);

        // If the current node is the sink, return true
        if (node == sink) {
            return true;
        }

        // Explore all neighbours of the current node
        for (int neighbour = 0;
             neighbour < residualGraph.length;
             neighbour++) {

            // If the neighbour is not visited and has a positive
            // capacity in the residual graph, recursively call DFS
            if (!visited.contains(neighbour) &&
                residualGraph[node][neighbour] > 0) {

                // If the DFS call returns true, propagate the result
                // back to the previous call
                if (dfs(residualGraph, visited, path, neighbour, sink)) {
                    return true;
                }
            }
        }

        // If no path to the sink is found, remove the current node
        // from the path
        path.remove(path.size() - 1);

        // If no path to the sink is found from this node, backtrack
        return false;
    }

    int maximumFlow(
        List<List<int[]>> graph,
        int source,
        int sink
    ) {
        // Number of nodes in the graph
        int N = graph.size();

        // If the graph is empty, return 0
        if (N == 0) {
            return 0;
        }

        // Create a residual graph and initialize it with the original
        // capacities
        int[][] residualGraph = new int[N][N];
        for (int node = 0; node < N; node++) {
            for (int[] edge : graph.get(node)) {
                int neighbour = edge[0];
                int capacity = edge[1];
                residualGraph[node][neighbour] = capacity;
            }
        }

        // Initialize the maximum flow
        int maxFlow = 0;

        // Find augmenting paths in the residual graph using
        // Depth-First Search
        while (true) {

            // Create a set to keep track of visited nodes
            Set<Integer> visited = new HashSet<>();

            // Vector to store the path from source to sink
            List<Integer> path = new ArrayList<>();

            // If no more augmenting paths exist, break
            if (!dfs(residualGraph, visited, path, source, sink)) {
                break;
            }

            // Find the minimum capacity along the augmenting path
            int pathFlow = Integer.MAX_VALUE;
            for (int i = 0; i < path.size() - 1; i++) {
                int u = path.get(i);
                int v = path.get(i + 1);
                pathFlow = Math.min(pathFlow, residualGraph[u][v]);
            }

            // Update the residual capacities and reverse edges along the
            // augmenting path
            for (int i = 0; i < path.size() - 1; i++) {
                int u = path.get(i);
                int v = path.get(i + 1);
                residualGraph[u][v] -= pathFlow;
                residualGraph[v][u] += pathFlow;
            }

            // Add the path flow to the maximum flow
            maxFlow += pathFlow;
        }

        return maxFlow;
    }

    int maximumBipartiteMatching(
        List<List<Integer>> graph,
        List<Integer> left,
        List<Integer> right
    ) {
        List<List<int[]>> flowGraph = new ArrayList<>();

        for (int i = 0; i < graph.size(); i++) {
            flowGraph.add(new ArrayList<>());
        }

        // Copy the connections from the input graph
        // to the flow graph with capacity 1
        for (int node = 0; node < graph.size(); node++) {
            for (int neighbour : graph.get(node)) {
                flowGraph.get(node).add(new int[]{neighbour, 1});
            }
        }

        // Get the index of the source node that will be added later
        int source = flowGraph.size();
        flowGraph.add(new ArrayList<>());

        // Connect the source node to all nodes
        // in the left partition with capacity 1
        for (int node : left) {
            flowGraph.get(source).add(new int[]{node, 1});
        }

        // Get the index of the sink node that will be added later
        int sink = flowGraph.size();
        flowGraph.add(new ArrayList<>());

        // Connect all nodes in the right partition
        // to the sink node with capacity 1
        for (int node : right) {
            flowGraph.get(node).add(new int[]{sink, 1});
        }

        // Call the Ford-Fulkerson maximum flow function to compute the
        // result
        return maximumFlow(flowGraph, source, sink);
    }
}
```