# Stacks
## What is a stack
A LIFO(Last In First Out) data structure.
The last element added to the stack will be the first element removed from the stack.
## How is it used
Think about a stack of plates, or a stack of markers, or a stack of ...anything.
As you pile it up the last thing (or the topmost thing) is what gets removed first.
## Where stacks are used
* Managing function invocations
* Undo / Redo
* Routing(the history object) is treated like a stack
## Creating a Stack with an Array
* Array.push() / Array.pop()
* Array.unshift() / Array.shift()

둘 모두 가능하지만 unshift와 shift는 배열의 인덱스를 재배열하는데 시간이 많이 걸리므로 push와 pop을 사용하도록 하자.
## Creating a Stack with a Linked List
Singly Linked List에서의 push가 $O(N)$인 관계로 shift와 unshift를 사용하여 $O(1)$로 동작되도록 한다.
Doubly Linked List에서는 push와 pop을 사용해도 상관이 없다.
### Push
* The function should accept a value
* Create a new node with that value
* If there are no nodes in the stack, set the first and last property to be the newly crated node
* If there is at least one node, create a variable that stores the current first property on the stack
* Reset the first property to be the newly created node
* Set the next property on the node to be the previously created variable
* Increment the size of the stack by 1
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}
class Stack {
    constructor() {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    push(val) {
        let newNode = new Node(val);
        if(!this.first) {
            this.first = newNode;
            this.last = newNode;
        } else {
            newNode.next = this.first;
            this.first = newNode;
        }
        return ++this.size;
    }
}
```
### Pop
* If there are no nodes in the stack, return null
* Create a temporary variable to store the first property on the stack
* If there is only 1 node, set the first and last property to be null
* If there is more than one node, set the first property to be the next property on the current first
* Decrement the size by 1
* Return the value of the node removed
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}
class Stack {
    constructor() {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    push(val) {
        /* */
    }
    pop() {
        if(!this.first) return null;
        let popNode = this.first;
        if(this.first === this.last) {
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return popNode.value;
    }
}
```
## Big O of Stacks
Insertion - $O(1)$
Removal - $O(1)$
Searching - $O(N)$
Access - $O(N)$
## Recap
* Stacks are a LIFO data structure where the last value in is always the first one out.
* Stacks are used to handle function invocations (the call stack), for operations like undo/redo, and for routing (remember pages you have visited and go back/forward) and much more
* They are not a build in data structure in JavaScript, but are relatively simple to implement