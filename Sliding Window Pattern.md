# Sliding Window Pattern
This pattern involves creating a window which can either be an array or number from one position to another
(이 패턴은 하나의 위치에서 다른 위치로 움직이는 배열 또는 숫자가 될 수있는 창을 생성하는 것과 관련이 있습니다)
Depending on a certain condition, the window either increases or closes (and a new window is created)
(특정 조건에 따라 윈도우의 수가 증가하거나 닫힙니다.)
Very useful for keeping track of a subset of data in an array/string etc.
(배열이나 문자열 등에서 데이터의 하위 집합을 추적하는데 매우 유용합니다.)
## An Example
```
Write a function called maxSubarraySum which accepts an array of integers and a number called n.
The function should calculate the maximum sum of n consecutive elements in the array.
```
```
정수 배열과 n이라는 숫자 변수를 입력받는 maxSubarraySum이라는 함수를 작성하세요.
이 함수는 배열에 있는 n 개의 연속 요소들의 최대 합을 계산해야합니다.
```
```javascript
maxSubarraySum([1,2,5,2,8,1,5],2) // 10
maxSubarraySum([1,2,5,2,8,1,5],4) // 17
maxSubarraySum([4,2,1,6],1) // 6
maxSubarraySum([4,2,1,6,2],4) // 13
maxSubarraySum([],4) // null
```
### A Naive Solution
```javascript
function maxSubarraySum(arr, num) {
    if(num > arr.length) {
        return null;
    }
    var max = -Infinity;
    for(let i = 0; i < arr.length - num + 1; i++) {
        temp = 0;
        for(let j = 0; j < num; j++) {
            temp += arr[i + j];
        }
        if(temp > max) {
            max = temp;
        }
    }
    return max;
}
```
Time Complexity - $O(N^2)$
### Refactored Solution
```javascript
function maxSubarraySum(arr, num) {
    let maxSum = 0;
    let tempSum = 0;
    if(arr.length < num) return null;
    for(let i = 0; i < num; i++) {
        maxSum += arr[i];
    }
    tempSum = maxSum;
    for(let i = num; i < arr.length; i++) {
        tempSum = tempSum - arr[i - num] + arr[i];
        maxSum = Math.max(maxSum, tempSum);
    }
    return maxSum;
}
```
Time Complexity - $O(N)$

