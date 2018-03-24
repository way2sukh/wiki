## Creating and Destroying Objects :
- ### Item 1: Consider static factory methods instead of constructors
	A class can provide a public static factory method, which is simply a static method that returns an instance of the class.
	```
	public static Boolean valueOf(boolean b) {
		return b ? Boolean.TRUE : Boolean.FALSE;
	}
	```
	#### Advantages : 
	- Unlike constructors, they have names.
	- Unlike constructors, they are not required to create a new object each time they’re invoked.
	- Unlike constructors, they can return an object of any subtype of their return type. One application of this flexibility is that an API can return objects without making their classes public. Hiding implementation classes in this fashion leads to a very compact API.
	- Class of the returned object need not exist when the class containing the method is written. Such flexible static factory methods form the basis of service provider frameworks, like the Java Database Connectivity API (JDBC). <br />
		There are three essential components in a service provider framework: a service interface, which represents an implementation; a provider registration API, which providers use to register implementations; and a service access API, which clients use to obtain instances of the service. The service access API may allow clients to specify criteria for choosing an implementation. In the absence of such criteria, the API returns an instance of a default implementation, or allows the client to cycle through all available implementations. The service access API is the flexible static factory that forms the basis of the service provider framework.
	  
	#### Disadvantages :
	- By providing only static factory methods is that classes without public or protected constructors cannot be subclassed. <br />
		For example, it is impossible to subclass any of the convenience implementation classes in the Collections Framework. Arguably this can be a blessing in disguise because it encourages programmers to use composition instead of inheritance, and is required for immutable types.
	- Static factory methods are hard for programmers to find.
- ### Item 2: Consider a builder when faced with many constructor parameters
    Static factories and constructors share a limitation: they do not scale well to large numbers of optional parameters. Why not use other avaialble options : 
	- Telescoping constructor pattern works, but it is hard to write client code when there are many parameters, and harder still to read it.
	- JavaBean may be in an inconsistent state partway through its construction.
	- JavaBeans pattern precludes the possibility of making a class immutable.
- ### Item 3: Enforce the singleton property with a private constructor or an enum type
	A single-element enum type is often the best way to implement a singleton as it is more concise, provides the serialization machinery for free, and provides an ironclad guarantee against multiple instantiation, even in the face of sophisticated serialization or reflection attacks. 
- ### Item 4: Enforce noninstantiability with a private constructor
	A class can be made noninstantiable by including a private constructor and throw exception inside constructor (optional) in case the constructor is accidentally invoked from within the class. Attempting to enforce noninstantiability by making a class abstract does not work. The class can be subclassed and the subclass instantiated. Furthermore, it misleads the user into thinking the class was designed for inheritance.
- ### Item 5: Prefer dependency injection to hardwiring resources
	Static utility classes and singletons are inappropriate for classes whose behavior is parameterized by an underlying resource. A simple pattern that satisfies this requirement is to pass the resource into the constructor when creating a new instance. This is one form of dependency injection.
- ### Item 6: Avoid creating unnecessary objects
	It is often appropriate to reuse a single object instead of creating a new functionally equivalent object each time it is needed. Reuse can be both faster and more stylish. An object can always be reused if it is immutable. <br />
	Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
- ### Item 7: Eliminate obsolete object references
	Memory leaks in garbage-collected languages (more properly known as unintentional object retentions) are insidious. If an object reference is unintentionally retained, not only is that object excluded from garbage collection, but so too are any objects referenced by that object, and so on. Even if only a few object references are unintentionally retained, many, many objects may be prevented from being garbage collected, with potentially large effects on performance.
- ### Item 8: Avoid finalizers and cleaners
	Finalizers are unpredictable, often dangerous, and generally unnecessary. Cleaners are less dangerous than finalizers, but still unpredictable, slow, and generally unnecessary.
- ### Item 9: Prefer try-with-resources to try-finally
	To be usable with this construct, a resource must implement the AutoCloseable interface, which consists of a single void-returning close method. 