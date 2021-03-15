# Intermediate Algorithm Scripting
- [link][link00]

[link00]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#intermediate-algorithm-scripting


## Sum All Numbers in a Range
- [link][link01]

- Challenge:
>We'll pass you an array of two numbers. Return the sum of those two numbers plus the sum of all the numbers between them. The lowest number will not always come first.

>For example, sumAll([4,1]) should return 10 because sum of all the numbers between 1 and 4 (both inclusive) is 10.

```
function sumAll(arr) {
  let funcArr = [...arr];

  // Numeric sort, from that lesson.
  funcArr.sort(function(a, b) {
    return a - b;
  });

  let total = 0;
  for ( let i = funcArr[0]; i <= funcArr[1]; i++ ) {
    total = total + i;
  }
  return total;
}

console.log(sumAll([1, 4]));
console.log(sumAll([4, 1]));
console.log(sumAll([5, 10]));
console.log(sumAll([10, 5]));
```

returns

```
10
10
45
45
```

[link01]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/sum-all-numbers-in-a-range


## Diff Two Arrays
- [link][link02]

- Challenge:
>Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.

>Note: You can return the array with its elements in any order.

```
function diffArray(arr1, arr2) {
  let result = [];

  let grind = function(a1, a2) {
    let fa1 = [...a1];
    let fa2 = [...a2];

    fa1
      .filter(item => fa2.indexOf(item) == -1)
      .map(item => result.push(item));
  }
  grind(funcArr1, funcArr2);
  grind(funcArr2, funcArr1);

  return result;
}

console.log(diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]));
console.log(diffArray(["diorite", "andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray(["andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray(["andesite", "grass", "dirt", "dead shrub"], ["andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray([1, "calf", 3, "piglet"], [1, "calf", 3, 4]));
console.log(diffArray([], ["snuffleupagus", "cookie monster", "elmo"]));
console.log(diffArray([1, "calf", 3, "piglet"], [7, "filly"]));
```

returns

```
[ 4 ]
[ 'pink wool' ]
[ 'pink wool', 'diorite' ]
[]
[ 'piglet', 4 ]
[ 'snuffleupagus', 'cookie monster', 'elmo' ]
[ 1, 'calf', 3, 'piglet', 7, 'filly' ]
```

We need to run `.filter() -> .map()` process twice, once in each direction. So,
make a function out of it. Also, since `grind()` is the only point where we
might be manipulating the arrays, we can take care of our mutation prevention
inside the second-tier function.


[link02]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/diff-two-arrays


## Seek and Destroy
- [link][link03]

- Challenge:
>You will be provided with an initial array (the first argument in the destroyer function), followed by one or more arguments. Remove all elements from the initial array that are of the same value as these arguments.

>Note: You have to use the arguments object.

```
function destroyer(arr) {
  let tests = Object.values(arguments).slice(1);

  return arr.filter(function(element) {
    return !tests.includes(element);
  });
}


console.log(destroyer([1, 2, 3, 1, 2, 3], 2, 3));
console.log(destroyer([1, 2, 3, 5, 1, 2, 3], 2, 3));
console.log(destroyer([3, 5, 1, 2, 2], 2, 3, 5));
console.log(destroyer([2, 3, 2, 3], 2, 3));
console.log(destroyer(["tree", "hamburger", 53], "tree", 53));
console.log(destroyer(["possum", "trollo", 12, "safari", "hotdog", 92, 65, "grandma", "bugati", "trojan", "yacht"], "yacht", "possum", "trollo", "safari", "hotdog", "grandma", "bugati", "trojan"));
```

returns

```
[ 1, 1 ]
[ 1, 5, 1 ]
[ 1 ]
[]
[ 'hamburger' ]
[ 12, 92, 65 ]
```

The [hints][hints03] were important, here. This is a good looking result, but
I have to stare at it a while to understand it. The `arguments` object is
particularly important to keep in mind.

