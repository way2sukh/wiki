## Classes and Interfaces
- ### Item 15: Minimize the accessibility of classes and members
	The rule of thumb is simple: make each class or member as inaccessible as possible.
- ### Item 16: In public classes, use accessor methods, not public fields
	If a class is accessible outside its package, provide accessor methods to preserve the flexibility to change the class’s internal representation. If a public class exposes its data fields, all hope of changing its representation is lost because client code can be distributed far and wide. <br /> 
	However, if a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields—assuming they do an adequate job of describing the abstraction provided by the class.
- ### Item 17: Minimize mutability
	To make a class immutable, follow these five rules:
	1. Don’t provide methods that modify the object’s state (known as mutators).
	2. Ensure that the class can’t be extended. 
	3. Make all fields final. 
	4. Make all fields private.
	5. Ensure exclusive access to any mutable components. <br />
	**Benefits :** 
	- Immutable objects are inherently thread-safe; they require no synchronization.
	- Immutable objects can be shared freely.
	- Not only can you share immutable objects, but they can share their internals.
	- Immutable objects make great building blocks for other objects.
	- Immutable objects provide failure atomicity for free. <br />
	*The major disadvantage of immutable classes is that they require a separate object for each distinct value.*
- ### Item 18: Favor composition over inheritance
	