---
## maxSubarraySum
```
Given an array of integers and a number, write a function called maxSubarraySum,
which finds the maximum sum of a subarray with the length of the number passed to the function.
Note that a subarray must consist of consecutive elements from the original array.
In the first example below, [100, 200, 300] is a subarray of the original array, but [100, 300] is not.
```
```
정수 배열과 숫자를 입력받는 maxSubarraySum이라는 함수를 작성합니다.
이 함수는 전달 된 숫자의 길이로 된 하위 배열의 변수들의 최대 합계를 찾습니다.
단, 하위 배열은 원래 배열의 연속 요소로 구성되어야합니다.
아래 첫 번째 예에서 [100, 200, 300]은 원래 배열의 하위 배열이지만 [100, 300]은 아닙니다.
```
```javascript
maxSubarraySum([100,200,300,400], 2) // 700
maxSubarraySum([1,4,2,10,23,3,1,0,20], 4) // 39
maxSubarraySum([-3,4,0,-2,6,-1], 2) // 5
maxSubarraySum([3,-2,7,-4,1,-1,4,-2,1], 2) // 5
maxSubarraySum([2,3], 3) // null
```
```javascript
function maxSubarraySum(arr, num){
    if(arr.length < num) return null;
    let maxSum = 0, tempSum = 0;
    for(let i = 0; i < num; i++) {
        maxSum += arr[i];
    }
    tempSum = maxSum;
    for(let i = num; i < arr.length; i++) {
        tempSum = tempSum - arr[i - num] + arr[i];
        maxSum = Math.max(maxSum, tempSum);
    }
    
    return maxSum;
}
```
---
## minSubArrayLen
```
Write a function called minSubArrayLen which accepts two parameters - an array of positive integers and
a positive integer. This function should return thie minimal length of a contiguous subarray of which 
the sum is greater than or equal to the integer passed to the function. If there isn't one, return 0 instead.
```
```
양수 및 양의 정수 배열을 사용하는 minSubArrayLen이라는 함수를 작성하십시오.
이 함수는 합계가 함수에 전달 된 정수보다 크거나 같은 인접한 하위 배열의 최소 길이를 반환해야합니다. 하나도 없으면 대신 0을 리턴하십시오.
```
```javascript
minSubArrayLen([2,3,1,2,4,3],7) // 2 -> because [4,3] is the smallest subarray
minSubArrayLen([2,1,6,5,4,],9) // 2 -> because [5,4] is the smallest subarray
minSubArrayLen([3,1,7,11,2,9,8,21,62,33,19],52) // 1 -> because [62] is greater than 52
minSubArrayLen([1,4,16,22,5,7,8,9,10],39) // 3
minSubArrayLen([1,4,16,22,5,7,8,9,10],55) // 5
minSubArrayLen([4,3,3,8,1,2,3,],11) // 2
minSubArrayLen([1,4,16,22,5,7,8,9,10],95) // 0
```
```javascript
function minSubArrayLen(arr, val) {
    let left = 0, right = 1;
    let sum = arr[left] + arr[right];
    let length = Infinity, tempLength = 0;
    
    while(right < arr.length) {
        if(sum < val) {
            right++;
            sum += arr[right];
        } else if(sum >= val) {
            tempLength = right - left;
            length = Math.min(length, tempLength);
            sum -= arr[left];
            left++;
        }
    }
    return length !== Infinity ? length + 1 : 0;
}
```
```javascript
function minSubArrayLen(nums, sum) {
    let total = 0;
    let start = 0;
    let end = 0;
    let minLen = Infinity;
    
    while (start < nums.length) {
        // if current window doesn't add up to the given sum then 
            // move the window to right
        if(total < sum && end < nums.length){
            total += nums[end];
            end++;
        }
        // if current window adds up to at least the sum given then
            // we can shrink the window 
        else if(total >= sum){
            minLen = Math.min(minLen, end-start);
            total -= nums[start];
            start++;
        } 
        // current total less than required total but we reach the end, need this or else we'll be in an infinite loop 
        else {
            break;
        }
    }
    
    return minLen === Infinity ? 0 : minLen;
}
```
---
## findLongestSubstring
```
Write a function called findLongestSubstring, 
which accepts a string and returns the length of the longest substring with all distinct characters.
```
```
findLongestSubstring이라는 함수를 작성합니다.
이 함수는 문자열을 받아들이고 모든 고유 문자가 있는 가장 긴 하위 문자열의 길이를 반환합니다.
```
```javascript
findLongestSubstring('') // 0
findLongestSubstring('rithmschool') // 7
findLongestSubstring('thisisawesome') // 6
findLongestSubstring('thecatinthehat') // 7
findLongestSubstring('bbbbbb') // 1
findLongestSubstring('longestsubstring') // 8
findLongestSubstring('thisishowwedoit') // 6
```
```javascript
function findLongestSubstring(str){
  let obj = {};
  let i = 0;
  let length = 0, tempLength = 0;
  while(i < str.length) {
      let letter = str[i];
      if(obj[letter]) {
          i = obj[letter];
          obj = {};
          length = Math.max(length, tempLength);
          tempLength = 0;
      } else {
          obj[letter] = i + 1;
          tempLength++;
          i++;
      }
  }
  length = Math.max(length, tempLength);
  return length;
}
```
```javascript
function findLongestSubstring(str) {
    let longest = 0;
    let seen = {};
    let start = 0;
    
    for (let i = 0; i < str.length; i++) {
        let char = str[i];
        if (seen[char]) {
            start = Math.max(start, seen[char]);
        }
        // index - beginning of substring + 1 (to include current in count)
        longest = Math.max(longest, i - start + 1);
        // store the index of the next char so as to not double count
        seen[char] = i + 1;
    }
    return longest;
}
```