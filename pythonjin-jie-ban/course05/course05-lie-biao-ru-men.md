# [course]05 —— 列表入门

## EX34 Accessing Elements of Lists


## EX38 Doing Things to Lists

```py
ten_things = "Apples Oranges Crows Telephone Light Sugar"

print("Wait there are not 10 things in that list. Let's fix that.")

stuff = ten_things.split(' ') more_stuff = ["Day", "Night", "Song", "Frisbee", "Corn", "Banana", "Girl", "Boy"]

while len(stuff) != 10:

next_one = more_stuff.pop() print("Adding: ", next_one) stuff.append(next_one) print(f"There are {len(stuff)} items now.")

print("There we go: ", stuff)

print("Let's do some things with stuff.")

print(stuff[1]) print(stuff[-1]) # whoa! fancy 
print(stuff.pop()) print(' '.join(stuff)) # what? cool!
print('#'.join(stuff[3:5])) # super stellar!
```

##EX39: Dictionaries, Oh Lovely Dictionaries

```py
# create a mapping of state to abbreviation 
states = { 'Oregon': 'OR', 'Florida': 'FL', 'California': 'CA', 'New York': 'NY', 'Michigan': 'MI' }

# create a basic set of states and some cities in them 
cities = {
'CA': 'San Francisco',
'MI': 'Detroit',
'FL': 'Jacksonville' }

# add some more cities 
cities['NY'] = 'New York' 
cities['OR'] = 'Portland'

# print out some cities 
print('-' * 10)

print("NY State has: ", cities['NY']) 
print("OR State has: ", cities['OR'])

# print some states 
print('-' * 10) 
print("Michigan's abbreviation is: ", states['Michigan'])
print("Florida's abbreviation is: ", states['Florida'])

# do it by using the state then cities dict 
print('-' * 10) 
print("Michigan has: ", cities[states['Michigan']]) 
print("Florida has: ", cities[states['Florida']])

# print every state abbreviation 
print('-' * 10) 
for state, abbrev in list(states.items()):
    print(f"{state} is abbreviated {abbrev}")

# print every city in state 
print('-' * 10) 
for abbrev, city in list(cities.items()):
    print(f"{abbrev} has the city {city}")

# now do both at the same time 
print('-' * 10) 
for state, abbrev in list(states.items()):
    print(f"{state} state is abbreviated {abbrev}") 
    print(f"and has city {cities[abbrev]}")

print('-' * 10) # safely get a abbreviation by state that might not be there 
state = states.get('Texas')

if not state:
    print("Sorry, no Texas.")

# get a city with a default value 
city = cities.get('TX', 'Does Not Exist') 
print(f"The city for the state 'TX' is: {city}")
```