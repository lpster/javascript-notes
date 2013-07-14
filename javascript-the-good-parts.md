#Javascript: The Good Parts by Doug Crockford
URL: http://shop.oreilly.com/product/9780596517748.do

**Background/Review:** Because this book was recommended by so many people, I started reading it about a year ago, but quickly got bored by the technical terms and transitioned to a tutorial about jQuery -- which was much easier to understand and had some satisfying immediate applications. I'm going back to this book, now, so that I can get a better grounding in the language that powers jQuery, which is really only a javascript library. Having gone through Codecademy's JS exercises and some immediate application practice with jQuery, I've found this second time read-through much easier to understand. Below contain my [rather thorough] notes of "The Good Parts." I will try to keep this document updated consistently until I reach the end of the book.

**Warning:** I would NOT recommend this book to a complete Javascript beginner, especially someone who's learning how to code for the first time. They'll have to wade through paragraphs describing "invocation patterns" or other simple, re-occurring javascript uses and be confused by it all. It's also somewhat boring to read when you're starting out with no idea about how you can use javascript. For someone who already has some experiences with javascript or other programming languages, however, this book is great.

##Chapter 1: Good Parts
- book will focus on the good parts with occasional warnings to avoid the bad

###1.2 Analyzing Javascript
- good ideas include functions, loose typing, dynamic objects, and object literal notation. 
- bad ideas include global variables.
- first lambda language to go mainstream
- "loosely typed" means JS compilers cannot detec type errors
- class-free object system: objects inherit properties directly from other objects
- BAD: depends on global variables for linkage. 

http://www.ecma-international.org/publications/files/ecma-st/ECMA-262.pdf -- standard that defines Javascript -- leaves out the bad parts. 

*JSLint* - a JS parser that can help you find the bad parts. 
URL: http://www.jslint.com/

Crockford goes on to talk about the importance of using Javascript. 

###1.3 A Simple Testing Ground

In program.js, write:
    document.writeIn('hello,world!');

A **method** method is used to define new methods. Its definition:
 
    Function.prototype.method = function (name,func) 
    	this.prototype[name] = func;
    	return this;
    	}; //Will be explained in chapter 4


##Chapter 2: Grammar
###2.1 Whitespace
- usually insignificant
- Two ways to write comments:
	1. /* */
	2. //
	Beware that /* */ can occur in regular expression literals, though, so using /* */ can occasionally cause a syntax error.

###2.1 Names
- names have to begin with a letter, but can be followed by letters, digits, underbars, etc. Names CANNOT be the following:
	- abstract boolean break byte case catch char class const continue debugger default delete do double else enum export extends false final finally float for funciton goto if implements import in instanceof int interface long native new null package private protected public return short static super switch synchronized this throw throws transient true try typeof var volatile void while with undefined NaN Infinity (the last three added on just because)
- do not use the above as names for object properties either

###2.3 Numbers
- JS: single number type, 64-bit floating point (same as Java)
- UNLIKE most other programming languages, 1 and 1.0 are the same value. This is convenient. 
- 100 can also be written as 1e2
- **NaN** means "not equal to any value, including itself." You can detect whether a number is NaN using the isNan( *number* ) function.
- **Infinity** == bigger than 1.79769313486231570e+308
- Numbers have methods. 
	1. For example: Math.floor( *number* ) converts the number into an integer. 
	Math is an object; floor is a method. 

###2.4 Strings
- \backslash is the escape character for strings. 
- "seven".length == 5
- Once a string is made, it cannot be changed. However, you can concatenate two strings together. For example: 'd' + 'o' + 'g' = 'dog'.
- Strings have methods. For example, 'dog'.toUpperCase( ) === 'DOG'

###2.5 Statements
- the "var" statement in a function defines a private variable. 
- switch, while, for, and do can optionally have "break" statements.
- unlike other languages, blocks in JS do not create a new scope (?), so variables should be defined at the top of functions and not within blocks [Note: not entirely sure what this means]
- *falsy* values include: false, null, undefined, empty string '', 0, NaN. All other values evaluate to true.

For statement:
1. initialization
2. condition
3. increment

For in statement:
- "on each iteration, another property name string from the *object* is assigned to the *variable*"
- Note: use object.hasOwnProperty(variable) to test whether the property name is truly a member of the object (Note: ???)

Do while statement:
- block will always be executed at least once. The "do" statement is tested after the block executes. 

Return:
- early return of a function. If the return expression is not specificied, the return will be undefined. 

Break:
- exits the loop

= operator is used for assignment. === is the equality operator.

###2.6 Expressions
- "?" ternrary operator takes three operands. If first is truthy, value of second operand is produced. If first is falsy, valeu of third operand is produced.
- possible results from 'typeof': numbers, string, boolean, undefined, function, object
- if the operand of ! is truthy, it produces false. Otherwise, it produces true.
- / operator can produce a noninteger
- && operator produces value of first operand if the first is false.
- || operator produces the value of the first operand if the first is truthy.
- invocation: ()

