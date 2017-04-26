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

# Avoid Creating Unnecessary Objects

### Why?

* faster
* less memory
* stylish + more concise

Example: using the string constructor inside of a loop.

An effective way to avoid creation of unnecessary objects is to use the Static Factory Method rather than constructors.

Example: when checking a boolean, rather than creating another boolean, use \`boolean.valueOf\(\)\`

### When this might not be a good idea?

This can be tricky when working with mutable data, where you have to keep track of state. For immutable elements, err on the side of reuse.

# Finalizers

Don't use them.  
Why:

* There is no guarantee whether it will happen and if it does, when it will happen
* Risk 'teardown' type functions not happening
* Leads running out of memory
* Actually increases run time of program

Many GUI memory dumps happen to be from people attempting to use finalizers.

When to use it:

* As a safety net or to terminate noncritical native resources.

# Should you override equals or not when creating classes

Equals is a base method for classes, that you usually don't want to override.

* Classes like thread are intentionally unique, so you wouldn't want to override equals
* If the super class already provides an adequate equals method, why override it?

But if you must...

1. It must be reflexive x.equals\(x\) must be true
2. It must be transitive. A = B and B = C then A = C
3. It must be consistent, the same objects will always be equals.
4. It must be symmetric x.equals\(y\) must return the same as y.equals\(x\)
5. For non null reference value, x.equals\(null\) must return false

# Override HashCodes when you override Equals

HashCodes should obey:

• repeated calls must yield same integer

• it is not required that two different objects has different HashCodes

If you forget to override HashCodes \(when you override equals\), you may run into issues with object matching.

For immutable objects, you can lazily cache your HashCodes, since your object won't change.

# toString\(\) method

in general the return value of toString\(\) is not very helpful, value return is in the format of: \[class name\], \[@\], \[hexdecimal\]

toString is automatically invoked with print or debug statement

always override toString\(\) to make it more useful, using unique characteristics of objects, i.e. for phone class, show phone number as toString return value

# Consider implementing comparable

When you have a class that has natural ordering, consider implementing comparable

* take advantage of things like sort, hashmaps, trees

compareTo\(object\) contract is

* returns an int -1 = less than, 0 = equal, 1 = greater than.
* Must be reflexive, symmetric and transitive

# Consider Overriding Cloneable Judiciously

It does not enforce any specific behavior, but is intended to indicate whether or not you can clone an object. 

Typically, `x.clone()` equals `x` , but this is not enforced. Takeaway, `clone` is messy, avoid it!



