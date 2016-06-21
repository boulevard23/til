# Multi-threads In Htop
When you have a JVM instance, use `htop` you will actually see a bunch of JVM instances, each using the same amount of memory.

This is because `htop` by default shows each thread as a separate process.

