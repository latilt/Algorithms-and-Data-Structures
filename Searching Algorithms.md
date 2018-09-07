# Searching Algorithms
## How do we serach?
Given an array, the simplest way to search for a value is to look at every element in the array and check if it's the value we want.
(배열을 감안할 때 값을 검색하는 가장 간단한 방법은 배열의 모든 요소를 보고 원하는 값인지 확인하는 것입니다.)
## Javascript has search
There are many different search methods on array in Javascript
* indexOf
* includes
* find
* findIndex

4가지 함수 모두 Linear Search 방법을 사용한다. 정렬되지 않은 배열을 탐색하는 가장 좋은 방법은 Linear Serach 이다. Time Complexity $O(N)$
## Linear Search
```
Write a function called linearSearch which accepts an array and a value,
and returns the index at which the value exists. If the value does not exist in the array, return -1.
```
```
linearSearch라는 함수를 작성합니다.이 함수는 배열과 값을 받아들이고 값이 존재하는 인덱스를 반환합니다.
값이 배열에 없으면 -1을 반환합니다.
```
```javascript
linearSearch([10, 15, 20, 25, 30], 15) // 1
linearSearch([9, 8, 7, 6, 5, 4, 3, 2, 1, 0], 4) // 5
linearSearch([100], 100) // 0
linearSearch([1,2,3,4,5], 6) // -1
linearSearch([9, 8, 7, 6, 5, 4, 3, 2, 1, 0], 10) // -1
linearSearch([100], 200) // -1
```
```javascript
function linearSearch(arr, val){
    for(let i = 0; i < arr.length; i++) {
        if(arr[i] === val) {
            return i;
        }
    }
    return -1;
}
```
## Binary Search
* Binary search is a much faster from of search
* Rather than eliminating one element at a time, you can eliminate half of the remaining elements at a time
* Binary search only works on sorted arrays
```
Write a function called binarySearch which accepts a sorted array and a value
and returns the index at which the value exists. Otherwise, return -1.
```
```
binarySearch라는 함수를 작성합니다. 이 함수는 정렬 된 배열과 값을 받아들이고 값이 존재하는 인덱스를 반환합니다.
그렇지 않으면 -1을 리턴합니다.
```
```javascript
binarySearch([1,2,3,4,5],2) // 1
binarySearch([1,2,3,4,5],3) // 2
binarySearch([1,2,3,4,5],5) // 4
binarySearch([1,2,3,4,5],6) // -1
binarySearch([5,6,10,13,14,18,30,34,35,37,40,44,64,79,84,86,95,96,98,99],10) // 2
binarySearch([5,6,10,13,14,18,30,34,35,37,40,44,64,79,84,86,95,96,98,99],95) // 16
binarySearch([5,6,10,13,14,18,30,34,35,37,40,44,64,79,84,86,95,96,98,99],100) // -1
```
```javascript
function binarySearch(arr, val){
    let left = 0, right = arr.length - 1, mid;
    while(left <= right) {
        mid = Math.floor((left + right) / 2);
        if(arr[mid] < val) {
            left = mid + 1;
        } else if(arr[mid] > val) {
            right = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```
## Naive String Search
* Suppose you want to count the number of times a smaller string appears in a longer string
* A straightforward approach involves checking pairs of characters individually
```javascript
function naiveSearch(long, short) {
    let count = 0;
    for(let i = 0; i < long.length; i++) {
        for(let j = 0; j < short.length; j++) {
            if(short[j] !== long[i + j]) break;
            if(j === short.length - 1) count++;
        }
    }
    return count;
}
```