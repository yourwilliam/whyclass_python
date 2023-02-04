# \[course04] 03 Advance String

### literator

```java
String str = "asdfghjkl";
for (int i = 0; i < str.length(); i++) {
    char ch = str.charAt(i);
}

// efficient
char[] c = str.toCharArray();
for (char cc : c) {
    print(cc);
}

// inefficiency
for (int i = 0; i < str.length(); i++) {
    String subStr = str.substring(i, i + 1);
}
```

### String concatenation has the same precedence as + and -, and is evaluated left to right.

![](https://ossp.pengjunjie.com/mweb/16384793688185.jpg)

### Every character has a corresponding integer value

* A variable of type char holds exactly one (Unicode) character/symbol.
* The digit characters '0'… '9' have consecutive integer values, as do the letters 'A'… 'Z' and 'a'… 'z'. Java uses this ordering to sort lexigraphically.

Conversions:

![](https://ossp.pengjunjie.com/mweb/16384795984907.jpg)
