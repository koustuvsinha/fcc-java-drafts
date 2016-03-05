# Java Basics

## Core Concepts

### The Java Virtual Machine (JVM) 

Java belongs to a family of languages called **Compiled Languages** (https://en.wikipedia.org/wiki/Compiled_language). Any code written in such a language needs to be converted (compiled) to an intermediate form that can then be understood by the host platform (the OS/platform in which the code runs). For Java, this intermediate form is called **Bytecode** which is then interpreted by a runtime called a Java Virtual Machine (JVM). Think of JVM (https://docs.oracle.com/javase/specs/jvms/se7/html/) as a piece of software that does the hard work of running your Java code. It takes care of memory allocation, thread management, garbage collection and so much more. Apart from Java, it also supports (read: able to run) code written in languages such as Groovy, Scala etc.

In Java, code is written and saved as `.java` files. The files are then run through a compiler (javac) to convert them to Bytecode `.class` files. Standalone Java programs are then run using the `java` command. More about this later. 

The following sections describe some of the basic building blocks of coding in Java.

### Variables

Variables store values. 

In [Java](https://github.com/FreeCodeCamp/FreeCodeCamp/wiki/Java), variables are [_strongly typed_](https://en.wikipedia.org/wiki/Strong_and_weak_typing#Definitions_of_.22strong.22_or_.22weak.22), which means you have to define the type for each variable whenever you declare it. Otherwise, the compiler will throw error at [compile time](https://en.wikipedia.org/wiki/Compile_time). Therefore, each variable has an associate data type of either :

* Primitive Type : `int`, `short`, `char`, `long`, `boolean`, `byte`, `float`, `double`
* Wrapper Type : `Integer`, `Short`, `Char`, `Long`, `Boolean`, `Byte`, `Float`, `Double`
* Object Type: `String`, `StringBuilder`, `Calendar`, `ArrayList` etc.

We made a distinction between **Wrapper Type** and general **Object Type** for a reason - wrapper types are closely linked with their primitive counterparts via [autoboxing and unboxing](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html).

Typically you can declare variables using the following syntax :

```java
//Primitive Data Type

int i = 10;

// Object Data Type
//initiates an Float object with value 1.0
// variable myFloat now points to the object
Float myFloat = new Float(1.0);
```

But there are more to these variables, [read about them here](#TODO).

### Classes & Objects

Classes are groups of variables and operations on them. A class can have variables, methods (or functions) and constructors (or methods which are used to initiate, more on that later!).

Think of a `Class` as a blueprint for creating something concrete. A `Class` tells you the 'what' and 'how' an `object` of that Class will look like once `instantiated`. In essence, it defines `properties` (say color, engine capacity) and `behavior` (stop, speed up, change gears, honk etc.) for a Car. 

Objects are _instances_ of a class. All objects are instances of a certain class. Imagine a class being a "template", which every Object copies to. When you create an Object, basically it creates a new object on the blueprint of a class. Now lets look at this from a little piece of code :

```java
// Car class
public class Car {
  // car name
  private String name;
	// car mannufacturer name
	private String manufacturerName;
  // Constructor
	public Car(String name, String man) {
		this.name = name;
		this.manufacturerName = man;
	}
  // Getter method
	public String getName() {
		return name;
	}
  // Getter method
	public String getManufacturerName() {
		return manufacturerName;
	}
}

Car modelS = new Car("Model S","Tesla");

System.out.println("Full Car Name = " + modelS.getManufacturerName() + " " + modelS.getName());
// prints Tesla Model S
```

So, `Car` is a Class, which has the fields or properties name and manufacturerName. `modelS` is an object of `Car` Class. So `modelS` also has the same properties and methods.

### Access Modifiers

Ok, so if `modelS` has all the same properties, I should be able to access `name` or `manufacturerName` right?

```java
System.out.println(modelS.name);
```
Results in :

```asciidoc
Main.java:13: error: name has private access in Car
		System.out.println(modelS.name);
		                         ^
1 error
```

Why? Notice we had mentioned `private` before the variable `name` in class `Car`. So since its private, we cant touch it from outside!

There are other kinds of access Modifiers like public, protected, default etc. [Read more about them here](#TODO).

### Constructors

What's the point then? I should be able to store data in it right?

Thats when we use either Getter / Setter methods or in this case Constructors to initialize a class. Basically every Java Class has a constructor, which is the method which is called first when any object of the class is initialized. Think of it as a bit of starter code.

When you write a Class without any constructor, then Java assumes it has a default constructor :

```java

public class Car {
	private String name;
}

Car modelS = new Car();
```

This initializing with no parameters is a way of calling the default constructor. You can also have a default constructor written yourself this way :

```java
public class Car {
	private String name;

	public Car() {
		name = "Tesla";
	}
}
```

Then, when calling `new Car()`, the variable `name` will get auto-initialized to `"Tesla"`.

Like what Constructors can do? [Dive into it more here](#TODO).

### Methods

`getName()` and `getManufacturerName()` are two "Getter" methods we have used here. Notice unlike JavaScript, we **have** to define the return type of any method we write, otherwise it will fail compile time. If you do not want a method to return anything, use `void` return type.

```java
public class Car {
	private String name;

	public void changeName() {
		name = "Tesla";
	}
}
```
As with any other language, methods (or functions, if you are here from JS world) are used often for their modularity and reusability. [Read more about them here](#TODO).

## Inheritance

So great you have successfully created a Car class. But, wait, isnt Tesla cars are supposed to be Electric variants? I want a Electric car class, but it also should have the properties of the original `Car` class.

Solution : Inheritance. Java provides a neat way to "inherit" parent properties :

```java
public class Car {
	private String name;
	private String manufacturerName;

	public Car(String name, String man) {
		this.name = name;
		this.manufacturerName = man;
	}
  // Getter method
	public String getName() {
		return name;
	}
  // Getter method
	public String getManufacturerName() {
		return manufacturerName;
	}
}

public class ElectricCar extends Car {
	public ElectricCar(String name, String man) {
		super(name, man);
  }

	public void charge() {
	 System.out.println("Charging ...");
	}
}

ElectricCar modelS = new ElectricCar("Model S","Tesla");
// prints Tesla
System.out.println(modelS.getName());
// prints Charging ...
modelS.charge();
```

See here that the class `ElecticCar` inherits or `extends` the public methods from `Car` class, as well as has its own methods and properties. Cool way to pass on information!

Also notice the usage of [super]() keyword here. Since our `Car` class had a constructor, so we have to initialize that constructor from the child class as well. We do that using the `super` keyword. Read more about [Inheritance here](#TODO).

### Interfaces

But wait, my manager has given me a set of strict specifications every class to create, but has told me you can implement it in whichever way you want. Incidentally, Java has a nifty feature of Interfaces which does exactly that!

```java
interface Car {
	public String getName();
	public String getManufacturerName();
}

class ElectricCar implements Car {
	private String name;
	private String manufacturerName;

	public ElectricCar(String name, String man) {
	  this.name = name;
	  this.manufacturerName = man;
    }

	public void charge() {
	 System.out.println("Charging ...");
	}

	// Getter method
	public String getName() {
		return name;
	}
  	// Getter method
	public String getManufacturerName() {
		return manufacturerName;
	}
}
```

So interface basically bounds you to a contract to follow, where you must _implement_ all the methods. If you don't, the compiler will complain! Know more about the [awesome power of Inheritance here](#TODO).

## Basic Operations

## Control Flow
