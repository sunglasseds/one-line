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
uh yeah. hopefully i shouldn't have to go more in depth on the subject of `lambda` and you have a full grasp on its use!!

anyway yeah everything will be a lambda statement in parenthesis followed by a call to the function in the statement. i don't like to keep my arguments in the call whenever i use them but we'll get into the alternatives later

by the way i'm going to be using pp in the headings it stands for "practice python" ok cool thanks

### [pp-01](https://www.practicepython.org/exercise/2014/01/29/01-character-input.html)
alright here we go really normal things going on over here. the prompt is as follows:
```markdown
create a program that asks the user to enter their name and their age. print
out a message addressed to them that tells them the year that they will turn
100 years old
	---
extras:
- add on to the previous program by asking the user for another number and
  printing out that many copies of the previous message (hint: order of
  operations exists in python)
- print out that many copies of the previous message on separate lines (hint:
  the string "\n" is the same as pressing the enter button)
```
