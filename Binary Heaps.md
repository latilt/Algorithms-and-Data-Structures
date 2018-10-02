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