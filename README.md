# one-line
#### hilarious joke gone horribly wrong
helo im quak. i figured out how to write awful and illegible one-liners in python without statements over the course of about a year. i'm writing this primarily for friends in high school computer science classes so if someone else happens to come across this sorry if i seem a bit pedantic or something

to structure this i'm going to go through a few exercises i've found online and write them both ways, while also explaining what i'm doing in what is hopefully too much detail

## TABLE OF CONTENTS
- [long-winded explanations](https://github.com/sunglasseds/one-line/tree/master/long-winded-explanations):
	- [intro](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/01-intro.md)
	- [basic things](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/02-basic-things.md)
	- [input / string manipulation](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/03-pp-01-input-and-string-manipulation.md)
	- [conditionals](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/04-pp-02-conditionals.md)
	- [list comprehensions](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/05-pp-03-list-comprehensions.md)
	- [inline imports / infinite/conditional loops](https://github.com/sunglasseds/one-line/blob/master/long-winded-explanations/06-pp-09-inline-imports-and-infinite-conditional-loops.md)
- [quick reference](https://github.com/sunglasseds/one-line#quick-reference)
	- [basics](https://github.com/sunglasseds/one-line#basics)
	- [inline if/else](https://github.com/sunglasseds/one-line#inline-ifelse)
	- [list comprehensions](https://github.com/sunglasseds/one-line#list-comprehensions)
	- [inline imports](https://github.com/sunglasseds/one-line#inline-imports)
	- [y-combinator](https://github.com/sunglasseds/one-line#y-combinator)

## quick reference
### basics
```python
# -- always put your code in at least one lambda function --

# bad
def add_two(x):
    return x+2
print(add_two(4))

# good
(lambda x: print(x+2))(4)

# -- don't do outside variables --

# bad
thing = 4
print(2+thing)

# good
print(2+4)

# -- this includes function calls like `input` --

# bad
name = input("what's your name? ")
print("hello, {}".format(name))

# good
print("hello, {}".format(input("what's your name? ")))

# -- if you want to do multiple function calls, put them in arrays --

# bad
print("yea")
print("ok")

# good
[print("yea"), print("ok")]
```
### inline if/else
```python
# bad
n = int(input())
if n > 2:
    print("greater than two")
else:
    print("ech")

# good
print("greater than two") if int(input()) > 2 else print("ech")

# also good
print("greater than two" if int(input()) > 2 else "ech")

# -- you can chain them pretty easily --

# bad
n = int(input("give me a number "))
if n % 4 == 0:
    print("divisible by 4")
elif n % 2 == 0:
    print("even and not divisible by 4")
else:
    print("odd")

# good
(lambda n: print("divisible by 4") if n % 4 == 0 else print("even and not divisible by 4") if n % 2 == 0 else print("odd"))(int(input("give me a number ")))
```
### list comprehensions
```python
# bad
for i in range(0, 10):
    print(i)

# good
[print(i) for i in range(0, 10)]

# -- you can also chain them --

# bad
for i in range(10):
    for j in range(i):
        print(i*j)

# good
[print(i*j) for i in range(10) for j in range(i)]
```
### inline imports
```python
# bad
import random

print(random.randint(1, 10))

# good
print(__import__("random").randint(1, 10))
```
### y-combinator
```python
# bad
while True:
    print("hey")

# good
(lambda a, b: a(a, b))(lambda f, x: [print(x), f(f, x)][-1], "hey")
#                                                       ^
#                                   indexed because i only want to return the function
#                                   call, not `print` (which evaluates to `None`). -1
#                                   returns the last element of an array

# bad
x = 0
while x < 4:
    print(x)
    x += 1
print("done!")

# good
(lambda a, b: a(a, b))(lambda f, d: [print(d["x"]), d.update({"x": d["x"]+1}), f(f, d)][-1] if d["x"] < 4 else print("done!"), {"x": 0})

# here to copy and paste
(lambda a, b: a(a, b))
```
have fun!