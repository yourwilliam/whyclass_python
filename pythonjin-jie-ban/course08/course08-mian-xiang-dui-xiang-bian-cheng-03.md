# [course]08 —— 面向对象编程03

## 1. **Type Testing (type, isinstance)** 

```py
class A(object): pass
a = A()
print(type(a))           # A (technically, < class '__main__.A' >)
print(type(a) == A)      # True
print(isinstance(a, A))  # True
```

## 2. **Special Methods**

### 1. **Equality Testing (__eq__)**

#### 1.The problem:** Shouldn't `a1 == a2`?

        

```py
class A(object):
    def __init__(self, x):
        self.x = x
a1 = A(5)
a2 = A(5)
print(a1 == a2)  # False!
```

#### 2. **The partial solution: __eq__**

The __eq__ method tells Python how to evalute the equality of two objects.

    

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def __eq__(self, other):
        return (self.x == other.x)
a1 = A(5)
a2 = A(5)
print(a1 == a2)  # True
print(a1 == 99)  # crash (darn!)
```

#### 3.**A better solution:**
Here we don't crash on unexpected types of `other`:

    

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def __eq__(self, other):
        return (isinstance(other, A) and (self.x == other.x))
a1 = A(5)
a2 = A(5)
print(a1 == a2)  # True
print(a1 == 99)  # False (huzzah!)
```

### 2. **Converting to Strings (__str__ and __repr__)** 
#### 1. **The problem:**
Just like with ==, Python doesn't really know how to print our objects... 

```py
class A(object):
    def __init__(self, x):
        self.x = x
a = A(5)
print(a) # prints <__main__.A object at 0x102916128> (yuck!)
```


####2. **The partial solution: __str__**
The `__str__` method tells Python how to convert the object to a string, but it is not used in some cases (such as when the object is in a list):

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def __str__(self):
        return "A(x=%d)" % self.x
a = A(5)
print(a) # prints A(x=5) (better)
print([a]) # prints [<__main__.A object at 0x102136278>] (yuck!)
```

#### 3. **The better solution: __repr__**
The `__repr__` method is used inside lists (and other places):

```py
# Note: repr should be a computer-readable form so that
# (eval(repr(obj)) == obj), but we are not using it that way.
# So this is a simplified use of repr.

class A(object):
    def __init__(self, x):
        self.x = x
    def __repr__(self):
        return "A(x=%d)" % self.x
a = A(5)
print(a) # prints A(x=5) (better)
print([a]) # [A(x=5)]
```

### 3. **Using in Sets and Dictionaries (__hash__ and __eq__)** 
**The problem:**
Objects do not seem to hash right by default:

```py
class A(object):
    def __init__(self, x):
        self.x = x

a = A(5)
b = A(5)

print(hash(a) == hash(b))       # False (this is surprising)
```

And that produces this unfortunate situation:

```py
class A(object):
    def __init__(self, x):
        self.x = x

s = set()
s.add(A(5))
print(A(5) in s) # False

d = dict()
d[A(5)] = 42
print(d[A(5)]) # crashes
```


**The solution: __hash__ and __eq__**

The `__hash__` method tells Python how to hash the object. The properties you choose to hash on should be immutable types and should never change (so `hash(obj)` is immutable).

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def __hash__(self):
        return hash(self.x)
    def __eq__(self, other):
        return (isinstance(other, A) and (self.x == other.x))

s = set()
s.add(A(5))
print(A(5) in s) # True (whew!)

d = dict()
d[A(5)] = 42
print(d[A(5)]) # works!
```

**A better (more generalizable) solution**
You can define the method `getHashables` that packages the things you want to hash into a tuple, and then you can use a more generic approach to `__hash__`:

