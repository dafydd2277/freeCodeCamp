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
