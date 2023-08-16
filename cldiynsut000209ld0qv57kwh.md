---
title: "10 JavaScript Tricks That Every Developer Should Know."
seoTitle: "10 JavaScript Tricks That Every Developer Should Know"
seoDescription: "Here are 10 javascript tricks you need to know and adopt while coding for readability and efficiency."
datePublished: Mon Jan 30 2023 15:23:44 GMT+0000 (Coordinated Universal Time)
cuid: cldiynsut000209ld0qv57kwh
slug: 10-javascript-tricks-that-every-developer-should-know
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FP_N_InBPdg/upload/2d799f358f52cbdf419e811c14e7c18c.jpeg
tags: javascript, developer, html5, howtos, iamkelv

---

Javascript is one of the most popular and uses JIT (just-in-time) programming language with first-class functions.

One of the ways to grow as a javascript developer is by adapting to the new coding pattern that is introduced and frequently used by most engineers

Here are 10 javascript tricks you need to know and adopt while coding for readability and efficiency.

### **1\. Use the optional chaining operator (?.)**

The operational chaining operator is denoted by (?.) which allows you only to access a function, object property or variable if it exists or if it's not found it returns undefined

Let's start with the old method for better understanding. we will use the `if` statement to check if a user entered his name or not.

```javascript
function user() {
    const profile = {
        username: 'Iamkelv',   
    }                
    //Using the if statement
    if(profile.username){
          return profile.username ;
      }else{
          return undefined
     }
};
```

The code above uses the normal `if` statement that will execute though the condition has multiple lines of code.

Using the *optional chaining operator,* we can achieve the same result with a single line of code as shown below

```javascript
function user() {
    const profile = {
        username: 'Iamkelv',   
        }                
    //Using the optional chaining operator
   return profile?.username
};
```

### 2\. Self-Invoking Functions

Self-Invoking functions are functions that execute themselves. This is all about scoping because any variable that is declared in a self-invoking function is only accessible within the function by default.

This allows the practice of naming variables without worrying about how the variable is named in another block on javascript and not being affected as shown below

```javascript
function user() {
    let firstName = "Kelvin"  
    console.log(firstName)
}
user()
console.log(lastName)
//The code above won't run because lastName is not defined
```

The code above won't run because `lastName` is not a defined variable so the execution will break

```javascript
(function user() {
    let firstName = "Kelvin"  
    console.log(firstName)
})();
console.log(lastName)
```

The code above will log `Kelvin` before showing the error that `lastName` is not defined because the function automatically executes itself.

### 3\. Array Copying with Spread (...)

Another trick is creating a copy of an array using the spread operator (...)

One of the best ways of using an array is to avoid mutating the array, rather you can create a copy of the original array and mutate the copy and one of the easiest ways is using the spread operator as shown below.

```javascript
const age = [10, 13, 20, 25, 30];
const newAge = [...age];

console.log(age,  newAge);
//output age: [10, 13, 20, 25, 30]
//output newAge: [10, 13, 20, 25, 30]
```

### 4\. Remove Array Duplicates

You must have been faced with scenarios where you want to remove duplicate elements from an array. one of the most common tricks is the use of the `Set` data structure

Since `Set` data structure doesn't allow duplicate elements we can take advantage of the data structure by turning the `Array` into a `Set` as shown below.

```javascript
const age = [10, 13, 20,10,14,13,30, 25, 30];
const noDuplicate = [...new Set(age)]

console.log(noDuplicate );
//OUPUT : [10, 13, 20, 14, 30, 25]
```

### 5\. **Merging arrays the right way**

Though this trick may sound familiar to some javascript developers by using the `array.concat()` method to merge two arrays as shown below.

```javascript
var arr1 = [1, 2]; 
var arr2 = [3, 4]; 
console.log(arr1.concat(arr2)); 
// OUTPUT [1,2,3,4];
```

The problem with the above method is that when you are dealing with big size of arrays it will consume a lot of memory while emerging the array

