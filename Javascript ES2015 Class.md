# Javascript ES2015 Class
## What is a class
A blueprint for creating objects with pre-defined properties and methods
## The Syntax
```javascript
class Student {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```
The method to create new objects must be called constructor
### Creating objects from classes
```javascript
let firstStudent = new Student("Colt", "Steele");
let secondStudent = new Student("Blue", "Steele");
```
We use new keyword
## Instance Methods
```javascript
class Student {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    fullName() {
        return `Your full name is ${this.firstName} ${this.lastName}`;
    }
}

let firstStudent = new Student("Colt", "Steele");

firstStudent.fullName(); // "Your full name is Colt Steele"
```
## Class Methods
```javascript
class Student {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    fullName() {
        return `Your full name is ${this.firstName} ${this.lastName}`;
    }
    static enrollStudents(...students) {
        // maybe send an email here
    }
}

let firstStudent = new Student("Colt", "Steele");
let secondStudent = new Student("Blue", "Steele");

Student.enrollStudents([firstStudent, secondStudent]);
```
## How we'll be using classes
```javascript
class DataStructures() {
    constructor() {
        // what default properties should it have?
    }
    someInstanceMethod() {
        // what should each object created from this class be able to do?
    }
}
```