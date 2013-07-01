#Javascript: The Good Parts by Doug Crockford
URL: http://shop.oreilly.com/product/9780596517748.do

Below contain my notes.

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



