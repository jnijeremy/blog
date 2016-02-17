---
layout: post
title: JavaScript Reference
update: 2016-2-16

---

My JaveScript reference.

`foo ? function1() : function2();`

### Type

`Bool:`

`null`, `undefined`, `0`, `NaA`, `''` is false, anything else is true in condition checking.

`Number:`

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

// nest objects:

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
var arr = [1, 2. 3.14, 'Hello', null, true];
arr.length; // 6

var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // [1,2,3,undefined, undefined, undefined]
arr.length = 2;
arr; // [1,2]

var arr = [1,2,3]
arr[5] = 'x';
arr; // [1,2,3,undefined,undefined,'x']

arr.indexOf(key) // return -1 if not found

var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // ['A','B','C']
arr.slice(3); // ['D', 'E', 'F', 'G']

// copy an array:
var a = [1,2,3]
var b = arr.slice();
b; // [1,2,3]
a === b; // false, An expression comparing Objects is only true if the operands reference the same Object.

var arr = [1,2];
arr.push('A', 'B'); // return 4
arr; // [1,2,'A','B']
arr.pop(); // return 'B'
arr; // [1,2,'A']
arr.pop(); arr.pop(); arr.pop();
arr; // []
arr.pop(); // return undefined
arr; // []

var arr = [1,2];
arr.unshift('A', 'B'); // 4
arr; // ['A','B',1,2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift();
arr; // []
arr.shift(); // return undefined
arr; // []

arr.sort() // inplace
// sort() by default sorts the values as string in alphabetical and ascending order, thus '100' < '25'.

nums.sort(function(a,b){return a-b});

arr.reverse()

var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']

var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'

```


### Object

```
var xiaohong = {
    name: 'xiaohong',
    'middle-school': 'No.1 Middle School'
};

xiaohong['middle-school']; // 'No.1 Middle School', has to use []
xiaohong['name']; // 'xiaohong'
xiaohong.name; // 'xiaohong'

var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
'name' in xiaoming; // true
'grade' in xiaoming; // false
'toString' in xiaoming; // true, inherent from object

var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false

```

### Map, Set

```
// ES6 added Map and Set

var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95

var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined

var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3

>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.add(4)
>>> s
{1, 2, 3, 4}

var s = new Set([1, 2, 3]);
s; // Set {1, 2, 3}
s.delete(3);
s; // Set {1, 2}
```

### Loop

```
var i;
for (i = 0; i < cars.length; i++) {
	text += cars[i] + "<br>";
}

var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    if (o.hasOwnProperty(key)) {
        alert(key); // 'name', 'age', 'city'
    }
}

var a = ['A', 'B', 'C'];
for (var i in a) {
    alert(i); // '0', '1', '2' !!! sting, not number
    alert(a[i]); // 'A', 'B', 'C'
}
```

### Function

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