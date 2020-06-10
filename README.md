# Javascript-Prototypes-and-Ineritance
A simple walkthrough of how they work

This is a simple object called parent. Using Object.create() is a way to make    
an instance of that object.
```
const parent = {
  name: "Frank",
  age: 44,
  heritage: "Swiss"
}

const child = Object.create(parent)
child.name = "Sally"
child.age = 5

console.log(child.age) // 5
```

#### Prototypes - a first pass
In its most simple form, a prototype is property on a function. More specifically, it's a property on a function that points to an object.  So a prototype is a property that every function in JS has. It allows us to share methods across all instances of a function.

```
function Animal(name, energy){
  let animal = Object.create(Animal.prototype)
  animal.name = name
  animal.energy = energy
  
  return animal
}

Animal.prototype.eat = function(amount){
  console.log(`${this.name} is eating.`)
  this.energy += amount
}
Animal.prototype.sleep = function(length){
  console.log(`${this.name} is sleeping.`)
  this.energy += length
}
Animal.prototype.play = function(length){
  console.log(`${this.name} is playing.`)
  this.energy -= length
}

const leo = Animal('Leo', 5);

console.log(leo.play(5)) // "leo is playing"
```


#### Prototypes - a second pass
This is a better solution than the one above.  This will use 'new' so we can remove the Object.create() and don't need to return the animal.

```
function Animal(name, energy){
  this.name = name
  this.energy = energy
}

Animal.prototype.eat = function(amount){
  console.log(`${this.name} is eating.`)
  this.energy += amount
}
Animal.prototype.sleep = function(length){
  console.log(`${this.name} is sleeping.`)
  this.energy += length
}
Animal.prototype.play = function(length){
  console.log(`${this.name} is playing.`)
  this.energy -= length
}

const leo = new Animal('Leo', 5)

console.log(leo.play(5)) // "leo is playing"
```


#### Prototypes - a third pass
This will use the ES6 Class.  This is an even better solution than the two above.

```
class Animal {
    constructor(name, energy){
        this.name = name;
        this.energy = energy
    }
    
    eat(amount){
       console.log(`${this.name} is eating.`)
       this.energy += amount
    }
    
    sleep(length){
       console.log(`${this.name} is sleeping.`)
       this.sleep += length
    }
    
    play(length){
      console.log(`${this.name} is playing.`)
      this.play -= length
    }
    
  }
  
  const leo = new Animal('Leo', 5)
  console.log(leo.eat()) // leo is eating

```

#### Inheritance ES5 version
```
function Animal(name, energy) {
    this.name = name
    this.energy = energy
}

Animal.prototype.eat = function(amount){
    console.log(`${this.name} is eating`)
    this.energy += amount;
}

Animal.prototype.sleep = function(length){
    console.log(`${this.name} is sleeping`)
    this.energy += length;
}

Animal.prototype.play = function(length){
    console.log(`${this.name} is playing`)
    this.energy += length;
}

// a Dog subclass
function Dog(name, energy, breed) {
    // inherit name and energy from Animal using call
    Animal.call(this, name, energy)
    // create a unique property to the instance
    this.breed = breed
}

// make sure that Dog is equal to the Animal
Dog.prototype = Object.create(Animal.prototype)
// reset constructor to be Dog
Dog.prototype.constructor = Dog;

// add another method to the Dog prototype
Dog.prototype.bark = function() {
    console.log('Woof Woof')
    this.energy -= .1
}


const fido = new Dog('Fido', 10, 'Rottweiler')
console.log(fido.play(5))
```

#### Inheritance ES6 version
This is much simpler than the ES5 version.

```

class Animal {
    constructor(name, energy){
        this.name = name;
        this.energy = energy
    }

    eat(amount) {
        console.log(`${this.name} is eating`);
        this.energy += amount
    }

    sleep(length) {
        console.log(`${this.name} is sleeping`);
        this.energy += length
    }

    play(length) {
        console.log(`${this.name} is playing`);
        this.energy += length
    }
}

class Dog extends Animal{
    constructor(name, energy, breed){
        super(name, energy)
        this.breed = breed;
    }

    bark(){
        console.log('Woof woof')
        this.energy -= .1
    }
}

const leo = new Dog('Leo', 7, "Doberman")
console.log(leo)
leo.sleep()
leo.eat()
leo.play()
leo.bark()
```