###2.7 Literals
- **Object literals** are a notation for specifying new objects. 
- the names of the properties are literal names, not variable names
- value of the properties are expressions
- **Array literals** specify new arrays. 
- more about regular expressions later.

###2.8 Functions
- function literal defines a function value. 
- can have an optional name to call itself recursively.
- can specify parameters
- more later

##Chapter 3: Objects
- there are numbers, strings, booleans, null, and undefined
- then there are *objects*
- numbers, strings, booleans, etc. have methods, but they are immutable
- objects are *mutable*. They include arrays, functions, regular expressions, and objects. 
- Definition: container of properties. Each property has a name and a value. Values can be any JS value except *undefined*.
- Objects in Javascript are class-free (?? what does this mean?)
- no constraints on the names of new properties or on values of properties
- objects can also contain other objects
- one object can inherit the properties of another. This feature allows for the reduction of object init time and memory consumption.

###3.1 Object Literals
-e.g. var something= {
	"a" = "1",
	"b" = "2",
	"c" = "3"
	 }
- quotation marks are optional for legal and non-reserved JS names, e.g. first_name
- objects can nest. e.g.
	var flight = {
		sport: 'quidditch',
		number: 12,
		beginning: {
			location: "bulgaria",
			type: "world cup",
			"players": "krum and fitchvizal"
	},
		ending: {
			location: "ireland",
			type: "world cup",
			"players": "irish"
	}
};

###3.2 Retrieval
- dot notation is preferred to []. Dot notation ca be used if the string expression is a string literal and a legal JS name (not reserved word).
- e.g. wizard["first-name"] // "Harry"
- e.g. instrument.broomstick.owner // "Harry"
- If the retrieval produces something nonexistent, will get //undefined.
- can use || to fill in default values, e.g. var name = wizard["first-name"] || "Gandalf";
- attempting to retrieve values from undefined will throw a TypeError exception. Can use && to fix ???


###3.3 Update
- values can be udpated by assigning another value to it

###3.4 Reference
- objects are passed around by reference, not copied. 
- references to the same object... references to different empty objects (see examples in book)

###3.5 Prototype
- every object are linked to object.prototype, from which it can inherit properties
- **create** method
- **beget** method create a new object that uses an old object as its prototype
- when you create a new object, you can select the object that should be its prototype
- if a property value from an object doesn't exist when we try to retrieve it, JS will try to retrieve the value from the prototyep object, and *its* prototype object, and so on until the default is **Object.prototype**. If the property value still does not exist, we get *undefined*. **Delegation**.

###3.6 Reflection
- **typeof** operator is useful in determining the type of a property
- e.g. typeof flight.number // 'number'
		- type of flight.status //'string'
		- typeof flight.arrival //'object'
		- typeof flight.manifest //'undefined'
		- typeof flight.toString //'function'
		- typeof flight.consructor // 'function'
- some values could be **functions** -- be careful!
- the **hasOwnProperty** methods returns *true* if the object has a particular property, and does not look at the prototype chain. So flight.hasOwnProperty('number') will return true, and flight.hasOwnProeprty('constructor') will return false.

###3.7 Enumeration
- the **for in** statement can loop over all of the property names in an object. 
- e.g. 
    var name;
    for (name in another_stooge) {
    	if (typeof anothe_stooge[name] !-- 'function') {
    		document.writeIn(name + ': ' + another_stooge[name]);
    }
}
- if you want the properties to appear in a particular order, avoid **for in**, and instead make an array containing the names of the properties are in the right order. Use a regular for loop.
- e.g. 
    var i;
    var properties = [
    	'first-name',
    	'last-name'
    ];
    for (i = 0; i< properties.length; i +=1 ) {
    document.writeIn(properties[i] + ': ' +
    another_stooge[properties[i]]);
}

###3.8 Delete 
- e.g. **delete another_stooge.nickname;**
- sometimes removing a property from an object might allow a property from the "prototype linkage" to reveal itself.

###3.9 Global Abatement
- it's easy to define global variables, but they should be avoided since they weaken the "resiliency" of programs
- one way to minimize global variables is to create a single global variable for your application. e.g. var MYAPP = {};
- You can then use MYAPP as a container. e.g.
    MYAPP.stooge = {
    	"first-name": "Harry",
    	"lst-name": "Potter"
};

MYAPP.flight = {
	airline: "Oceanic",
	number: 815,
	departure: {
		IATA: "SYD",
		time: "2004-09-22 14:55",
		city: "Oakland"
},
	arrival: {
		IATA: "LAX",
		time: "2004-09-23 10:42",
		city: "Los Angeles"
}
};
- you can reduce your chance of bad interactions with other applications, widgets, and libraries if you reduce your global footprint to a single name. 
- Next chapter introduces the concept of closure for information hiding

##Chapter 4: Functions