[link03]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/seek-and-destroy
[hints03]: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-seek-and-destroy/16046


## Wherefore art thou
- [link][link04]

- Challenge:
>Make a function that looks through an array of objects (first argument) and returns an array of all objects that have matching name and value pairs (second argument). Each name and value pair of the source object has to be present in the object from the collection if it is to be included in the returned array.

>For example, if the first argument is ``[{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }]``, and the second argument is ``{ last: "Capulet" }``, then you must return the third object from the array (the first argument), because it contains the name and its value, that was passed on as the second argument.

```
function whatIsInAName(collection, source) {
  var srcKeys = Object.keys(source);

  return collection.filter(function(obj) {
    return srcKeys.every(function(key) {
      return obj.hasOwnProperty(key) && obj[key] === source[key];
    });
  });
}

console.log(whatIsInAName([{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }], { last: "Capulet" }));
console.log(whatIsInAName([{ "apple": 1 }, { "apple": 1 }, { "apple": 1, "bat": 2 }], { "apple": 1 }));
console.log(whatIsInAName([{ "apple": 1, "bat": 2 }, { "bat": 2 }, { "apple": 1, "bat": 2, "cookie": 2 }], { "apple": 1, "bat": 2 }));
console.log(whatIsInAName([{ "apple": 1, "bat": 2 }, { "apple": 1 }, { "apple": 1, "bat": 2, "cookie": 2 }], { "apple": 1, "cookie": 2 }));
console.log(whatIsInAName([{ "apple": 1, "bat": 2 }, { "apple": 1 }, { "apple": 1, "bat": 2, "cookie": 2 }, { "bat":2 }], { "apple": 1, "bat": 2 }));
console.log(whatIsInAName([{"a": 1, "b": 2, "c": 3}], {"a": 1, "b": 9999, "c": 3}));
```

returns

```
[ { first: 'Tybalt', last: 'Capulet' } ]
[ { apple: 1 }, { apple: 1 }, { apple: 1, bat: 2 } ]
[ { apple: 1, bat: 2 }, { apple: 1, bat: 2, cookie: 2 } ]
[ { apple: 1, bat: 2, cookie: 2 } ]
[ { apple: 1, bat: 2 }, { apple: 1, bat: 2, cookie: 2 } ]
[]
```

I needed the [hints][hints04] here, too. This breaks my brain. But, I need to
learn it, or at least have a library to review.

[link04]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/wherefore-art-thou
[hints04]: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-wherefore-art-thou/16092


## Spinal Tap Case
- [link][link05]

- Challenge:
>Convert a string to spinal case. Spinal case is
all-lowercase-words-joined-by-dashes.

```
function spinalCase(str) {
  let arrOut = [];
  let arrIn = str
              // Add a space before collections of UC.
              .replace(/([A-Z])+/g, ' $1')
              // Then split on non-text boundaries.
              .split(/[\W_-]/);

  arrIn.forEach(
    (element) => {
      if (element.length > 0) {
        arrOut.push(element.toLowerCase())
      }
    }
  );
  return arrOut.join('-');
}

console.log(spinalCase('This Is Spinal Tap'));
console.log(spinalCase("thisIsSpinalTap"));
console.log(spinalCase("The_Andy_Griffith_Show"));
console.log(spinalCase("Teletubbies say Eh-oh"));
console.log(spinalCase("AllThe-small Things"));
```

returns

```
this-is-spinal-tap
this-is-spinal-tap
the-andy-griffith-show
teletubbies-say-eh-oh
all-the-small-things
```

This one started with cribbing the code from the [URL Slugs][slugs] lesson.
Then, how do deal with the stranger (eg. camelCase) constructions? Ah. By
revisiting RegExp lesson called
[Use Capture Groups to Search and Replace][regexp].

[link05]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/spinal-tap-case
[regexp]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/use-capture-groups-to-search-and-replace
[slugs]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/apply-functional-programming-to-convert-strings-to-url-slugs


