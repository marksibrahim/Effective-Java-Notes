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





