# Singly Linked Lists
## What is a linked list
A data structure that contains a head, tail, and length property.
Linked Lists consist of nodes, and each node has a value and a pointer to another node or null
## Comparisons with Arrays
### Lists
* Do not have indexes
* Connected via nodes with a next pointer
* Random access is no allowed
### Arrays
* Indexed in order
* Insertion and deletion can be expensive
* Can quickly be accessed at a specific index
---
## Pushing
Adding a new node to the end of the Linked List.
* This function should accept a value
* Create a new node using the value passed to the function
* If there is no head property on the list, set the haed and tail to be the newly created node
* Otherwise set the next property on the tail to be the new node and set the tail property on the list to be the newly created node
* Increment the length by one
* Return the linked list
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        let newNode = new Node(val);
        if(!this.head) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }
}
```
## Poping
Removing a node from the end of the Linked List
* If there are no nodes in the list, return undefined
* Loop through the list until you reach the tail
* Set the next property of the 2nd to last node to be null
* Set the tail to be the 2nd to last node
* Decrement the length of the list by 1
* Return the value of the node removed
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        if(!this.head) return undefined;
        let current = this.head;
        let newTail = current;
        while(current.next) {
            newTail = current;
            current = current.next;
        }
        this.tail = newTail;
        this.tail.next = null;
        this.length--;
        if(this.length === 0) {
            this.head = null;
            this.tail = null;
        }
        return current;
    }
}
```
## Shifting
Removing a new node from the beginning of the Linked List
* If there are no nodes, return undefined
* Store the current head property in a variable
* Set the head property to be the current head's next property
* Decrement the length by 1
* Return the value of the node removed
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        if(!this.head) return undefined;
        let currentHead = this.head;
        this.head = currentHead.next;
        this.length--;
        if(this.length === 0) {
            this.tail = null;
        }
        return currentHead;
    }
}
```
## Unshifting
Adding a new node to the beginning of the Linked List
* This function should accept a value
* Create a new node using the value passed to the function
* If there is no head property on the list, set the head and tail to be the newly created node
* Otherwise set the newly created node's next property to be the current head property on the list
* Set the head property on the list to be that newly created node
* Increment the length of the list by 1
* Return the linked list
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        let newNode = new Node(val);
        if(!this.head) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
}
```
## Get
Retrieving a node by it's position in the Linked List
* This function should accept an index
* If the index is less than zero or greater than or equal to the length of the list, return null
* Loop through the list until you reach the index and return the node at that specific index
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        /* */
    }
    get(index) {
        if(index < 0 || index >= this.length) return null;
        let count = 0;
        let current = this.head;
        while(count !== index) {
            current = current.next;
            count++;
        }
        return current;
    }
}
```
## Set
Changing the value of a node based on it's position in the Linked List
* This function should accept a value and an index
* Use your get function to find the specific node.
* If the node is not found, return false
* If the node is found, set the value of that node to be the value passed to the function and return true
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        /* */
    }
    get(index) {
        /* */
    }
    set(index, val) {
        let foundNode = this.get(index);
        if(foundNode) {
            foundNode.val = val;
            return true;
        }
        return false;
    }
}
```
## Insert
Adding a node to the Linked List at a specific position
* If the index is less than zero or greater than the length, return false
* If the index is the same as the length, push a new node to the end of the list
* If the index is 0, unshift a new node to the start of the list
* Otherwise, using the get method, access the node at the index - 1
* Set the next property on that node to be the new node
* Set the next property on the new node to be the previous next
* Increment the length
* Return true
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        /* */
    }
    get(index) {
        /* */
    }
    set(index, val) {
        /* */
    }
    insert(index, val) {
        if(index < 0 || index > this.length) return null;
        if(index === this.length) return !!this.push(val);
        if(index === 0) return !!this.unshift(val);
        let newNode = new Node(val);
        let prevNode = this.get(index - 1);
        newNode.next = prevNode.next;
        prevNode.next = newNode;
        this.length++;
        return true;
    }
}
```
## Remove
Removing a node from the Linked List at a specific position
* If the index is less than zero or greater than the length, return undefined
* If the index is the same as the length-1, pop
* If the index is 0, shift
* Otherwise, using the get method, access the node at the index - 1
* Set the next property on that node to be the next of the next node
* Decrement the length
* Return the value of the node removed
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        /* */
    }
    get(index) {
        /* */
    }
    set(index, val) {
        /* */
    }
    insert(index, val) {
        /* */
    }
    remove(index) {
        if(index < 0 || index >= this.length) return undefined;
        if(index === this.length - 1) return this.pop();
        if(index === 0) return this.shift();
        let prevNode = this.get(index - 1);
        let removeNode = prevNode.next;
        prevNode.next = removeNode.next;
        this.length--;
        return removeNode;
    }
}
```
## Reverse
Reversing the Linked List in place
* Swap the head and tail
* Create a variable called next
* Create a variable called prev
* Create a variable called node and initialize it to the head property
* Loop through the list
* Set next to be the next property on whatever node is
* Set the next property on the node to be whatever prev is
* Set prev to be the value of the node variable
* Set the node variable to be the value of the next variable
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        /* */
    }
    shift() {
        /* */
    }
    unshift(val) {
        /* */
    }
    get(index) {
        /* */
    }
    set(index, val) {
        /* */
    }
    insert(index, val) {
        /* */
    }
    remove(index) {
        /* */
    }
    reverse() {
        let node = this.head;
        this.head = this.tail;
        this.tail = node;
        this next;
        this prev = null;
        for(let i = 0; i < this.length; i++) {
            next = node.next;
            node.next = prev;
            prev = node;
            node = next;
        }
        return this;
    }
}
```
## Big O of Singly Linked Lists
Insertion - $O(1)$
Removal - It depends $O(1)$ or $O(N)$
Searching - $O(N)$
Access - $O(N)$
## Recap
* Singly Linked Lists are an excellent alternative to arrays when insertion and deletion at the beginning are frequently required
* Arrays contain a build in index whereas Linked Lists do not
* The idea of a list data structure that consists of nodes is the foundation for other data structures like Stacks and Queues