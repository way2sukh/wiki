#Effective Java 3rd edition 
- ##Creating and Destroying Objects :
  - Item 1: Consider static factory methods instead of constructors
    A class can provide a public static factory method, which is simply a static method that returns an instance of the class.
	```
	public static Boolean valueOf(boolean b) {
        return b ? Boolean.TRUE : Boolean.FALSE;
    }
	```
	####Advantages : 
	- Unlike constructors, they have names.
	- Unlike constructors, they are not required to create a new object each time they’re invoked. This allows immutable classes to use preconstructed instances, or to cache instances as they’re constructed, and dispense them repeatedly to avoid creating unnecessary duplicate objects.
	- Unlike constructors, they can return an object of any subtype of their return type. One application of this flexibility is that an API can return objects without making their classes public. Hiding implementation classes in this fashion leads to a very compact API.
	- Class of the returned object can vary from call to call as a function of the input parameters.
	- Class of the returned object need not exist when the class containing the method is written. Such flexible static factory methods form the basis of service provider frameworks, like the Java Database Connectivity API (JDBC).
	    There are three essential components in a service provider framework: a service interface, which represents an implementation; a provider registration API, which providers use to register implementations; and a service access API, which clients use to obtain instances of the service. The service access API may allow clients to specify criteria for choosing an implementation. In the absence of such criteria, the API returns an instance of a default implementation, or allows the client to cycle through all available implementations. The service access API is the flexible static factory that forms the basis of the service provider framework.
	  
	####Disadvantages :
	- By providing only static factory methods is that classes without public or protected constructors cannot be subclassed.
	    For example, it is impossible to subclass any of the convenience implementation classes in the Collections Framework. Arguably this can be a blessing in disguise because it encourages programmers to use composition instead of inheritance, and is required for immutable types.
	- Static factory methods are hard for programmers to find