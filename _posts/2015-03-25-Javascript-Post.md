---
layout: post
title:  "JavaScript Functions"
date:   2015-03-25
categories: JavaScript
---

## What are functions?

Functions in JavaScripts are objects. That means that they have a key, which defines the name of the function. That also means that they have a value, which is where the actual function process lives.

Since functions are objects they can be passed around like any other value.

## Function Literal

Functions can be created through a function literal:

{% highlight js %}
var add = function (a, b) {
    return a + b;
};
{% endhighlight %}

Function literals have four parts:

1. The `function` keyword.
2. The function name (after the var keyword).
3. The parameters of the function located in the parentheses.
4. The function statements located in between the curly braces.

## Function Invocation

When a function is created it receives a bonus name/value pair called `this`. Depending on how the function is invoked will change the value of `this`.

#### Method Invocation

When a function is stored as a property (called a method of an object) `this` becomes the object.

{% highlight js %}
var coinJar = {
    totalAmount: 0,
    addCoins: function(amount) {
        this.totalAmount += amount; // this = coinJar
    }
};
{% endhighlight %}

#### Function Invocation

If a function is invoked in the same scope it is created in then `this` is bound to the global object. This means that a function within a function will not recognize the `this` of the outer function. The workaround is creating a `that` variable.

{% highlight js %}
coinJar.double = function() {
    var that = this;
    var amount = 1;

    var helperMethod = function () {
        that.amount += that.amount; // that.amount = 1
    }

    helperMethod();
}
{% endhighlight %}

#### Constructor Invocation

A constructor is the psuedo-classical way of creating an object. By appending the `new` keyword to a constructor function we can create an object that shares characteristics with the original object.

{% highlight js %}
var MyObject = function(string) {
    this.name = string;
};

MyObject.prototype.get_name = function() {
    return this.name;
}

var newObject = new MyObject("potato");

console.log(newObject.get_name()); // potato
{% endhighlight %}

#### Apply Invocation

In JavaScript functions can also have methods. `apply` allows us to invoke a method and send two arguments. The first argument sets `this` while the second argument is an array of parameters.

{% highlight js %}
var statusObject = {
    status: "A-OK";
}

SomeTotallyUnrelatedObject.prototype.get_status = function() {
    return this.status;
};

var status = SomeTotallyUnrelatedObject.get_status.apply(statusObject) 
// status is 'A-OK'
{% endhighlight %}

## Arguments

Functions also receive a second bonus variable, the `arguments` array-like object. This object is constructed from **all** the parameters passed in the order they were given and only given the length method.

{% highlight js %}
var sum = function() {
    var total = 0;
    for(var i = 0; i < arguments.length; i++;) {
        total += arguments[i];
    }
    return total;
}
{% endhighlight %}