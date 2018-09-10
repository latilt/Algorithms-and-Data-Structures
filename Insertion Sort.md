# Insertion Sort
Builds up the sort by gradually creating a larger left half which is always sorted
## Insertion Sort Pseudocode
* Start by picking the second element in the array
* Now compare the second element with the one before it and swap if necessary.
* Continue to the next element and if it is in the incorrect order, iterate through the sorted portion(i.e. the left side) to place the element in the correct place.
* Repeat until the array is sorted.
```javascript
function insertionSort(arr) {
    for(var i = 1; i < arr.length; i++) {
        let currentValue = arr[i];
        for(var j = i - 1; j >= 0 && arr[j] > currentValue; j--) {
            arr[j + 1] = arr[j];
        }
        arr[j + 1] = currentValue;
    }
    return arr;
}
```
```javascript
function insertionSort(arr) {
    for(let i = 1; i < arr.length; i++) {
        let currentValue = arr[i];
        let index = i - 1;
        for(let j = i - 1; j >= 0 && arr[j] > currentValue; j--) {
            arr[j + 1] = arr[j];
            index = j - 1;
        }
        arr[index + 1] = currentValue;
    }
    return arr;
}
```