# Binary Heaps
## What is a Binary Heap
Very similar to a binary search tree, but with some different rules
* In a MaxBinaryHeap, parent nodes are always larger tahn child nodes.
* In a MinBinaryHeap, parent nodes are always smaller than child nodes
## Max Binary Heap
*  Each parent has at most two child nodes
* The value of each parent node is always greater than its child nodes
* In a max Binay Heap the parent is greater than the children, but there are no guarantees between sibling nodes.
* A binary heap is as compact as possible. All the children of each node are as full as they can be and left children are filled out first
## Why do we need to know this
Binary Heaps are used to implement Priority Queues, which are very commonly used data structures.
They are also used quite a bit, with graph traversal algorithms
## Store Heap at Array
* Parent -> Child
    * For any index of an array n
    * The left child is stored at 2n + 1
    * The right child is at 2n + 2
* Child -> Parent
    * For any child node at index n
    * Its parent is at index (n-1)/2
## Adding to a MaxBinaryHeap
* Add to the End
* Bubble UP
### Insert pseudocode
* Push the value into the values property on the heap
* Bubble the value up to its correct spot
    * Create a variable called index which is the length of the values property - 1
    * Create a variable called parentIndex which is the floor of (index-1)/2
    * keep looping as long as the values element at the parentIndex is less than the values element at the child index
        * Swap the value of the values element at the parentIndex with the value of the element property at the child index
        * Set the index to be the parentIndex, and start over
```javascript
class MaxBinayHeap {
    constructor() {
        this.values = [];
    }
    insert(element) {
        this.values.push(element);
        this.bubbleUp();
    }
    bubbleUp() {
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while(idx > 0) {
            let parentIdx = Math.floor((idx - 1)/2);
            let parent = this.values[parentIdx];
            if(element <= parent) break;
            this.values[idx] = parent;
            this.values[parentIdx] = element;
            idx = parentIdx;
        }
    }
}
```
## Removing from a Heap
* Remove the root
* Replace with the most recently added
* Adjust (sink down)
### Removing Pseudocode
* Swap the first value in the values property with the last one
* Pop from the values property, so you can return the value at the end.
* Have the new root "sink down" to the correct spot
    * Your parent index starts at 0 (the root)
    * Find the index of the left child: 2 * index + 1 (make sure its not out of bounds)
    * Find the index of the right child: 2 * index + 2 (make sure its not out of bounds)
    * If the left or right child is greater than the lement...swap. If both left and right children are larger, swap with the largest child.
    * The child index you swapped to now becomes the new parent index.
    * Keep looping and swapping until neither child is larger than the lement.
* Return the old root
```javascript
class MaxBinayHeap {
    constructor() {
        this.values = [];
    }
    insert(element) {
        /* */
    }
    bubbleUp() {
        /* */
    }
    extractMax() {
        const max = this.values[0];
        const end = this.values.pop();
        if(this.values.length > 0) {
            this.values[0] = end;
            this.sinkDown();
        }
        return max;
    }
    sinkDown() {
        let idx = 0;
        const element = this.values[0];
        const length = this.values.length;
        while(true) {
            let leftChildIdx = 2 * idx + 1;
            let rightChildIdx = 2 * idx + 2;
            let leftChild, rightChild;
            let swap = null;
            if(leftChildIdx < length) {
                leftChild = this.values[leftChlidIdx];
                if(element < leftChild) {
                    swap = leftChildIdx;
                }
            }
            if(rightChildIdx < length) {
                rightChild = this.values[rightChildIdx];
                if(
                    (swap === null && element < rightChild) ||
                    (swap !== null && leftChild < rightChild)
                ) {
                    swap = rightChildIdx;
                }
            }
            if(swap === null) break;
            this.values[idx] = this.values[swap];
            this.values[swap] = element;
            idx = swap;
        }
    }
}
```
## Big O of Binary Heaps
Insertion - $O(logN)$
Removal - $O(logN)$
Search - $O(N)$
## Recap
* Binary Heaps are very useful data structures for sorting, and implementing other data structures like priority queues
* Binary Heaps are either MaxBinaryHeaps or MinBinaryHeaps with parents either being smaller or larger than their children
* With just a little bit of math, we can represent heaps using arrays
# Priority Queue
## What is a Priority Queue
A data structure where each element has a priority.
Element with higher priorities are served before elements with lower priorities.
## Priority Queue Pseudocode
* Write a Min Binary Heap - lower number means higher priority.
* Each Node has a val and a priority. Use the priority to build the heap.
* Enqueue method accepts a value and priority, makes a new node, and puts it in the right spot based off of its priority.
* Dequeue method removes root element, returns it, and rearranges heap using priority.
```javascript
class PriorityQueue {
    constructor() {
        this.values = [];
    }
    enqueue(value, priority) {
        let newNode = new Node(value, priority);
        this.values.push(newNode);
        this.bubbleUp();
    }
    bubbleUp() {
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while(idx > 0) {
            let parentIdx = Math.floor((idx - 1)/2);
            let parent = this.values[parentIdx];
            if(element.priority >= parent.priority) break;
            this.values[idx] = parent;
            this.values[parentIdx] = element;
            idx = parentIdx;
        }
    }
    dequeue() {
        const min = this.values[0];
        const end = this.values.pop();
        if(this.values.length > 0) {
            this.values[0] = end;
            this.sinkDown();
        }
        return min;
    }
    sinkDown() {
        let idx = 0;
        const element = this.values[0];
        const length = this.values.length;
        while(true) {
            let leftChildIdx = 2 * idx + 1;
            let rightChildIdx = 2 * idx + 2;
            let leftChild, rightChild;
            let swap = null;
            if(leftChildIdx < length) {
                leftChild = this.values[leftChlidIdx];
                if(element.priority > leftChild.priority) {
                    swap = leftChildIdx;
                }
            }
            if(rightChildIdx < length) {
                rightChild = this.values[rightChildIdx];
                if(
                    (swap === null && element.priority > rightChild.priority) ||
                    (swap !== null && leftChild.priority > rightChild.priority)
                ) {
                    swap = rightChildIdx;
                }
            }
            if(swap === null) break;
            this.values[idx] = this.values[swap];
            this.values[swap] = element;
            idx = swap;
        }
    }
}
class Node {
    constructor(value, priority) {
        this.value = value;
        this.priority = priority;
    }
}
```