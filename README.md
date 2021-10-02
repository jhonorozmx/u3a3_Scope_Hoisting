# Unit 3 Activity 2: Hoisting and Scope
## Write the console.log for each hoisting and scope case. 

### Question 1 
```js
console.log('bar:', bar);
bar =15;
var foo = 1;
console.log(foo, bar);
var bar;
```
**Answer:**
```js
bar: undefined
1 15
```
**Explanation:** The first `console.log` calls for `bar` when it hasn't been declared yet therefore, it is hoisted to the top with a value of `undefined`. Then, in the next expression we assign `bar=15` and after that we initialize `foo=1` that's why in the second `console.log` we get the output `1 15`.

---

## Question 2 
```js
var foo = 5;
console.log("foo:", foo);
var foo;
var bar = 10;
var bar;
console.log("bar:", bar);
var baz = 10;
var baz = 12;
console.log("baz:", baz);
```
**Answer**:
```js
foo: 5
bar: 10
baz: 12
```
**Explanation:** Variables declared with `var` can be both re-declared and re-assigned. So, just before the second `console.log`, when we're re-declaring `foo` and `bar` it doesn't affect the value assigantion of 5 and 10 respectively it is just a re-declararion. On contrast, when we re-declare and re-assign `baz` changing its value from 10 to 12 we're mutating the varible and that's why the last `console.log` throws `baz:12`.

## Question 3
```js
function foo() {
  function bar() {
    return 5;
  }
  return bar();
  function bar() {
    return 10;
  }
}
console.log(foo());
```
**Answer:**
```js
10
```

**Explanation:** When the main funcion `foo()` is called inside `console.log` both declarations of function `bar()` are moved to the top of its scope, which means that the second instance of `bar()` which returns 10, will overwrite the first one and will be returned instead. We can even move the `return bar()` statement wherever we want inside `foo()` and the sencond instance of `bar()` will always overwrite the first one.

---

## Question 4
```js
function foo() {
  var bar = "I'm a bar variable";
  function bar() {
    return "I'm a bar function";
  }
  return bar();
}
console.log(foo());
```
**Answer:**
```js
C:\Users\joroz\Desktop\ITK JS\Unit 3\u3_a3.js:41
return bar();
         ^
TypeError: bar is not a function
```

**Explanation:** To explain this error first, we need to understand two things. The first one is that  when declaring a functiona as `function bar(){...}` is the same as 
`var bar=function(){...}`, in other words is like creating a variable named `bar` and storing a function in it. The second thing is that in JS all the function declarations are always moved to the top of the current scope. Therefore, when we declare `function bar(){...}` this is moved above the expression `var bar="I'm a bar variable"` which can be interpreted as a re-declaration and re-assignment of the variable `bar` with the string value `"I'm a bar variable"`. And because of that when we try to `return bar()` we get the error that `bar` is not a `function` because now it is a `string`.

---

## Question 5
```js
greeting();

var greeting = function () {
  console.log("Good Morning");
};
greeting();

function greeting() {
  console.log("Good Evening");
}
greeting();
```
**Answer:**
```js
Good Evening
Good Morning
Good Morning
```

**Explanation:** Just like in question 4. In the first call of `greeting()` the function declaration `function greeting(){...}` is hoisted to the top of the scope, that's why we get a `Good Evening` in the first log. But then, because we have variable assigment on the `greeting` variable, its value is replaced with the anonymous function that logs `Good Morning` and that's why the last too calls of `greeting()` returns that `Good Morning` string.

---

## Question 6
```js
var foo = 5;
console.log('foo:', foo);
var foo = 10;
console.log('foo:', foo);
```
**Answer:**
```js
foo: 5
foo: 10
```

**Explanation:** Nothing special here, first we declare and assign `var foo=5` and log it on to the console, then we re-declare and re-assign it as `var foo=10` and log it again. Pretty straight forward.

---
  
## Question 7

```js
console.log(foo());

function foo() {
  var bar = function () {
    return 3;
  };

  return bar();
  
  var bar = function () {
    return 8;
  };
}

```
**Answer:**
```js
3
```

**Explanation:** In the above example when we call `foo()` inside `console.log` before declaring it first, the function is simply hoisted to the top of the scope, and then, since the second declaration and assignment of `bar` is after the `return` statement it is just ignored. Therefore the `foo()` function simply returns a `3` wchich is the return value of the first instance of `bar()`.

---

## Question 8
```js
//global scope
var x = "foo";

(function () {
  //function scope
  console.log("x: " + x);
  var x = "bar";
  console.log("x: " + x);
})();
```
**Answer:**
```js
x: undefined
x: bar
```

**Explanation:** The expressions `var x="foo"` and `var x="bar"`are in different scopes, while the first one is in the global scope, the second one is in the scope of the anonymous IIFE. 
Then, when we try to log the variable `x` in the first `console.log` within the function without having declared it yet, the declaration is hoisted and that's why we get an `undefined` value for `x` in the first log. Finally, as we assign the value `"bar"` to `x` and log it on to the console we can see `x: bar`.

---

## Question 9
```js
function foo() {
  console.log("First");
}

foo();

function foo() {
  console.log("Second");
}

```
**Answer:**
```js
Second
```

**Explanation:** Just as explained in ***Question 3*** when we have two functions with the same name existing within the same scope, and no matter where the function call is located, the second instance will always override the first one. That's why the instance of `foo()` that logs `First` is overwritten by the one that logs `Second`.

---

## Question 10
```js
//global scope
var foo = 5;

function baz() {
  //baz scope
  foo = 10;
  return;
  function foo() {}
}

baz();
console.log(foo);
```
**Answer:**
```js
5
```

**Explanation:** As we mentioned before ***function declarations are always moved to the top of their scope***, therefore, the `function foo(){}` statement within the `baz()` function, implicitly creates  a new variable named `foo` within the scope of `baz()` which then is assigned the value `10`. Then, because this new `foo` is in another the scope, the variable `var foo=5` in the global scope is not modified at all and since the `console.log(foo)` can only access the variables in the same scope, it simply logs `5` into the console.

---
