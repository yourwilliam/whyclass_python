# [course]05 dictionary

## 1. **Quick Example**

```py
# A dictionary is a data structure that maps keys to values in the same way
# that a list maps indexes to values. However, keys can be any immutable value!

stateMap = { 'pittsburgh':'PA', 'chicago':'IL', 'seattle':'WA', 'boston':'MA' }
city = input("Enter a city name --> ").lower()
if (city in stateMap):
    print(city.title(), "is in", stateMap[city])
else:
    print("Sorry, never heard of it.")
```

**Another Example:**

```py
counts = dict()
while True:
    n = int(input("Enter an integer (0 to end) --> "))
    if (n == 0): break
    if (n in counts):
        counts[n] += 1
    else:
        counts[n] = 1
    print("I have seen", n, "a total of", counts[n], "time(s)")
print("Done, counts:", counts)
```

## 2. **Creating Dictionaries** 
    
### 1. **Create an empty dictionary**

```py
d = dict()
print(d)    # prints {}

# We can also use empty braces
d = { }
print(d)    # prints {}
```

### 2. **Create a dictionary from a list of (key, value) pairs**

```py
pairs = [("cow", 5), ("dog", 98), ("cat", 1)]
d = dict(pairs)
print(d)    # unpredictable order!
```

### 3. **Statically-allocate a dictionary**

```py
d = { "cow":5, "dog":98, "cat":1 }
print(d)    # ditto!
```

## 3. **Using Dictionaries**

```py
# We can interact with dictionaries in a similar way to lists/sets
d = { "a" : 1, "b" : 2, "c" : 3 }

print(len(d)) # prints 3, the number of key-value pairs

print("a" in d) # prints True
print(2 in d) # prints False - we check the keys, not the values
print(2 not in d) # prints True
print("a" not in d) # prints False

print(d["a"]) # finds the value associated with the given key. Crashes if the key is not in d
print(d.get("z", 42)) # finds the value of the key if the key is in the dictionary,
# or returns the second (default) value if the key is not in d

d["e"] = "wow" # adds a new key-value pair to the dictionary, or updates the value of a current key
del d["e"] # removes the key-value pair specified from the dictionary. Crashes if the key is not in d

for key in d:
    print(key, d[key]) # we can iterate over the keys, then print out the keys or corresponding values
```


## 4.**Properties of Dictionaries** 

### 1. **Dictionaries Map Keys to Values**

```py
ages = dict()
key = "fred"
value = 38
ages[key] = value  # "fred" is the key, 38 is the value
print(ages[key])
```

### 2. **Keys are Sets**

* **Keys are unordered**

```py
d = dict()
d[2] = 100
d[4] = 200
d[8] = 300
print(d)  # unpredictable order
```

* **Keys are unique**

```py
d = dict()
d[2] = 100
d[2] = 200
d[2] = 400
print(d)  # { 2:400 }
```

* **Keys must be immutable**

    

```py
d = dict()
a = [1] # lists are mutable, so...
d[a] = 42 # Error: unhashable type: 'list'
```

### 3. **Values are Unrestricted**

```py
# values may be mutable
d = dict()
a = [1,2]
d["fred"] = a
print(d["fred"])
a += [3]
print(d["fred"]) # sees change in a!

# but keys may not be mutable
d[a] = 42       # TypeError: unhashable type: 'list'
```

## 5. **Dictionaries are Very Efficient**
As mentioned above, a dictionary's keys are stored as a set. This means that finding where a key is stored takes constant time. This lets us look up a dictionary's value based on a key in constant time too!

## 6. **Some Worked Examples Using Dictionaries**

* **mostFrequent(L)** 

```py
def mostFrequent(L):
    # Return most frequent element in L, resolving ties arbitrarily.
    maxValue = None
    maxCount = 0
    counts = dict()
    for element in L:
        count = 1 + counts.get(element, 0)
        counts[element] = count
        if (count > maxCount):
            maxCount = count
            maxValue = element
    return maxValue

def testMostFrequent():
    print("Testing mostFrequent()... ", end="")
    assert(mostFrequent([2,5,3,4,6,4,2,4,5]) == 4)
    assert(mostFrequent([2,3,4,3,5,3,6,3,7]) == 3)
    assert(mostFrequent([42]) == 42)
    assert(mostFrequent([]) == None)
    print("Passed!")

testMostFrequent()
```

* **isAnagram(s1, s2)**   video

Here we rewrite [the 1d-list isAnagram example](http://www.cs.cmu.edu/~112/notes/notes-1d-lists-examples.html#anagrams) only using a dictionary instead.

    

```py
def letterCounts(s):
    counts = dict()
    for ch in s.upper():
        if ((ch >= "A") and (ch <= "Z")):
            counts[ch] = counts.get(ch, 0) + 1
    return counts

def isAnagram(s1, s2):
    return (letterCounts(s1) == letterCounts(s2))

def testIsAnagram():
    print("Testing isAnagram()...", end="")
    assert(isAnagram("", "") == True)
    assert(isAnagram("abCdabCd", "abcdabcd") == True)
    assert(isAnagram("abcdaBcD", "AAbbcddc") == True)
    assert(isAnagram("abcdaabcd", "aabbcddcb") == False)
    print("Passed!")

testIsAnagram()
```

        