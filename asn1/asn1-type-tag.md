# `ASN.1`常用类型标签`Type/Tag`

## TT=`0x00`

- 特殊用途（`EoC`作为内容结束标志）
- T（00）L（00）V（无）

## TT=`0x01`

- BOOLEAN（布尔值）
- T（01）L（01）V（00）-- `FALSE` [0]
- T（01）L（01）V（01 - FF） -- `TRUE` [!0]

## TT=`0x02`

- Integer（整型）
- 内容前9比特不能全为1或全为0，即不能1111 1111 1xxx xxxx，也不能0000 0000 0xxx xxxx

## TT=`0x03`

- BIT String（比特流）
- 分组传输需要也可进行结构化编码`23`
- 内容首字节（00~07）指示比特数需填充多少位成为8的倍数，一般末尾填充0补齐

```text
bitString BITString ::= {"0110 1110 0101 1101 11"b}

T（03）L（04）V（06 6e 5d c0）
```

## TT=`0x04`

- OCTET String（字节流）
- 分组传输需要也可进行结构化编码`24`

## TT=`0x05`

- NULL（空）
- T（05）L（00）V（无）

## TT=`0x06`

- Object Identifier（对象标识）

## TT=`0x09`

- Real（实数）

### 实数零（0）

- T（09）L（00）V（无）

### 实数非零（!0）

内容首字节前两位b[7-6]含义如下：

- `00`表示采用十进制编码
- `01`表示两个特殊值`01 000000`正无穷（PLUS-INFINITY）和`01 000001`负无穷（MINUS-INFINITY）
- `10`表示采用二进制编码正实数
- `11`表示采用二进制编码负实数

内容首字节前两位b[7-6]取值`1x`时，次两位b[5-4]含义如下：

- `00` 基数为2
- `01` 基数为8
- `10` 基数为16
- `11` 保留

## TT=`0x0A`

- Enumerated（枚举）
- 内容应该为枚举值对应的整数值的编码

## TT=`0x0C`

- UTF8 String（UTF8编码字符）

## TT=`0x0D`

- Relative-OID（标准对象标识）

## TT=`0x12`

- NumericString（数字字符0-9）

## TT=`0x13`

- PrintableString（可打印字符）

## TT=`0x14`

- PrintableString（可打印字符）

## TT=`0x15`

- VideotexString

## TT=`0x16`

- IA5String（ASCII码任意字符串）

## TT=`0x17`

- UTC Time

## TT=`0x19`

- GraphicString

## TT=`0x1A`

- VisibleString、ISO646String

## TT=`0x1B`

- GeneralString

## TT=`0x1C`

- UniversalString

## TT=`0x1E`

- BMPString

## TT=`0x30`

- Sequence（有序）
- SEQUENCE OF（单一序列）
- 元素除带OPTIONAL或DEFAULT（可选但非必要）外，需按顺序进行编码

## TT=`0x31`

- Set（无序）
- SET OF（单一集合）
- 元素除带OPTIONAL或DEFAULT（可选但非必要）外，按选定顺序进行编码，即无顺序限制

## TT=`xxH`

- CHOICE（可选项）
- 编码值应与被选择类型一致
