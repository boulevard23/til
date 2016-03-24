# Set JAVA_HOME in Mac

```
export JAVA_HOME=`/usr/libexec/java_home`
```

This `java_home` can return the Java version specified in Java Preferences for the current users.

```
$ /usr/libexec/java_home -V
Matching Java Virtual Machines (1):
    1.8.0_51, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_51.jdk/Contents/Home
```

I have only one installed in my Mac now.