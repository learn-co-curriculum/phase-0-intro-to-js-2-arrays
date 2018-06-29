# Arrays

## Problem Statement

We've talked about data types in JavaScript. But what if we need a way of
organizing data? We'll need to reach for a data structure, and one of the most
useful data structures is an array.

## Objectives

- Identify data structures and arrays
- Create arrays
- Access the elements in an array
- Add elements to an array
- Remove elements from an array
- Replace elements in an array
- Identify nested arrays

## Identify Data Structures and Arrays

A _data structure_ is a means for associating and organizing information.
Outside of the programming world, we use data structures all the time. For
example, we might have a shopping list of the items we need to buy on our next
grocery run or an address book for organizing contact information.

If we have a lot of related data, it's best to represent it in a related system.
Imagine that we're working on a lottery application that has to represent the
winning lottery numbers. We could do that as follows:

```js
const firstNumber = 32;
const secondNumber = 9;
const thirdNumber = 14;
const fourthNumber = 33;
const fifthNumber = 48;
const powerBall = 5;
```

We've represented all six pieces of data, but they aren't related in any
meaningful way. Every single time we want to reference that combination of
winning numbers, we need to remember and type out six different variable names:

```js
const firstNumber = 32;
const secondNumber = 9;
const thirdNumber = 14;
const fourthNumber = 33;
const fifthNumber = 48;
const powerBall = 5;

function logWinningNumbers (first, second, third, fourth, fifth, power) {
  console.log('Winning numbers:', first, second, third, fourth, fifth, power);
}

logWinningNumbers(firstNumber, secondNumber, thirdNumber, fourthNumber, fifthNumber, powerBall);
// LOG: Winning numbers: 32 9 14 33 48 5
// => undefined
```

That's so much typing! There are much, much better ways to keep organize data in
JavaScript. Let's learn about one of the most common: the _array_.

## Create Arrays

An array is a list, with the items listed in a particular order, surrounded by
square brackets (`[]`):

```js
['This', 'is', 'an', 'array', 'of', 'strings.'];
// => ["This", "is", "an", "array", "of", "strings."]
```

The _members_ or _elements_ in an array can be data of any type:

```js
['Hello, world!', 42, null, NaN];
// => ["Hello, world!", 42, null, NaN]
```

Arrays are _ordered_, meaning that the elements in them will always appear in
the same order. The array `[1, 2, 3]` is different from the array `[3, 2, 1]`.

Just like any other type of JavaScript data, we can assign an array to a
variable:

```js
const primeNumbers = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37];

const tvShows = ['Game of Thrones', 'True Detective', 'The Good Wife', 'Empire'];
```

We can find out how many elements an array contains by checking the array's
built-in `length` property:

```js
const myArray = ['This', 'array', 'has', 5, 'elements'];

myArray.length;
// => 5
```

We defined the above arrays using the _array literal_ syntax — that is, we
literally typed out the array that we wanted to create, square brackets and all.
There are other ways to create new arrays, but they are only necessary for very
rare circumstances. For now, use array literals.

To get a sense of just how effective arrays are at keeping data organized, let's
rewrite our lottery code to use an array:

```js
const winningNumbers = [32, 9, 14, 33, 48, 5];

function logWinningNumbers (numbers) {
  console.log('Winning numbers:', numbers);
}

logWinningNumbers(winningNumbers);
// LOG: Winning numbers: [32, 9, 14, 33, 48, 5]
// => undefined
```

The array organization, and we only have to remember one identifier
(`winningNumbers`) instead of six (`firstNumber`, `secondNumber`, and so on).

The one benefit of storing all six lottery numbers separately is that we had a
really easy way to access each individual number. For example, we could just
reference `powerBall` to grab the sixth number. Luckily, arrays offer an equally
simple syntax for accessing individual members. How can we access particular
elements in an array when we need it?

## Access the Elements in an Array

Every element in an array is assigned a unique index value that corresponds to
its place within the collection. The first element in the array is at index `0`,
the fifth element at index `4`, and the 428th element at index `427`.

To access an element, we use the _computed member access operator_, which,
conveniently enough, looks exactly like an array:

```js
const winningNumbers = [32, 9, 14, 33, 48, 5];
// => undefined

winningNumbers[0];
// => 32

winningNumbers[3];
// => 33
```

