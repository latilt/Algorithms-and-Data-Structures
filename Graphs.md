# Graphs
## What are Graphs
A graph data structure consists of a finite (and possibly mutable) set of vertices or nodes or points, together with a set of unordered pairs of these vertices for an undirected graph or a set of ordered pairs for a directed graph.
Nodes + Connections
## Uses for Graphs
* Social Networks
* Location / Mapping
* Routing Algorithms
* Visual Hierarchy
* File System Optimizitions
## Types of Graphs
* Directed Graph
* Undirected Graph
* Weighted Graph
## Representing a graph
* Adjacency Matrix
* Adjacency List
## Difference and Big O of Adjacency List and Matrix
[V] - number of vertices
[E] - number of edges
Operation | Adjacency List | Adjacency Matrix |
--------- | -------------- | ---------------- | 
Add Vertex | O(1) | O([V^2])
Add Edge | O(1) | O(1)
Remove Vertex | O([V] + [E]) | O([V^2])
Remove Edge | O([E]) | O(1)
Query | O([V] + [E]) | O(1)
Storage | O([V] + [E]) | O([V^2])

Adjacency List | Adjacency Matrix |
--- | --- |
Can take up less space (in sparse graphs) | Takes up more space (in sparse graphs) |
Faster to iterate over all edges | Slower to iterate over all edges |
Can be slower to lookup specific edge | Faster to lookup specific edge |
## We use an Adjacency List
Most data in the real-world tends to lend itself to sparser and/or larger graphs.
## Graph Class
We are building an undirected graph.
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
}
```
### Adding a Vertex
* Write a method called addVertex, which accepts a name of a vertex
* It should add a key to the adjacency list with the name of the vertex and set its value to be and empty array
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
}
```
### Adding an Edge
* This function should accept two vertices, we can call them vertex1 and vertex2
* The function should find in the adjacency list the key of vertex1 and push vertex2 to the array
* The function should find in the adjacency list the key of vertex2 and push vertex1 to the array
* Don't worry about handling errors/invalid vertices
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
    addEdge(v1, v2) {
        this.adjacencyList[v1].push(v2);
        this.adjacencyList[v2].push(v1);
    }
}
```
### Removing an Edge
This function should accept two vertices, we'll call them vertex1 and vertex2
The function should reassign the key of vertex1 to be an array that does not contain vertex2
The function should reassign the key of vertex2 to be an array that does not contain vertex1
Don't worry about handing errors/invalid vertices
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
    addEdge(v1, v2) {
        this.adjacencyList[v1].push(v2);
        this.adjacencyList[v2].push(v1);
    }
    removeEdge(vertex1, vertex2) {
        this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(
            v => v !== vertex2
        );
        this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(
            v => v !== vertex1
        );
    }
}
```
### Removing a Vertex
The function should accept a vertex to remove
The function should loop as long as there are any other vertices in the adjacency list for that vertex
Inside of the loop, call our removeEdge function with the vertex we are removing and any values in the adjacency list for that vertex
delete the key in the adjacency list for that vertex
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
    addEdge(v1, v2) {
        this.adjacencyList[v1].push(v2);
        this.adjacencyList[v2].push(v1);
    }
    removeEdge(vertex1, vertex2) {
        this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(
            v => v !== vertex2
        );
        this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(
            v => v !== vertex1
        );
    }
    removeVertex(vertex) {
        while(this.adjacencyList[vertex].length) {
            const adjacencyVertex = this.adjacencyList[vertex].pop();
            this.removeEdge(vertex, adjacencyVertex);
        }
        delete this.adjacencyList[vertex];
    }
}
```