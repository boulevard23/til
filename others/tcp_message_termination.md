# TCP Message Framing

TCP does not operate on packets of data, it operates on streams of data. In real world, you must design a **message framing** protocol that will wrap the messages sent back and forth.

There are 2 common ways to design a **message framing**.

### Length prefixing

To send a message, a length info prepends the message. 4-bytes signed little-endian is a common choice.

To recieve, you first allocates a buffer, e.g 4-bytes, to receive the length info. Once you get that info, allocates another buffer based on the length. When the second buffer is full, you know that you've already received the whole message.

### Delimiters

Use some characters to indicate the end. e.g `\n`

This is hard to get it right. When sending, any delimiter characters in the data must be replaced, usually with an escaping function. The receiving code cannot predict the message size, so it must append all received data onto the end of the buffer, growing the buffer as necessary.