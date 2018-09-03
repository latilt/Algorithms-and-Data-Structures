## Analyzing Performance Arrays and Objects

#### When to use Objects
- When you don't need order
- When you need fast access / insertion and removal

##### Big O of Objects
Insertion - $O(1)$
Removal - $O(1)$
Searching - $O(N)$
Access - $O(1)$

정렬이 필요 없을 경우 객체를 선택하는게 좋다.

##### Big O of Objects Methods
Object.key - $O(N)$
Object.values - $O(N)$
Object.entries - $O(N)$
hasOwnProperty - $O(1)$

---

#### When to use Arrays
- When you need order
- When you need fast access / insertion and removal(sort of ...)

##### Big O of Arrays
Insertion - It depends...
Removal - It depneds...
Searching - $O(N)$
Access - $O(1)$

배열의 끝 부분에서의 추가, 삭제는 변수의 추가와 인덱스 설정만 하면 되므로 빠르지만
배열의 시작 부분에서의 추가, 삭제는 배열의 인덱스를 재설정해야 하므로 $O(N)$으로 느리다.

##### Big O of Array Operations
push - $O(1)$
pop - $O(1)$
shift - $O(N)$
unshift - $O(N)$
concat - $O(N)$
slice - $O(N)$
splice - $O(N)$
sort - $O(NlogN)$
forEach/map/filter/reduce/etc. - $O(N)$

