# Sorting Algorithm
## What is sorting?
Sorting is the process of rearranging the items in a collection (e.g. an array) so that the items are in some kind of order.
## Why do we need to learn this?
* Sorting is an incredibly common task, so it's good to know how it works
* There are many different ways to sort things, and different techniques have their own advantages and disadvantages
* Sorting sometimes has quirks, so it's good to understand how to navigate them
## Javascript Sort Method
자바스크립트 자체 정렬 함수가 있지만 유니코드를 기반으로 정렬하기 때문에 잘못된 결과가 나타날 수도 있다. 그에 대비해 어떤 방식으로 정렬할지 함수형식으로 방식을 알려 줄 수 있다.
* The built-in sort method accepts an optional comparator function
* You can use this comparator function to tell JavaScript how you want it to sort
* The comparator looks at pairs of elements (a and b), determines their sort order based on the return value
    * If it returns a negative number, a should come before b
    * If it returns a positive number, a should come after b,
    * If it returns 0, a and b are the same as far as the sort is concerned
## Big O of Sorting Algorithms
Algorithm | Time Complexity(Best) | Time Complexity(Average) | Time Complexity(Worst) | Space Complexity
------| --------- | --------- | ------ | -----
Bubble Sort | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$
Insertion Sort | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$
Selection Sort | $O(N^2)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$
* 버블정렬은 데이터가 어느 정도 정렬이 되어 있을때 효율이 좋다.
* 선택정렬은 배우기가 쉽다는 장점이 있다.
* 삽입정렬은 이미 정렬된 데이터의 뒤쪽으로 데이터를 삽입한 후 정렬할 때 효율이 좋다.