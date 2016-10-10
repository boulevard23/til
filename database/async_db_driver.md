# What the hell is Async JDBC

* If you are using the original JDBC, which is sync, you can move the blocking db calls to a thread, avoid blocking the main thread. But at some point, somewhere, there's going to be a thread blocking waiting for response.
	
	*Question: So I totally agree with this, the problem is then I don't see what is async JDBC. Seems like the best you can do is to put the db calls into another thread. That can be simply done by wrapping the calls into a Future. No need to create async JDBC?*

