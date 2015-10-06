# JavaScript Hoisting Worksheet

## Instructions
1. Review each code snippet below.
2. Fill in what will be output to the console.
3. Run the code to see if you were correct.
4. Describe why the code behaved as it did.
5. Re-write the code snippet to maintain the same output, but to avoid hoisting.
<hr>

##Snippet One
```js
var myvar = 'my value'; 
  
(function() { 
    console.log(myvar);
    var myvar = 'local value'; 
})();
```

###output:
> `undefined`
>
###why?
>- because the local variable gets hoisted to the top of the function scope, 
>- but the initialization wasn't hoisted so that value of myvar is undefined
>-
###rewrite without hoisting

```js
var myvar = 'my value';

(function(){
    var myvar = 'local value';
    console.log(myvar)
})();
```
<hr>

##Snippet Two

```js
var flag = true; 
  
function test() {
    if(flag) {
        var flag = false;
        console.log('Switch flag from true to false');
    }
    else {
        flag = true;
        console.log('Switch flag from false to true');
    }
}
test();
```

###output:
>- `Switch flag from false to true`
###why?
>- flag is undefined, which is falsey, which means that the `else` is run
###rewrite without hoisting

```js
function test() {
    var flag = true;
    if(flag) {
        flag = false;
        console.log('switch flag from true to false');
    }
    else {
        flag = true;
        console.log('Switch flag from false to true');
    }
}
test();
```
<hr>

##Snippet Three
```js
var message = 'Hello world'; 
  
function saySomething() {
    console.log(message);
    var message = 'Foo bar';
}
saySomething();
```

###output:
>- `undefined`
###why?
>- var message is hoisted to the top of the function scope, but it doesn't 
>- bring initialized value with it
###rewrite without hoisting

```js
var message = 'Hello world';

function saySomething() {
    var message = 'Foo bar'
    console.log(message);
}
saySomething();
```
<hr>

##Snippet Four
```js
var message = 'Hello world'; 
  
function saySomething() {
    console.log(message);
    message = 'Foo bar';
}
saySomething();
```

###output:
>- `Hello world`
###why?
>- `var message` is hoisted above the function so that the function knows what 
>- message is.
###rewrite without hoisting

```js
function saySomething() {
    var message = 'Hello World';
    console.log(message);
    message = 'Foo bar'
}
saySomething();
```

<hr>
##Snippet Five

```js
function test() {
    console.log(a);
    console.log(foo());

    var a = 1;
    function foo() {
        return 2;
    }
}
 
test();
```

###output:
 1. `console.log = undefined`
 2. `console.log = 2`

###why?
>- So the first one is undefined because `a` is hoisted up the function scope 
>- but the value isn't taken with it.<br> The second one is return the value 
>- of 2

###rewrite without hoisting

```js
function test() {
    var a = 1;
    function foo(){
        return 2;
    }
    console.log(a);
    console.log(foo());
}
test();
```

<hr>
##Snippet Six

```js
(function() {
    console.log(bar);
    foo();

    function foo() {
        console.log('aloha');
    }

    var bar = 1;
    baz = 2;
})();
```

###output:

1. `undefined`
2. `aloha`

### why?
>- so the first `console.log` is undefined because bar's value didn't come 
>- with it when it was hoisted <br> the second one is console logging aloha 
>- because your calling the function foo that was hoisted
###rewrite without hoisting

```js
(function(){
    var bar = 1;
    function foo() {
        console.log('aloha')
    }
    console.log(bar);
    foo();
    baz = 2;
})();
```

<hr>
##Snippet Seven

```js
var run = false;

function fancy(arg1, arg2) {
    if(run) {
        console.log('I can run');
    }
    else {
        console.log('I can\'t run');
    }

    function run() {
        console.log('Will I run?');
    }
}
fancy();
```

###output:
>- `I can run`
###why?
>- so the function run is hoisted up to the top of the function fancy which is 
>- a truthy value because of the returned string to the console, so the if 
>- statement is run
###rewrite without hoisting

```js
var run = false;

function fancy(arg1, arg2) {
    function run(){
        console.log('Will I run?');
    };
    if(run) {
        console.log('I can run');
    }else {
        console.log('I can\'t run');
    }
}
fancy();
```
<hr>

##Snippet Eight
```js
var run = false;

function fancy(arg1, arg2) {
    if(run) {
        console.log('I can run');
    }
    else {
        console.log('I can\'t run');
    }

    var run = function() {
        console.log('Will I run?');
    }
}
fancy();
```

###output:
>- `I can't run`
###why?
>- so run is a named function which isn't hoisted at all, thus making run 
>- undefined, which causes the else statement to run
###rewrite without hoisting

```js
var run = false;

function fancy(arg1, arg2) {
    var run = function() {
        console.log('Will I run?')
    }

    if(run) {
        console.log('I can run')
    }else {
        console.log('I can\'t run')
    }
}
fancy();
```
