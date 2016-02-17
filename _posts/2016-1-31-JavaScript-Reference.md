---
layout: post
title: JavaScript Reference
update: 2016-2-16

---

My JaveScript reference.

`foo ? function1() : function2();`

`sort()` by default sorts the values as string in alphabetical and ascending order, thus '100' < '25'.

`nums.sort(function(a,b){return a-b});`

### type

`Number`

```
123;
0.456;
1.2345e3; // 1234.5
-99;
NaN; // not a number
Infinity;

0xff00;

```

`String`, `Boolean`, `Null`, `Undefined`

`Null` is nothing, something that doesn't exist.
`Undefined` is a variable without a value.

```
'abd';
"abc";

true;
false;

```

`==` // equal in value

`===` // equal in both value and type, better

`!==`

`!a` // always returns boolean value
`!!a` // convert a variable to boolean

```
NaN === NaN; // false, special case
ifNaN(NaN); // true, use function

1 / 3 === (1 - 2 / 3); // false, rounding error
Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true

```

`array`

```
var are = [1, 2, 3.14, 'Hello', null, true];
```

`object`: a collection of properties, the `name:value` pairs are called `properties`.

```
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    'zip code': 12345
}

nest objects:

var myProfile = {
    name: "John Smith",
    email: "johnsmith@gmail.com",
    city: "San Francisco",
    points: 1234,
    isInvited: true,
    friends: [
        {
            name: "John Doe",
            email: "johndeo@gmail.com"
        },
        {
            name: "Jane Doe",
            email: "janedoe@gmail.com"
        }
    ]
}

Post.findOne({ title: 'My First Post' });
// {title: 'My First Post'} is an anonymous JavaScript object.

```

`var`

The `var` keyword makes variable local, restrict its scope to the function you're declaring it in (or the file, if you declare it outside of any function); 

```
i  = 10;
// i will be global variable.  If i is decalared this way in multiple js file for the same page, it will be hard to debug.

'use strict'; // enforce use of var

```

`$`, `_` may be user-defined variable name for `jQuery` and `Underscore` library.

### String

```
var s = 'Hello, world!";
s.length; // 13

// string is inmutable
var s = 'Test'
s[0] = 'X'
alert(x); // 'Test'

// these methods return copy of original string
s.toUpperCase();
s.toLowerCase();
var s = 'hello, world';
s.indexOf('world'); // 7
s.indexOf('notexist'); // -1
s.substring(0, 5); // 'hello'
s.substring(7); // 'world'
```

### Array

```

```

### Loops

```
var i;
for (i = 0; i < cars.length; i++) {
	text += cars[i] + "<br>";
}

// The For/In Loop loops through the properties of an object.

var person = {fname:"John", lname:"Doe", age:25};
var text = "";
var x;
for (x in person) {
	text += person[x];
}
```

### function

```
var myAwesomeFunction = function (myArgument) {
    // do sth
}

square = function (a) {
    return a*a;
}
applyOperation = function (f, a) {
    return f(a);
}
applyOperation (square, 10); // 100
    
```

### Anonymous Functions

```
applyOperation = function (f, a) {
    return f(a);
}

applyOperation(
    function(a){
        return a*a;
    },
    10
) // 100
```

### Arrows

```
var digits = [0,1,2,3,4,5,6,7,8,9,10];
var even_digits = digits.filter( num => num % 2 === 0 );
console.log(even_digits); // 0,2,4,6,8]


var names = [ "Hacker", "Rank", "Website" ];
var names_length = names.map( name => name.length );
console.log(names_length);  // [ 6, 4, 7 ]


var employee = {
    _name : "Vineet",
    _task : ["test the beta.", "debug the code.", "create challenges."],
    _printTask() {
        this._task.forEach( t => console.log(this._name + " has to " + t));
    }
};

employee._printTask();
// Vineet has to test the beta.
// Vineet has to debug the code.
// Vineet has to create challenges.
```

### This
`this` keyword lets you access the object on which you're currently working.

```
myFunction = function (a, b) {
    console.log(this);
    // do sth
}

myFunction = function (a, b) {
    var myObject = this;
    // do sth
}
        
```

```
Template.postEdit.events({
  'submit form': function(event) {
    event.preventDefault();

    var currentPostId = this._id;

    var postProperties = {
      url: $(event.target).find('[name=url]').val(),
      title: $(event.target).find('[name=title]').val()
    }

    Posts.update(currentPostId, {$set: postProperties}, function(error) {
      if (error) {
        // display the error to the user
        throwError(error.reason);
      } else {
        Router.go('postPage', {_id: currentPostId});
      }
    });
  }
});
```

### JSON

```
JSON.stringfy(object);
```

### Closures

Closures are functions that refer to independent (free) variables.  In other words, the function defined in the closure remembers the environment in which it was created.

**Lexical scoping**:
In JavaScript, the scope of a variable is defined by its location within the source code (it is apparent lexically) and nested functinos have access to variables declared in their outer scope.

```
function init() {
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() { // displayName() is the inner function, a closure
    alert(name); // use variable declared in the parent function    
  }
  displayName();    
}
init();
```

**Closure**: A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.

In the following example, `myFunc` has become a closure that incorporates both the `displayName` function and the `Mozilla` string that existed when the closure was created.

```
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

**emulating private methods with closures**

```
var counter = (function() {
	var privateCounter = 0;
	function changeBy(val) {
		privateCounter += val;
	}
	return {
		increment: function() {
			changeBy(1);
		},
		decrement: function() {
			changeBy(-1);
		},
		value: function() {
			return privateCounter;
		}
	};
})();

console.log(counter.value()); // 0
counter.increment();
counter.increment();
console.log(counter.value()); // 2
counter.decrement();
console.log(counter.value()); // 1
```