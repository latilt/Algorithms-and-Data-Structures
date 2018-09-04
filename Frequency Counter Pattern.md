# Frequency Counter Pattern

This pattern uses objects or sets to collect values/frequencies of values
(이 패턴은 변수와 변수의 빈도를 수집하기 위해 Object(객체)나 Sets(집합)을 사용합니다)
This can often avoid the need for nested loops or O(N^2) operations with arrays / strings
(이 패턴은 배열이나 문자열을 사용하는 $O(N^2)$ 연산이나 중첩루프를 피할 수 있게 해줍니다.)

## An Example
```
Write a function called same, which accepts two arrays. The function should return true 
if every value in the array has it's corresponding value squared in the second array.
The frequency of values must be the same.
```
```
두 개의 배열을 입력받는 same이라는 함수를 작성하십시오.
첫번째 배열의 변수들의 제곱이 두 번째 배열의 변수들 일 경우 이 함수는 true를 반환합니다.
값의 빈도는 동일해야합니다.
```
```javascript
same([1,2,3], [4,1,9]) // true
same([1,2,3], [1,9]) // false
same([1,2,1], [4,4,1]) // false (must be same frequency)
```

### A Naive Solution
```javascript
function same(arr1, arr2) {
    if(arr1.length !== arr2.length) {
        return false;
    }
    for(let i = 0; i < arr1.length; i++) {
        let correctIndex = arr2.indexOf(arr[i] ** 2);
        if(correctIndex === -1) {
            return false;
        }
        arr2.splice(correctIndex, 1);
    }
    return true;
}
```
arr1 배열의 for문 루프를 돌면서 값의 제곱값과 일치하는 arr2 배열의 인덱스 값을 찾아 없으면 false를 반환하고 있으면 배열의 값을 삭제하는 알고리즘이다.
루프가 중첩되므로 $O(N^2)$ 시간복잡도를 가진다.
### Refactored Solution
```javascript
function same(arr1, arr2) {
    if(arr1,length !== arr2.length) {
        return false;
    }
    let frequencyCounter1 = {};
    let frequencyCounter2 = {};
    for(let val of arr1) {
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1;
    }
    for(let val of arr2) {
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1;
    }
    for(let key in frequencyCounter1) {
        if(!(key ** 2 in frequencyCounter2)) {
            return false;
        }
        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]) {
            return false;
        }
    }
    return true;
}
```
객체를 사용하여 중첩된 루프를 없애고 $O(N)$의 시간복잡도를 가지게 되었다.

---
## Anagrams
```
Given two strings, write a function to determine if the second string is an anagram of the first.
An anagram is a word, phrase, or name formed by rearranging the letters of another,
such as cinema, formed from iceman.
```
```
두 개의 문자열이 주어지면 두 번째 문자열이 첫 번째 문자열의 아나그램인지 확인하는 함수를 작성하십시오.
아나그램은 cinema를 iceman으로 바꾸듯이 문자를 재배열하여 다른 단어의 문자로 만드는 방식입니다.
```
```javascript
validAnagram('', '') // true
validAnagram('aaz', 'zza') // false
validAnagram('anagram', 'nagaram') // true
validAnagram('rat', 'car') // false
validAnagram('awesome', 'awesom') // false
validAnagram('qwerty', 'qeywrt') // true
validAnagram('texttwisttime', 'timetwisttext') // true
```
```javascript
function validAnagram(str1, str2){
    if(str1.length !== str2.length) {
        return false;
    }
    let freCounter1 = {};
    let freCounter2 = {};
    for(let char of str1) {
        freCounter1[char] = (freCounter1[char] || 0) + 1;
    }
    for(let char of str2) {
        freCounter2[char] = (freCounter2[char] || 0) + 1;
    }
    for(let key in freCounter1) {
        if(!(key in freCounter2)) {
            return false;
        }
        if(freCounter1[key] !== freCounter2[key]) {
            return false;
        }
    }
    return true;
}
```
```javascript
function validAnagram(first, second) {
    if(first.length !== seconde.length) {
        return false;
    }

    const lookup = {};

    for(let i = 0; i < first.length; i++) {
        let letter = first[i];
        lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
    }

    for(let i = 0; i < second.length; i++) {
        let letter = second[i];
        if(!lookup[letter]) {
            return false;
        } else {
            lookup[letter] -= 1;
        }
    }
    
    return true;
}
```

---
## sameFrequency
```
Write a function called sameFrequency. Given two positive integers,
find out if the two numbers have the same frequency of digits.
```
```
sameFrequency라는 함수를 작성하십시오. 두 개의 양의 정수가 주어 졌을 때
두 숫자의 숫자가 같은 자릿수인지 확인하십시오.
```
```javascript
sameFrequency(182, 281) // true
sameFrequency(34, 14) // false
sameFrequency(3589578, 5879385) // true
sameFrequency(22, 222) // false
```
```javascript
function sameFrequency(num1, num2){
    if(num1.length !== num2.length) return false;

    const freCounter = {};

    while(num1 > 0) {
        let num = num1 % 10;
        freCounter[num] = (freCounter[num] || 0) + 1;
        num1 = Math.floor(num1 / 10);
    }

    while(num2 > 0) {
        let num = num2 % 10;
        if(!freCounter[num]) {
            return false;
        } else {
            freCounter[num] -= 1;
        }
        num2 = Math.floor(num2 / 10);   
    }

    return true;
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
function areThereDuplicates() {
    const freCounter = {};
    
    for(let i = 0; i < arguments.length; i++) {
        if(freCounter[arguments[i]]) {
            return true;
        } else {
            freCounter[arguments[i]] = 1;
        }
    }
    
    return false;
}
```
#### areThereDuplicates One Liner Solution
```javascript
function areThereDuplicates() {
  return new Set(arguments).size !== arguments.length;
}
```