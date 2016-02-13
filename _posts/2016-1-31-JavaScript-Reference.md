---
layout: post
title: JavaScript Reference

---

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

`string`, `bool`, `null`, `undefined`

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

`object`: the `name:value` pairs are called `properties`.

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

`$`, `_` may be user-defined variable name for `jQuery` and `Underscore` library.

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