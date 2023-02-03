---
title: Advanced Python Dictionary Techniques You Should Know
date: 2022-06-12T23:54:31+08:00
author: 1rfan
avatar: /img/ss.jpeg
cover: /img/pydict.png
images:
  -
categories:
  - ENG
tags:
  - Python
---

_I come to tip the balance!_

<!--more-->

## From Nothing to Something.

Let's try to get a feel of what a python dictionary actually is before diving deep into its rabbit hole.

A Python dictionary is a data structure that allows us to easily write very efficient code. 
In many other languages, this data structure is called a hash table because its keys are hashable.

A Python dictionary is a collection of _**key:value**_ pairs. You can think about them as words and their meaning in an ordinary dictionary. Values are said to be mapped to keys.

![pydict](https://www.jeevangupta.com/wp-content/uploads/2021/10/Dictionary-in-Python-1024x742.png)

<br/>

```python
d = {"Ember Spirit": 29, "Void Spirit": 24, "Earth Spirit": 22}
print(d)
```
Our output would look like this:
```text
{'Ember Spirit': 29, 'Void Spirit': 24, 'Earth Spirit': 22}
```
<br/>


What if we want to add one year to each age and save the result in a new dictionary? We can do it with a for loop.

```python
# Dictionary to store new ages
new_d = {}

# Add one year to each age in the dictionary
for name, age in d.items(): # .items() method displays dictionary keys and values as a list of tuple pairs
    new_d[name] = age + 1
print(new_d)
```

Our output would look like this:
```text
{'Ember Spirit': 29, 'Void Spirit': 24, 'Earth Spirit': 22}
```

That's all for this section. Let's jump right ahead to the next.

## Advanced Python Dictionary Comprehension

Let’s make our code shorter. The for loop can be rewritten in just one line using dictionary comprehension.

```python
# Add one year to each age in the dictionary using comprehension
new_d = {name: age + 1 for name, age in d.items()}

print(new_d)
```

How about using a Python dictionary comprehension to filter a dictionary?

```python
stocks = {
    'AAPL': 121,
    'AMZN': 3380,
    'MSFT': 219,
    'BIIB': 280,
    'QDEL': 266,
    'LVGO': 144
}

selected_stocks = {}
for symbol, price in stocks.items():
    if price > 200:
        selected_stocks[symbol] = price

print(selected_stocks)
```

> How do we write this better?

```python
stocks = {
    'AAPL': 121,
    'AMZN': 3380,
    'MSFT': 219,
    'BIIB': 280,
    'QDEL': 266,
    'LVGO': 144
}

selected_stocks = {s: p for (s, p) in stocks.items() if p > 200}

print(selected_stocks)
```


<br/>


## Advanced dictionary Use Cases
Sometimes, we need to work with a nested dictionary, i.e., when we have a dictionary inside another dictionary. Let’s first of all, create a nested dictionary.



Say we have a dataset(I'm not actually giving out the dataset here). Just pretend we do. And the dataset is about games. Lots and lots of games.

Let's try to make something out of this pretending...

### How to use comprehension in a nested dictionary

[https://media.geeksforgeeks.org/wp-content/uploads/Dictionary-Creation-1.jpg]


```PYTHON
# Create a nested dictionary
nested_d = {}
for n, p, dt in zip(name, platform, date):
    nested_d[n] = {"platform": p, "date": dt}

# Print the first five items of the nested dictionary
print(list(nested_d.items())[:5])
```
would output something like this

```text
[('The Legend of Zelda: Ocarina of Time', {'platform': 'Nintendo64', 'date': 'November 23, 1998'}), ("Tony Hawk's Pro Skater 2", {'platform': 'Nintendo64', 'date': 'August 21, 2001'}), ('Grand Theft Auto IV', {'platform': 'PC', 'date': 'December 2, 2008'}), ('SoulCalibur', {'platform': 'Xbox360', 'date': 'July 2, 2008'}), ('Super Mario Galaxy', {'platform': 'Wii', 'date': 'November 12, 2007'})]
```

There is a way to rewrite the above for loop using dictionary comprehension. Do it for practice.

In order to not complicate things, we will be using only the platform in the inner value. Very often, this is the format the data is delivered to us via [API](/posts/api).

```PYTHON
# Create another nested dictionary
nested_d = {}
for n, dt in zip(name, date):
    nested_d[n] = {"date": dt}

# Print the first five items of the dictionary
print(list(nested_d.items())[:5])
```
would output something like this

```text
[('The Legend of Zelda: Ocarina of Time', {'date': 'November 23, 1998'}), ("Tony Hawk's Pro Skater 2", {'date': 'August 21, 2001'}), ('Grand Theft Auto IV', {'date': 'December 2, 2008'}), ('SoulCalibur', {'date': 'July 2, 2008'}), ('Super Mario Galaxy', {'date': 'November 12, 2007'})]
```

</br>

If your code gets pretty complicated at some point, realize it is just not worth it to keep trying using dictionary comprehension. Remember that one of the <a href="https://peps.python.org/pep-0020/#the-zen-of-python" target="_blank">main principles of Python</a> is readability.




###  How to sort a dictionary

Another use of dictionary comprehension in Python is dictionary sorting. For example, let’s say we want to sort the dictionary with game titles and years by year from the first to the latest year? 

Let’s first transform years from str data type into int data type (using comprehension!).

```PYTHON
# Convert years from strings into intergers
year_dict_int = {key: int(value) for key, value in year_dict.items()}

# Sort by year
sorted_year = {key: value for key, value in sorted(year_dict_int.items(), key=lambda x: x[1])}

# Print the first five items of the dictionary sorted by year
print(list(sorted_year.items())[:5])
```
would output something like this

```text
[('Full Throttle', 1995), ("Sid Meier's Civilization II", 1996), ('Diablo', 1996), ('Super Mario 64', 1996), ('Wipeout XL', 1996)]
```
We used the sorted function which accepts the key argument that we need to tell the function which element we want to sort on. In this case, we have two options: sort on dictionary keys or values. Values come second, so the index should be 1, while for keys it would be 0. 

Keys are usually assigned to lambda functions which are anonymous functions often used in Python. Do you think it is possible to apply a for loop to achieve the same result?

### How to flatten a dictionary

Sometimes we face a list of dictionaries or even nested dictionaries, and we want one single dictionary. It can also be done with dictionary comprehension.

![nested-dict](https://media.geeksforgeeks.org/wp-content/uploads/Dictionary-Creation-1.jpg)
<!-- ![pydict](https://www.jeevangupta.com/wp-content/uploads/2021/10/Dictionary-in-Python-1024x742.png) -->


_**Method #1: Using Naive Approach**_

```python
# code to convert ini_dict to flattened dictionary
# default separator '_'
def flatten_dict(dd, separator ='_', prefix =''):
    return { prefix + separator + k if prefix else k : v
             for kk, vv in dd.items()
             for k, v in flatten_dict(vv, separator, kk).items()
             } if isinstance(dd, dict) else { prefix : dd }
         
# initialising_dictionary
ini_dict = {'geeks': {'Geeks': {'for': 7}},
            'for': {'geeks': {'Geeks': 3}},
            'Geeks': {'for': {'for': 1, 'geeks': 4}}}
 
# printing initial dictionary
print ("initial_dictionary", str(ini_dict))

# printing final dictionary
print ("final_dictionary", str(flatten_dict(ini_dict)))
```

```text
Output
initial_dictionary {‘geeks’: {‘Geeks’: {‘for’: 7}}, ‘Geeks’: {‘for’: {‘geeks’: 4, ‘for’: 1}}, ‘for’: {‘geeks’: {‘Geeks’: 3}}} 
final_dictionary {‘Geeks_for_for’: 1, ‘geeks_Geeks_for’: 7, ‘for_geeks_Geeks’: 3, ‘Geeks_for_geeks’: 4} 
```
<br/>

_**Method #2: Using mutuableMapping**_

```python
from collections import MutableMapping
 
# code to convert ini_dict to flattened dictionary
# default separator '_'
def convert_flatten(d, parent_key ='', sep ='_'):
    items = []
    for k, v in d.items():
        new_key = parent_key + sep + k if parent_key else k
 
        if isinstance(v, MutableMapping):
            items.extend(convert_flatten(v, new_key, sep = sep).items())
        else:
            items.append((new_key, v))
    return dict(items)
         
# initialising_dictionary
ini_dict = {'geeks': {'Geeks': {'for': 7}},
            'for': {'geeks': {'Geeks': 3}},
            'Geeks': {'for': {'for': 1, 'geeks': 4}}}
 
# printing initial dictionary
print ("initial_dictionary", str(ini_dict))
 
 
# printing final dictionary
print ("final_dictionary", str(convert_flatten(ini_dict)))
```
```text
Output: 
initial_dictionary {‘Geeks’: {‘for’: {‘for’: 1, ‘geeks’: 4}}, ‘for’: {‘geeks’: {‘Geeks’: 3}}, ‘geeks’: {‘Geeks’: {‘for’: 7}}} 
final_dictionary {‘Geeks_for_geeks’: 4, ‘for_geeks_Geeks’: 3, ‘geeks_Geeks_for’: 7, ‘Geeks_for_for’: 1} 
```

_**Method #3: Using Python Generators**_

```python
from collections import MutableMapping
 
# code to convert ini_dict to flattened dictionary
# default separator '_'
def convert_flatten(d, parent_key ='', sep ='_'):
    items = []
    for k, v in d.items():
        new_key = parent_key + sep + k if parent_key else k
 
        if isinstance(v, MutableMapping):
            items.extend(convert_flatten(v, new_key, sep = sep).items())
        else:
            items.append((new_key, v))
    return dict(items)
         
# initialising_dictionary
ini_dict = {'geeks': {'Geeks': {'for': 7}},
            'for': {'geeks': {'Geeks': 3}},
            'Geeks': {'for': {'for': 1, 'geeks': 4}}}
 
# printing initial dictionary
print ("initial_dictionary", str(ini_dict))
 
 
# printing final dictionary
print ("final_dictionary", str(convert_flatten(ini_dict)))
```

```text
Output: 
initial_dictionary {‘Geeks’: {‘for’: {‘for’: 1, ‘geeks’: 4}}, ‘for’: {‘geeks’: {‘Geeks’: 3}}, ‘geeks’: {‘Geeks’: {‘for’: 7}}} 
final_dictionary {‘Geeks_for_geeks’: 4, ‘for_geeks_Geeks’: 3, ‘geeks_Geeks_for’: 7, ‘Geeks_for_for’: 1} 
```

### How to compute the word frequency in a string

One of the steps in Natural Language Processing is counting the word occurences in a text. A natural way to represent this data is by using a dictionary, where the key is the word, and the value is the number of times this word appears in the text. It is also a job for dictionary comprehension!

```python
# Quote by Henry Van Dyke
quote = """time is too slow for those who wait too swift for those who fear too long for
those who grieve too short for those who rejoicebut for those who love, time is eternity"""

# Count frequency of words in the quote
frequency_dict = {word: quote.split(" ").count(word) for word in quote.split(" ")}

print(frequency_dict)
```
```text
{'time': 2, 'is': 2, 'too': 4, 'slow': 1, 'for': 5, 'those': 4, 'who': 5, 'wait': 1, 'swift': 1, 'fear': 1, 'long': 1, '\nthose': 1, 'grieve': 1, 'short': 1, 'rejoicebut': 1, 'love,': 1, 'eternity': 1}
```

Congratulations if you've made it through all of the snippets. Now get out out there and apply your new found knowledge into some of your codebase.

## References :

- [Python PEPs](https://peps.python.org/)
- [Geeks4Geeks](https://www.geeksforgeeks.org/python-convert-nested-dictionary-into-flattened-dictionary/)
