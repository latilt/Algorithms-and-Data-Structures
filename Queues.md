# Queues
## What is a Queue
A FIFO(First In First Out) data structure
## How is it used
Queues exist everwhere. Think about the last time you waited in line.
## Where Queues are used
* Background tasks
* Uploading resourses
* Printing / Task processing
## Creating a Queue with an Array
* Array.push() / Array.shift()
* Array.unshift() / Array.pop()

둘 모두 인덱스를 재배열하는데 시간이 많이 걸린다.
## Creating a Queue with a Linked List
### Enqueue
* This function accepts some value
* Create a new node using that value passed to the function
* If there are no nodes in the queue, set this node to be the first and last property of the queue
* Otherwise, set the next property on the current last to be that node, and then set the last property of the queue to be that node
* Increment the size of the queue by 1
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null
    }
}
class Queue {
    constructor() {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    enqueue(val) {
        let newNode = new Node(val);
        if(!this.first) {
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        return ++this.size;
    }
}
```
### Dequeue
* If there is no first property, just return null
* Store the first property in a variable
* See if the first is the same as the last (check if there is only 1 node). If so, set the first and last to be null
* If there is more than 1 node, set the first property to be the next property of first
* Decrement the size by 1
* Return the value of the node dequeued
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null
    }
}
class Queue {
    constructor() {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    enqueue(val) {
        /* */
    }
    dequeue() {
        if(!this.first) return null;
        let temp = this.first;
        if(this.first === this.last) {
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```
## Big O of Queues
Insertion - $O(1)$
Removal - $O(1)$
Searching - $O(N)$
Access - $O(N)$
## Recap
* Queues are a FIFO data structure, all elements are first in first out.
* Queues are useful for processing tasks and are foundational for more complex data structures
* Insertion and Removal can be done in $O(1)$