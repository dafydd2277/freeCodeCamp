# Basic Algorithm Scripting

- [link][]

[link]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#basic-algorithm-scripting


## Convert Celsius to Fahrenheit

```
function convertToF(celsius) {
  return (9/5 * celsius) +32;
}

console.log(convertToF(-30));
console.log(convertToF(-10));
console.log(convertToF(0));
console.log(convertToF(20));
console.log(convertToF(30));
```


## Reverse a String

```
function reverseString(str) {
  let result = '';

  for ( let i = str.length-1; i >= 0; i-- ) {
    result = result + str[i];
  }

  return result;
}

console.log(reverseString("hello"));
console.log(reverseString("Greetings from Earth"));
```


## Factorialize a Number

```
function factorialize(num) {
  if ( num === 0 ) {
    return 1;
  }

  let result = 1;
  for ( let i = num; i >= 1; i-- ) {
      result = result * i;
  }
  return result;
}

console.log(factorialize(5));
console.log(factorialize(10));
console.log(factorialize(20));
console.log(factorialize(0));
```


## Find the Longest Word in a String

```
function findLongestWordLength(str) {
  let regEx = /\S*/g
  let wordArray = str.match(regEx);
  let maxLength = 0;

  for ( let i = 0; i < wordArray.length; i++ ) {
    if (wordArray[i].length > maxLength) {
      maxLength = wordArray[i].length;
    }
  }
  return maxLength;
}

console.log(findLongestWordLength("The quick brown fox jumped over the lazy dog"));
console.log(findLongestWordLength("May the force be with you"));
console.log(findLongestWordLength("Google do a barrel roll"));
console.log(findLongestWordLength("What is the average airspeed velocity of an unladen swallow"));
console.log(findLongestWordLength("What if we try a super-long word such as otorhinolaryngology"));
```


## Return Largest Numbers in Arrays

```
function largestOfFour(arr) {
  let arrResult = [];

  for ( let i = 0; i < arr.length; i++ ) {
    let intResult = -9999;
    for ( let j = 0; j < arr[i].length; j++ ) {
        if ( arr[i][j] > intResult ) {
          intResult = arr[i][j];
        }
    }
    arrResult.push(intResult);
  }

  return arrResult;
}

console.log(largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]));
console.log(largestOfFour([[13, 27, 18, 26], [4, 5, 1, 3], [32, 35, 37, 39], [1000, 1001, 857, 1]]));
console.log(largestOfFour([[4, 9, 1, 3], [13, 35, 18, 26], [32, 35, 97, 39], [1000000, 1001, 857, 1]]));
console.log(largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]]));
```


## Confirm the Ending

```
function confirmEnding(str, target) {
  let position = str.length - target.length;

  if ( str.substring(position) == target ) {
    return true;
  }
  return false;
}

console.log(confirmEnding("Bastian", "n"));
console.log(confirmEnding("Congratulation", "on"));
console.log(confirmEnding("Connor", "n"));
console.log(confirmEnding("Walking on water and developing software from a specification are easy if both are frozen", "specification"));
console.log(confirmEnding("He has to give me a new name", "name"));
console.log(confirmEnding("Open sesame", "same"));
console.log(confirmEnding("Open sesame", "sage"));
console.log(confirmEnding("Open sesame", "game"));
console.log(confirmEnding("If you want to save our world, you must hurry. We dont know how much longer we can withstand the nothing", "mountain"));
console.log(confirmEnding("Abstraction", "action"));
```


## Repeat a String Repeat a String

```
function repeatStringNumTimes(str, num) {
  let result = '';

  for ( let i = 1; i <= num; i++ ) {
    result = result + str;
  }

  return result;
}

console.log(repeatStringNumTimes("*", 3));
console.log(repeatStringNumTimes("abc", 3));
console.log(repeatStringNumTimes("abc", 4));
console.log(repeatStringNumTimes("abc", 1));
console.log(repeatStringNumTimes("*", 8));
console.log(repeatStringNumTimes("abc", -2));
console.log(repeatStringNumTimes("abc", 0));
```


## Truncate a String

```
function truncateString(str, num) {
  if (str.length > num) {
    return str.substring(0,num) + '...';
  }
  return str;

}

console.log(truncateString("A-tisket a-tasket A green and yellow basket", 8));
console.log(truncateString("Peter Piper picked a peck of pickled peppers", 11));
console.log(truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length));
console.log(truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length + 2));
console.log(truncateString("A-", 1));
console.log(truncateString("Absolutely Longer", 2));
```


## Finders Keepers

```
function findElement(arr, func) {

  for ( let i = 0; i < arr.length; i++ ) {
    if ( func(arr[i]) ) {
      return arr[i];
    }
  }
  return undefined;
}

console.log(findElement([1, 2, 3, 4], num => num % 2 === 0));
console.log(findElement([1, 3, 5, 8, 9, 10], function(num) { return num % 2 === 0; }));
console.log(findElement([1, 3, 5, 9], function(num) { return num % 2 === 0; }));
```


## Boo who

