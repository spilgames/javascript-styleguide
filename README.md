# JavaScript Style Guide

> "Programs are meant to be read by humans, and only incidentally for computers to execute."
> - _Donald Knuth_

A style guide is a set of standards for the writing and design of code.
 
The goal of a style guide is that all code in any code-base should look like a single person typed 
it, even when many people are contributing to it. Consistency in code style and formatting makes 
code more readable, and thus more easier to maintain. 

## Goals

- Clear overview of rules
    - Commonly-agreed upon standards
    - Living document
- Style checker
    - Verify if style is correct
    - Runs via command line, integrated in build process
    - Run in editor (SublimeText, etc.)
    - Provide .editorconfig
- Style fixer: Automatically fix code (e.g., via CodePainter)

## Style Guide

- [Indentation](#indentation)
- [Line Length](#line-length)
- [Primitive Literals](#primitive-literals)
- [Operator Spacing](#operator-spacing)
- [Parentheses Spacing](#parentheses-spacing)
- [Object Literals](#object-literals)
- [Comments](#comments)
    - [Single-Line Comments](#single-line-comments)
    - [Multiline Comments](#multiline-comments)
    - [Comment Annotations](#comment-annotations)
- [Variable Declarations](#variable-declarations)
- [Function Declarations](#function-declarations)
- [Naming](#naming)
- [Strict Mode](#strict-mode)
- [Assignments](#assignments)
- [Equality Operators](#equality-operators)
- [Ternary Operators](#ternary-operators)
- [Statements](#statements)
    - [Simple Statements](#simple-statements)
    - [`return` Statement](#return-statement)
    - [Compound Statements](#compound-statements)
    - [`if` Statement](#if-statement)
    - [`for` Statement](#for-statement)
    - [`while` Statement](#while-statement)
    - [`do` Statement](#do-statement)
    - [`switch` Statement](#switch-statement)
    - [`try` Statement](#try-statement)
- [White Space](#white-space)
- [Things To Avoid](#things-to-avoid)

### Indentation
Each indentation level is made up of four spaces. No tabs.

```javascript
//Good
if (true) {
    doSomething();
}
```

[&uarr; Back to top](#style-guide)

### Line Length
Each line should be no longer than 100 characters. If a line goes longer than 100 characters, it 
should be wrapped after an operator (comma, plus, etc.) The following line should be indented two
levels (eight spaces.)

```javascript
// Good
doSomething(argument1, argument2, argument3, argument4,
        argument5);

// Bad: Following line only indented four spaces
doSomething(argument1, argument2, argument3, argument4,
    argument5);

// Bad: Breaking before operator
doSomething(argument1, argument2, argument3, argument4
    , argument5);
```

[&uarr; Back to top](#style-guide)

### Primitive Literals
Strings should always use single quotes and should always be on a single line.

```javascript
// Good
var name = 'SpilGames';

// Bad: Double quotes
var name = "SpilGames";

// Bad: Wrapping to second line
var longString = 'This is a string spanning \
multiple lines.';
```

Numbers should be written as decimal integers, e-notation integers, hexadecimal integers, or 
floating-point decimals with at least one digit before and one digit after the decimal point. 
_Never_ use octal literals.

```javascript
// Good
var count = 10;

// Good
var price = 10.0;

// Good
var price = 10.00;

// Good
var num = 0xA2;

// Good
var num = 1e23;

// Bad: Hanging decimal point
var price = 10.;

// Bad: Leading decimal point
var price = .1;

// Bad: Octal (base 8) is deprecated
var num = 010;
```

The special value `null` should be used only in the following situations:

- To initialize a variable that may later be assigned an object value
- To compare against an initialized variable that may or may not have an object value
- To pass into a function where an object is expected
- To return from a function where an object is expected

Examples:

```javascript    
// Good
var person = null;

// Good
function getPerson() {
    if (condition) {
        return new Person("John");
    } else {
        return null;
    }
}

// Good
var person = getPerson();
if (person !== null){
    doSomething();
}

// Bad: Testing against uninitialized variable
var person;
if (person != null){
    doSomething();
}

// Bad: Testing to see if an argument was passed
function doSomething(arg1, arg2, arg3, arg4){
    if (arg4 != null){
        doSomethingElse();
    }
}
```

Never use the special value `undefined`. To see if a variable has been defined, use the `typeof`
operator:

```javascript
// Good
if (typeof variable === "undefined") {
    // do something
}

// Bad: Using undefined literal
if (variable === undefined) {
    // do something
}
```

[&uarr; Back to top](#style-guide)

### Operator Spacing
Operators with two operands must be preceded and followed by a single space to make
the expression clear. Operators include assignments and logical operators.

```javascript
// Good
var found = (values[i] === item);

// Good
if (found && (count > 10)) {
    doSomething();
}

// Good
for (i = 0; i < count; i++) {
    process(i);
}

// Bad: Missing spaces
var found = (values[i]===item);

// Bad: Missing spaces
if (found&&(count>10)) {
    doSomething();
}

// Bad: Missing spaces
for (i=0; i<count; i++) {
    process(i);
}
```

[&uarr; Back to top](#style-guide)

### Parentheses Spacing
When parentheses are used, there should be no white space immediately after the
opening paren or immediately before the closing paren.

```javascript
// Good
var found = (values[i] === item);

// Good
if (found && (count > 10)) {
    doSomething();
}

// Good
for (i = 0; i < count; i++) {
    process(i);
}

// Bad: Extra space after opening paren
var found = ( values[i] === item);

// Bad: Extra space before closing paren
if (found && (count > 10) ) {
    doSomething();
}

// Bad: Extra space around argument
for (i = 0; i < count; i++) {
    process( i );
}
```

[&uarr; Back to top](#style-guide)

### Object Literals
Object literals should have the following format:

- The opening brace should be on the same line as the containing statement.
- Each property-value pair should be indented one level with the first property appearing on the 
next line after the opening brace.
- Each property-value pair should have an unquoted property name, followed by a colon (no space 
preceding it), followed by the value.
- If the value is a function, it should wrap under the property name and should have a blank line 
both before and after the function.
- Additional empty lines may be inserted to group related properties or otherwise improve 
readability.
- The closing brace should be on a separate line.

Examples:

```javascript
// Good
var object = {
    key1: value1,
    key2: value2,

    func: function() {
        // do something
    },

    key3: value3
};

// Bad: Improper indentation
var object = {
                key1: value1,
                key2: value2
            };

// Bad: Missing blank lines around function
var object = {
    key1: value1,
    key2: value2,
    func: function() {
        // do something
    },
    key3: value3
};
```

When an object literal is passed to a function, the opening brace should be on the same
line as if the value is a variable. All other formatting rules listed earlier still apply.

```javascript
// Good
doSomething({
    key1: value1,
    key2: value2
});

// Bad: All on one line
doSomething({ key1: value1, key2: value2 });
```

[&uarr; Back to top](#style-guide)

### Comments
Make frequent use of comments to aid others in understanding your code. Use comments
when:

- Code is difficult to understand.
- The code might be mistaken for an error.
- Browser-specific code is necessary but not obvious.
- Documentation generation is necessary for an object, method, or property (use appropriate 
documentation comments).

[&uarr; Back to top](#style-guide)

#### Single-Line Comments
Single-line comments should be used to documentation one line of code or a group of related lines of code. A single-line comment may be used in three ways:

- On a separate line, describing the code beneath it
- At the end of a line, describing the code before it
- On multiple lines, to comment out sections of code

When on a separate line, a single-line comment should be at the same indentation level as the code it describes and be preceded by a single line. Never use multiple single-line comments on consecutive lines; use a multiline comment instead.

```javascript
// Good
if (condition){

    // if you made it here, then all security checks passed
    allowed();
}

// Bad: No empty line preceding comment
if (condition){
    // if you made it here, then all security checks passed
    allowed();
}

// Bad: Wrong indentation 
if (condition){
// if you made it here, then all security checks passed
    allowed();
}

// Bad: This should be a multiline comment
// This next piece of code is quite difficult, so let me explain.
// What you want to do is determine if the condition is true
// and only then allow the user in. The condition is calculated
// from several different functions and may change during the
// lifetime of the session.
if (condition){
    // if you made it here, then all security checks passed
    allowed();
}
```

For single-line comments at the end of a line, ensure that there is at least one indentation level between the end of the code and the beginning of the comment:

```javascript
// Good
var result = something + somethingElse;    // somethingElse will never be null

// Bad: Not enough space between code and comment
var result = something + somethingElse;// somethingElse will never be null
```

The only acceptable time to have multiple single-line comments on successive lines is to comment out large sections of code. Multiline comments should not be used for this purpose.

```javascript
// Good
// if (condition){
//     doSomething();
//     thenDoSomethingElse();
// }
```

[&uarr; Back to top](#style-guide)

#### Multiline Comments
Multiline comments should be used to document code that requires more explanation. Each multiline comment should have at least three lines:

1. The first line contains only the `/*` comment opening. No further text is allowed on this line.
2. The next line or lines have a `*` aligned with the `*` in the first line. Text is allowed on these lines.
3. The last line has the `*/` comment opening aligned with the preceding lines. No other text is allowed on this line.

The first line of multiline comments should be indented to the same level as the code it describes. Each subsequent line should have the same indentation plus one space (for proper alignment of the `*` characters). Each multiline comment should be preceded by one empty line.

```javascript
// Good
if (condition){

    /*
     * if you made it here,
     * then all security checks passed
     */
    allowed();
}

// Bad: No empty line preceding comment
if (condition){
    /*
     * if you made it here,
     * then all security checks passed
     */
    allowed();
}

// Bad: Missing a space after asterisk 
if (condition){

    /*
     *if you made it here,
     *then all security checks passed
     */
    allowed();
}

// Bad: Wrong indentation
if (condition){
/*
 * if you made it here,
 * then all security checks passed
 */
    allowed();
}

// Bad: Don't use multi-line comments for trailing comments
var result = something + somethingElse;    /*somethingElse will never be null*/
```

[&uarr; Back to top](#style-guide)

#### Comment Annotations
Comments may be used to annotate pieces of code with additional information. These annotations take the form of a single word followed by a colon. The acceptable anno- tations are:

- TODO
- HACK
- XXX
- FIXME
- REVIEW

##### TODO
Indicates that the code is not yet complete. Information about the next steps should be included.

##### HACK
Indicates that the code is using a shortcut. Information about why the hack is being used should be included. This may also indicate that it would be nice to come up with a better way to solve the problem.

##### XXX
Indicates that the code is problematic and should be fixed as soon as possible.

##### FIXME
Indicates that the code is problematic and should be fixed soon. Less important than ```XXX```.

##### REVIEW
Indicates that the code needs to be reviewed for potential changes.

These annotations may be used with either single-line or multiline comments and should follow the same formatting rules as the general comment type.

Examples:

```javascript
// Good
// TODO: I'd like to find a way to make this faster
doSomething();

// Good
/*
 * HACK: Have to do this for IE. I plan on revisiting in
 * the future when I have more time. This probably should
 * get replaced before v1.2.
 */
if (document.all) {
    doSomething();
}

// Good
// REVIEW: Is there a better way to do this? 
if (document.all) {
    doSomething();
}

// Bad: Annotation spacing is incorrect
// TODO : I'd like to find a way to make this faster
doSomething();

// Bad: Comment should be at the same indentation as code 
    // REVIEW: Is there a better way to do this?
if (document.all) {
    doSomething();
}
```

[&uarr; Back to top](#style-guide)

### Variable Declarations
All variables should be declared before they are used. Variable declarations should take place at the beginning of a function using a single var statement with one variable per line. All lines after the first should be indented one level so that the variable names line up. Variables should be initialized when declared if applicable, and the equals operator should be at a consistent indentation level. Initialized variables should come first followed by uninitialized variables.

```javascript
// Good
var count   = 10,
    name    = "Nicholas",
    found   = false, 
    empty;

// Bad: Improper initialization alignment
var count = 10,
    name = "Nicholas",
    found= false,
    empty;

// Bad: Incorrect indentation
var count = 10,
name = "Nicholas",
found = false,
empty;

// Bad: Multiple declarations on one line
var count = 10, name = "Nicholas",
    found = false, empty;

// Bad: Uninitialized variables first 
var empty,
    count   = 10,
    name    = "Nicholas",
    found   = false;

// Bad: Multiple var statements 
var count   = 10,
    name    = "Nicholas";

var found   = false,
    empty;
```

Always declare variables. Implied globals should not be used.

[&uarr; Back to top](#style-guide)

### Function Declarations
Functions should be declared before they are used. When a function is not a method (that is, not attached to an object), it should be defined using the function declaration format (not function expression format or using the `Function` constructor). There should be no space between the function name and the opening parenthesis. There should be one space between the closing parenthesis and the right brace. The right brace should be on the same line as the `function` keyword. There should be no space after the opening parenthesis or before the closing parenthesis. Named arguments should have a space after the comma but not before it. The function body should be indented one level.

```javascript
// Good
function doSomething(arg1, arg2) {
    return arg1 + arg2;
}

// Bad: Improper spacing of first line
function doSomething (arg1, arg2){
    return arg1 + arg2;
}

// Bad: Function expression
var doSomething = function(arg1, arg2) {
    return arg1 + arg2;
};

// Bad: Left brace on wrong line
function doSomething(arg1, arg2)
{
    return arg1 + arg2;
}

// Bad: Using Function constructor
var doSomething = new Function("arg1", "arg2", "return arg1 + arg2");
```

Functions declared inside of other functions should be declared immediately after the var statement.

```javascript
// Good
function outer() {

    var count = 10,
        name = "Nicholas",
        found = false,
        empty;

    function inner() {
        // code
    }

    // code that uses inner()
}

// Bad: Inner function declared before variables 
function outer() {
    function inner() { 
        // code
    }
    
    var count
        name = "Nicholas",
        found = false,
        empty;

    // code that uses inner()
}
```

Anonymous functions may be used for assignment of object methods or as arguments to other functions. There should be no space between the `function` keyword and the opening parenthesis.

```javascript
// Good
object.method = function() {
    // code
};

// Bad: Incorrect spacing 
object.method = function () {
    // code
};
```

Immediately invoked functions should surround the entire function call with paren- theses.

```javascript
// Good
var value = (function() {
    
    // function body
    
    return {
        message: "Hi"
    }
}());

// Bad: No parentheses around function call 
var value = function() {
    
    // function body
    
    return {
        message: "Hi"
    }
}();

// Bad: Improper parentheses placement 
var value = (function() {
    
    // function body
    
    return {
        message: "Hi"
    }
})();
```

[&uarr; Back to top](#style-guide)

### Naming
Care should be taken to name variables and functions properly. Names should be limited to alphanumeric characters and, in some cases, the underscore character. Do not use the dollar sign (`$`) or backslash (`\`) characters in any names.

Variable names should be formatted in camel case with the first letter lowercase and the first letter of each subsequent word uppercase. The first word of a variable name should be a noun (not a verb) to avoid confusion with functions. Do not use underscores in variable names.

```javascript
// Good
var accountNumber = "8401-1";

// Bad: Begins with uppercase letter
var AccountNumber = "8401-1";

// Bad: Begins with verb
var getAccountNumber = "8401-1";

// Bad: Uses underscore
var account_number = "8401-1";
```

Function names should also be formatted using camel case. The first word of a function name should be a verb (not a noun) to avoid confusion with variables. Do not use underscores in function names.

```javascript
// Good
function doSomething() {
    // code
}

// Bad: Begins with uppercase letter
function DoSomething() {
    // code
}

// Bad: Begins with noun
function car() {
    // code
}

// Bad: Uses underscores
function do_something() {
    // code
}
```

Constructor functions -functions used with the `new` operator to create new objects— should be formatted in camel case but must begin with an uppercase letter. Constructor function names should begin with a nonverb, because `new` is the action of creating an object instance.

```javascript
// Good
function MyObject() {
    // code
}

// Bad: Begins with lowercase letter
function myObject() {
    // code
}

// Bad: Uses underscores
function My_Object() {
    // code
}

// Bad: Begins with verb
function getMyObject() {
    // code
}
```

Variables that act as constants (values that won’t be changed) should be formatted using all uppercase letters with words separated by a single underscore.

```javascript
// Good
var TOTAL_COUNT = 10;

// Bad: Camel case
var totalCount = 10;

// Bad: Mixed case
var total_COUNT = 10;
```

Object properties follow the same naming conventions as variables. Object methods follow the same naming conventions as functions. If a property or method is meant to be private, then it should be prefixed with an underscore character.

```javascript
// Good
var object = {
    _count: 10,

    _getCount: function () {
        return this._count;
    }
};
```

[&uarr; Back to top](#style-guide)

### Strict Mode
Strict mode should be used only inside of functions, never globally.

```javascript
// Bad: Global strict mode
"use strict";

function doSomething() {
    // code
}

// Good
function doSomething() {
    "use strict";
    // code
}
```

If you want strict mode to apply to multiple functions without needing to write `"use strict"` multiple times, use immediate function invocation:

```javascript
// Good
(function() {
    "use strict";

    function doSomething() {
        // code
    }

    function doSomethingElse() {
        // code
    }
}());
```

[&uarr; Back to top](#style-guide)

### Assignments
When assigning a value to a variable, use parentheses around a right-side expression that contains a comparison.

```javascript
// Good
var flag = (i < count);

// Bad: Missing parentheses
var flag = i < count;
```

[&uarr; Back to top](#style-guide)

### Equality Operators
Use `===` and `!==` instead of `==` and `!=` to avoid type coercion errors.

```javascript
// Good
var same = (a === b);

// Bad: Using ==
var same = (a == b);
```

[&uarr; Back to top](#style-guide)

### Ternary Operators
The ternary operator should be used only for assigning values conditionally and never as a shortcut for an `if` statement.

```javascript
// Good
var value = condition ? value1 : value2;

// Bad: no assignment, should be an if statement 
condition ? doSomething() : doSomethingElse();
```

[&uarr; Back to top](#style-guide)

### Statements

#### Simple Statements
TODO

#### `return` Statement
TODO

#### Compound Statements
TODO

#### `if` Statement
TODO

#### `for` Statement
TODO

#### `while` Statement
TODO

#### `do` Statement
TODO

#### `switch` Statement
TODO

#### `try` Statement
TODO


[&uarr; Back to top](#style-guide)

### White Space
TODO

[&uarr; Back to top](#style-guide)

### Things To Avoid
TODO

[&uarr; Back to top](#style-guide)

## Sources

A lot of content in this document originated from the following sources:

- ["Maintainable JavaScript" - _Nicolas C. Zakas_](http://shop.oreilly.com/product/0636920025245.do)
- http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/
- https://github.com/rwaldron/idiomatic.js/
