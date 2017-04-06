This file serves as an introduction to your Knowledge Base, it is displayed on the homepage of your website. Use it to provide more context to your visitors.

## Static Factory Methods over Constructors

Benefits

* can have different names, rather than relying on parameters to specify constructor
* not required to create a new object \(so you can cache instances or track their creation\)
* can guarantee a **singleton** \(a single instance is created\)
* can limit what classes you expose 

Enum class is a good example.

Disadvantages

* can't be subclassed
* Java Doc doesn't distinguish Static Factory Method from any other static method \(unlike constructors\)

# Considering Builder Class over Constructors

Benefits

* When you have a lot of optional parameters
  * Without builder class, you need a constructor for each variant
* Pass all of the required parameters in initially to a builder
  * Call setters for the optional parameters
  * Lastly, build\(\) to get the object
* Setter methods return the builder object, so you can string them together
  * Ex. SomeObject = new SomeObject.Builder\(100, 10\).setX\(2\).setY\(4\).build\(\)

Disadvantages

* Adds code complexity
  ## Enforce the singleton property with a private constructor \(or enum type\)

What's the best way to implement a singleton? There are two common ways to implement a singleton:

1. **Private Constructor** with a public instance as an attribute
2. **Public Constructor** constructor that returns an instance if one has been created

Both of these these patterns raise problems during **serialization. **These patterns also suffer from reflection attacks \(?\).

The best approach is declare your class as an **enum type** to define the **singleton**.

> enum types contains a fixed set of named values

The enum type declaration, with INSTANCE containing an instance of your class functions just like a public constructor version and is compatible with serialization.

**Plain English**: declare you class an an enum type to make sure only a single instance of your class is ever created. 

# Using private constructors over abstract classes

When writing a class that only contain static methods/attributes, a group of methods operating on primitives.

You want to prevent users from creating instances of these classes.

There is temptation to make abstract classes, but those can be subclassed then instantiated.

JVM default gives you a constructor if you don't supply one, so just leaving it out isn't good enough.  
The method is to use a private constructor, that throws an assertion error if anyone ever tried calling it.

