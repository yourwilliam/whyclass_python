# [course]04 —— String

## Learn Python3 The Hard Way

### EX6

格式化字符串 Format String

```py
types_of_people = 10 
x = f"There are {types_of_people} types of people."

binary = "binary" 
do_not = "don't" 
y = f"Those who know {binary} and those who {do_not}."

print(x) 
print(y)

print(f"I said: {x}") 
print(f"I also said: '{y}'")

hilarious = False 
joke_evaluation = "Isn't that joke so funny?! {}"

print(joke_evaluation.format(hilarious)) w = "This is the left side of..."

e = "a string with a right side."

print(w + e)
```

### EX7

print方法及其参数

```py
print("Mary had a little lamb.") 
print("Its fleece was white as {}.".format('snow')) 
print("And everywhere that Mary went.") 
print("." * 10) # what'd that do?

end1 = "C" 
end2 = "h" 
end3 = "e" 
end4 = "e" 
end5 = "s" 
end6 = "e" 
end7 = "B" 
end8 = "u" 
end9 = "r" 
end10 = "g" 
end11 = "e" 
end12 = "r"

# watch end = ' ' at the end. try removing it to see what happens 
print(end1 + end2 + end3 + end4 + end5 + end6, end=' ') 
print(end7 + end8 + end9 + end10 + end11 + end12)
```

### EX8 

format string变量
```py
formatter = "{} {} {} {}"

print(formatter.format(1, 2, 3, 4)) 
print(formatter.format("one", "two", "three", "four")) print(formatter.format(True, False, False, True)) print(formatter.format(formatter, formatter, formatter, formatter)) print(formatter.format(
    "Try your",
    "Own text here",
    "Maybe a poem",
    "Or a song about fear" ))
```

### EX9

Escape sequence  转义字符串
```py
# Here's some new strange stuff, remember type it exactly.

days = "Mon Tue Wed Thu Fri Sat Sun" 
months = "Jan\nFeb\nMar\nApr\nMay\nJun\nJul\nAug"

print("Here are the days: ", days) 
print("Here are the months: ", months)

print(""" 
There's something going on here.
With the three double-quotes.
We'll be able to type as much as we like. 
Even 4 lines if we want, or 5, or 6.
""")
```

