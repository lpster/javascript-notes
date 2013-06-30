#Javascript: The Good Parts by Doug Crockford
URL: http://shop.oreilly.com/product/9780596517748.do

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

A *method* method is used to define new methods. Its definition:

    Function.prototype.method = function (name,func) 
    	this.prototype[name] = func;
    	return this;
    	}; //Will be explained in chapter 4