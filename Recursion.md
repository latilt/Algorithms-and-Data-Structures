# Recursion
## What is Recursion?
A process(a function in our case) that calls ifself.
## Why do I need to know this?
It's everywhere used all the time.
* JSON.parse / JSON.stringify
* document.getElementById and Dom traversal algorithms
* Object traversal
* We will see it with more complex data structures
* It's sometimes a cleaner alternative iteration
## But first... Let's talk about functions
* In almost all program languages, there is a built in data structure that manages what happens when functions are invoked
* Javascript named the call stack.
## The call stack
* It's a stack data structure
* Any time a function is invoked it is placed (pushed) on the top of the call stack
* When Javascript sees the return keyword or when the function ends, the compiler will remove(pop)
## What do I care?
* You're used to function being pushed on the call stack and popped off when they are done
* When we write recursive functions, we keep pushing new functions onto the call stack
## How recursive functions work
* Invoke the same function with a different input until you reach your base case
### Base Case
* The Condition when the recursion ends.
* This is the most important concept to understand
## Two essential parts of a recursive function
* Base Case
* Different Input
## Our first recursive function
```javascript
function countDown(num) {
    if(num <= 0) {
        console.log("All done!");
        return ;
    }
    console.log(num);
    num--;
    countDown(num);
}
```
## Our second recursive function
```javascript
function sumRange(num) {
    if(num === 1) return 1;
    return num + sumRange(num - 1);
}
```
* Can you spot the base case?
* Do you notice the different input?
* What would happen if we didn't return?
## Factorial
### Iteratively
```javascript
function factorial(num) {
    let total = 1;
    for(let i = num; i > 1; i--) {
        total *= i;
    }
    return total;
}
```
### Recursively
```javascript
function factorial(num) {
    if(num === 1) return 1;
    return num * factorial(num - 1);
}
```
## Where things go wrong
* No base case or wrong base case
* Forgetting to return or returning the wrong thing
* Stack overflow
## Helper Method Recursion
```javascript
function outer(input) {
    var outerScopedVariable = [];

    function helper(helperInput) {
        // modify the outerScopedVariable
        helper(helperInput--);
    }
    helper(input);

    return outerScopedVariable;
}
```
### Collect all of the odd values in an array
```javascript
function collectOddValues(arr) {
    let result = [];

    function helper(helperInput) {
        if(helperInput.length === 0) {
            return ;
        }

        if(helperInput[0] % 2 !== 0) {
            result.push(helperInput[0]);
        }

        helper(helperInput.slice(1));
    }
    helper(arr);

    return result;
}
```
### Pure Recrusion
```javascript
function collectOddValues(arr) {
    let newArr = [];

    if(arr.length === 0) {
        return newArr;
    }

    if(arr[0] % 2 !== 0) {
        newArr.push(arr[0]);
    }

    newArr = newArr.concat(collectOddValues(arr.slice(1)));
    return newArr;
}
```
#### Pure Recrusion Tips
* For arrays, use methods like slice, the spread opertaor, and concat that make copies of arrays so you do not mutate them
* Remember that strings are immutable so you will need to use methods like slice, substr, or substring to make copies of strings
* To make copies of objects use Object.assign, or the spread operator
---
## Recursion Problems
### Power
```
Write a function called power which accepts a base and an exponent.
The function should return the power of the base to the exponent.
This function should mimic the functionality of Math.pow()
- do not worry about negative bases and exponents.
```
```
밑과 지수를 입력받는 Power라는 함수를 작성하세요.
이 함수는 밑을 지수로 거듭제곱한 값을 반환해야합니다.
이 함수는 Math.pow ()의 기능을 모방해야합니다.
- 부정적인 밑 및 지수에 대해 고려하지 마십시오.
```
```javascript
power(2,0) // 1
power(2,2) // 4
power(2,4) // 16
```
```javascript
function power(base, exponent){
    if(exponent === 0) return 1;
    return base * power(base, exponent - 1);
}
```
---
### Factorial
```
Write a function factorial which accepts a number and returns the factorial of that number.
A factorial is the product of an integer and all the integers below it; e.g., factorial four(4!) is equal to 24,
because 4 * 3 * 2 * 1 equals 24. factorial zero (0!) is always 1.
```
```
숫자를 받아들이고 해당 숫자의 계승을 반환하는 함수 factorial를 작성하십시오.
factorial은 정수와 그 아래 모든 정수의 곱셈의 값입니다.
4 * 3 * 2 * 1이 24이기 때문에 4!는 24와 같습니다. 계승 0 (0!)은 항상 1입니다.
```
```javascript
factorial(1) // 1
factorial(2) // 2
factorial(4) // 24
factorial(7) // 5040
```
```javascript
function factorial(num){
   if(num === 1 || num === 0) return 1;
   return num * factorial(num - 1);
}
```
---
### Product Of Array
```
Write a function called productOfArray which takes in an array of numbers and return the product of them all.
```
```
productOfArray라는 함수를 작성합니다. 이 함수는 숫자 배열을 취하여 모든 변수를 곱한 값을 반환합니다.
```
```javascript
productOfArray([1,2,3]) // 6
productOfArray([1,2,3,10]) // 60
```
```javascript
function productOfArray(arr) {
    if(arr.length === 0) {
        return 1;
    }
    return arr[0] * productOfArray(arr.slice(1));
}
```
---
### Recursive Range
```
Write a function called recursiveRange which accepts a number
and adds up all the numbers from 0 to the number passed to the function
```
```
recursiveRange라는 함수를 작성합니다. 이 함수는 입력받은 숫자의 0부터 숫자까지의 합을 반환합니다.
```
```javascript
recursiveRange(6) // 21
recursiveRange(10) // 55 
```
```javascript
function recursiveRange(num){
   if(num === 0) return 0;
   return num + recursiveRange(num - 1);
}
```
---
### Fibonacci
```
Write a recursive function called fib which accepts a number and returns the nth number in the Fibonacci sequence.
Recall that the Fibonacci sequence is the sequence of whole number 1, 1, 2, 3, 5, 8, ... which starts with
1 and 1, and where every number thereafter is equal to the sum of the previous two numbers.
```
```
fib를 호출하고 피보나치 시퀀스에서 n 번째 숫자를 반환하는 재귀 함수를 작성하십시오.
피보나치 수열은 1과 1로 시작하는 정수 1, 1, 2, 3, 5, 8, ...의 순차이며
그 이후의 모든 수는 이전 두 수의 합과 같습니다.
```
```javascript
fib(4) // 3
fib(10) // 55
fib(28) // 317811
fib(35) // 9227465
```
```javascript
function fib(n){
    if (n <= 2) return 1;
    return fib(n-1) + fib(n-2);
}
```
---
### Reverse
```
Write a recursive function called reverse which accepts a string and returns a new string in reverse.
```
```
문자열을 입력받아 역순으로 반환하는 재귀 함수를 reverse를 작성합니다.
```
```javascript
reverse('awesome') // 'emosewa'
reverse('rithmschool') // 'loohcsmhtir'
```
```javascript
function reverse(str){
  if(str.length <= 1) return str;
  return reverse(str.substring(1)) + str[0];
}
```
---
### Palindrome
```
Write a recursive function called isPalindrome which returns true 
if the string passed to it is a palindrome(reads the same forward and backward). Otherwise it returns false.
```
```
isPalindrome이라는 재귀 함수를 작성합니다. isPalindrome은 전달 된 문자열이 회귀식 (앞뒤를 동일하게 읽음)이면
true를 반환합니다. 그렇지 않은 경우는 false를 리턴합니다.
```
```javascript
isPalindrome('awesome') // false
isPalindrome('foobar') // false
isPalindrome('tacocat') // true
isPalindrome('amanaplanacanalpanama') // true
isPalindrome('amanaplanacanalpandemonium') // false
```
```javascript
function isPalindrome(str){
    if(str.length <= 1) return true; 
    if(str[0] !== str[str.length-1]) return false;
    return isPalindrome(str.substring(1, str.length-1));
}
```
```javascript
function isPalindrome(str){
    if(str.length === 1) return true;
    if(str.length === 2) return str[0] === str[1];
    if(str[0] === str.slice(-1)) return isPalindrome(str.slice(1,-1))
    return false;
}
```
---
### someRecursive
```
Write a recursive function called someRecursive which accepts an array and a callback.
The function returns true if a single value in the array returns true when passed to the callback.
Otherwise it returns false.
```
```
배열과 콜백을 입력받는 someRecursive라는 재귀 함수를 작성하십시오. 
이 함수는 배열의 단일 값이 콜백에 전달 될 때 true를 반환하면 true를 반환합니다.
그렇지 않은 경우는 false를 리턴합니다.
```
```javascript
// const isOdd = val => val % 2 !== 0;
someRecursive([1,2,3,4], isOdd) // true
someRecursive([4,6,8,9], isOdd) // true
someRecursive([4,6,8], isOdd) // false
someRecursive([4,6,8], val => val > 10); // false
```
```javascript
function someRecursive(arr, callback){
    if(arr.length === 0) return false;
    if(callback(arr[0])) return true;
    return someRecursive(arr.slice(1), callback);
}
```
---
### Flatten
```
Write a recursive function called flatten which accepts an array of arrays
and returns a new array with all values flattened.
```
```
flatten이라는 재귀 함수를 작성합니다.
이 함수는 다차원배열을 받아들이고 모든 값이 병합 된 일차원배열을 반환합니다.
```
```javascript
flatten([1, 2, 3, [4, 5] ]) // [1, 2, 3, 4, 5]
flatten([1, [2, [3, 4], [[5]]]]) // [1, 2, 3, 4, 5]
flatten([[1],[2],[3]]) // [1,2,3]
flatten([[[[1], [[[2]]], [[[[[[[3]]]]]]]]]]) // [1,2,3
```
```javascript
function flatten(arr){
    let newArr = [];
    if(arr.length === 0) return newArr;
    if(typeof arr[0] === "object") {
        newArr = newArr.concat(flatten(arr[0]));
    } else {
        newArr.push(arr[0]);
    }
    newArr = newArr.concat(flatten(arr.slice(1)));
    return newArr;
}
```
```javascript
function flatten(oldArr){
    var newArr = []
        for(var i = 0; i < oldArr.length; i++){
            if(Array.isArray(oldArr[i])){
                newArr = newArr.concat(flatten(oldArr[i]))
            } else {
                newArr.push(oldArr[i])
            }
    } 
    return newArr;
}
```
---
### capitalizeFirst
```
Write a recursive function called capitalizeFirst. 
Given an array of strings, capitalize the first letter of each string in the array.
```
```
capitalizeFirst라는 재귀 함수를 작성하십시오.
문자열 배열의 각 문자열 첫 글자를 대문자로 변환하여 반환하십시오..
```
```javascript
capitalizeFirst(['car','taco','banana']); // ['Car','Taco','Banana']
```
```javascript
function capitalizeFirst (arr) {
    if(arr.length === 0) return [];
    let str = arr[0][0].toUpperCase() + arr[0].slice(1);
    return [str].concat(capitalizeFirst(arr.slice(1)));
}
```
---
### nestedEvenSum
```
Write a recursive function called nestedEvenSum.
Return the sum of all even numbers in an object which may contain nested objects.
```
```
nestedEvenSum이라는 재귀 함수를 작성하십시오.
중첩 된 객체를 포함 할 수 있는 객체의 모든 짝수의 합을 반환합니다.
```
```javascript
var obj1 = {
    outer: 2,
    obj: {
        inner: 2,
        otherObj: {
        superInner: 2,
        notANumber: true,
        alsoNotANumber: "yup"
        }
    }
}

var obj2 = {
    a: 2,
    b: {b: 2, bb: {b: 3, bb: {b: 2}}},
    c: {c: {c: 2}, cc: 'ball', ccc: 5},
    d: 1,
    e: {e: {e: 2}, ee: 'car'}
};

nestedEvenSum(obj1); // 6
nestedEvenSum(obj2); // 10
```
```javascript
function nestedEvenSum (obj) {
    let sum = 0;
    for(let key in obj) {
        if(typeof obj[key] === "object") {
            sum += nestedEvenSum(obj[key]);
        }
        if(typeof obj[key] === "number" && obj[key] % 2 === 0) {
            sum += obj[key];
        }
    }
    
    return sum;
}
```
---
### capitalizeWords
```
Write a recursive function called capitalizeWords. 
Given an array of words, return a new array containing each word capitalized.
```
```
capitalizeWords라는 재귀 함수를 작성하십시오.
각각의 단어를 대문자로 변환한 배열을 반환합니다.
```
```javascript
let words = ['i', 'am', 'learning', 'recursion'];
capitalizedWords(words); // ['I', 'AM', 'LEARNING', 'RECURSION']
```
```javascript
function capitalizeWords (arr) {
    let newArr = []
    if(arr.length === 0) return newArr;
    newArr.push(arr[0].toUpperCase());
    return newArr.concat(capitalizeWords(arr.slice(1)));
}
```
---
### stringifyNumbers
```
Write a function called stringifyNumbers which takes in an object and finds all of the values
which are numbers and converts them to strings. Recursion would be a great way to solve this.
```
```
stringifyNumbers라는 함수를 작성합니다. 이 함수는 객체 안의 숫자인 값을 찾아서 문자열로 변환합니다.
재귀는 이것을 해결할 수있는 좋은 방법입니다.
```
```javascript
let obj = {
    num: 1,
    test: [],
    data: {
        val: 4,
        info: {
            isRight: true,
            random: 66
        }
    }
}
stringifyNumbers(obj)
{
    num: "1",
    test: [],
    data: {
        val: "4",
        info: {
            isRight: true,
            random: "66"
        }
    }
}

```
```javascript
function stringifyNumbers(obj) {
    let newObj = {};
    for(let key in obj) {
        if(typeof obj[key] === "object" && !Array.isArray(obj[key])) {
            newObj[key] = stringifyNumbers(obj[key]);
        } else if(typeof obj[key] === "number") {
            newObj[key] = obj[key] + "";
        } else {
            newObj[key] = obj[key];
        }
    }
    
    return newObj;
}
```
---
### collectString
```
Write a function called collectStrings which accepts an object
and returns an array of all the values in the object that have a typeof string
```
```
객체의 모든 값 중 문자열들인 값을 담은 배열을 반환하는 collectStrings라는 함수를 작성하십시오.
```
```javascript
const obj = {
    stuff: "foo",
    data: {
        val: {
            thing: {
                info: "bar",
                moreInfo: {
                    evenMoreInfo: {
                        weMadeIt: "baz"
                    }
                }
            }
        }
    }
}

collectStrings(obj) // ["foo", "bar", "baz"])
```
```javascript
function collectStrings(obj) {
    let result = [];
    for(let key in obj) {
        if(typeof obj[key] === "object") {
            result = result.concat(collectStrings(obj[key]));   
        }
        if(typeof obj[key] === "string") {
            result.push(obj[key]);
        }
    }
    
    return result;
}
```