# Hash Tables
## What is a Hash Table
* Hash tables are used to store key-value pairs.
* They are like arrays, but the keys are not ordered.
* Unlike arrays, hash tables are fast for all of the following operations: finding values, adding new values, and removing values
## Hash Tables in the wild
* Python has Dictionaries
* JS has Objects and Maps
* Java, Go, & Scala have Maps
* Ruby has...Hashes
## The Hash Part
* To implement a hash table, we'll be using an array.
* In order to look up values by key, we need a way to convert keys into valid array indices.
* A function that performs this task is called a hash function.
### What makes a good hash
(not a cryptographically secure one)
1. Fast (i.e. constant time)
2. Doesn't cluster outputs at specific indices, but distributes uniformly
3. Deterministic (same input yields same output)
### Basic Hash Function
```javascript
function hash(key, arrayLen) {
    let total = 0;
    for(let char of key) {
        let value = char.charCodeAt(0) - 96;
        total = (total + value) % arrayLen;
    }
    return total;
}
```
#### Refining our hash
Problems with our current hash
1. Only hashes strings (we won't worry about this)
2. Not constant time - linear in key length
3. Could be a little more random
### Improving Hash Function
```javascript
function hash(key, arrayLen) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for(let i = 0; i < Math.min(key.length, 100); i++) {
        let char = key[i];
        let value = char.charCodeAt(0) - 96;
        total = (total * WEIRD_PRIME + value) % arrayLen;
    }
    return total;
}
```
1. Math.min으로 key의 길이값을 비교하여 key의 길이가 길어도 100이상 루프를 돌지 않도록 만들었다.
2. 소수를 곱해줌으로써 랜덤성을 조금 향상시켰다.
### Dealing with Collisions
Even with a large array and a great hash function, collision are inevitable.
There are many strategies for dealing with collisions, but we'll focus on two:
1. Separate Chaining
2. Linear Probing
#### Separate Chaining
With separate chaining, at each index in out array we store values using a more sophisticated data structure (e.g. an array or a linked list).
This allows us to store multiple key-value pairs at the same index.
#### Linear Probing
With linear probing, when we find a collision, we search through the array to find the next empty slot.
Unlike with separate chaining, this allows us to store a single key-value at each index.
## A HashTable Class
```javascript
class HashTable {
    constructor(size=53) {
        this.keyMap = new Array(size);
    }
    _hash(key) {
        let total = 0;
        let WEIRD_PRIME = 31;
        for(let i = 0; i < Math.min(key.length, 100); i++) {
            let char = key[i];
            let value = char.charCodeAt(0) - 96;
            total = (total * WEIRD_PRIME + value) % this.keyMap.length;
        }
        return total;
    }
}
```
### Set
1. Accepts a key and a value
2. Hashes the key
3. Stores the key-value pair in the hash table array via separate chainining
```javascript
class HashTable {
    constructor(size=53) {
        this.keyMap = new Array(size);
    }
    _hash(key) {
        /* */
    }
    set(key, value) {
        let index = this._hash(key);
        if(!this.keyMap[index]) {
            this.keyMap[index] = [];
        }
        this.keyMap[index].push([key, value]);
    }
}
```
### Get
1. Accepts a key
2. Hashes the key
3. Retrieves the key-value pair in the hash table
4. If the key isn't found, returns undefined
```javascript
class HashTable {
    constructor(size=53) {
        this.keyMap = new Array(size);
    }
    _hash(key) {
        /* */
    }
    set(key, value) {
        /* */
    }
    get(key) {
        let index = this._hash(key);
        if(this.keyMap[index]) {
            for(let i = 0; i < this.keyMap[index].length; i++) {
                if(key === this.keyMap[index][i][0]) {
                    return this.keyMap[index][i][1];
                }
            }
        }
        return undefined;
    }
}
```
### Keys
1. Loops through the hash table array and returns an array of keys in the table
```javascript
class HashTable {
    constructor(size=53) {
        this.keyMap = new Array(size);
    }
    _hash(key) {
        /* */
    }
    set(key, value) {
        /* */
    }
    get(key) {
        /* */
    }
    keys() {
        let keysArr = [];
        for(let i = 0; i < this.keyMap.length; i++) {
            if(this.keyMap[i]) {
                for(let j = 0; j < this.keyMap[i].length; j++) {
                    if(!keysArr.includes(this.keyMap[i][j][0])) {
                        keysArr.push(this.keyMap[i][j][0]);
                    }
                }
            }
        }
        return keysArr;
    }
}
```
### Values
1. Loops through the hash table array and returns an array of values in the table
```javascript
class HashTable {
    constructor(size=53) {
        this.keyMap = new Array(size);
    }
    _hash(key) {
        /* */
    }
    set(key, value) {
        /* */
    }
    get(key) {
        /* */
    }
    keys() {
        /* */
    }
    values() {
        let valuesArr = [];
        for(let i = 0; i < this.keyMap.length; i++) {
            if(this.keyMap[i]) {
                for(let j = 0; j < this.keyMap[i].length; j++) {
                    if(!valuesArr.includes(this.keyMap[i][j][1])) {
                        valuesArr.push(this.keyMap[i][j][1]);
                    }
                }
            }
        }
        return valuesArr;
    }
}
```
## Big O of Hash Tables
* Insert - $O(1)$
* Deletion - $O(1)$
* Access - $O(1)$
## Recap
* Hash tables are collections of key-values pairs
* Hash tables can find values quickly given a key
* Hash tables can add new key-values quickly
* Hash tables store data in a large array, and work by hashing the keys
* A good hash should be fast, distribute keys uniformly, and be deterministic
* Separate chaining and linear probing are two strategies used to deal with two keys that hash to the same index