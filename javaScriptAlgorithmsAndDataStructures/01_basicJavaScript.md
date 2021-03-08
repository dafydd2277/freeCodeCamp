# Basic JavaScript

- [link][]

[link]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#basic-javascript


## Arrays

```
myArray = [];
myArray.push(value); // Add a value to the end of an array.

myArray.unshift(value); // Add a value to the beginning of an array.

myValue = myArray.pop();  // Remove the high-index element from the array and
                          // assign it to myValue.

myValue = myArray.shift() // Remove the zero-index element from the array and
                          // assign it to myValue.
```

Equality operator: ==
Strict equality operator: ===

```
if (condition) {
  code
} else if (condition) {
  code
} else {
  code
}


switch (num) {
  case value1:
    statement1;
    break;
  case value2:
    statement2;
    break;
//...
  default:
    defaultStatement;
    break;
}
```

JS "Objects" are Perl "hashes" or Python "dictionaries:" key:value pairs. Keys
and their values can be added through dot or bracket notation. Keys are also
called "properties" of the object.

```
var object = {
  'key0': value0,
  'key1': 'value1',
}
object.key2 = value1;
object['key3'] = value2;
delete object.key3;
delete object['key2'];
```

If your property is a variable, you need to use bracket notation. Dot notation
won't work in that use case.

return `<object>[<property>];``

`<object>.hasOwnProperty[<property>]; // returns true/false`
