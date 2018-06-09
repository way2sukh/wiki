## Generics
- ### Item 26: Don’t use raw types
	<p>Difference between the raw type List and the parameterized type List<Object>? <br />
	You lose type safety if you use a raw type such as List, but not if you use a parameterized type such as List<Object>. While you can pass a List<String> to a parameter of type List, you can’t pass it to a parameter of type List<Object>.
	</p>
	<p>
	What is the difference between the unbounded wildcard type Set<?> and the raw type Set? <br />
	You can’t put any element (other than null) into a Collection<?>. Attempting to do so will generate a compile-time error message like this.
	</p>
- ### Item 27: Eliminate unchecked warnings
	If you can’t eliminate a warning, but you can prove that the code that provoked the warning is typesafe, then (and only then) suppress the warning with an @SuppressWarnings("unchecked") annotation. Always use the SuppressWarnings annotation on the smallest scope possible. Every time you use a @SuppressWarnings("unchecked") annotation, add a comment saying why it is safe to do so.
- ### Item 28: Prefer lists to arrays
	Arrays differ from generic types in two important ways. First, arrays are covariant. This scary-sounding word means simply that if Sub is a subtype of Super, then the array type Sub[] is a subtype of the array type Super[]. Generics, by contrast, are invariant: for any two distinct types Type1 and Type2, List<Type1> is neither a subtype nor a supertype of List<Type2>. You might think this means that generics are deficient, but arguably it is arrays that are deficient. <br />
	The second major difference between arrays and generics is that arrays are reified. This means that arrays know and enforce their element type at runtime. If you try to put a String into an array of Long, you’ll get an ArrayStoreException. Generics, by contrast, are implemented by erasure. This means that they enforce their type constraints only at compile time and discard (or erase) their element type information at runtime. Erasure is what allowed generic types to interoperate freely with legacy code that didn’t use generics, ensuring a smooth transition to generics in Java 5.
- ### Item 29: Favor generic types
	Generic types are safer and easier to use than types that require casts in client code. When you design new types, make sure that they can be used without such casts. 
- ### Item 30: Favor generic methods
	Generic methods, like generic types, are safer and easier to use than methods requiring their clients to put explicit casts on input parameters and return values. 
- ### Item 31: Use bounded wildcards to increase API flexibility
	For maximum flexibility, use wildcard types on input parameters that represent producers or consumers. If an input parameter is both a producer and a consumer, then wildcard types will do you no good: you need an exact type match, which is what you get without any wildcards. <br />
	Here is a mnemonic to help you remember which wildcard type to use: <br />
	**PECS stands for producer-`extends`, consumer-`super`** <br />
	*Do not use bounded wildcard types as return types*
- ### Item 32: Combine generics and varargs judiciously
	Varargs and generics do not interact well because the varargs facility is a leaky abstraction built atop arrays, and arrays have different type rules from generics. Though generic varargs parameters are not typesafe, they are legal. If you choose to write a method with a generic (or parameterized) varargs parameter, first ensure that the method is typesafe, and then annotate it with `@SafeVarargs` so it is not unpleasant to use.
- ### Item 33: Consider typesafe heterogeneous containers
	The normal use of generics restricts you to a fixed number of type parameters per container. You can get around this restriction by placing the type parameter on the key rather than the container. You can use `Class` objects as keys for such typesafe heterogeneous containers. A `Class` object used in this fashion is called a type token. You can also use a custom key type. 