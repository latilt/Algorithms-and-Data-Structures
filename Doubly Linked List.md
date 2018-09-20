# Doubly Linked List
Almost identical to Singly Linked Lists, except every node has another pointer, to the previouse node
## Pushing
Adding a node to the end of the Doubly Linked List
* Create a new node with the value passed to the function
* If the head property is null set the head and tail to be the newly created node
* If not, set the next property on the tail to be that node
* Set the previous property on the newly created node to be the tail
* Set the tail to be the newly created node
* Increment the length
* Return the Doubly Linked List
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val) {
        let newNode = new Node(val);
        if(this.length === 0) {
            this.head = newNode;
            this.tail = ndeNode;
        } else {
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }
}
```
## Popping
Removing a node from the end of the Doubly Linked List
* If there is no head, return undefined
* Store the current tail in a variable to return later
* If the length is 1, set the head and tail to be null
* Update the tail to be the previous Node.
* Set the newTail's next to null
* Decrement the length
* Return the value removed
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        let poppedNode = this.tail;
        if(this.length === 1) {
            this.head = null;
            this.tail = null;
        } else {
            this.tail = poppedNode.prev;
            this.tail.next = null;
            poppedNode.prev = null;
        }
        this.length--;
        return poppedNode;
    }
}
```
## Shifting
Removing a node from the beginning of the Doubly Linked List
* If length is 0, return undefined
* Store the current head property in a variable
* If the length is on
    * set the head to be null
    * set the tail to be null
* Update the head to be the next of the old head
* Set the head's prev preperty to null
* Set the old head's next to null
* Decrement the length
* Return old head
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        if(this.length === 0) return undefined;
        let oldHead = this.head;
        if(this.length === 1) {
            this.head = null;
            this.tail = null;
        } else {
            this.head = oldHead.next;
            this.head.prev = null;
            oldHead.next = null;
        }
        this.length--;
        return oldHead;
    }
}
```
## Unshifting
Adding a node to the beginning of the Doubly Linked List
* Create a new node with the value passed to the function
* If the length is 0
    * Set the head to be the new node
    * Set the tail to be the new node
* Otherwise
    * Set the prev property on the head of the list to be the new node
    * Set the next property on the new node to be the head preperty
* Update the head to be the newnode
* Increment the length
* Return the list
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        if(this.length === 0) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.head.prev = newNode;
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
}
```
## Get
Accessing a node in a Doubly Linked List by its position
* If the index is less than 0 or greater or equal to the length, return null
* If the index is less than or equal to half the length of the list
    * Loop through the list starting from the head and loop towards the middle
    * Return the node once it is found
* If the index is greater than half the length of the list
    * Loop through the list starting from the tail and loop towards the middle
    * Return the node once it is found
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        let count, current;
        if(index <= this.length / 2) {
            count = 0;
            current = this.head;
            while(count !== index) {
                current = current.next;
                count++;
            }
        } else {
            count = this.length - 1;
            current = this.tail;
            while(count !== index) {
                current = current.prev;
                count--;
            }
        }
        return current;
    }
}
```
## Set
Replacing the value of a node to the in a Doubly Linked List
* Create a variable which is the result of the get method at the index passed to the function
    * If the get method returns a valid node, set the value of that node to be the value passed to the function
    * Return true
* Otherwise, return false
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        if(foundNode !== null) {
            foundNode.val = val;
            return true;
        }
        return false;
    }
}
```
## Insert
Adding a node in a Doubly Linked List by a certain position
* If the index is less than zero or greater than the length return false
* If the index is 0, unshift
* If the index is the same as the length, push
* Use the get method to access the index - 1
* Set the next and prev preperties on the correct nodes to link everything together
* Increment the length
* Return true
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        if(index < 0 || index > this.length) return false;
        if(index === 0) return !!this.unshift(val);
        if(index === this.length) return !!this.push(val);
        let newNode = new Node(val);
        let beforeNode = this.get(index - 1);
        let afterNode= beforeNode.next;
        beforeNode.next = newNode, newNode.prev = beforeNode;
        newNode.next = afterNode, afterNode.prev = newNode;
        this.length++;
        return true;
    }
}
```
## Remove
Removing a node in a Doubly Linked List by a certain position
* If the index is less than zero or greater than or equal to the length return undefined
* If the index is 0, shift
* If the index is the same as the length - 1, pop
* Use the get method to retrieve the item to be removed
* Update the next and prev properties to remove the found node from the list
* Set next and prev to null on the found node
* Decrement the length
* Return the removed node
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
        if(index === 0) return this.shift();
        if(index === this.length - 1) return this.pop();
        let removedNode = this.get(index);
        let beforeNode = removedNode.prev;
        let afterNode = removedNode.next;
        beforeNode.next = afterNode;
        afterNode.prev = beforeNode;
        /*  removedNode.prev.next = removedNode.next;
            removedNode.next.prev = removedNode.prev;  */
        removedNode.next = null, removedNode.prev = null;
        this.length--;
        return removedNode;
    }
}
```
## Reverse
Reversing the Linked List in place
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
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
    reverse(){
        let node = this.head;
        this.head = this.tail;
        this.tail = node;
        let nextNode;
        for(let i = 0; i < this.length; i++) {
            nextNode = node.next;
            node.next = node.prev;
            node.prev = nextNode;
            node = nextNode;
        }
        return this;
    }
}
```
## Big O of Doubly Linked Lists
Insertion - $O(1)$
Removal - $O(1)$
Searching - $O(N)$
Access - $O(N)$
Technically searching is $O(N / 2)$, but that's still $O(N)$
## Recap
* Doubly Linked Lists are almost identical to Singly Linked Lists except there is an additional pointer to previous nodes
* Better than Singly Lnked Lists for finding nodes and can be done in half the time
* However, they do take up more memory considering the extra pointer