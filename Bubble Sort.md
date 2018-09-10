# Bubble Sort
A sorting algorithm where the largest values bubble up to the top.
## Swap Function
```javascript
// ES5
function swap(arr, idx1, idx2) {
    var temp = arr[idx1];
    arr[idx1] = arr[idx2];
    arr[idx2] = temp;
}
// ES2015
const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
}
```
## BubbleSort Pseudocode
* Start looping from with a variable called i the end of the array towards the beginning
* Start an inner loop with a variable called j from the beginning until i - 1
* If arr[j] is greater than arr[j+1], swap those two values
* Return the sorted array
### ES5
```javascript
function bubbleSort(arr) {
    for(let i = arr.length; i > 0; i--) {
        for(let j = 0; j < i - 1; j++) {
            if(arr[j] > arr[j+1]) {
                let temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
    return arr;
}
```
### ES2015
```javascript
function bubbleSort(arr) {
    const swap = (arr, idx1, idx2) => {
        [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
    };

    for(let i = arr.length; i > 0; i--) {
        for(let j = 0; j < i - 1; j++) {
            if(arr[j] > arr[j+1]) {
                swap(arr, arr[j], arr[j+1]);
            }
        }
    }
    return arr;
}
```
## Optimized with noSwaps
버블소트로 정렬을 하다보면 정렬이 이미 끝났지만 남은 루프를 계속 돌며 시간을 낭비할 때가 있다. 스왑유무를 판별하여 스왑이 하나도 이뤄지지 않았으면 루프를 끝내므로써 낭비를 줄일 수 있다.
```javascript
function bubbleSort(arr) {
    let noSwaps;
    for(let i = arr.length; i > 0; i--) {
        noSwaps = true;
        for(let j = 0; j < i - 1; j++) {
            if(arr[j] > arr[j+1]) {
                let temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                noSwaps = false;
            }
        }
        if(noSwaps) break;
    }
    return arr;
}
```