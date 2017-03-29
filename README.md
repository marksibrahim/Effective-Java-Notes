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