```py
# Your getHashables method should return the values upon which
# your hash method depends, that is, the values that your __eq__
# method requires to test for equality.
# CAVEAT: a proper hash function should only test values that will not change!

class A(object):
    def __init__(self, x):
        self.x = x
    def getHashables(self):
        return (self.x, ) # return a tuple of hashables
    def __hash__(self):
        return hash(self.getHashables())
    def __eq__(self, other):
        return (isinstance(other, A) and (self.x == other.x))

s = set()
s.add(A(5))
print(A(5) in s) # True (still works!)

d = dict()
d[A(5)] = 42
print(d[A(5)]) # works!
```

### 4. **Fraction Example**

    

```py
# Very simple, partly-implemented Fraction class
# to demonstrate the OOP ideas from above.
# Note that Python actually has a full Fraction class that
# you would use instead (from fractions import Fraction),
# so this is purely for demonstrational purposes.

def gcd(x, y):
    if (y == 0): return x
    else: return gcd(y, x%y)

class Fraction(object):
    def __init__(self, num, den):
        # Partial implementation -- does not deal with 0 or negatives, etc
        g = gcd(num, den)
        self.num = num // g
        self.den = den // g

    def __repr__(self):
        return '%d/%d' % (self.num, self.den)

    def __eq__(self, other):
        return (isinstance(other, Fraction) and
                ((self.num == other.num) and (self.den == other.den)))

    def times(self, other):
        if (isinstance(other, int)):
            return Fraction(self.num * other, self.den)
        else:
            return Fraction(self.num * other.num, self.den * other.den)

    def __hash__(self):
        return hash((self.num, self.den))

def testFractionClass():
    print('Testing Fraction class...', end='')
    assert(str(Fraction(2, 3)) == '2/3')
    assert(str([Fraction(2, 3)]) == '[2/3]')
    assert(Fraction(2,3) == Fraction(2,3))
    assert(Fraction(2,3) != Fraction(2,5))
    assert(Fraction(2,3) != "Don't crash here!")
    assert(Fraction(2,3).times(Fraction(3,4)) == Fraction(1,2))
    assert(Fraction(2,3).times(5) == Fraction(10,3))
    s = set()
    assert(Fraction(1, 2) not in s)
    s.add(Fraction(1, 2))
    assert(Fraction(1, 2) in s)
    s.remove(Fraction(1, 2))
    assert(Fraction(1, 2) not in s)
    print('Passed.')

if (__name__ == '__main__'):
    testFractionClass()
```

## 3. **Class-Level Features**

### 1. **Class Attributes**  
Class Attributes are values specified in a class that are shared by **all** instances of that class! We can access class attributes from any instance of that class, but changing those values anywhere changes them for every instance.

```py
class A(object):
    dirs = ["up", "down", "left", "right"]

# typically access class attributes directly via the class (no instance!)
print(A.dirs) # ['up', 'down', 'left', 'right']

# can also access via an instance:
a = A()
print(a.dirs)

# but there is only one shared value across all instances:
a1 = A()
a1.dirs.pop() # not a good idea
a2 = A()
print(a2.dirs) # ['up', 'down', 'left'] ('right' is gone from A.dirs)
```

### 2. **Static Methods** 
Static Methods in a class can be called directly without necessarily making and/or referencing a specific object.

```py
class A(object):
    @staticmethod
    def f(x):
        return 10*x

print(A.f(42)) # 420 (called A.f without creating an instance of A)
```

### 3. **Playing Card Demo** 