***NOTE:*** Most people just call it _bracket notation_ or the _bracket operator_,
so don't worry too much about remembering the term _computed member access
operator_.

Let's take a minute to think about how we could access the **last** element in
any array.

If `myArray` contains 10 elements, the final element will be at `myArray[9]`. If
`myArray` contains 15000 elements, the final element will be at
`myArray[14999]`. So the index of the final element is always one less than the
number of elements in the array. If only we had an easy way to figure out how
many elements are in the array...

```js
const alphabet = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
// => undefined

alphabet.length;
// => 26

alphabet[alphabet.length - 1];
// => "z"
```

This is why it's called the ***computed*** _member access operator_. We put an
expression (`alphabet.length - 1`) inside the square brackets, and the
JavaScript engine _computed_ the value of that expression to determine which
element we were trying to access. In this case, `alphabet.length - 1` evaluated
to `25`, so `alphabet[alphabet.length - 1]` became `alphabet[25]`.

## Add Elements to an Array

JavaScript allows us to manipulate the members in an array in a number of ways.

### `.push()` and `.unshift()`

With the `.push()` method, we can add elements to the end of an array:
```js
const superheroes = ['Catwoman', 'She-Hulk', 'Jessica Jones'];

superheroes.push('Wonder Woman');
// => 4

superheroes;
// => ["Catwoman", "She-Hulk", "Jessica Jones", "Wonder Woman"]
```

We can also `.unshift()` elements onto the beginning of an array:

```js
const cities = ['New York', 'San Francisco'];

cities.unshift('Los Angeles');
// => 3

cities;
// => ["Los Angeles", "New York", "San Francisco"]
```

Notice that the value returned by both methods is the `length` of the updated
array.

#### Destructive vs. Nondestructive

Both `.push()` and `.unshift()` update or _mutate_ the original array, adding
elements directly to it. Operations that modify the original collection are
_destructive_, and those that leave the original collection intact are
_nondestructive_.

Mutating the original array isn't necessarily a bad thing, but there's also a
way to add elements nondestructively, leaving the original array intact.

### Spread Operator

ES2015 introduced the _spread operator_, which looks like an ellipsis: `...`.
The spread operator allows us to spread out the contents of an existing array
into a new array, adding new elements but preserving the original:

```js
const coolCities = ['New York', 'San Francisco'];

const allCities = ['Los Angeles', ...coolCities];

coolCities;
// => ["New York", "San Francisco"]

allCities;
// => ["Los Angeles", "New York", "San Francisco"]
```

We created a new array instead of modifying the original one — our `coolCities`
array was untouched. We can also use the spread operator to add a new item to
the end of an array without modifying the original:

```js
const coolCats = ['Hobbes', 'Felix', 'Tom'];

const allCats = [...coolCats, 'Garfield'];

coolCats;
// => ["Hobbes", "Felix", "Tom"]

allCats;
// => ["Hobbes", "Felix", "Tom", "Garfield"]
```

## Remove Elements from an Array

As complements for `.push()` and `.unshift()`, respectively, we have `.pop()`
and `.shift()`.

### `.pop()` and `.shift()`

The `.pop()` method removes the last element in an array, destructively updating
the original array:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.pop();
// => "Sun"

days;
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

The `.shift()` method removes the first element in an array, also mutating the
original:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.shift();
// => "Mon"

days;
// => [Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

Notice that the return value for the `.pop()` and `.shift()` methods is the
element that was removed.

### `.slice()`

To remove elements from an array nondestructively (without manipulating the
original array), we can use the `.slice()` method. Just as the name implies, the
`.slice()` method returns a portion, or **slice**, of an array.

#### With No Arguments

If we don't provide any arguments, `.slice()` will return a copy of the original
array with all elements intact:

```js
const primes = [2, 3, 5, 7];

const copyOfPrimes = primes.slice();

primes;
// => [2, 3, 5, 7]

copyOfPrimes;
// => [2, 3, 5, 7]
```

Note that the array returned by `.slice()` has the same elements as the
original, but it's a copy — **the two arrays point to different objects in
memory**. If you add an element to one of the arrays, it does **not** get added
to the other:

```js
const primes = [2, 3, 5, 7];

const copyOfPrimes = primes.slice();

primes.push(11);
// => 5

primes;
// => [2, 3, 5, 7, 11]

copyOfPrimes;
// => [2, 3, 5, 7]
```

#### With Arguments

