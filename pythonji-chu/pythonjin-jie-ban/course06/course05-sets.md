# \[course\]06 —— sets

## 1. **Quick Example**

```python
# A set is a data structure that can hold multiple elements in no particular order
# We cannot index into it, but we can iterate over it.
s = set([2,3,5])
print(3 in s)          # prints True
print(4 in s)          # prints False
for x in range(7):
    if (x not in s):
        print(x)       # prints 0 1 4 6
```

## 2. **Creating Sets**

### 1. **Create an empty set**

```python
s = set()
print(s)     # prints set(), the empty set
```

### 2. **Create a set from a list**

```python
s = set(["cat", "cow", "dog"])
print(s)     # prints {'cow', 'dog', 'cat'}
```

### 3. **Create a statically-allocated set**

```python
s = { 2, 3, 5 }
print(s)    # prints { 2, 3, 5 }
```

### 4. **Caution: { } is not an empty set!**

```python
s = { }
print(type(s) == set)  # False!
print(type(s))         # This is a dict (we'll learn about those soon)
```

## 3. **Using Sets**

```python
# Sets can do many of the same things as lists and tuples...
s = set([1, 2, 3])

print(len(s)) # prints 3

print(2 in s) # prints True
print(4 in s) # prints False
print(4 not in s) # prints True
print(2 not in s) # prints False

s.add(7)      # use add instead of append to add an element to a set
s.remove(3)   # removes 3 from the set; raises an error if 3 is not in s

for item in s:
print(item) # we can loop over the items in s
```

## 4. **Properties of Sets**

Though sets are very similar to lists and tuples, they have a few important differences...

### 1. **Sets are Unordered**

```python
# Elements may be arranged in a different order than they are provided,
# and we cannot index into the set.
s = set([2,4,8])
print(s)          # prints {8, 2, 4} in standard Python (though not in brython)
for element in s: # prints 8, 2, 4
    print(element)
```

### 2. **Elements are Unique**

```python
# Sets can also only hold one of each unique element. Duplicates are removed.
s = set([2,2,2])
print(s)          # prints {2}
print(len(s))     # prints 1
```

### 3. **Elements Must Be Immutable**

```python
# Sets can only hold elements that are immutable (cannot be changed),
# such as numbers, booleans, strings, and tuples
a = ["lists", "are", "mutable"]
s = set([a])       # TypeError: unhashable type: 'list'
print(s)
```

### 4.**Another example:**

```python
s1 = set(["sets", "are", "mutable", "too"])
s2 = set([s1])     # TypeError: unhashable type: 'set'
print(s)
```

### 5. **Sets are Very Efficient**

The whole point of having sets is because they are very efficient, in fact O\(1\), for most common operations including adding elements, removing elements, and checking for membership.

## 5. **How Sets Work: Hashing**

Sets achieve their blazing speed using an algorithmic approach called **hashing**.

A **hash function** takes any value as input and returns an integer. The function returns the same integer each time it is called on a given value, and should generally return different integers for different values, though that does not always need to be the case. We actually don't need to build the hash function ourselves, as Python has one already, a built-in function called **hash**.

Python stores items in a set by creating a **hash table**, which is a list of N lists \(called 'buckets'\). Python chooses the bucket for an element based on its hash value, using `hash(element) % n`. Values in each bucket are not sorted, but the size of each bucket is limited to some constant K.

We get O\(1\) \(constant-time\) adding like so: 1. Compute the bucket index `hash(element) % n` -- takes O\(1\). 2. Retrieve the bucket hashTable\[bucketIndex\] -- takes O\(1\). 3. Append the element to the bucket -- takes O\(1\). We get O\(1\) \(constant-time\) membership testing \('in'\) like so: 1. Compute the bucket index `hash(element) % n` -- takes O\(1\). 2. Retrieve the bucket hashTable\[bucketIndex\] -- takes O\(1\). 3. Check each value in the bucket if it equals the element -- takes O\(1\) because there are at most K values in the bucket, and K is a constant. Q: How do we guarantee that each bucket is no larger than size K? A: Good question! If we need to add a \(K+1\)th value to a bucket, instead we **resize** our hashtable, making it say twice as big, and then we **rehash** every value, basically adding it to the new hashtable. This takes O\(N\) time, but we do it very rarely, so the **amortized worst case** remains O\(1\).

A practical example of how sets are faster than lists is shown below:

```python
# 0\. Preliminaries
import time
n = 1000

# 1\. Create a list [2,4,6,...,n] then check for membership
# among [1,2,3,...,n] in that list.

# don't count the list creation in the timing
a = list(range(2,n+1,2))

print("Using a list... ", end="")
start = time.time()
count = 0
for x in range(n+1):
    if x in a:
        count += 1
end = time.time()
elapsed1 = end - start
print("count=", count," and time = %0.4f seconds" % elapsed1)

# 2\. Repeat, using a set
print("Using a set.... ", end="")
start = time.time()
s = set(a)
count = 0
for x in range(n+1):
    if x in s:
        count += 1
end = time.time()
elapsed2 = end - start
print("count=", count," and time = %0.4f seconds" % elapsed2)
print("With n=%d, sets ran about %0.1f times faster than lists!" %
      (n, elapsed1/elapsed2))
print("Try a larger n to see an even greater savings!")
```

## 6. **Some Worked Examples Using Sets**

### 1. **isPermutation\(L\)**

```python
def isPermutation(L):
    # return True if L is a permutation of [0,...,n-1]
    # and False otherwise
    return (set(L) == set(range(len(L))))

def testIsPermutation():
    print("Testing isPermutation()...", end="")
    assert(isPermutation([0,2,1,4,3]) == True)
    assert(isPermutation([1,3,0,4,2]) == True)
    assert(isPermutation([1,3,5,4,2]) == False)
    assert(isPermutation([1,4,0,4,2]) == False)
    print("Passed!")

testIsPermutation()
```

### 2. **repeats\(L\)**

```python
def repeats(L):
    # return a sorted list of the repeat elements in the list L
    seen = set()
    seenAgain = set()
    for element in L:
        if (element in seen):
            seenAgain.add(element)
        seen.add(element)
    return sorted(seenAgain)

def testRepeats():
    print("Testing repeats()...", end="")
    assert(repeats([1,2,3,2,1]) == [1,2])
    assert(repeats([1,2,3,2,2,4]) == [2])
    assert(repeats(list(range(100))) == [ ])
    assert(repeats(list(range(100))*5) == list(range(100)))
    print("Passed!")

testRepeats()
```