## Pig Latin
- [link][link06]

- Challenge:
>Pig Latin is a way of altering English Words. The rules are as follows:

>
- If a word begins with a consonant, take the first consonant or consonant
cluster, move it to the end of the word, and add ay to it.
- If a word begins with a vowel, just add way at the end.

>Translate the provided string to Pig Latin. Input strings are guaranteed to be
English words in all lowercase.

The case of starting with consonant clusters was relatively easy. What about
words starting with vowels?

```
function translatePigLatin(str) {
  if (str.match(/^([^aeiou]+)/)) {
    return str.replace(/^([^aeiou]+)(.*)/, '$2$1ay');
  }
  return str + 'way'
}

console.log(translatePigLatin("consonant"));
console.log(translatePigLatin("california"));
console.log(translatePigLatin("paragraphs"));
console.log(translatePigLatin("glove"));
console.log(translatePigLatin("algorithm"));
console.log(translatePigLatin("eight"));
console.log(translatePigLatin("schwartz"));
console.log(translatePigLatin("rhythm"));
```

returns

```
onsonantcay
aliforniacay
aragraphspay
oveglay
algorithmway
eightway
artzschway
rhythmay
```

Can I use `match()` as a conditional? Yes, as it turns out.

[link06]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/pig-latin


## Search and Replace
- [link][link07]

- Challenge:
>Perform a search and replace on the sentence using the arguments provided and return the new sentence.

>First argument is the sentence to perform the search and replace on.

>Second argument is the word that you will be replacing (before).

>Third argument is what you will be replacing the second argument with (after).

>Note: Preserve the case of the first character in the original word when you are replacing it. For example if you mean to replace the word Book with the word dog, it should be replaced as Dog

The search and replace part is relatively straightforward.

```
function myReplace(str, before, after) {
  return str.replace(before, after);
}
```

The capitalization part, though?

```
function myReplace(str, before, after) {
  if (/^[A-Z]/.test(before)) {
    after = after[0].toUpperCase() + after.substring(1)
  } else {
    after = after[0].toLowerCase() + after.substring(1)
  }

  return str.replace(before, after);
}

console.log(myReplace("A quick brown fox jumped over the lazy dog", "jumped", "leaped"));
console.log(myReplace("Let us go to the store", "store", "mall"));
console.log(myReplace("He is Sleeping on the couch", "Sleeping", "sitting") );
console.log(myReplace("I think we should look up there", "up", "Down"));
console.log(myReplace("This has a spellngi error", "spellngi", "spelling") );
console.log(myReplace("His name is Tom", "Tom", "john"));
console.log(myReplace("Let us get back to more Coding", "Coding", "algorithms"));
```

returns

```
A quick brown fox leaped over the lazy dog
Let us go to the mall
He is Sitting on the couch
I think we should look down there
This has a spelling error
His name is John
Let us get back to more Algorithms
```

I wound up using solution 2 from the [hints][hints07] as the most elegant. I
want to remember using regex like that in a conditional.

[link07]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/search-and-replace
[hints07]: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-search-and-replace/16045


## DNA Pairing
- [link][link08]

- Challenge:
>The DNA strand is missing the pairing element. Take each character, get its
pair, and return the results as a 2d array.

>Base pairs are a pair of AT and CG. Match the missing element to the provided
character.

>Return the provided character as the first element in each array.

>For example, for the input GCG, return [["G", "C"], ["C","G"], ["G", "C"]]

>The character and its pair are paired up in an array, and all the arrays are
grouped into one encapsulating array.



