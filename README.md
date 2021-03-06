# Functional Programming Abstract
* [Pure functions](#pure-functions)
* [Immutability](#immutability)
* [Function Composition](#function-composition)
* [Recursion](#recursion)
* [Higher-ordered Functions](#higher-ordered-functions)
* [Curring](#curring)
* [Closures](#closures)

## Pure functions
A pure function must satisfy both of the following properties:
* Referential transparency: The function always gives the same return value for the same arguments. This means that the function cannot depend on any mutable state.
* Side-effect free: The function cannot cause any side effects. Side effects may include I/O (e.g., writing to the console or a log file), modifying a mutable object, reassigning a variable, etc.
* Pure function should return value.

There are several benefits to pure functions:
* They're easier to reason about and debug because they don't depend on mutable state.
* The return value can be cached or "memoized" to avoid recomputing it in the future.
* They're easier to test because there are no dependencies (such as logging, Ajax, database, etc.) that need to be mocked.

```js
const multiply = (a, b) => a * b;
```

## Immutability
Immutable data cannot change its structure or the data in it. It’s setting a value on a variable that cannot change, making that value a fact.

There are several benefits to immutable data:
* When you keep your application architecture immutable and mental model simple it becomes easier to predict the data in the state at any given time and then you can rest assured that it won’t create any nasty side effects. 
* One of the advantages of immutability is that you can optimize your application by making use of reference and value equality. This makes it easy to identify if anything has changed.

## Function Composition
The act of putting two functions together to form a third function where the output of one function is the input of the other.

```js
import { compose } from 'ramda';

const h = (x) => x + 1;
const g = (x) => x * x;
const f = (x) => x.toString();
const composite = compose(f, g, h);

console.log(composite(1)); // Prints: '4'
```

## Recursion
Recursion is a programming pattern that is useful in situations when a task can be naturally split into several tasks of the same kind, but simpler. Or when a task can be simplified into an easy action plus a simpler variant of the same task. Or, as we’ll see soon, to deal with certain data structures.
When a function solves a task, in the process it can call many other functions. A partial case of this is when a function calls itself. That’s called recursion.

```js
const pow = (x, n) => n === 1 ? x : x * pow(x, n - 1);
```

## Higher-ordered Functions
A function which takes a function as an argument and/or returns a function.

```js
import { pipe, filter, map, mean } from 'ramda';

const vehicles = [
  { make: 'Honda', model: 'CR-V', type: 'suv', price: 24045 },
  { make: 'Honda', model: 'Accord', type: 'sedan', price: 22455 },
  { make: 'Mazda', model: 'Mazda 6', type: 'sedan', price: 24195 },
  { make: 'Mazda', model: 'CX-9', type: 'suv', price: 31520 },
  { make: 'Toyota', model: '4Runner', type: 'suv', price: 34210 },
  { make: 'Toyota', model: 'Sequoia', type: 'suv', price: 45560 },
  { make: 'Toyota', model: 'Tacoma', type: 'truck', price: 24320 },
  { make: 'Ford', model: 'F-150', type: 'truck', price: 27110 },
  { make: 'Ford', model: 'Fusion', type: 'sedan', price: 22120 },
  { make: 'Ford', model: 'Explorer', type: 'suv', price: 31660 }
];

const averageSUVPrice = pipe(
  filter(value => value.type === 'suv'),
  map(value => value.price),
  mean
);

console.log(averageSUVPrice(vehicles)); // Prints: 33399
```

## Curring
The process of converting a function that takes multiple arguments into a function that takes them one at a time.
Each time the function is called it only accepts one argument and returns a function that takes one argument until all arguments are passed.

```js
import { curry } from 'ramda';

const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);

console.log(curriedSum(1)(2)(3)); // Prints: 6
```

## Closures
A closure is a way of accessing a variable outside its scope. Formally, a closure is a technique for implementing lexically scoped named binding. It is a way of storing a function with an environment.

A closure is a scope which captures local variables of a function for access even after the execution has moved out of the block in which it is defined. ie. they allow referencing a scope after the block in which the variables were declared has finished executing.
