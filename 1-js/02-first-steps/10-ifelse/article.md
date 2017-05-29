# Conditional operators: if, '?'

Sometimes we need to perform different actions basing on a condition.

There's an `if` operator for that and also the "question mark" operator: `"?"` for conditional evaluation.

[cut]

## The "if" operator

The "if" operator gets a condition, evaluates it and -- if the result is `true` -- executes the code.

For example:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

*!*
if (year == 2015) alert( 'You are right!' );
*/!*
```

In the example above, the condition is a simple equality check: `year == 2015`, but it can be much more complex.

If there's more than one command to execute -- we can use a code block in figure brackets:

```js
if (year == 2015) {
  alert( "That's correct!" );
  alert( "You're so smart!" );
}
```

It is recommended to use figure brackets every time with `if`, even if there's only one command. That improves readability.

## Boolean conversion

The `if (…)` operator evaluates the expression in parentheses and converts it to the boolean type.

Let's recall the conversion rules:

- A number `0`, an empty string `""`, `null`, `undefined` and `NaN` are `false`,
- Other values -- `true`.

So, the code under this condition would never execute:

```js
if (0) { // 0 is falsy
  ...
}
```

...And inside this condition -- always works:

```js
if (1) { // 1 is truthy
  ...
}
```

We can also pass a pre-evaluated boolean value to `if`, like here:

```js
let cond = (year == 2015); // equality evaluates to true or false

if (cond) {
  ...
}
```

## The "else" clause

The `if` operator may contain an optional "else" block. It executes when the condition is wrong.

For example:
```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' ); // any value except 2015
}
```

## Several conditions: "else if"

Sometimes we'd like to test several variants of a condition. There's an `else if` clause for that.

For example:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

In the code above JavaScript first checks `year < 2015`, if it is falsy then goes to the next condition `year > 2015`, and otherwise shows the last `alert`.

There can be more `else if` blocks. The ending `else` is optional.

## Ternary operator '?'

Sometimes we need to assign a variable depending on a condition.

For instance:

```js run no-beautify
let accessAllowed;
let age = prompt('How old are you?', '');

*!*
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
*/!*

alert(accessAllowed);
```

The so-called "ternary" or "question mark" operator allows to do that shorter and simpler.

The operator is represented by a question mark `"?"`.  The formal term "ternary" means that the operator has 3 operands. It is actually the one and only operator in JavaScript which has that many.

The syntax is:
```js
let result = condition ? value1 : value2
```

The `condition` is evaluated, if it's truthy then `value1` is returned, otherwise -- `value2`.

For example:

```js
let accessAllowed = (age > 18) ? true : false;
```

Technically, we can omit parentheses around `age > 18`. The question mark operator has a low precedence. It executes after the comparison `>`, so that'll do the same:

```js
// the comparison operator "age > 18" executes first anyway
// (no need to wrap it into parentheses)
let accessAllowed = age > 18 ? true : false;
```

...But parentheses make the code more readable. So it's recommended to put them.

````smart
In the example above it's possible to evade the question mark operator, because the comparison by itself returns `true/false`:

```js
// the same
let accessAllowed = age > 18;
```
````

## Multiple '?'

A sequence of question mark `"?"` operators allows to return a value depending on more than one condition.

For instance:
```js run
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

It may be difficult at first to grasp what's going on. But after a closer look we can see that it's just an ordinary sequence of tests.

1. The first question mark checks whether `age < 3`.
2. If true -- returns `'Hi, baby!'`, otherwise -- goes after the colon `":"` and checks for `age < 18`.
3. If that's true -- returns `'Hello!'`, otherwise -- goes after the next colon `":"` and checks for `age < 100`.
4. If that's true -- returns `'Greetings!'`, otherwise -- goes after the last colon `":"` and returns `'What an unusual age!'`.

The same logic using `if..else`:

```js
if (age < 3) {
  message = 'Hi, baby!';
} else if (a < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

## Non-traditional use of '?'

Sometimes the question mark `'?'` is used as a replacement for `if`:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
*/!*
```

Depending on the condition `company == 'Netscape'`, either the first or the second part after `"?"` gets executed and shows the alert.

We don't assign a result to a variable here, the idea is to execute different code depending on the condition.

**It is not recommended to use the question mark operator in this way.**

The notation seem to be shorter than `if`, that appeals to some programmers. But it is less readable.

Here's the same with `if` for comparison:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
if (company == 'Netscape') {
  alert('Right!');
} else {
  alert('Wrong.');
}
*/!*
```

Our eyes scan the code vertically. The constructs which span several lines are easier to understand than a long horizontal instruction set.

The idea of a question mark `'?'` is to return one or another value depending on the condition. Please use it for exactly that. There's `if` to execute different branches of the code.