Here is the trick, whenever you are dealing with a big-size array always use `array.push.apply(arr1, arr2)` which uses less memory compared to using the `array.concat(arr1)` as shown below.

```javascript
var arr1 = [1, 2]; 
var arr2 = [3, 4]; 
console.log(arr1.push.apply(arr1, arr2)); 
// OUTPUT : [1,2,3,4];
```

### 6\. **Swapping two variables without the third variable**

Since adding a variable requires more memory, removing the third variable will make the code a bit more efficient.

The old way of swapping variables has been creating a third variable mostly called a temporary variable as shown below.

```javascript
let a = 10;
let b = 20;

let temp = x;
a = b;
b = temp
console.log(a,b)  // 20 10
```

However, because the creation of a variable necessitates additional memory, the code above will not be as efficient as the one below, which only employs two variables.

```javascript
let a = 10;
let b = 20;
[a, b] = [b, a]; // x = 20, y = 10
```

### **7\. Resize or Empty an Array Using array.length**

Resizing the size of an array can be achieved in different ways in javascript but which include using the inbuilt array method.

But one of the most common tricks being used in many codebases is reassigning a new array size as shown below.

```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];

console.log(arr.length); // returns the length as 15

arr.length = 4;

console.log(arr.length); // returns the length as 4
console.log(arr); // returns [1, 2, 3, 4]
```

### 8\. **Check Falsy Values in an Array**

Another common trick to note as a javascript developer is the value falsy value in an array.

You must have used the `some`, `every`, and `filler` array methods but most have not thought of using a boolean type to check if values exist in an array or not as shown below.

```javascript
const myArr = [false, 'Mercy', undefined, 0, null, 'Kelvin'];

// filter falsy values
const filtered = myArr.filter(Boolean);
console.log(filtered); // returns ['Mercy', 'Kelvin']

// check if at least one value is truthy
const checkAnyTruthy = myArr.some(Boolean);
console.log(checkAnyTruthy); // returns true

// check if all values are truthy
const allValTruthy = myArr.every(Boolean);
console.log(allValTruthy); // returns false
```

### 9\. **Flattening Arrays of Arrays**

You may familiar with the Array `flat` prototype. One of the use cases of the `flat` prototype is when working on a nested array and you may be trying to convert it to an array.

The flat method lets you make a single array from a nested array as shown below.

```javascript
const myArr = [[1,3,4], [5,6], 7, 8];
console.log(myArr)  //return [[1,3,4], [5,6], 7, 8]

const flattedArr = myArr.flat(); 
console.log(flattedArr) //return [1, 3, 4, 5, 6, 7, 8]
```

### 10\. **Leverage the destructuring assignment syntax**

Last but not least our top trick is leveraging the destructuring assignment.

Destructuring assignments make it possible to unpack values from arrays or properties from objects to distinct variables.

One of the use cases of leveraging destructuring assignment is when you want to extract specific properties or elements from an array or object as shown below.

```javascript
const { first_Name, last_Name } = {first_Name:"Kelvin", last_Name:'Moses', values:[1,2,34,5,6,7,8]};

console.log(first_Name) // return Kelvin



const { first_Name: firstName, last_Name: lastName } = {first_Name:"Kelvin", last_Name:'Moses', values:[1,2,34,5,6,7,8]};

console.log(firstName) // return Kelvin
```

## **Conclusion**

The article discusses 10 useful JavaScript tricks for developers to improve their coding efficiency and readability.

These tricks include using the optional chaining operator, self-invoking functions, array copying with spread, removing array duplicates, merging arrays efficiently, swapping variables without a third variable, and resizing or emptying an array using array.length, checking falsy values in an array, flattening arrays of arrays, and leveraging the destructuring assignment syntax.

I hope you find these resources helpful 😊

I'd love to connect with you on **Twitter** | **LinkedIn** | [**GitHub**](https://github.com/iamkelv/)

See you in my next blog article. Take care!!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675076292013/375947bb-2b24-4bc4-8801-500bad65c123.gif align="center")