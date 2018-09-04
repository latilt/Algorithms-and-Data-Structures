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
---
## areThereDuplicates
```
Implement a function called, areThereDuplicates which accepts a variable number of arguments, 
and checks whether there are any duplicates among the arguments passed in. 
You can solve this using the frequency counter pattern OR the multiple pointers pattern.
```
```
가변 개수의 인수를 허용하는 areThereDuplicates 함수를 구현하고 전달 된 인수 사이에 중복이 있는지 확인합니다.
주파수 카운터 패턴 또는 다중 포인터 패턴을 사용하여 이를 해결할 수 있습니다.
```
```javascript
areThereDuplicates(1, 2, 3) // false
areThereDuplicates(1, 2, 2) //true
areThereDuplicates('a', 'b', 'c', 'a') // true
```
```javascript
function areThereDuplicates(...args) {
    args.sort((a,b) => a > b);
    let start = 0;
    let next = 1;
    while(next < args.length){
        if(args[start] === args[next]){
            return true;
        }
        start++;
        next++;
    }
    return false;
}
```
---
## averagePair
```
Write a function called averagePair. Given a sorted array of integers and a target average, 
determine if there is a pair of values in the array where the average of ther pair equals the target average. 
There may be more than one pair that matches the average target.
```
```
averagePair라는 함수를 작성하십시오. 정렬 된 정수 배열과 목표 평균을 입력받으면 
배열의 쌍의 평균값이 목표 평균과 같은 쌍이 있는지 확인하십시오. 
평균 목표와 일치하는 쌍이 둘 이상 있을 수 있습니다.
```
```javascript
averagePair([1,2,3],2.5) // true
averagePair([1,3,3,5,6,7,10,12,19],8) //true
averagePair([-1,0,3,4,5,6],4.1) // false
averagePair([],4) // false
```
```javascript
function averagePair(arr, target){
    let left = 0, right = arr.length - 1;
    while(left < right) {
        let ave = (arr[left] + arr[right]) / 2;
        if(ave < target) {
            left++;
        } else if(ave > target) {
            right--;
        } else {
            return true;
        }
    }
    
    return false;
}
```
---
## isSubSequence
```
Write a function called isSubsequence which takes in two strings and checks 
whether the characters in the first string from a subsequence of the characters in the second string.
In other words, the function should check whether the characters in the first string appear 
somewhere in the second string, without their order changing.
```
```
isSubsequence라는 함수를 작성합니다. 이 함수는 두 개의 문자열을 입력받고
두 번째 문자열의 하위 시퀀스에서 첫 번째 문자열의 문자가 있는지 확인합니다.
즉 함수는 첫 번째 문자열의 문자가 두 번째 문자열의 어딘가에 순서가 변경되지 않고 나타나는지 확인해야합니다.
```
```javascript
isSubsequence('hello', 'hello world'); // true
isSubsequence('sing', 'sting'); // true
isSubsequence('abc', 'abracadabra'); // true
isSubsequence('abc', 'acb'); // false (order matters)
```
```javascript
function isSubsequence(str1, str2) {
  if(str1.length > str2.length) return false;
  let point1 = 0, point2 = 0;
  
  while(point2 < str2.length) {
      if(str1[point1] === str2[point2]) {
          point1++;
      }
      point2++;
      if(point1 === str1.length) {
          return true;
      }
  }
  return false;
}
```
#### isSubSequence Recursive but not O(1) Space
```javascript
function isSubsequence(str1, str2) {
    if(str1.length === 0) return true
    if(str2.length === 0) return false
    if(str2[0] === str1[0]) return isSubsequence(str1.slice(1), str2.slice(1))  
    return isSubsequence(str1, str2.slice(1))
}
```