We can provide two arguments to `.slice()`, the index where the slice should
begin and the index **before which** it should end:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(2, 5);
// => ["Wed", "Thu", "Fri"]
```

If no second argument is provided, the slice will run from the index specified
by the first argument to the end of the array:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(5);
// => ["Sat", "Sun"]
```

To remove the first element and return a new array, we call `.slice(1)`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(1);
// => ["Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

And we can remove the last element in a way that will look familiar from earlier
in this lesson:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(0, days.length - 1);
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

In fact, `.slice()` provides an easier syntax for grabbing the last element in
an array:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(-1);
// => ["Sun"]

days.slice(-3);
// => ["Fri", "Sat", "Sun"]
```

When we provide a negative index, the JavaScript engine knows to start counting
from the last element in the array instead of the first.

### `.splice()`

While `.slice()` allows us to return a piece of an array without mutating the
original (nondestructive), `.splice()` performs destructive actions. Let's
familiarize ourselves with the [MDN documentation][splice]:

![`Array.prototype.splice()` documentation on MDN](https://user-images.githubusercontent.com/17556281/29643370-b7f81d3e-883c-11e7-9ce4-f514d90c1727.png)

The documentation shows three ways to use `.splice()`:

```js
array.splice(start)
array.splice(start, deleteCount)
array.splice(start, deleteCount, item1, item2, ...)
```

#### With a Single Argument

```js
array.splice(start)
```

The first argument expected by `.splice()` is the index at which to begin the
splice. If we only provide the one argument, `.splice()` will destructively
remove a chunk of the original array beginning at the provided index and
continuing to the end of the array:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.splice(2);
// => ["Wed", "Thu", "Fri", "Sat", "Sun"]

days;
// => ["Mon", "Tue"]
```

Notice that `.splice()` returns the removed chunk and leaves the remaining
elements in the original array.

With a negative 'start' index, the opposite happens:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]

days.splice(-2);
// => ["Sat", "Sun"]

days;
// => ["Mon", "Tue", "Wed", "Thu", "Fri"]
```

#### With Two Arguments

```js
array.splice(start, deleteCount)
```

When we provide two arguments to `.splice()`, the first is still the index at
which to begin splicing, and the second dictates how many elements we want to
remove from the array. For example, to remove `3` elements, starting with the
element at index `2`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]

days.splice(2, 3);
// => ["Wed", "Thu", "Fri"]

days;
// => ["Mon", "Tue", "Sat", "Sun"]
```

## Replace Elements in an Array

### `.splice()` with 3+ arguments

```js
array.splice(start, deleteCount, item1, item2, ...)
```

After the first two, every additional argument passed to `.splice()` will be
inserted into the array at the position indicated by the first argument. We can
replace a single element in an array as follows, discarding a card and drawing a
new one:

```js
const cards = ['Ace of Spades', 'Jack of Clubs', 'Nine of Clubs', 'Nine of Diamonds', 'Three of Hearts'];

cards.splice(2, 1, 'Ace of Clubs');
// => ["Nine of Clubs"]

cards;
// => ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

Or we can remove two elements and insert three new ones as our restaurant
expands its vegetarian options:

```js
const menu = ['Jalapeno Poppers', 'Cheeseburger', 'Fish and Chips', 'French Fries', 'Onion Rings'];

menu.splice(1, 2, 'Veggie Burger', 'House Salad', 'Teriyaki Tofu');
// => ["Cheeseburger", "Fish and Chips"]

menu;
// => ["Jalapeno Poppers", "Veggie Burger", "House Salad", "Teriyaki Tofu", "French Fries", "Onion Rings"]
```

We aren't required to remove anything with `.splice()` — we can use it to
insert elements anywhere within an array. Here we're adding new books to our
library in alphabetical order:

```js
const books = ['Bleak House', 'David Copperfield', 'Our Mutual Friend'];

books.splice(2, 0, 'Great Expectations', 'Oliver Twist');
// => []

books;
// => ["Bleak House", "David Copperfield", "Great Expectations", "Oliver Twist", "Our Mutual Friend"]
```

Notice that `.splice()` returns an empty array when we provide a second argument
of `0`. This makes sense because the return value is the set of elements that
were removed, and we're telling it to remove `0` elements.

Keep playing around with `.splice()` in your browser's console to get
comfortable with it.

### Using the Computed Member Access Operator to Replace Elements

If we only need to replace a single element in an array, there's a simpler
solution than `.splice()`:

```js
const cards = ['Ace of Spades', 'Jack of Clubs', 'Nine of Clubs', 'Nine of Diamonds', 'Three of Hearts'];

