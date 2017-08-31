# Test Your Knowledge
Can you tell what would these three `console.log` below prints out?

```
console.log('x is', x)

var x

console.log('x is', x)

x = 5

console.log('x is', x)
```

If not, stay with me, and I’ll try my best to demystify hoisting.
And even if you know what they print out, if you can’t explain the _why_,
stick around. You might learn something new!


# Hoisting
Hoisting is notoriously one of the most confusing aspects for those
who are new to the language, or even with some experience — you’ve
heard of them, you know it exists, you know it happens… but you don’t
really know what exactly is happening behind the scene.

The source of the confusion lies within often misleading descriptions:

- _… variable declaration is moved to the top of the function or global code._
 — MDN web docs
- _Hoisting is JavaScript’s default behavior of moving declarations to the top._
— W3Schools

Often it’s explained as if the variable and function declarations are _physically_
moved to the top of the code. But that’s not what is happening. In order to understand
hoisting, you really need to understand different phases in which **JavaScript engine**
goes through your code.

**Note:** `let/const/class` declarations behave differently. I think it’s best to
understand hoisting with `var/function` first, so I will keep them for another time.
In this post, I will start off by explaining **variable hoisting**.

# JavaScrip Engine
We can’t talk about JavaScript without JavaScript engine. It is a programme which
reads and runs JavaScript code. It’s the core of what makes it possible to run your
beautiful code in web browsers. For now, it’s enough to know that it does its job in
**two phases**: the _memory creation phase_ and the _execution phase_, and that our
code won’t be executed until the second phase.


# Variable Hoisting
Enough talking! Let’s go through some examples of hoisting.

Here’s the first one.

```javascript runnable
// Example 1

console.log(x)
```

Okay, I hear you. This is not actually an example of hoisting. The variable `x` is
not declared anywhere in the code, so it will result in a big red `ReferenceError`,
complaining that `x is not defined` — fair enough!

What about this one?

```javascript runnable
// Example 2

console.log(x)
var x
```

At the first glance, you may think that it’s a lot like the first example. However,
this code doesn’t throw an error. It executes and prints out a value of `undefined`.

It’s important to note that, in JavaScript, `undefined` is an _actual value_.
So this is basically JavaScript engine interpreting `var x = undefined`, just like
`var x = 5` or `var x = ‘string’`.

The key here is that _`x` is defined and available before its declaration_ — yes,
this is a legitimate example of hoisting. Hence, the example 2 is practically same as:

```
var x
console.log(x)
```

But _who sets_ the value of `x` to `undefined`? I certainly didn’t, did I?

This is a job of the JavaScript engine. During the _memory creation phase_, it recognises
variable declarations as it reads the code, _initialises_ them to `undefined` and
puts them into memory to be used during the execution phase.

Let’s look at another example. What will the `console.log` output?

```javascript runnable
// Example 3

console.log(x)
var x = 10
```

You might have guessed that it would print out `10`, because you _initialised_ `x` to `10`.
But the `console.log` outputs `undefined`. Why??

Here is the gotcha… **initialisations are not hoisted**.

During the memory creation phase, the JavaScript engine recognised the declaration of `x`
(`var x`), automatically initialised `x` to `undefined`, and made it available. However,
as the initialisation (`= 10`) didn’t get hoisted, value of `x` stayed as `undefined`
when the execution reached `console.log` at line 3.

If we add another `console.log` at line 5, the second output will be `10`, because by
then the reassignment of `x` to `10` has been executed.

```javascript runnable
// Example 4

console.log(x)
var x = 10
console.log(x)
```

The example 4 is practically the same as running below.

```
var x
console.log(x)
x = 10
console.log(x)
```

# Wrap-up
Cool. So that is variable hoisting. We’ve covered a lot of stuff here — **JavaScript engine**,
**memory creation phase**, **execution phase**, **variable declaration**, **initialisation**,
**reassignment** etc...

Let’s test our understanding of variable hoisting, before moving onto function hoisting.

Here’s a piece of code that I’ve put in the beginning of this article. Can you tell what would
the two `console.log` outputs now?

```javascript runnable
console.log('x is', x)

var x

console.log('x is', x)

x = 5

console.log('x is', x)
```

Got it?

If you got this right, you understood variable hoisting. Don’t worry if you didn’t get it right,
understanding comes with practice. Explore more by creating your own examples, until it becomes
familiar.

I will go through **function hoisting** in the next section.

Thanks!