###4.1 Function Objects
- Functions are objects. 
- Objects are collections of name/value pairs that have a hidden link to a prototype object
- Objects produced from object literals are linked to **Object.prototype**.
- Function objects are linked to **Function.prototype**, which is itself linked to object.prototype 
- Every function is created with two hidden properties: the function's context and the code that implements the function's behavior.
- Function objects are created with a prototype property, whose value is an object with a constructor property, whose value is the function. //wow, convoluted much?
- Functions are objects, so can be stored in variables, objects, and arrays, passed as arguments to functions, and returned from functions, and can have methods. 
- Special thing about functions: they can be *invoked*. 

###4.2 Function Literal
- **Function objects** are created with **function literals**.
- For example:
    var add = function(a,b) {
    return a+b;
    }
- Four parts to a function literal:
	1. function
	2. the function's name (if no name, it is *anonymous*)
	3. set of parameters of the function, wrapped in parentheses. There can be 0 or more parameter names, separated by commas, in here. These names are defined as variables in the function. Instead of being initialized to **undefined** as with normal variables, they are initialized to the "arguments supplied when the function is invoked."
	4. { }
- functions can be defined inside of other functions. An inner function has access to the outer function's parameters and variables.
- the function object created by a function literal contains a link to that outer context ??? - which is called **closure**. Enormous expressive power??

###4.3 Invocation
- invoking a function stops the execution of the current function and passes control/parameters to the new function.
- in addition to the declared parameters, every function receives 2 additional parameters: **this** and **arguments**.
- the value of "this" is determined by the **invocation pattern**, of which there are four patterns:
	1. method invocation pattern
	2. function invocation pattern
	3. constructor invocation pattern
	4. apply invocation pattern
- "The patterns differ in how the bonus parameter **this** is initialized." ??
- invocation operator: (), which can contain 0 or more expressions.
- There is no runtime error when the number of arguments and the number of parameters do not match. 
- *Undefined* will be substituted for the missing values if there are too few argument values, and extra argument values will be ignored.
- There is no type checkign on the argument values; any type of value can be passed to any parameter. 

###4.3.1 The Method Invocation Pattern
- When a function is stored as a property of an object, we call it a *method*.
- when a method is invoked, "this" is bound to the object

###4.3.2 The Function Invocation Pattern
- when a function is invoked e.g. var sum = add(3,4); , *this* is bound to the global object.
- mistake in the design of the language
- if had been designed correctly, when inner function invoked, *this* would be bound to the *this* variable of the outer function.

###4.3.3 The Constructor Invocation Pattern
- the language of JS is class-free, which means that objects can inherit properties directly from other objects. It's a *prototypal* inheritance language.
- most languages are *classical*. JS also offers an object-making syntax that's reminiscent of the classical languages. 
- the **new** prefix creates a new objectwith a hidden link to the value of the function's **prototype** member, and **this** will be bound to that new object. Functions that use **new** are called *constructors*.

###4.3.4 The Apply Invocation Pattern
- functions can have methods
- The **apply** method constructs an array of arguments to use to invoke a function, and lets us choose the value of **this**. The **apply** method takes two parameters: 1) the value that should be bound to **this**; 2) array of parameters. 
 e.g.

     //Make an array of two numbers and add them
     var array = [3,4];
     var sum = add.apply(null, array);

     //Make an object with a status member.

     var statusObject = {
     	status: 'A-OK'
 	 };

 	 var status = Quo.prototype.get_status.apply(statusObject);

###4.4 Arguments
- bonus parameter available to functions when they're invoked: the **arguments** array. It gives the function access to all of the arguments that were supplied with the invocation, including excess arguments that were not assigned to parameters. This makes it possible to write functions that take an unspecified number of parameters:

e.g. function that adds a lot of numbers
    var sum = function() {
    var i, sum = 0;
    for (i=0; i < arguments.length; i+=1) {
    	sum += arguments[i];
    }
    return sum;
};

document.writeIn(sum(4,8,15,16,23,42)); // 108
- Chapter 6: add a similar method to an array.
- Because of a design error, **arguments** is not really an array. Has a **length** element, but **lacks all** of the array methods.

###4.5 Return
- the **return** statement can be used to cause the function to return early, before it hits the } tag. Will execute immediately without executing the remaining statements.
- A function **always** returns a value. If the **return** value is not specified, then **undefined** is returned.
- If the function was invoked with the **new** prefix and the **return** value is NOT an object, **this** (the new object) is returned instead.

###4.6 Exceptions
- **Exceptions**: mishaps that interfere with the normal flow of a program.
- when it's detected, the browser will throw an exception.
- the **throw** statement interrupts execution of the function.
- if an exception is thrown within a **try** block, control will go to its **catch** clause.
e.g.
   var try_it = function() {
	    try {
		    add("seven");
    } catch (e) {
	   	document.writeIn(e.name + ': ' + e.message);
    }
    }
    try_it ( );
###4.7 Augmenting Types

