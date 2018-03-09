# testClass

 - Why is inheritance important?
 - What is a practical example in which we use inheritance?

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
In order to 

In Javascript each object has a private property which holds a link to another object called its prototype.
When trying to access a property of an object, if the property cannot be found on the object itself, we will look on the prototype of the object, then the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.

Every single object in javascript has a prototype.

So how would you create a blueprint in Javascript?

There are several methods an I will show you 2 of them:

1) One is creating a factory function - a function that creates other objects

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
All instance of Animal will be able to access this function, also when I change the method, it will be automatically applied to all instances.
