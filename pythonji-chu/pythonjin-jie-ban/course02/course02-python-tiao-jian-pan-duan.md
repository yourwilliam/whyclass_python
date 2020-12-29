# \[course\]02 —— Python 条件判断

> EX29

```python
people = 20
cats = 30
dogs = 15

if people < cats:
    print("Too many cats! The world is doomed!")

if people > cats:
    print("Not many cats! The world is saved!")

if people < dogs:
    print("The world is drooled on!")

if people > dogs:
    print("The world is dry!")

dogs += 5

if people >= dogs:
    print("People are greater than or equal to dogs.")

if people <= dogs:
    print("People are less than or equal to dogs.")

if people == dogs:
    print("People are dogs.")

print(id(dogs))
print(id(20))
dogs += 1
print(id(dogs))

mydog = "wangcai"
print(id(mydog))
print(id("wangcai"))

x = 25
if x > 20 and x < 30:
    print(x)

if 20 < x < 30:
    print(x)

if 20 <= x <= 30:
    print(x)

if x in range(20, 30):
    print(x)
```

> EX30

```python
people = 30
cars = 40
buses = 15

if cars > people:
    print("We should take the cars.")
    if cars > people + 5:
        pass
elif cars < people:
    print("We should not take the cars.")
else:
    print("We can't decide.")

if buses > cars:
    print("That's too many buses.")
elif buses < cars:
    print("Maybe we could take the buses.")
else:
    print("We still can't decide.")

if people > buses:
    print("Alright, let's just take the buses.")
else:
    print("Fine, let's stay home then.")
```

