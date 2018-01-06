---
layout: post
title: Visier Tech Workshop
update: 2016-02-11

---

[Visier](http://www.visier.com/) is a workforce analytics company based in Vancouver.  I went to Visier HQ today joining a one day bootcamp and it was fantastic. (no kidding, I learned some great new technologies and went back home with several cool swags, including a google chromecast!)

![_config.yml]({{ site.baseurl }}/images/visier.jpg)

Before the bootcamp there was an email for environment setup.  The actual day consists of several workshops and some interesting challenges.  Workshops about [Typescript](http://www.typescriptlang.org/), [Angular2](https://angular.io/) and [Play Framework](https://www.playframework.com/) are given by Visier engineers and they are also available all day as TAs for help.  

The technologies are quite new and the syntax and tools come with some learning curve. I managed to solve the standard challenge which is to implememnt some features based on some analytics dashboard skeleton code.  All three technologies are being used in production at Visier and I can see the engineers are very proud of that.

Some notes for the day:

## environment
- Java
- [Activator](https://www.typesafe.com/activator/download)
- Node
- [Intellij IDE](https://www.jetbrains.com/idea/download/)(note: the community version doesn't have typescript plugin installed)
- sample project provided by Visier

## typescript

Why typescript?

There is no typing in javascript, thus hard to maintain.

- developed by Microsoft, recommanded by Angular2
- adds class based oop
- typescript is transpired to javascript

**syntax:**

boolean: `var isRequired: boolean = false;`

number: `var age: number = 20`

string: `var name: string = "string"`

Arrays:
`var list: string[] = ["a"]` 
or
`var list: Array<string> = ["a"]`

Any: `var a:any = 1`

**Interfaces**

```
interface Month {
	name: string;
	shorName?: string;
	numOfDays: number;
}

var m: Month = {name: "January", shortName: "Jan", numOfDays: 31}
var optionalm: Month = {name: "January", numOfDays: 31}
```

**Modules**
modules provides a way to organize code

## angular 2

**Module**

- basic building blocks
- export things (classes, functions, values) that other modules import

**Component**

- something that controls a portion of screen real estate (view)

**Template**

- html + stuff

**Service**

- anything with specific purpose

