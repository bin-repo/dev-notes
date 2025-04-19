# ASN.1 - RSA

## RSA公钥语法

```text
RSAPublicKey ::= SEQUENCE {
    modulus           INTEGER, -- n（模数）
    publicExponent    INTEGER  -- e（公钥指数）
}
```

## RSA私钥语法

```text
RSAPrivateKey ::= SEQUENCE {
    version           Version,
    modulus           INTEGER,  -- n
    publicExponent    INTEGER,  -- e
    privateExponent   INTEGER,  -- d
    prime1            INTEGER,  -- p
    prime2            INTEGER,  -- q
    exponent1         INTEGER,  -- d mod (p-1)
    exponent2         INTEGER,  -- d mod (q-1)
    coefficient       INTEGER,  -- (inverse of q) mod p
    otherPrimeInfos   OtherPrimeInfos OPTIONAL
}
```
