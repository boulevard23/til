# Base64

## What
Base64 is a character encoding algorithm. It uses 64 characters to encode any data, that's why it is called Base64. And also, there are Base32, Base16.

## Why
The purpose is to make sure all the characters in the data are legal, which are permitted by the transfer protocol

## How
1. Get the binary code of the original string
2. Calculate the decimal value for every 6 bits (2^6 = 64)
3. Find the corresponding character in Base64 encoding table for this decimal value.

*Note: Base64 will pad 0, and six 0 is converted into `A`. In the standard Base64, `A` in the end is replaced by `=`, this is why sometimes we saw `SGVsbG8hIQ==`*

## Reference
[Base64编码原理与应用](http://blog.xiayf.cn/2016/01/24/base64-encoding/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)