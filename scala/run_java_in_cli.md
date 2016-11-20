# Run Java in CLI

* Syntax: 
	
	```java
	java [<option>] <fully-qualified-class=name> [<argument>]
	```
	
	Example
	
	```java
	java -Xmx100m com.acme.example.Hello Eric`
	```
	
	Several things to notice:
	* Use `javac` to generate the `.class` file first.
	* Class name doesn't end with `.class`
	* Class name must be fully qualified.

* Java finds class in this order:
	* Bootstrap classes: default in `jre/lib`, mostly in `rt.jar`
	* Extension classes: default in `jre\lib\ext`
	* User classes: default in `.` You can set the env `CLASSPATH`, but that is not flexible, so it's better to use `-classpath/-cp` option.