```py
# oopy-playing-cards-demo.py
# Demos class attributes, static methods, repr, eq, hash

import random

class PlayingCard(object):
    numberNames = [None, "Ace", "2", "3", "4", "5", "6", "7",
                   "8", "9", "10", "Jack", "Queen", "King"]
    suitNames = ["Clubs", "Diamonds", "Hearts", "Spades"]
    CLUBS = 0
    DIAMONDS = 1
    HEARTS = 2
    SPADES = 3

    @staticmethod
    def getDeck(shuffled=True):
        deck = [ ]
        for number in range(1, 14):
            for suit in range(4):
                deck.append(PlayingCard(number, suit))
        if (shuffled):
            random.shuffle(deck)
        return deck

    def __init__(self, number, suit):
        # number is 1 for Ace, 2...10,
        #           11 for Jack, 12 for Queen, 13 for King
        # suit is 0 for Clubs, 1 for Diamonds,
        #         2 for Hearts, 3 for Spades
        self.number = number
        self.suit = suit

    def __repr__(self):
        return ("<%s of %s>" %
                (PlayingCard.numberNames[self.number],
                 PlayingCard.suitNames[self.suit]))

    def getHashables(self):
        return (self.number, self.suit) # return a tuple of hashables

    def __hash__(self):
        return hash(self.getHashables())

    def __eq__(self, other):
        return (isinstance(other, PlayingCard) and
                (self.number == other.number) and
                (self.suit == other.suit))

# Show this code in action
print("Demo of PlayingCard will keep creating new decks, and")
print("drawing the first card, until we see the same card twice.")
print()
cardsSeen = set()
diamondsCount = 0

# Now keep drawing cards until we get a duplicate
while True:
    deck = PlayingCard.getDeck()
    drawnCard = deck[0]
    if (drawnCard.suit == PlayingCard.DIAMONDS):
        diamondsCount += 1
    print("  drawnCard:", drawnCard)
    if (drawnCard in cardsSeen): break
    cardsSeen.add(drawnCard)

# And then report how many cards we drew
print("Total cards drawn:", 1+len(cardsSeen))
print("Total diamonds drawn:", diamondsCount)
```

## 4. **Inheritance**
A subclass inherits all the methods from its superclass, and then can add or modify methods.
### 1. **Specifying a Superclass** 

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def f(self):
        return 10*self.x

class B(A):
    def g(self):
        return 1000*self.x

print(A(5).f()) # 50
print(B(7).g()) # 7000
print(B(7).f()) # 70 (class B inherits the method f from class A)
print(A(5).g()) # crashes (class A does not have a method g)
```

### 2. **Overriding methods**
We can change a method's behavior in a subclass by overriding it.

        

```py
class A(object):
    def __init__(self, x):
        self.x = x
    def f(self):
        return 10*self.x
    def g(self):
        return 100*self.x

class B(A):
    def __init__(self, x=42, y=99):
        super().__init__(x) # call overridden init!
        self.y = y
    def f(self):
        return 1000*self.x
    def g(self):
        return (super().g(), self.y)

a = A(5)
b = B(7)
print(a.f()) # 50
print(a.g()) # 500
print(b.f()) # 7000
print(b.g()) # (700, 99)
```

### 3. **isinstance vs type in inherited classes** 

```py
class A(object): pass
class B(A): pass
a = A()
b = B()
print(type(a) == A) # True
print(type(b) == A) # False
print(type(a) == B) # False
print(type(b) == B) # True
print()
print(isinstance(a, A)) # True
print(isinstance(b, A)) # True (surprised?)
print(isinstance(a, B)) # False
print(isinstance(b, B)) # True
```

### 4. **Monster Demo**

```py
# This is our base class
class Monster(object):
    def __init__(self, strength, defense):
        self.strength = strength
        self.defense = defense
        self.health = 10

    def attack(self): # returns damage to be dealt
        if self.health > 0:
            return self.strength

    def defend(self, damage): # does damage to self
        self.health -= damage

class MagicMonster(Monster):
    def __init__(self, strength, defense):
        super().__init__(strength, defense) # most properties are the same
        self.health = 5 # but they start out weaker

    def heal(self): # only magic monsters can heal themselves!
        if 0 < self.health < 5:
            self.health += 1

class NecroMonster(Monster):
    def attack(self): # NecroMonsters can attack even when 'killed'
        return self.strength
```

## 5. **Additional Reading**
For more on these topics, and many additional OOP-related topics, check the following links:
     [https://docs.python.org/3/tutorial/classes.html](https://docs.python.org/3/tutorial/classes.html)
     [https://docs.python.org/3/reference/datamodel.html](https://docs.python.org/3/reference/datamodel.html)