cards[2] = 'Ace of Clubs';
// => "Ace of Clubs"

cards;
// => ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

However, using the computed member access operator (`[]`) is still _destructive_
— it modifies the original array. There's a _nondestructive_ way to replace or
add items at arbitrary points within an array, and it involves two of the
concepts we learned earlier.

### Slicing and Spreading

Combining `.slice()` and the spread operator allows us to replace elements
_nondestructively_, leaving the original array unharmed:

```js
const menu = ['Jalapeno Poppers', 'Cheeseburger', 'Fish and Chips', 'French Fries', 'Onion Rings'];

const newMenu = [...menu.slice(0, 1), 'Veggie Burger', 'House Salad', 'Teriyaki Tofu', ...menu.slice(3)];

menu;
// => ["Jalapeno Poppers", "Cheeseburger", "Fish and Chips", "French Fries", "Onion Rings"]

newMenu;
// => ["Jalapeno Poppers", "Veggie Burger", "House Salad", "Teriyaki Tofu", "French Fries", "Onion Rings"]
```

Play around with this a bit until it makes sense. It's the trickiest thing that
we've encountered in this lesson, so don't sweat it if it takes a little while
to sink in!

## Identify Nested Arrays

In the above 'slicing and spreading' example, if we don't use the spread
operator we're left with an interesting result:

```js
const menu = ['Jalapeno Poppers', 'Cheeseburger', 'Fish and Chips', 'French Fries', 'Onion Rings'];

const newMenu = [menu.slice(0, 1), 'Veggie Burger', 'House Salad', 'Teriyaki Tofu', menu.slice(3)];

newMenu;
// => [["Jalapeno Poppers"], "Veggie Burger", "House Salad", "Teriyaki Tofu", ["French Fries", "Onion Rings"]]
```

Holy nested arrays, Batman!

![Is this the array or the array within an array?](https://curriculum-content.s3.amazonaws.com/web-development/js/data-structures/arrays-readme/insheeption.gif)

That's right — an array can contain elements of **any** data type, including
**other arrays**:

```js
const egregiouslyNestedArray = ['How', ['deep', ['can', ['we', ['go', ['?'], 'Pretty'], 'dang'], 'deep,'], 'it'], 'seems.'];
```

Pop that into your browser's JS console and check out the nesting:

![`egregiouslyNestedArray` in the JS console](https://curriculum-content.s3.amazonaws.com/web-development/js/data-structures/arrays-readme/egregiouslyNestedArray_in_JS_console.png)

It's great that arrays allow us to store other arrays inside them, but this is a
terrible way to represent a deeply nested data structure. In general, try to
keep your arrays to no more than two levels deep. Two levels is perfect for
representing two-dimensional things like a tic-tac-toe board:

```js
const board = [
  ['X', 'O', ' '],
  [' ', 'X', 'O'],
  ['X', ' ', 'O']
];

board;
// => [["X", "O", " "], [" ", "X", "O"], ["X", " ", "O"]]
```

The cool thing about representing a game board like that is in how we can access
the different squares by specifying coordinates. The first `[]` operator grabs
the row that we want, top (`board[0]`), middle (`board[1]`), or bottom
(`board[2]`). For example:

```js
board[1];
// => [" ", "X", "O"]
```

The second `[]` operator specifies the square within that row, left
(`board[1][0]`), middle (`board[1][1]`), or right (`board[1][2]`). For example:

```js
board[0][0];
// => "X"

board[0][2];
// => " "

board[2][2];
// => "O"
```

Effectively, we're using X and Y coordinates to refer to data within a two-
dimensional structure.

## Conclusion

We dove into data structures and the array, including how to create arrays, access elements in an array, add elements to an array, remove elements from an array and replace elements in an array. We also covered the difference between destructive and non-destructive array manipulation.

## Resources
- MDN
  + [Array][array]
  + [`.slice()`][slice]
  + [`.splice()`][splice]

[array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
[slice]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice
[splice]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice

<p class='util--hide'>View <a href='https://learn.co/lessons/js-data-structures-arrays-readme'>Arrays</a> on Learn.co and start learning to code for free.</p>
