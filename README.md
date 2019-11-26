# one-line
#### hilarious joke gone horribly wrong
---
helo im quak. i figured out how to write awful and illegible one-liners in python without statements over the course of about a year. i'm writing this primarily for friends in high school computer science classes so if someone else happens to come across this sorry if i seem a bit pedantic or something

to structure this i'm going to go through a bunch of exercises i've found online and write them both ways, while also explaining what i'm doing in what is hopefully too much detail

## basic things

### boilerplate
before i even get to examples, i'm going to show you the very basic structure everything that looks like this takes:
```python
(lambda x: print(x+2))(4) # => prints '6'
```
`lambda` is syntactic sugar for a nameless, inline function, and i'm already abusing it by defining and calling it on the same line. below is what you probably should be writing:
```python
add_two = lambda x: x+2
print(add_two(4)) # => prints '6'
```
which, if you want to be even more normal, would look like:
```python
def add_two(n):
    return x + 2

print(add_two(4)) # => prints '6'
```
uh yeah. hopefully i shouldn't have to go more in depth on the subject

