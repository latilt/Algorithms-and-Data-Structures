# Divide And Conquer Pattern
This pattern involves dividing a data set into smaller chunks and then repeating a process with a subset of data.
(이 패턴은 데이터 세트를 더 작은 크기로 나눈 데이터의 서브 세트로 프로세스를 반복하는 패턴입니다.)
This pattern can tremendously decrease time complexity
(이 패턴은 시간 복잡성을 엄청나게 줄일 수 있습니다.)
## An Example
```
Given a sorted array of integer, write a function called search,
that accepts a value and returns the index where the value passed to the function is located.
If the value is not found, return -1
```
```
정렬 된 정수 배열과 숫자를 입력받는 search라는 함수를 작성하십시오.
이 함수는 입력받은 값을 배열에서 찾아 값이 있는 배열의 인덱스를 반환합니다.
값을 찾지 못하면 -1을 반환합니다.
```
```javascript
search([1,2,3,4,5,6],4) // 3
search([1,2,3,4,5,6],6) // 5
serach([1,2,3,4,5,6],11) // -1
```
### A Naive Solution
```javascript
function search(arr, val) {
    for(let i = 0; i < arr.length; i++) {
        if(arr[i] === val) {
            return i;
        }
    }
    return -1;
}
```
Time Complexity - $O(N)$
### Refactored Solution
```javascript
function search(arr, val) {
    let min = 0, max = arr.length - 1;

    while(min <= max) {
        let mid = Math.floor((min + max) / 2);

        if(arr[mid] < val) {
            min = mid + 1;
        } else if(val < arr[mid]) {
            max = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```
Time Complexity - $O(Log(N))$
Binary Search Algorithm