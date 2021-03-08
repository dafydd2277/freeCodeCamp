# Object Oriented Programming

- [link][link01]

Objects can have functions as properties.

```
let dog = {
  name: "Spot",
  numLegs: 4,
  sayLegs: function() {return "This dog has " + dog.numLegs + " legs."},
};

console.log(dog.sayLegs());
```

Note that `self.numLegs` doesn't work, here. That seems to only be a `class`
thing.

Ah! In an object, it's `this`, not `self`!

```
let dog = {
  name: "Spot",
  numLegs: 4,
  sayLegs: function() {return "This dog has " + this.numLegs + " legs.";}
};

console.log(dog.sayLegs());
```

[link01]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#object-oriented-programming


## Constructor Functions
- [link][link02]

This is important, and will probably be key to many future lessons.

[link02]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/object-oriented-programming/define-a-constructor-function


## Set the Constructor Property
- [link][link03]

[link03]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/object-oriented-programming/remember-to-set-the-constructor-property-when-changing-the-prototype


## Override Inherited Methods
- [link][link04]

I have a problem with this one. Look at this code:

```
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};

function Bird() { }

// Inherit all methods from Animal
Bird.prototype = Object.create(Animal.prototype);

// Bird.eat() overrides Animal.eat()
Bird.prototype.eat = function() {
  return "peck peck peck";
};
```

Why are the prototype settings and modifications done outside the Constructor?
Can they be done within the Constructor? Say, like this?

```
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};

function Bird() {
  this.prototype = Object.create(Animal.prototype);
  this.prototype.constructor = Bird;
  this.prototype.eat = function() {
    return "peck peck peck";
  };
}
```

I think that would result in tidier code.

[link04]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/object-oriented-programming/override-inherited-methods


### Protect Properties Within an Object
- [link][link05]

Variables/Constants/Properties within a Constructor that don't start with the
`this.` construction are private variables, and can't be read or changed from
outside the constructor. Access them through an associated function.

```
function Bird() {
  let weight = 15;

  this.getWeight = function() {
    return weight;
  }
}
```

[link05]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/object-oriented-programming/use-closure-to-protect-properties-within-an-object-from-being-modified-externally
