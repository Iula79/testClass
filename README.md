# testClass

 - Why is inheritance important?
 - What is a practical example in which we use inheritance?

## Classical inheritance

We saw how Ruby does inheritance last week:

```
class Animal
  #without the attr_accessor I would not be able to access the variable name using . notation
    attr_accessor :name
    def initialize(name, species)
        @name = name
        @species = species
        @toys = []
    end
    def add_toy(toy)
        @toys.push(toy)
    end
end

class Dog < Animal 
    def barks()
      puts "Woof Woof"
    end
end

fido = Dog.new("Fido", "dog")
```
We see that the class Dog inherits all the properties and behaviors of the class component.
Dog also has it's own properties that are not available in the parent class.
Classical inheritance is intuitive but can also cause issues especially in the case of inheritance from multiple classes. 
See "Diamond Problem"

## How do we achieve the same behaviour in Javascript?

In Javascript each object has a private property which holds a link to another object called its prototype.
When trying to access a property of an object, if the property cannot be found on the object itself, we will look on the prototype of the object, then the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.

![alt text](https://wit-tutors.github.io/modules/edel-full-stack-1/topic-03-js+dom/talk-3-arrays-objs-functions/arrays-objs-functions.png)

Every single object in javascript has a prototype.

So how would you create a blueprint in Javascript?

There are several methods but the most popular is to create a factory function - a function that creates other objects

Consider this:

```
function Animal(name, species){
  this.name = name;
  this.species = species;
  this.toys = [];
  this.add_toy = function(toy){
    toys.push(toy)
  }
 ```
 this is a factory function in the sense that I can use it to create and instance of an object:
 
 ```
 let fido = new Animal('Fido', 'Dog')
}

//fido is an object with 3 properties and a method
//I can add properties just to fido:

fido.bark = function(){
  console.log('Woof Woof')
}
fido.bark() //Woof Woof
```
Now let say I want to change animal and all the instances that inherit from it. 
In classical inheritance I would just add a new method to the class, but with prototype I can add methods like this:

```
Animal.prototype.jump =function(){
  console.log(this.name + " is jumping!")
}
```
All instance of Animal will be able to access this function. When I change the method, it will be automatically applied to all instances.

What if I want to reuse the Dog code?

```

let Dog = function(){
  this.bark =function(){
    console.log('Woof Woof!')
  }
}

Dog.prototype = new Animal();
let fidor = new Dog()
fidor.bark()
```
the problem here is that I am not copying over the pro
```
let Cat = function(name){
  //in prototypal inheritance you can hand pick which properties to copy and which properties to omit from different prototypes
  //here we are reusing the properties of Animal
  Animal.call(this, name, "Cat")
}
Cat.prototype = new Animal();
let matisser = new Cat('Matisse')

Cat.prototype.meow = function(){
    console.log('Meeeow!')
  }
 
matisser.meow()
// matisser.bark()
matisser.jump()
```

## Object.Create()

Another option to create inheritance is to use let obj = Object.Create(otherobject).
obj.prototype will be assigned otherobject 