![](http://ossp.pengjunjie.com/mweb/15727647097999.jpg)


## **String Literals** 

### **1. 四种类型的字符串**

```py
# Quotes enclose characters to tell Python "this is a string!"
# single-quoted or double-quoted strings are the most common
print('single-quotes')
print("double-quotes")

# triple-quoted strings are less common (though see next section for a typical use)
print('''triple single-quotes''')
print("""triple double-quotes""")

# The reason we have multiple kinds of quotes is partly so we can have strings like:
print('The professor said "No laptops in class!" I miss my laptop.')
```

```py
# See what happens if we only use one kind of quote.
# It causes a syntax error! We don't even know how to color this.
print("The professor said "No laptops in class!" I miss my laptop.")
```

### **2. 换行的几种方式**

1. `\n` 转义字符  
2. 多行字符串 `"""` 或 `'''`

```py
# A character preceded by a backslash, like \n, is an 'escape sequence'.
# Even though it looks like two characters, Python treats it as one special character.

# Note that these two print statements do the same thing!
print("abc\ndef")  # \n is a single newline character.
print("""abc
def""")

print("""\
You can use a backslash at the end of a line in a string to exclude
the newline after it. This should almost never be used, but one good
use of it is in this example, at the start of a multi-line string, so
the whole string can be entered with the same indentation (none, that is).
""")
```

### **3. More Escape Sequences**

```
print("Double-quote: \"")
print("Backslash: \\")
print("Newline (in brackets): [\n]")
print("Tab (in brackets): [\t]")

print("These items are tab-delimited, 3-per-line:")
print("abc\tdef\tg\nhi\tj\\\tk\n---")
```

### **4. An escape sequence produces a single character:**

```
s = "a\\b\"c\td"
print("s =", s)
print("len(s) =", len(s))
```

### **5. repr() 和 print() 方法**    

```py
print("These look the same when we print them!")
s1="abc\tdef"
s2="abc  def"

print("print s1: ",s1)
print("print s2: ",s2)

print("\nThey aren't really though...")
print("s1==s2?", s1==s2)

print("\nLet's try repr instead")
print("repr s1: ",repr(s1))
print("repr s2: ",repr(s2))

print("\nHere's a sneaky one")
s1="abcdef"
s2="abcdef             \t"

print("print s1: ",s1)
print("print s2: ",s2)

print("s1==s2?", s1==s2)

print("repr s1: ",repr(s1))
print("repr s2: ",repr(s2))
print("repr() lets you see the spaces^^^")
```

### **6. 多行注释**

```py
"""
Python does not have multiline comments, but you can do something similar
by using a top-level multiline string, such as this. Technically, this is
not a comment, and Python will evaluate this string, but then ignore it
and garbage collect it!
"""
print("wow!")
```

## **2. String常量** 

```py
import string
print(string.ascii_letters)   # abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.ascii_lowercase) # abcdefghijklmnopqrstuvwxyz
print("-----------")
print(string.ascii_uppercase) # ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)          # 0123456789
print("-----------")
print(string.punctuation)     # '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
print(string.printable)       # digits + letters + punctuation + whitespace
print("-----------")
print(string.whitespace)      # space + tab + linefeed + return + ...
```

## **3. String 操作符**


### **1. String 的 加号 和 乘号**

```py
print("abc" + "def")  # What do you think this should do?
print("abc" * 3)  # How many characters do you think this prints?
print("abc" + 3)  # ...will this give us an error? (Yes)
```

### **2. in 操作符**

String的in操作符： in操作符用于查找是否存在子字符串
```py
# The "in" operator is really really useful!
print("ring" in "strings")
print("wow" in "amazing!")
print("Yes" in "yes!")
print("" in "No way!")
```

### **3. String indexing and slicing**

#### **1. Indexing a single character**

```py
# Indexing lets us find a character at a specific location (the index)
s = "abcdefgh"
print(s)
print(s[0])
print(s[1])
print(s[2])

print("-----------")
print("Length of ",s,"is",len(s))

print("-----------")
print(s[len(s)-1])
print(s[len(s)])  # crashes (string index out of range)
```

#### **2. Negative indexes**

```py
s = "abcdefgh"
print(s)
print(s[-1])
print(s[-2])
```

#### **3. string 切片**

```py
# Slicing is like indexing, but it lets us get more than 1 character.
# ...how is this like range(a,b)?

s = "abcdefgh"
print(s)
print(s[0:3])
print(s[1:3])
print("-----------")
print(s[2:3])
print(s[3:3])
```

             
#### **4. 切片的默认参数**

```py
s = "abcdefgh"
print(s)
print(s[3:])
print(s[:3])
print(s[:])
```
       
#### **5. 切片的步长参数 step**

```py
print("This is not as common, but perfectly ok.")
s = "abcdefgh"
print(s)
print(s[1:7:2])
print(s[1:7:3])
```

#### **6. 字符串反转**

使用切片进行字符串反转

```py
s = "abcdefgh"

print("This works, but is confusing:")
print(s[::-1])

print("This also works, but is still confusing:")
print("".join(reversed(s)))

print("Best way: write your own reverseString() function:")

def reverseString(s):
    return s[::-1]

print(reverseString(s)) # crystal clear!
```


## **4. Looping over Strings** 

### **1. "for" 循环索引字符串**

```py
s = "abcd"
for i in range(len(s)):
    print(i, s[i])
```

### **2. "for" loop without indexes**

```py
s = "abcd"
for c in s:
    print(c)
```

### **3. "for" loop with split**

```py
# By itself, names.split(",") produces something called a list.
# Until we learn about lists (soon!), do not store the result of
# split() and do not index into that result.  Just loop over the
# result, as shown here:

names = "fred,wilma,betty,barney"
for name in names.split(","):
    print(name)
```

### **4. "for" loop with splitlines**

    
```py
# splitlines() also makes a list, so only loop over its results,
# just like split():

# quotes from brainyquote.com
quotes = """\
Dijkstra: Simplicity is prerequisite for reliability.
Knuth: If you optimize everything, you will always be unhappy.
Dijkstra: Perfecting oneself is as much unlearning as it is learning.
Knuth: Beware of bugs in the above code; I have only proved it correct, not tried it.
Dijkstra: Computer science is no more about computers than astronomy is about telescopes.
"""
for line in quotes.splitlines():
    if (line.startswith("Knuth")):
        print(line)
```

## **5. Example: isPalindrome**

A string is a **palindrome** if it is exactly the same forwards and backwards.

    

```py
# There are many ways to write isPalindrome(s)
# Here are several.  Which way is best?

def reverseString(s):
    return s[::-1]

def isPalindrome1(s):
    return (s == reverseString(s))

def isPalindrome2(s):
    for i in range(len(s)):
        if (s[i] != s[len(s)-1-i]):
            return False
    return True

def isPalindrome3(s):
    for i in range(len(s)):
        if (s[i] != s[-1-i]):
            return False
    return True

def isPalindrome4(s):
    while (len(s) > 1):
        if (s[0] != s[-1]):
            return False
        s = s[1:-1]
    return True

print(isPalindrome1("abcba"), isPalindrome1("abca"))
print(isPalindrome2("abcba"), isPalindrome2("abca"))
print(isPalindrome3("abcba"), isPalindrome3("abca"))
print(isPalindrome4("abcba"), isPalindrome4("abca"))
```

## **6. Strings are 

### **1. 字符串是不可以修改的，不要修改字符串**

```py
s = "abcde"
s[2] = "z"  # Error! Cannot assign into s[i]
```

### **2. 要修改字符串应该重新创建一个字符串**

```py
s = "abcde"
s = s[:2] + "z" + s[3:]
print(s)
```

## **7. 字符串的默认方法** 

### **1. str() and len()**

```py
name = input("Enter your name: ")
print("Hi, " + name + ". Your name has " + str(len(name)) + " letters!")
```

### **2. chr() and ord()**

```py
print(ord("A")) # 65
print(chr(65))  # "A"
print(chr(ord("A")+1)) # ?
```

### **3. eval()**

```py
# eval() works but you should not use it!
s = "(3**2 + 4**2)**0.5"
print(eval(s))

# why not? Well...
s = "reformatMyHardDrive()"
print(eval(s)) # no such function!  But what if there was?
```

## **8. String方法** 

Methods are a special type of function that we call "on" a value, like a string. You can tell it's a method because the syntax is in the form of value.function(), like s.islower() in the code below.
    
### **1. Character types: isalnum(), isalpha(), isdigit(), islower(), isspace(), isupper()**


```py
# Run this code to see a table of isX() behaviors
def p(test):
    print("True     " if test else "False    ", end="")
def printRow(s):
    print(" " + s + "  ", end="")
    p(s.isalnum())
    p(s.isalpha())
    p(s.isdigit())
    p(s.islower())
    p(s.isspace())
    p(s.isupper())
    print()
def printTable():
    print("  s   isalnum  isalpha  isdigit  islower  isspace  isupper")
    for s in "ABCD,ABcd,abcd,ab12,1234,    ,AB?!".split(","):
        printRow(s)
printTable()
```

### **2. String edits: lower(), upper(), replace(), strip()**

```py
print("This is nice. Yes!".lower())
print("So is this? Sure!!".upper())
print("   Strip removes leading and trailing whitespace only    ".strip())
print("This is nice.  Really nice.".replace("nice", "sweet"))
print("This is nice.  Really nice.".replace("nice", "sweet", 1)) # count = 1

print("----------------")
s = "This is so so fun!"
t = s.replace("so ", "")
print(t)
print(s) # note that s is unmodified (strings are immutable!)
```

### **3. Substring search: count(), startswith(), endswith(), find(), index()**

```py
print("This is a history test".count("is")) # 3
print("This IS a history test".count("is")) # 2
print("-------")
print("Dogs and cats!".startswith("Do"))    # True
print("Dogs and cats!".startswith("Don't")) # False
print("-------")
print("Dogs and cats!".endswith("!"))       # True
print("Dogs and cats!".endswith("rats!"))   # False
print("-------")
print("Dogs and cats!".find("and"))         # 5
print("Dogs and cats!".find("or"))          # -1
print("-------")
print("Dogs and cats!".index("and"))        # 5
print("Dogs and cats!".index("or"))         # crash!
```

## **9. String Formatting**  
   
### **1. format a string with %s**

```py
breed = "beagle"
print("Did you see a %s?" % breed)
```

### **2. format an integer with %d**

```py
dogs = 42
print("There are %d dogs." % dogs)
```

### **3. format a float with %f**

```py
grade = 87.385
print("Your current grade is %f!" % grade)
```

### **4. format a float with %.[precision]f**

You can control how many fractional digits of a float are included in the string by changing the number to the right of the decimal point.

```py
grade = 87.385
print("Your current grade is %0.1f!" % grade)
print("Your current grade is %0.2f!" % grade)
print("Your current grade is %0.3f!" % grade)
print("Your current grade is %0.4f!" % grade)
```

### **5. format multiple values**

```py
dogs = 42
cats = 18
exclamation = "Wow"
print("There are %d dogs and %d cats. %s!!!" % (dogs, cats, exclamation))
```

### **6. format right-aligned with %[minWidth]**


```py
dogs = 42
cats = 3
print("%10s %10s" % ("dogs", "cats"))
print("%10d %10d" % (dogs, cats))
```

### **7. format left-aligned with %-[minWidth]**

```py
dogs = 42
cats = 3
print("%-10s %-10s" % ("dogs", "cats"))
print("%-10d %-10d" % (dogs, cats))
```

### **8. String Formatting with f Strings**    

```py
# We saw this example back in week1!
# It shows a nice relatively new way to format strings:

x = 42
y = 99
# Place variable names in {squiggly braces} to print their values, like so:
print(f'Did you know that {x} + {y} is {x+y}?')
```

## **10. Basic File IO**  

文件操作

```py
# Note: As this requires read-write access to your hard drive,
#       this will not run in the browser in Brython.

def readFile(path):
    with open(path, "rt") as f:
        return f.read()

def writeFile(path, contents):
    with open(path, "wt") as f:
        f.write(contents)

contentsToWrite = "This is a test!\nIt is only a test!"
writeFile("foo.txt", contentsToWrite)

contentsRead = readFile("foo.txt")
assert(contentsRead == contentsToWrite)

print("Open the file foo.txt and verify its contents.")
```

    