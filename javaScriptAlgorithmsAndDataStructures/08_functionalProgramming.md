# Functional Programming
- [link][link01]

Really, everything here needs to be studied a couple times.

[link01]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#functional-programming


## Understand Functional Programming Terminology
- [link][link02]

This is important ground work.

[Here's the hint page][hint].

The biggest hint has to do with how `splice()` operates, and the fix is this
modified `tabClose()` function:

```
Window.prototype.tabClose = function (index) {

  // Only change code below this line

  var tabsBeforeIndex = this.tabs.splice(0, index); // Get the tabs before the tab
  var tabsAfterIndex = this.tabs.splice(1); // Get the tabs after the tab

  this.tabs = tabsBeforeIndex.concat(tabsAfterIndex); // Join them together

  // Only change code above this line

  return this;
 };
```

Since `splice()` basically does a mass `unshift()` from `tabs[]` and leaves
index 0 as an empty string, the remaining items in `tabs[]` start at index 1.

[hint]: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-understand-the-hazards-of-using-imperative-code/301241
[link02]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/understand-functional-programming-terminology


## Using the map() Method to Extract Data from an Array.
- [link][link03]

I can see the utility of this, but it's deeper than I'm good at, so far. Again,
I'm going to need to keep coming back to this entire section. Particularly,
I need more practice at passing a function into a method.

[link03]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-the-map-method-to-extract-data-from-an-array


## Implement map() on a Prototype
- [link][link04]

```
Array.prototype.myMap = function(callback) {
  var newArray = [];
  // Only change code below this line
  this.forEach(item => newArray.push(callback(item)));
  // Only change code above this line
  return newArray;
};
```

[link04]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/implement-map-on-a-prototype


## Use the filter() Method to Extract Data from an Array
- [link][link05]

Note the `filteredList.push()` which actually adds the mapped items into the
final array.

```
var filteredList = [];

watchList
  .filter(item => +(item.imdbRating) >= 8.0 )
  .map(item => filteredList.push({"title": item.Title, "rating": item.imdbRating}));
```

The `+` sign tells python to variable type of `item.imdbRating` as a float.

[link05]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-the-filter-method-to-extract-data-from-an-array


## Implement the filter() Method on a Prototype
- [link][link06]

```
Array.prototype.myFilter = function(callback) {
  // Only change code below this line
  var newArray = [];
  this.forEach(function(item) { if (callback(item)) { newArray.push(item)}});
  // Only change code above this line
  return newArray;
};
```

[link06]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/implement-the-filter-method-on-a-prototype


## Return Part of an Array Using the slice() Method
- [link][link07]

The line `var localArray = [...anim]` creates a duplicate of `anim[]`, rather
than a reference. This means the elements of `anim[]` can be changed or
deleted without breaking the original array.

```
function sliceArray(anim, beginSlice, endSlice) {
  // Only change code below this line
  var localArray = [...anim];
  return localArray.slice(beginSlice, endSlice);
  // Only change code above this line
}
var inputAnim = ["Cat", "Dog", "Tiger", "Zebra", "Ant"];

console.log(inputAnim);
console.log(sliceArray(inputAnim, 1, 3));
```

[link07]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/return-part-of-an-array-using-the-slice-method


## Remove Elements from an Array Using slice() Instead of splice()
- [link][link08]

>Rewrite the function `nonMutatingSplice()` by using slice instead of splice. It
should limit the provided cities array to a length of 3, and return a new
array with only the first three items.

>Do not mutate the original array provided to the function.

```
function nonMutatingSplice(cities) {
  // Only change code below this line
  let localArray = [...cities];

  return localArray.slice(0, 3);

  // Only change code above this line
}
var inputCities = ["Chicago", "Delhi", "Islamabad", "London", "Berlin"];

console.log(nonMutatingSplice(inputCities));
console.log(inputCities);
```

[link08]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/remove-elements-from-an-array-using-slice-instead-of-splice


## Use the reduce() Method to Analyze Data
- [link][link09]

>The variable watchList holds an array of objects with information on several
movies. Use reduce to find the average IMDB rating of the movies directed by
Christopher Nolan. Recall from prior challenges how to filter data and map over
it to pull what you need. You may need to create other variables, and return
the average rating from getRating function. Note that the rating values are
saved as strings in the object and need to be converted into numbers before
they are used in any mathematical operations.

```
function getRating(watchList){
  // Add your code below this line
  var averageRating =
  watchList
    // Use filter to find films directed by Christopher Nolan
    .filter(film => film.Director === "Christopher Nolan")
    // Use map to convert their ratings from strings to numbers
    .map(film => Number(film.imdbRating))
    // Use reduce to add together their ratings
    .reduce((sumOfRatings, rating) => sumOfRatings + rating) /
  // Divide by the number of Nolan films to get the average rating
  watchList.filter(film => film.Director === "Christopher Nolan").length;
  // Add your code above this line
  return averageRating;
}
console.log(getRating(watchList));
```

and again, without the comments and with some indentation.

```
function getRating(watchList){
  // Add your code below this line
  var averageRating =
  watchList
    .filter(film => film.Director === "Christopher Nolan")
    .map(film => Number(film.imdbRating))
    .reduce((sumOfRatings, rating) => sumOfRatings + rating)
      / watchList.filter(film => film.Director === "Christopher Nolan").length;
  // Add your code above this line
  return averageRating;
}
console.log(getRating(watchList));
```

Working out how this works, step by step, is important. I'm going to need to
review the `map()` function some more. I basically had to crib this solution,
and I don't get how the callback function in the `reduce()` element works.

[link09]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-the-reduce-method-to-analyze-data


## Use Higher-Order Functions map(), filter(), or reduce() to Solve a Complex Problem

>We have defined a function named squareList. You need to complete the code for
the squareList function using any combination of map(), filter(), and reduce()
so that it returns a new array containing only the square of only the positive
integers (decimal numbers are not integers) when an array of real numbers is
passed to it. An example of an array containing only real numbers is
[-3, 4.8, 5, 3, -3.2].

>Note: Your function should not use any kind of for or while loops or the forEach() function.

```
const squareList = arr => {
  // Only change code below this line
  var filteredList = [];
  arr
  .filter(item => Number(item) > 0)
  .filter(item => Math.floor(Number(item)) == Number(item))
  .map(item => filteredList.push(item * item));
  return filteredList;
  // Only change code above this line
};

const squaredIntegers = squareList([-3, 4.8, 5, 3, -3.2]);
console.log(squaredIntegers);
```

I'm starting to like how this works. I need to see more tutorials on the
`reduce()` method, though. I got this one without help, but note I didn't use
the hard method...

[link10]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-higher-order-functions-map-filter-or-reduce-to-solve-a-complex-problem


## Sort an Array Alphabetically using the sort Method
- [link][link11]

- Lesson excerpt:
>When such a callback function, normally called compareFunction, is supplied,
the array elements are sorted according to the return value of the
compareFunction: If compareFunction(a,b) returns a value less than 0 for two
elements a and b, then a will come before b. If compareFunction(a,b) returns a
value greater than 0 for two elements a and b, then b will come before a. If
compareFunction(a,b) returns a value equal to 0 for two elements a and b, then
a and b will remain unchanged.

- Challenge:
>Use the sort method in the alphabeticalOrder function to sort the elements of
arr in alphabetical order.

```
function alphabeticalOrder(arr) {
  // Only change code below this line
  return arr.sort(function(a, b) {
    return a === b ? 0 : a > b ? 1 : -1;
  });


  // Only change code above this line
}
console.log(alphabeticalOrder(["a", "d", "c", "a", "z", "g"]));
console.log(alphabeticalOrder(["x", "h", "a", "m", "n", "m"]));
console.log(alphabeticalOrder(["a", "a", "a", "a", "x", "t"]));
```

returns

```
[ 'a', 'a', 'c', 'd', 'g', 'z' ]
[ 'a', 'h', 'm', 'm', 'n', 'x' ]
[ 'a', 'a', 'a', 'a', 't', 'x' ]
```

The sort function in the lesson is the same as the interior `return` line here,
except that `a < b` for the reverse sort in the lesson.

[link11]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/sort-an-array-alphabetically-using-the-sort-method


## Return a Sorted Array Without Changing the Original Array
- [link][link12]

>Use the sort method in the nonMutatingSort function to sort the elements of an
array in ascending order. The function should return a new array, and not
mutate the globalArray variable.

```
var globalArray = [5, 6, 3, 2, 9];
function nonMutatingSort(arr) {
  // Only change code below this line
  let localArray = [...arr];
  return localArray.sort(function(a, b) {
    return a === b ? 0 : a > b ? 1 : -1;
  });

  // Only change code above this line
}

console.log(globalArray);
console.log(nonMutatingSort(globalArray));
```

returns

```
[ 5, 6, 3, 2, 9 ]
[ 2, 3, 5, 6, 9 ]
```

- Note that I could have used

```
function ascendingOrder(arr) {
  return arr.sort(function(a, b) {
    return a - b;
  });
}
ascendingOrder([1, 5, 2, 3, 4]);
```

from the previous lesson.

[link12]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/return-a-sorted-array-without-changing-the-original-array


## Split a String into an Array Using the split Method
- [link][link13]

- Lesson:
>The split method splits a string into an array of strings. It takes an
argument for the delimiter, which can be a character to use to break up the
string or a regular expression. For example, if the delimiter is a space, you
get an array of words, and if the delimiter is an empty string, you get an
array of each character in the string.

- Challenge:
>Use the split method inside the splitify function to split str into an array
of words. The function should return the array. Note that the words are not
always separated by spaces, and the array should not contain punctuation.

This is easy, since a short cut for "not an alphabetic character" (`\W`)
exists.

```
function splitify(str) {
  // Only change code below this line
  return str.split(/\W/);

  // Only change code above this line
}
console.log(splitify("Hello World,I-am code"));
console.log(splitify("Earth-is-our home"));
console.log(splitify("This.is.a-sentence"));
```

returns

```
[ 'Hello', 'World', 'I', 'am', 'code' ]
[ 'Earth', 'is', 'our', 'home' ]
[ 'This', 'is', 'a', 'sentence' ]
```

[link13]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/split-a-string-into-an-array-using-the-split-method


## Combine an Array into a String Using the join Method
- [link][link14]

- Lesson:
>The join method is used to join the elements of an array together to create a
string. It takes an argument for the delimiter that is used to separate the
array elements in the string.

- Challenge:
>Use the join method (among others) inside the sentensify function to make a
sentence from the words in the string str. The function should return a string.
For example, I-like-Star-Wars would be converted to I like Star Wars. For this
challenge, do not use the replace method.

This is going to be a split-then-join, I'm pretty sure...

```
function sentensify(str) {
  // Only change code below this line

  return str.split(/\W/).join(" ");

  // Only change code above this line
}

console.log(sentensify("May-the-force-be-with-you"));
console.log(sentensify("The.force.is.strong.with.this.one"));
console.log(sentensify("There,has,been,an,awakening"));
```

returns

```
May the force be with you
The force is strong with this one
There has been an awakening
```

[link14]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/combine-an-array-into-a-string-using-the-join-method


## Apply Functional Programming to Convert Strings to URL Slugs
- [link][link15]

- Lesson:
>Many content management sites (CMS) have the titles of a post added to part of
the URL for simple bookmarking purposes. For example, if you write a Medium
post titled Stop Using Reduce, it's likely the URL would have some form of the
title string in it (.../stop-using-reduce). You may have already noticed this
on the freeCodeCamp site.

- Challenge:
>Fill in the urlSlug function so it converts a string title and returns the
hyphenated version for the URL. You can use any of the methods covered in this
section, and don't use replace.

```
// Only change code below this line
function urlSlug(title) {
  let arrIn = title.split(/\W/);
  let arrOut = [];

  arrIn.forEach(
    (element) => {
      if (element.length > 0) {
        arrOut.push(element.toLowerCase())
      }
    }
  );

  return arrOut.join('-');

}
// Only change code above this line

console.log(urlSlug("Winter Is Coming"));
console.log(urlSlug(" Winter Is  Coming"));
console.log(urlSlug("A Mind Needs Books Like A Sword Needs A Whetstone"));
console.log(urlSlug("Hold The Door"));
```

returns

```
winter-is-coming
winter-is-coming
a-mind-needs-books-like-a-sword-needs-a-whetstone
hold-the-door
```

The syntax of the function inside the `forEach()` method was the sticking
point.

[link15]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/apply-functional-programming-to-convert-strings-to-url-slugs


## Use the every Method to Check that Every Element in an Array Meets a Criteria
- [link][link16]

- Lesson:
>The every method works with arrays to check if every element passes a
particular test. It returns a Boolean value - true if all values meet the
criteria, false if not.

- Challenge:
>Use the every method inside the checkPositive function to check if every
element in arr is positive. The function should return a Boolean value.

```
function checkPositive(arr) {
  // Only change code below this line
  return arr.every((element) => {
    if (element > 0) {
      return true;
    }
    return false;
  })
  // Only change code above this line
}
console.log(checkPositive([1, 2, 3, -4, 5]));
console.log(checkPositive([1, 2, 3, 4, 5]));
console.log(checkPositive([1, -2, 3, -4, 5]));
```

returns

```
false
true
false
```

[link16]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-the-every-method-to-check-that-every-element-in-an-array-meets-a-criteria


## Use the some Method to Check that Any Elements in an Array Meet a Criteria
- [link][link17]

- Lesson:
>The some method works with arrays to check if any element passes a particular
test. It returns a Boolean value - true if any of the values meet the criteria,
false if not.

- Challenge:
>Use the some method inside the checkPositive function to check if any element
in arr is positive. The function should return a Boolean value.

```
function checkPositive(arr) {
  // Only change code below this line
  return arr.some((element) => {
    if (element > 0) {
      return true;
    }
    return false;
  })
  // Only change code above this line
}
console.log(checkPositive([1, 2, 3, -4, 5]));
console.log(checkPositive([1, 2, 3, 4, 5]));
console.log(checkPositive([-1, -2, -3, -4, -5]));
```

returns

```
true
true
false
```

The power of taking notes includes recognizing the value of copy/paste/edit. I
only needed to change one word in the function, and the third called test.
(The real power is having both cases here, where I can easily see them.)

[link17]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-the-some-method-to-check-that-any-elements-in-an-array-meet-a-criteria


## Introduction to Currying and Partial Application
- [link][link18]

- Lesson:
>The arity of a function is the number of arguments it requires. Currying a
function means to convert a function of N arity into N functions of arity 1.

>In other words, it restructures a function so it takes one argument, then
returns another function that takes the next argument, and so on.

- Challenge:
>Fill in the body of the add function so it uses currying to add parameters x,
y, and z.

```
function add(x) {
  // Only change code below this line

  return function(y) {
    return function(z) {
      return x + y + z;
    }
  }
  // Only change code above this line
}
console.log(add(10)(20)(30));
console.log(add(1)(2)(3));
console.log(add(11)(22)(33));
```

returns

```
60
6
66
```

This hurts my brain. You still need to know how many ending arguments you're
going to need. So, how flexible is this, really? I may find a use case for
this, but it will be a while.

[link18]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/introduction-to-currying-and-partial-application
