# Rijndael 256

AES is actuall a subset of the family of block ciphers: Rijindael.

PHP uses `MCRYPT_RIJNDAEL_128` to designate Rijndael with 128-bit keys and 128-bit blocks, this is the same as AES-128. But `MCRYPT_REINDAEL_256` is 256-bit key and 256-bit blocks, this is not one of the AES variants.

There is no support in any of the Sun JCE providers for anything other than Rijndael with the 128-bit block size. The [BouncyCastle](http://www.bouncycastle.org/java.html) library works though.