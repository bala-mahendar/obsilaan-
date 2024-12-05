![[Pasted image 20241129223413.png]]

  `let` This keyword is designed for block-scoping, meaning it is ideal for use in loops and conditionals where you want each iteration to have its own scope.
 
 `const` Constants are also used to store certain values, but once values have been entered into them during initialization, they can no longer be modified.
 
 If we declare any variable or constant using let or const, respectively, outside the code blocks, they will be **global**. By this we mean that their names will be visible throughout the program, outside blocks, inside blocks, in functions, and so on.
 This will create a local variable or constant.
 
==================================================================================================
After this short introduction to functions (this is obviously not our last meeting with them) let's return to the keyword `var` and variable scopes.

If we declare a variable using the keyword `var` inside a function, its scope will be limited only to the inside of that function (it's a local scope). This means that the variable name will be correctly recognized only inside this function.
```
var  globalGreeting  =  "Good  ";
   
function  testFunction()  {
         var  localGreeting  =  "Morning  ";    
         console.log("function:");
         console.log(globalGreeting);
         console.log(localGreeting);
}
   
testFunction();
   
console.log("main  program:");
console.log(globalGreeting);
console.log(localGreeting);  //  ->  Uncaught  ReferenceError:  localGreeting  is  not  defined
```

The `typeof`  operator just mentioned is unary (it takes only one argument) and informs us of the type of data.


### Formatting 

```
let  country  =  "Malawi";
let  continent  =  "Africa";
   
let  sentence  =  `${country}  is  located  in  ${continent}.`;
console.log(sentence);  //  ->  Malawi  is  located  in  Africa.
```

### String manipulation

*.length*
*.slice(beginindex , endindex)
.charAt(index)
.split(charater)*
[]()
```
let  str  =  "java  script  language";
   
console.log(str.length);  //  ->  20
console.log('test'.length);  //  ->  4
   
console.log(str.charAt(0));  //  ->  'j'
console.log('abc'.charAt(1));  //  ->  'b'
   
console.log(str.slice(0,  4));  //  ->  'java'
console.log('test'.slice(1,  3));  //  ->  'es'
   
console.log(str.split('  '));  //  ->  ['java',  'script',  'language']
console.log('192.168.1.1'.split('.'));    //  ->  ['192',  '168',  '1',  '1']
```

## Complex Data Types 

##### Objects:

```
let testob = {
name : "A",
rno : 1,
email : "a@gmial.com"
};
console.log(testob.name);
```

###### Modilfication / Deletion :
deleting  : `delete users.name`
modification :  `user.age = 24`


#### Arrays :  We can easily create an array containing elements of different type

```
let days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
console.log(days[0]);
```

#### Combination of Array and object : 
```
let  users  =[ //opening array 
         { // opening object
                 name:  "Calvin",
                 surname:  "Hart",
                 age:  66,
                 email:  "CalvinMHart@teleworm.us"
         },
         {
                 name:  "Mateus",
                 surname:  "Pinto",
                 age:  21,
                 email:  "MateusPinto@dayrep.com"
         } // closing object
]; // closing array
   
console.log(users[0].name); 
console.log(users[1].age);  

```

If we would like to make sure that the variable contains an array, we can do it using the instanceof operator, among others. It is closely related to object-oriented programming.

```
let  days  =  ["Sun",  "Mon",  "Tue",  "Wed",  "Thu",  "Fri",  "Sat"];
let  day  =  "Sunday";
   
console.log(days  instanceof  Array);  //  ->  true
console.log(day  instanceof  Array);  //  ->  false

```

##### Array operation 

*list.length
list.indexOf("---")
list.push("------") ==> pushes in the end (n)
list.unshift("------") ==> pushes in the front (0)
list.pop() ==> removes from end
list.shift() ==> shift by 1 length 
list.reverse()
list.slice( begin , last)
list1.concat(list2)
list

#### Operator and User Interaction : 

The AND operator will return the first operand if it evaluates to false, and the second operand otherwise. The OR operator will return its first operand if it evaluates to true, and the second operand otherwise.

```
console.log(true && 1991); // -> 1991
console.log(false && 1991); // -> false
console.log(2 && 5); // -> 5
console.log(0 && 5); // -> 0
console.log("Alice" && "Bob"); // -> Bob
console.log("" && "Bob"); // -> empty string
 
 
console.log(true || 1991); // -> true
console.log(false || 1991); // -> 1991
console.log(2 || 5); // -> 2
console.log(0 || 5); // -> 5
console.log("Alice" || "Bob"); // -> Alice
console.log("" || "Bob"); // -> Bob

```



we can use either the **identity** (strict equality) operator === or the **equality** operator ==
console.log(0 == false); // -> true
console.log(0 === false); // -> false

#### Comparison operators:
```
console.log(10 === 5); // -> false
console.log(10 === 10); // -> true
console.log(10 === 10n); // -> false
console.log(10 === "10"); // -> false
console.log("10" === "10"); // -> true
console.log("Alice" === "Bob"); // -> false
console.log(0 === false); // -> false
console.log(undefined === false); // -> false

```


```
console.log(10 !== 5); // -> true
console.log(10 !== 10); // -> false
console.log(10 !== 10n); // -> true
console.log(10 !== "10"); // -> true
console.log("10" !== "10"); // -> false
console.log("Alice" !== "Bob"); // -> true
console.log(0 !== false); // -> true
console.log(undefined !== false); // -> true
console.log(10 != 5); // -> true
console.log(10 != 10); // -> false
console.log(10 != 10n); // -> false
console.log(10 != "10"); // -> false
console.log("10" != "10"); // -> false
console.log("Alice" != "Bob"); // -> true
console.log(0 !=  false); // -> false
console.log(undefined != false); // -> true
console.log(NaN != NaN); // -> true

console.log(10 > 100); // -> false
console.log(101 > 100); // -> true
console.log(101 > "100"); // -> true 
console.log(101 < 100); // -> false
console.log(100n < 102); // -> true
console.log("10" < 20n); // -> true
console.log(101 <= 100); // -> false
console.log(10 >= 10n); // -> true
console.log("10" <=  20); // -> true

console.log("b" > "a"); // -> true
console.log("a" > "B"); // -> true
console.log("B" > "A"); // -> true
console.log("A" > "4"); // -> true
console.log("4" > "1"); // -> true 
console.log("ab1" < "ab4"); // -> true
console.log("ab4" < "abA"); // -> true
console.log("abB" < "aba"); // -> true
console.log("aba" < "abb"); // -> true
console.log("ab" < "ab4"); // -> true


```


##### Ternary operator
```
let name = 1 > 2 ? "Alice" : "Bob";
console.log(name); // -> Bob
```


#### Precedence : (Important)
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators

### Simple program using the PROMPT() (user interaction) : 
```
let contacts = [{
name: "Maxwell Wright",
phone: "(0191) 719 6495",
email: "Curabitur.egestas.nunc@nonummyac.co.uk"
}, {
name: "Raja Villarreal",
phone: "0866 398 2895",
email: "posuere.vulputate@sed.com"
}, {
name: "Helen Richards",
phone: "0800 1111",
email: "libero@convallis.edu"
}];

let  name1 = prompt("What is your name ?")
let  phone1 = prompt("What is your phone ?")
let  email1 = prompt("What is your email ?")

contacts[1].name = name1;
contacts[1].phone = phone1;
contacts[1].email = email1;
let last = contacts.length - 1;

console.log(`${contacts[0].name} / ${contacts[0].phone} / ${contacts[0].email}`);
console.log(`${contacts[1].name} / ${contacts[1].phone} / ${contacts[1].email}`);
console.log(`${contacts[last].name} / ${contacts[last].phone} / ${contacts[last].email}`);
```

##### Conditional Looping :
###### for.. in ===> iteration of key : value 

```
let user = {
    name: "Calvin",
    surname: "Hart",
    age: 66,
    email: "CalvinMHart@teleworm.us"
};
for (let key in user) {
    console.log(key); // -> name, surname, age, email
};
```
###### for...of  ===> iteration of array, set , Maps

```
let cities = [
    { name: "New York", population: 18.65e6 },
    { name: "Cairo", population: 18.82e6 },
    { name: "Mumbai", population: 19.32e6 },
    { name: "São Paulo", population: 20.88e6 },
    { name: "Mexico City", population: 21.34e6 },
    { name: "Shanghai", population: 23.48e6 },
    { name: "Delhi", population: 25.87e6 },
    { name: "Tokyo", population: 37.26e6 }
];
for (let city of cities) {
    if (city.population > 20e6) {
     console.log(`${city.name} (${city.population})`);
    }
}
```
###### for  ===> Traditional one 

###### while and do while 


![[Pasted image 20241130222844.png]]

# Functions :
## Parameters validation : 

```
function getMeanTemp(temperatures) {
     if (!(temperatures instanceof Array)) {
      return NaN;
     }
}
//// checking the temperatures is instance of the ARRAY
```

## Recursion : (Factorial is Example)

```
function factorial (n) {
     return n > 1 ? n * factorial(n - 1) : 1;
}
console.log(factorial(6)); // -> 720
```

## Functions as first-class members:
 
The Function which can be stored in variables or passed as arguments to other functions.

#### Storing in Variable :
```
function showMessage(message) {
     console.log(`Message: ${message}`);
}
let sm = showMessage;
sm("This Works !!!@!!! "); 
```

#### Storing in Function :
```
function add(a, b) {
     return a + b;
}
function multiply(a, b) {
     return a * b;
}
function operation(func, first, second) {
     return func(first, second);
}
console.log(operation(add, 10, 20)); // -> 30
console.log(operation(multiply, 10, 20)); // -> 200

```


## Function as an expression :

Storing the function in variable itself instead of 
variable = function_name instead of  we use the varaible = function function_name(){   }

example : 
```
let myAdd = function add(a, b) {
     return a + b;
}
console.log(myAdd(10, 20)); // -> 30
console.log(add(10, 20)); // -> 30

```


### Callback Function : 

- **Synchronous Callbacks**: These are executed immediately after the outer function is called.
- **Asynchronous Callbacks**: These are invoked after some asynchronous operation has completed, such as fetching data from a server or waiting for a timer to finish
#### Synchronous :  
```
let inner = function () 
{
console.log("Inner 1");
}
let outer = function (callback) 
{
console.log("outer 1");
callback();  //  DIRECTLY CALLING USING ()
console.log("outer 2");
}

console.log("test 1");
outer(inner);
console.log("test 2");
```
##### Asynchronous:
```
let inner = function() {
console.log('inner 1');
}

let outer = function(callback) {
console.log('outer 1');
setTimeout(callback, 1000) /*ms*/; // WE DIDNT USE THE () FOR INTERVAL TIMER
console.log('outer 2');
}

console.log('test 1');
outer(inner);
console.log('test 2');

```

##### setTimeout / setInterval /clearInterval :

```
let inner = function() 
{
console.log('inner 1');
}


let outer = function(callback) 
{
console.log('outer 1');
let timerId = setInterval(callback, 1000);
console.log('outer 2');
setTimeout(function(){clearInterval(timerId);}, 5500);
}

console.log('test 1');
outer(inner);
console.log('test 2');

```

### Arrow functions :

An **Arrow function** is a shorter form of a function expression. An arrow function expression is composed of: parentheses containing zero to multiple parameters (if exactly one parameter is present, the parentheses can be omitted); an arrow that looks like this **"=>"**; and the body of the function, which can be surrounded by curly brackets if the body is longer.
###### Using "function" keyword :
```
let add = function(a, b) {
     return a + b;
}
console.log(add(10, 20)); // -> 30

```
##### Using Arrow Function : 
```
let add = (a, b) => {
     return a + b;
}
console.log(add(10, 20)); // -> 30
```


## Error handling statement:

##### Basic Types of Errors:
##### => SyntaxError : 
##### => Reference Error  : (accessing the undefined one (var / function) ).
##### =>TypeError : (occurs in the thing is not in expected format).
##### => RangeError : (accessing / initializing the index out of range).
##### => EvalError / InternalError / URIError ==> Rare Errors or use in networking or unexpected way of accessing

Syntax : 
```
try {
 ***********
 ***********
}
catch(error)
{
*************
*************
}
```
## Conditional Error Handling :
###### Checking the occurred error using the "instanceof ".
```
1. SYNTAX :  variable instanceof type
or
2. let result  = error instanceof ReferenceError;

Example : 
let a = -2;
try 
{
    a = b; // b is not declared / initialized
} 
catch (error) 
{
    if (error instanceof ReferenceError) {
        console.log("Reference error, reset a to -2");
        a = -2;
    } 
    else console.log("Other error - " + error);
}
console.log(a); // -> -2

```

## ``finally``  statement:
Can be used with / without catch statement. Always execute after the try...catch statement

```
Example : 
let a = 10;
try {
    a = 5;
} finally {
    console.log(a); // -> 5
}
console.log(a); // -> 5
```