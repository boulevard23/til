# Difference Between Dependency Injection and Service Locator
* Dependency Injection
	
	```java
	public class Foo {
		private Bar bar;
	
		public Foo(Bar bar) {
			this.bar = bar;
		}
	}
	```
	
	DI uses a constructor or setter to inject the dependencies.
	
* Service Locator

	```java
	public class Foo {
		private Bar bar;
		
		public Foo() {
			this.bar = Containe.get<Bar>()
		}
	}
	```
	
For the service locator, the class still ness to create the dependencies. But for the DI example, DI container actually creates the dependencies, the class doesn't know where these dependencies come from.



