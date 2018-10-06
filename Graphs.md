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
## Essential graph terms
* Vertex - a node
* Edge - connection between nodes
* Weighted/Unweighted - values assigned to distances between vertices
* Directed/Undirected - directions assigned to distances between vertices
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
# Graph Traversal
## Graph Traversal Uses
* Peer to peer networking
* Web crawlers
* Finding "closest" matches/recommendations
* Shortest path problems
    * GPS Navigation
    * Solving mazes
    * AI (shortest path to win the game)
## Depth First
Explore as far as possible down one branch before "backtracking"
### Recursive DFS Pseudocode
```
DFS(vertex):
    if vertex is empty
        return (this is base case)
    add vertex to results list
    mark vertex as visited
    for each neighbor in vertex's neighbors:
        if neighbor is not visited:
            recursively call DFS on neighbor
```
* The function should accept a starting node
* Create a list to store the end result, to be returned at the very end
* Create an object to store visited vertices
* Create a helper function which accepts a vertex
    * The helper function should return early if the vertex is empty
    * The helper function should place the vertex it accepts into the visited object and push that vertex into the result array
    * Loop over all of the values in the adjacencyList for that vertex
    * If any of those values have not been visited, recursively invoke the helper function with that vertex
* Invoke the helper function with the starting vertex
* Return the result array
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        /* */
    }
    addEdge(v1, v2) {
        /* */
    }
    removeEdge(vertex1, vertex2) {
        /* */
    }
    removeVertex(vertex) {
        /* */
    }
    depthFirstRecursive(start) {
        const result = [];
        const visited = {};
        const adjacencyList = this.adjacencyList;

        (function dfs(vertex) {
            if(!vertex) return null;
            visited[vertex] = true;
            result.push(vertex);
            adjacencyList[vertex].forEach(neighbor => {
                if(!visited[neighbor]) {
                    return dfs(neighbor);
                }
            });
        })(start);

        return result;
    }
}
```
### Iterative DFS Pseudocode
```
DFS-iterative(start):
    let S be a stack
    S.push(start)
    while S is not empty
        vertex = S.pop()
        if vertex is not labeled as discovered:
            visit vertex (add to result list)
            label vertex as discovered
            for each of vertex's neighbors, N do
                S.push(N)
```
* The function should accept a starting node
* Create a stack to help use keep track of vertices (use a list/array)
* Create a list to store the end result, to be returned at the very end
* Create an object to store visited vertices
* Add the starting vertex to the stack, and mark it visited
* Whild the stack has something in it:
    * Pop the next vertex from the stack
    * If that vertex hasn't been visited yet:
        * Mark it as visited
        * Add it to the result list
        * Push all of its neighbors into the stack
* Return the result array
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        /* */
    }
    addEdge(v1, v2) {
        /* */
    }
    removeEdge(vertex1, vertex2) {
        /* */
    }
    removeVertex(vertex) {
        /* */
    }
    depthFirstRecursive(start) {
        /* */
    }
    depthFirstIterative(start) {
        const stack = [start];
        const result = [];
        const visited = {};
        let currentVertex;

        visited[start] = true;
        while(stack.length) {
            currentVertex = stack.pop();
            result.push(currentVertex);

            this.adjacencyList[currentVertex].forEach(neighbor => {
                if(!visited[neighbor]) {
                    visited[neighbor] = true;
                    stack.push(neighbor);
                }
            });
        }
        return result;
    }
}
```
## Breadth First
Visit neighbors at current depth first
### Breadth First Pseudocode
* This function should accept a starting vertex
* Create a queue (you can use an array) and place the starting vertex in it
* Create an array to store the nodes visited
* Create an object to store nodes visited
* Mark the starting vertex as visited
* Loop as long as there is anything in the queue
* Remove the first vertex from the queue and push it into the array that stores nodes visited
* Loop over each vertex in the adjacency list for the vertex you are visiting
* If it is not inside the object that stores nodes visited, mark it as visited and enqueue that vertex
* Once you have finished looping, return the array of visited nodes
```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex) {
        /* */
    }
    addEdge(v1, v2) {
        /* */
    }
    removeEdge(vertex1, vertex2) {
        /* */
    }
    removeVertex(vertex) {
        /* */
    }
    depthFirstRecursive(start) {
        /* */
    }
    depthFirstIterative(start) {
        /* */
    }
    breadthFirst(start) {
        const queue = [start];
        const result = [];
        const visited = {};
        let currentVertex;

        visited[start] = true;
        while(queue.length) {
            currentVertex = queue.shift();
            result.push(currentVertex);

            this.adjacencyList[currentVertex].forEach(neighbor => {
                if(!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            });
        }
        return result;
    }
}
```