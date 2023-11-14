## definition

Monads are a [[design pattern]] permitting the [[abstraction]] of a series of functions on a particular object. They work by wrapping the object in a helper class that can call another function on itself, and can potentially contain other pieces of information (logs, for instance).

Using monads, it can be a lot easier to check for potential exceptions in a declarative way, rather than imperative.

## examples

Consider the following script performing chain actions on an object :

```c#
myPerson.getBestFriend().gender.equals("male");
```

At any point, these values could be invalid or `null`. So, in order to write maintainable code, we would write :

```c#
if(myPerson != null) 
{
	if(myPerson.getBestFriend() != null)
	{
		if(myPerson.getBestFriend(). gender != null)
		{
			return myPerson.getBestFriend().gender.equals("male");
		}
	}
}
```

Or we can do a try/catch.

Monads handle the situation differently. We would firstly need a wrapper object :

```c#
class MyMonad {
	var value;
	constructor(value){
		this.value = value;
	}

	bind = function(func){
		value = func(this.value);
		return MyMonad(value);
	}
}
```

Then, the desired output can be [[composed]] through the chaining of these monads. 

```c#
var isMale = MyMonad(myPerson)
.bind(person => person.getBestFriend())
.bind(person => person.gender)
.bind(gender => gender.equals("male"));
```

Null references and error handling can be done within the wrapper class, and we could potentially include more data than we started with (an array of log strings, for instance).