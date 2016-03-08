# TCP Message Termination

2 ways to decide if the whole message is sent.

1. Design one field indicating the payload length.
2. Use some characters to indicate the end. e.g `\n`