```
function pairElement(str) {
  // An empty string inside the split() splits on every character.
  let testArr = str.split('');
  let returnArr = [];

  // arr.forEach(name => {function using name;})
  testArr.forEach(element => {
    let pairArr = [];
    switch (element) {
      case 'A':
        pairArr = [ 'A', 'T'];
        break;
      case 'T':
        pairArr = [ 'T', 'A'];
        break;
      case 'C':
        pairArr = [ 'C', 'G'];
        break;
      case 'G':
        pairArr = [ 'G', 'C'];
        break;
    }
    returnArr.push(pairArr);
  });

  return returnArr;
}

console.log(pairElement("GCG"));
console.log(pairElement("ATCGA"));
console.log(pairElement("TTGAG"));
console.log(pairElement("CTCTA"));
```

returns

```
[ [ 'G', 'C' ], [ 'C', 'G' ], [ 'G', 'C' ] ]
[ [ 'A', 'T' ],
  [ 'T', 'A' ],
  [ 'C', 'G' ],
  [ 'G', 'C' ],
  [ 'A', 'T' ] ]
[ [ 'T', 'A' ],
  [ 'T', 'A' ],
  [ 'G', 'C' ],
  [ 'A', 'T' ],
  [ 'G', 'C' ] ]
[ [ 'C', 'G' ],
  [ 'T', 'A' ],
  [ 'C', 'G' ],
  [ 'T', 'A' ],
  [ 'A', 'T' ] ]
```

[link08]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/dna-pairing


## Missing letters
- [link][link09]

- Challenge:
>Find the missing letter in the passed letter range and return it.

>If all letters are present in the range, return `undefined`.


```
function fearNotLetter(str) {
  // Set the ASCII value of the first letter in the string.
  let compare = str.charCodeAt(0);
  let missing; // Starts out undefined.

  str.split("").map(function(letter, index) {
    if (str.charCodeAt(index) == compare) {
      ++compare;
    } else {
      missing = String.fromCharCode(compare);
    }
  });

  return missing;
}

console.log(fearNotLetter("abce"));
console.log(fearNotLetter("abcdefghjklmno"));
console.log(fearNotLetter("stvwx"));
console.log(fearNotLetter("bcdf"));
console.log(fearNotLetter("abcdefghijklmnopqrstuvwxyz"));
```

returns

```
d
i
u
e
undefined
```

I totally punted on this one, and went straight to the hints. This solution was
my favorite. See [the documentation][hint09] for `array.map()` for further
hints. Note that we never actually use the letter itself. We just use its
index in the string to get its ASCII value. Then, compare that value to the
expected (`compare`) value. If you get a mismatch, you've found your missing
letter.

[link09]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/missing-letters
[hint09]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map


## Sorted Union
- [link][link10]

- Challenge:
>Write a function that takes two or more arrays and returns a new array of unique values in the order of the original provided arrays.

>In other words, all values present from all arrays should be included in their original order, but with no duplicates in the final array.

>The unique numbers should be sorted by their original order, but the final array should not be sorted in numerical order.

>Check the assertion tests for examples.

```
function uniteUnique() {
  var concatArr = [];
  var i = 0;
  while (arguments[i]) {
    // Concatenate the elemental arrays into a single array. This will have
    // duplicate entries.
    concatArr = concatArr.concat(arguments[i]);
    i++;
  }
  let uniqueArray = concatArr.filter(function(item, pos) {
    return concatArr.indexOf(item) == pos;
  });
  return uniqueArray;
}

console.log(uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]));
console.log(uniteUnique([1, 2, 3], [5, 2, 1]));
console.log(uniteUnique([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]));
```

returns

```
[ 1, 3, 2, 5, 4 ]
[ 1, 2, 3, 5 ]
[ 1, 2, 3, 5, 4, 6, 7, 8 ]
```

I punted on this one, as well. This solution is my favorite because of the way
it uses `concatArr.indexOf(item) == pos`. That only returns `true` the first
time `item` is encountered in the array, because `arr.indexOf()` returns the
position of the first hit of `item`. So, a duplicate of `item` will have a
different `pos`, the conditional return `false`, and `item` won't be
duplicated in the `uniqueArray`.

