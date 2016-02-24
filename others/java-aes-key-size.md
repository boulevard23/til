# Java AES Key Size

Default security policy for AES support only 16 Byte (128 Bit) key. If you want to support 24 Byte (192 Bit) or 32 Byte (256 Bit) key, you have to download Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files. And put them into `$JAVA_HOME/jre/lib/security/`