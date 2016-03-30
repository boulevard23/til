# Getters and Setters

Why using getters and setters instead of simply using `public` fields?

* Easy to change the behavior without change every place that using the `public` fields in the codebase.
	* Perform validation.
	* Change the value you want to set.
	* Hide the internel representation. `getAddress` could actually grab serveral things and combine them for you.
	* Lazy loading.
* Easy to mock, serialize, or do reflection.
* Allow different access level. `get` could be `public`, but the `set` are `protected`.

*Note: You can set the fields to be public if the class is immutable, like `case class` in scala*