```
function booWho(bool) {

  if ( typeof(bool) === "boolean" ) {
    return true
  }
  return false;
}

console.log(booWho(true));
console.log(booWho(false));
console.log(booWho([1, 2, 3]));
console.log(booWho([].slice));
console.log(booWho({ "a": 1 }));
console.log(booWho(1));
console.log(booWho(NaN));
console.log(booWho("a"));
console.log(booWho("true"));
console.log(booWho("false"));
```


##  Title Case A Sentence

```
function titleCase(str) {
  let strArray = str.toLowerCase().split(' ');

  for ( let i = 0; i < strArray.length; i++ ) {
    strArray[i] = strArray[i].charAt(0).toUpperCase() +
      strArray[i].substring(1);
  }

  return strArray.join(' ');
}

console.log(titleCase("I'm a little tea pot"));
console.log(titleCase("sHoRt AnD sToUt"));
console.log(titleCase("HERE IS MY HANDLE HERE IS MY SPOUT"));
```

The solutions page is a good reference: https://forum.freecodecamp.org/t/freecodecamp-challenge-guide-title-case-a-sentence/16088


## Slice and Splice

```
function frankenSplice(arr1, arr2, n) {
  let arrFinal = arr2.slice();

  for ( let i=0; i < arr1.length; i++ ) {
      arrFinal.splice(n+i, 0, arr1[i]);
  }

  return arrFinal;
}

console.log(frankenSplice([1, 2, 3], [4, 5, 6], 1));
console.log(frankenSplice([1, 2, 3], [4, 5], 1));
console.log(frankenSplice([1, 2], ["a", "b"], 1));
console.log(frankenSplice(["claw", "tentacle"], ["head", "shoulders", "knees", "toes"], 2));
```


## Falsy Bouncer

```
function bouncer(arr) {
  let outArray = [];

  for ( let i in arr ) {
    if ( Boolean(arr[i]) ) {
      outArray.push(arr[i]);
    }
  }
  return outArray;
}

console.log(bouncer([7, "ate", "", false, 9]));
console.log(bouncer(["a", "b", "c"]));
console.log(bouncer([false, null, 0, NaN, undefined, ""]));
console.log(bouncer([null, NaN, 1, 2, undefined]));
```


## Where Do I Belong
See [here][] for hints.

```
function getIndexToIns(arr, num) {
  // Adding the function makes the sort() numeric instead of string.
  let arrSorted = arr.sort(function(a, b){return a - b});

  for ( let i = 0; i < arrSorted.length; i++ ) {
    //console.log( arrSorted[i]);
    if ( num > arrSorted[i] && num <= arrSorted[i+1]) {
      return i+1;
    } else if ( num > arrSorted[i] && i+1 == arrSorted.length ) {
      return i+1;
    }
  }
  return 0;
}

console.clear();
console.log(getIndexToIns([10, 20, 30, 40, 50], 35));
console.log(getIndexToIns([10, 20, 30, 40, 50], 30));
console.log(getIndexToIns([40, 60], 50));
console.log(getIndexToIns([3, 10, 5], 3));
console.log(getIndexToIns([5, 3, 20, 3], 5));
console.log(getIndexToIns([2, 20, 10], 19));
console.log(getIndexToIns([2, 5, 10], 15));
console.log(getIndexToIns([], 1));
```

[here]: https://www.geeksforgeeks.org/how-to-sort-numeric-array-using-javascript/


## Mutations

```
function mutation(arr) {
  let arrField = arr[0].toLowerCase();
  let arrMatch = arr[1].toLowerCase();
  let result = true;

  for ( let i in arrMatch ) {
    if ( arrField.indexOf(arrMatch.charAt(i)) < 0 ) {
      result = false;
    }
  }
  return result;
}

console.log(mutation(["hello", "hey"]));
console.log(mutation(["hello", "Hello"]));
console.log(mutation(["zyxwvutsrqponmlkjihgfedcba", "qrstu"]));
console.log(mutation(["Mary", "Army"]));
console.log(mutation(["Mary", "Aarmy"]));
console.log(mutation(["Alien", "line"]));
console.log(mutation(["floor", "for"]));
console.log(mutation(["hello", "neo"]));
console.log(mutation(["voodoo", "no"]));
console.log(mutation(["ate", "date"]));
console.log(mutation(["Tiger", "Zebra"]));
console.log(mutation(["Noel", "Ole"]));
```


## Chunky Monkey

```
function chunkArrayInGroups(arr, size) {
  let arrSource = arr;
  let arrResult = [];

  while ( arr.length > size ) {
    // Create the chunks.
    let arrChunk = [];
    for ( let i = 0; i < size; i++ ) {
      arrChunk[i] = arrSource.shift();
    }
    arrResult.push([...arrChunk]);
  }
  // Add the final, remaining chunk.
  arrResult.push([...arrSource]);
  return arrResult;
}

console.log(chunkArrayInGroups(["a", "b", "c", "d"], 2));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5], 3));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5], 2));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5], 4));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 4));
console.log(chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 2));
```
