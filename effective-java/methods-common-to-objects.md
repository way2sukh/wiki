## Methods Common to All Objects
Although `Object` is a concrete class, it is designed primarily for extension. All of its nonfinal methods (`equals, hashCode, toString, clone, and finalize`) have explicit general contracts because they are designed to be overridden. It is the responsibility of any class overriding these methods to obey their general contracts; failure to do so will prevent other classes that depend on the contracts (such as HashMap and HashSet) from functioning properly in conjunction with the class.
- ### Item 10: Obey the general contract when overriding equals
	The equals method implements an equivalence relation. It has these properties:
	- *Reflexive*: For any non-null reference value x, x.equals(x) must return true.
	- *Symmetric*: For any non-null reference values x and y, x.equals(y) must return true if and only if y.equals(x) returns true.
	- *Transitive*: For any non-null reference values x, y, z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) must return true.
	- *Consistent*: For any non-null reference values x and y, multiple invocations of x.equals(y) must consistently return true or false.
	- For any non-null reference value x, x.equals(null) must return false.
- ### Item 11: Always override hashCode when you override equals
	- If two objects are equal according to the equals(Object) method, then calling hashCode on the two objects must produce the same integer result.
	- If two objects are unequal according to the equals(Object) method, it is not required that calling hashCode on each of the objects must produce distinct results. However, the programmer should be aware that producing distinct results for unequal objects may improve the performance of hash tables. <br />
	*Tips*
	- *Don't use Objects.hash in performance critical applications as they run more slowly because they entail array creation to pass a variable number of arguments, as well as boxing and unboxing if any of the arguments are of primitive type.*
	- *If a class is immutable and the cost of computing the hash code is significant, you might consider caching the hash code in the object rather than recalculating it each time it is requested.*
- ### Item 12: Always override toString
	Providing a good toString implementation makes your class much more pleasant to use and makes systems using the class easier to debug. 
- ### Item 13: Override clone judiciously
	The Cloneable interface was intended as a mixin interface for classes to advertise that they permit cloning. Unfortunately, it fails to serve this purpose. It's primary flaw is that it lacks a clone method, and Object’s clone method is protected.
- ### Item 14: Consider implementing Comparable
	Whenever you implement a value class that has a sensible ordering, you should have the class implement the Comparable interface so that its instances can be easily sorted, searched, and used in comparison-based collections. When comparing field values in the implementations of the compareTo methods, avoid the use of the < and > operators. Instead, use the static compare methods in the boxed primitive classes or the comparator construction methods in the Comparator interface.
	