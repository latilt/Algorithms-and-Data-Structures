# Mutiple Pointers Pattern
Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition
(인덱스 또는 위치에 해당하는 포인터 또는 값을 만들고 특정 조건에 따라 시작, 끝 또는 중간 위치에서 이동하게 만든다)
Very efficient for solving problems with minimal space complexity as well
(최소한의 공간 복잡성으로 문제를 해결하는 데 매우 효율적이다.)
## An Example
```
Write a function called sumZero which accepts a sorted array of integers.
The function should find the first pair where the sum is 0.
Return an array that includes both values that sum to zero or undefined if a pair does not exist.
```
```
정렬된 정수 배열을 입력받는 sumZero 함수를 작성하십시오.
함수는 합계가 0인 첫번째 쌍을 찾아야합니다.
두 값이 모두 포함 된 배열을 반환하거나 쌍이 없는 경우 undefined를 반환하십시오.
```
```javascript
sumZero([-3,-2,-1,0,1,2,3]) // [-3,3]
sumZero([-2,0,1,3]) // undefined
sumZero([1,2,3]) //undefined
```
### A Naive Solution
```javascript
function sumZero(arr) {
    for(let i = 0; i < arr.length; i++) {
        for(let j = i + 1; j < arr.length; j++) {
            if(arr[i] + arr[j] === 0) {
                return [arr[i], arr[j]];
            }
        }
    }
}
```
Time Complexity - $O(N^2)$
Space Complexity - $O(1)$
### Refactored Solution
```javascript
function sumZero(arr) {
    let left = 0;
    let right = arr.length - 1;
    while(left < right) {
        let sum = arr[left] + arr[right];
        if(sum === 0) {
            return [arr[left], arr[right]];
        } else if(sum > 0) {
            right--;
        } else {
            left++;
        }
    }
}
```
Time Complexity - $O(N)$
Space Complexity - $O(1)$

---
## countUniqueValues
```
Implement a function called countUniqueValues,
which accepts a sorted array, and counts the unique values in the array.
There can be negative numbers in the array, but it will always be sorted.
```
```
countUniqueValues라는 함수를 구현합니다.
이 함수는 정렬 된 배열을 받아들이고 배열의 고유한 값이 몇개인지 계산합니다.
배열에는 음수가 있을 수 있지만 항상 정렬되어 있습니다.
```
```javascript
countUniqueValues([1,1,1,1,1,2]) // 2
countUniqueValues([1,2,3,4,4,4,7,7,12,12,13]) // 7
countUniqueValues([]) // 0
countUniqueValues([-2,-1,-1,0,1]) // 4
```
```javascript
function countUniqueValues(arr){
    let begin = 0;
    let flag = 1;
    
    while(flag < arr.length) {
        if(arr[begin] !== arr[flag]) {
            arr[++begin] = arr[flag];
        } 
        flag++;
    }
    
    return begin ? begin + 1 : begin;
}
```
```javascript
function countUniqueValues(arr) {
    if(arr.length === 0) return 0;
    var i = 0;
    for(var j = 1; j < arr.length; j++) {
        if(arr[i] !== arr[j]) {
            i++;
            arr[i] = arr[j];
        }
    }
    return i + 1;
}
```
```javascript
function countUniqueValues(arr){
  let answer = 0;
  for(let i = 0; i < arr.length; i++) {
      if(arr[i] !== arr[i + 1]) {
          answer++;
      }
  }
  return answer;
}
```