[link10]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/sorted-union


## Convert HTML Entities
- [link][link11]

- Challenge:
>Convert the characters &, <, >, " (double quote), and ' (apostrophe), in a
string to their corresponding HTML entities.

```
function convertHTML(str) {
  let inArr = str.split('');
  let outArr = [];

  inArr.forEach(element => {
    switch (element) {
      case '&':
        outArr.push('&amp;');
        break;
      case '<':
        outArr.push('&lt;');
        break;
      case '>':
        outArr.push ('&gt;');
        break;
      case '"':
        outArr.push ('&quot;');
        break;
      case '\'':
        outArr.push ('&apos;');
        break;
      default:
        outArr.push(element);
    }
  });
  return outArr.join('');
}

console.log(convertHTML("Dolce & Gabbana"));
console.log(convertHTML("Hamburgers < Pizza < Tacos"));
console.log(convertHTML("Sixty > twelve"));
console.log(convertHTML('Stuff in "quotation marks"'));
console.log(convertHTML("Schindler's List"));
console.log(convertHTML("<>"));
console.log(convertHTML("abc"));
```

returns

```
console.log(convertHTML("Dolce & Gabbana"));
console.log(convertHTML("Hamburgers < Pizza < Tacos"));
console.log(convertHTML("Sixty > twelve"));
console.log(convertHTML('Stuff in "quotation marks"'));
console.log(convertHTML("Schindler's List"));
console.log(convertHTML("<>"));
console.log(convertHTML("abc"));
```

This was just another `split()` and `switch()`, like a couple challenges ago.
The second solution on the [hints page][hints11] is much cleaner:

```
function convertHTML(str) {
  // Use Object Lookup to declare as many HTML entities as needed.
  const htmlEntities = {
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&apos;"
  };
  // Using a regex, replace characters with it's corresponding html entity
  return str.replace(/([&<>\"'])/g, match => htmlEntities[match]);
}
```

That's much more elegant than my solution. Note that the `match` variable in
the regex `replace()` function is the contents of the parenthesized regex range
in the first argument.

In my browser at least, the third solution would throw an error for trying to
do `str.split().map()`. My browser wouldn't recognize that the `.map()`
function was working on an array created by the `split()` function. It would
think I was trying to run an array function on the string `str`, and throw an
error.

[link11]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/convert-html-entities

## Sum All Odd Fibonacci Numbers
- [link][link12]

- Challenge:
>Given a positive integer num, return the sum of all odd Fibonacci numbers that
are less than or equal to num.

>The first two numbers in the Fibonacci sequence are 1 and 1. Every additional
number in the sequence is the sum of the two previous numbers. The first six
numbers of the Fibonacci sequence are 1, 1, 2, 3, 5 and 8.

>For example, sumFibs(10) should return 10 because all odd Fibonacci numbers
less than or equal to 10 are 1, 1, 3, and 5.

```
function sumFibs(num) {
 let prevNumber = 0;
  let currNumber = 1;
  let result = 0;
  while (currNumber <= num) {
    if (currNumber % 2 !== 0) {
      result += currNumber;
    }
    currNumber += prevNumber;
    prevNumber = currNumber - prevNumber;
  }

  return result;
}

console.log(sumFibs(1));
console.log(sumFibs(1000));
console.log(sumFibs(4000000));
console.log(sumFibs(4));
console.log(sumFibs(75024));
console.log(sumFibs(75025));
```

returns

```
2
1785
4613732
5
60696
135721
```

I punted on this one as well, and went with [solution 1][hints12]. Why is the
result of `sumFibs(1)` equal to 2? Because the odd elements of the Fib sequence
&lt;= 1 are 0, 1, 1.

[link12]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/intermediate-algorithm-scripting/sum-all-odd-fibonacci-numbers
[hints12]: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-sum-all-odd-fibonacci-numbers/16084
