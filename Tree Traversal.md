# Tree Traversal
## Traversing a Tree
* Breadth-first Search
* Depth-first Search
### BFS(Breadth-First Search)
Steps - Iteratively
* Create a queue(this can be an array) and a variable to store the values of nodes visited
* Place the root node in the queue
* Loop as long as there is anything in the queue
    * Dequeue a node from the queue and push the value of the node into the variable that stores the nodes
    * If there is a left property on the node dequeued - add it to the queue
    * If there is a right property on the node dequeued - add it to the queue
* Return the variable that stores the values
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }   
}
class BinarySearchTree {
    constructor() {
        this.root = null;
    }
    insert(value) {
        /* */
    }
    find(value) {
        /* */
    }
    contains(value) {
        /* */
    }
    BFS() {
        let node = this.root, data = [], queue = [];
        queue.push(node);
        while(queue.length) {
            node = queue.shift();
            data.push(node.value);
            if(node.left) queue.push(node.left);
            if(node.right) queue.push(node.right);
        }
        return data;
    }
}
```
### DFS - PreOrder
Can be used to 'export' a tree structure so that it is easily reconstructed or copied.
Steps - Recursively
* Create a variable to store the values of nodes visited
* Store the root of the BST in a variable called current
* Write a helper function which accepts a node
    * Push the value of the node to the variable that stores the values
    * If the node has a left property, call the helper function with the left property on the node
    * If the node has a right property, call the helper function with the right property on the node
* Invoke the helper function with the current variable
* Return the array of values
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }   
}
class BinarySearchTree {
    constructor() {
        this.root = null;
    }
    insert(value) {
        /* */
    }
    find(value) {
        /* */
    }
    contains(value) {
        /* */
    }
    BFS() {
        /* */
    }
    DFSPreOrder() {
        let data = [];
        let current = this.root;
        function traverse(node) {
            data.push(node.value);
            if(node.left) traverse(node.left);
            if(node.right) traverse(node.right);
        }
        traverse(current);
        return data;
    }
}
```
### DFS - PostOrder
Steps - Recursively
* Create a variable to store the values of nodes visited
* Store the root of the BST in a variable called current
* Write a helper function which accepts a node
    * If the node has a left property, call the helper function with the left property on the node
    * If the node has a right property, call the helper function with the right property on the node
    * Push the value of the node to the variable that stores the values
* Invoke the helper function with the current variable
* Return the array of values
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }   
}
class BinarySearchTree {
    constructor() {
        this.root = null;
    }
    insert(value) {
        /* */
    }
    find(value) {
        /* */
    }
    contains(value) {
        /* */
    }
    BFS() {
        /* */
    }
    DFSPreOrder() {
        /* */
    }
    DFSPostOrder() {
        let data = [];
        let current = this.root;
        function traverse(node) {
            if(node.left) traverse(node.left);
            if(node.right) traverse(node.right);
            data.push(node.value);
        }
        traverse(current);
        return data;
    }
}
```
### DFS - InOrder
Used commonly with BST's
Notice we get all nodes in the tree in their underlying order
Steps - Recursively
* Create a variable to store the values of nodes visited
* Store the root of the BST in a variable called current
* Write a helper function which accepts a node
    * If the node has a left property, call the helper function with the left property on the node
    * Push the value of the node to the variable that stores the values
    * If the node has a right property, call the helper function with the right property on the node
* Invoke the helper function with the current variable
* Return the array of values
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }   
}
class BinarySearchTree {
    constructor() {
        this.root = null;
    }
    insert(value) {
        /* */
    }
    find(value) {
        /* */
    }
    contains(value) {
        /* */
    }
    BFS() {
        /* */
    }
    DFSPreOrder() {
        /* */
    }
    DFSPostOrder() {
        /* */
    }
    DFSInOrder() {
        let data = [];
        let current = this.root;
        function traverse(node) {
            if(node.left) traverse(node.left);
            // node.left && traverse(node.left);
            data.push(node.value);
            if(node.right) traverse(node.right);
            // node.right && traverse(node.right);
        }
        traverse(current);
        return data;
    }
}
```
## Recap
* Trees are non-linear data structures that contain a root and child nodes
* Binary Trees can have values of any types, but at most two children for each parent
* Binary Search Trees are a more specific version of binary trees where every node to the left of a parent is less than it's value and every node to the right is greater
* We can search through Trees using BFS and DFS