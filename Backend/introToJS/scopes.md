## Scopes & Declaring Variables

- I learned about scopes, I specifically learned about global, local and block scopes.  Along with the different variables like var, let, and const.

## Scopes

- A global scope is something like a variable being defined, this global variable lets you use that variable anywhere. Meanwhile the local scope is when a variable is defined inside a function, that variable is only accessible in the function you cant access it outside it. So you can have two variables with the same name and not overwrite each other as long as one variable is local. A block scope is when you declare a variable not just in a function, but anything that has curly brackets like an object, if and else statements, and loops.

## Declaring Variables

- var, let, and const are all ways to declare a variable, but they all have different properties that make them unique. The var variable can be easily overwritten and its the most flexible of all three because of this if you accidentally declare another variable with the same name and the previous variable was declared using var instead of showing errors it will just overwrite the previous one and it will make debugging harder since it wont show the error on the console. Unlike var, when you declare a variable with let that variable can only be declared with that name once, it wont let you assign a variable with the same name. Finally when a variable is declared with const, it has the same properties as let, but variables declared with const are set as read only meaning it can't be reassigned and redeclared, but that doesn't mean that the values inside the variable can't be changed.
