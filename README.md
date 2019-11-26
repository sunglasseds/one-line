# one-line
#### hilarious joke gone horribly wrong
---
helo im quak. i figured out how to write awful and illegible one-liners in python without statements over the course of about a year. i'm writing this primarily for friends in high school computer science classes so if someone else happens to come across this sorry if i seem a bit pedantic or something

to structure this i'm going to go through a bunch of exercises i've found online and write them both ways, while also explaining what i'm doing in what is hopefully too much detail

## intro
<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Guido_van_Rossum_OSCON_2006.jpg/220px-Guido_van_Rossum_OSCON_2006.jpg" alt="guido"></p>

the soft bearded beer-toting bear pictured above is named "Guido van Rossum." he wrote the first version of python in about a month's worth of free time and is known as python's benevolent dictator for life. he has various [negative opinions](https://www.artima.com/weblogs/viewpost.jsp?thread=98196) on the inclusion of the techniques i am about to show you in python, which are usually referred to as "functional programming." this is essentially going to be a very convoluted and disgusting guide to functional programming as well as evidence that it should not be as prevalent in python as it is now

i desperately hope that this never happens; i love that python gives me the freedom to write awful code like this

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

### [pp-01: input and string manipulation](https://www.practicepython.org/exercise/2014/01/29/01-character-input.html)
alright here we go really normal things going on over here. the prompt is as follows:
```markdown
create a program that asks the user to enter their name and their age. print
out a message addressed to them that tells them the year that they will turn
100 years old
    ----    ----    ----    ----    ----    ----    ----    ----    ----
extras:
- add on to the previous program by asking the user for another number and
  printing out that many copies of the previous message (hint: order of
  operations exists in python)
- print out that many copies of the previous message on separate lines (hint:
  the string "\n" is the same as pressing the enter button)
```
and after hours of deliberation i came up with this code that fulfills the basic requirement (not doing the extras yet):
```python
(lambda n: print("{}, you will be 100 years old in the year {}".format(input("what's your name? "), 2119 - int(input("how old are you? ")))))()
```
im not using the `datetime` module because i don't think that's the intent of the exercise but there is a way to import libraries in one liners!!

so we're going to go step by step here. i'm not going to explain what `input`, `print`, and `format` do here. we're just going to stick to making this look normal
```python
print("{}, you will be 100 years old in the year {}".format(input("what's your name? "), 2119 - int(input("how old are you? "))))
```
this particular one will work just fine without the lambda. this is extremely rare; normally you will need the lambda for various reasons i have yet to reveal. let's keep going
```python
name = input("what's your name? ")
age = int(input("how old are you? "))

print("{}, you will be 100 years old in the year {}".format(name, 2119 - age))
```
if you're going to take away anything from this example, you should
# REPLACE ALL YOUR VARIABLES WITH THEIR DEFINITIONS
i'll go over the extra stuff now. the practicepython page actually has the method by which i'm going to do this (there's no functional programming popping up except for lambda right now). very simply, we can change the cleaned code to:
```python
name = input("what's your name? ")
age = int(input("how old are you? "))
times = int(input("how many times do you want me to repeat myself? "))

print("{}, you will be 100 years old in the year {}\n".format(name, 2119 - age) * times)
```
and i mean you should know what to do from here based on what i just did with the other stuff and the huge all-caps text i typed a few minutes ago. i'm just gonna keep going

## [pp-02: conditionals](https://www.practicepython.org/exercise/2014/02/05/02-odd-or-even.html)
ok cool what are we doing now, pp
```markdown
ask the user for a number. depending on whether the number is even or odd,
print out an appropriate message to the user. Hint: how does an even / odd
number react differently when divided by 2?
    ----    ----    ----    ----    ----    ----    ----    ----    ----
extras:
- if the number is a multiple of 4, print out a different message.
- ask the user for two numbers: one number to check (call it num) and one
number to divide by (check). if check divides evenly into num, tell that to the
user. if not, print a different appropriate message.
```
super easy. i won't even use lambda
```python
print("your number is " + ["even", "odd"][int(input("give me a number ")) % 2])
```
above is definitely the least intuitive and extensible way to do it, but it's also really nice-looking. here are two consecutive alternate solutions
```python
print("your number is " + {True: "even", False: "odd"}[int(input("give me a number ")) % 2 == 0])
```
```python
print("your number is " + ["odd", "even"][int(int(input("give me a number ")) % 2 == 0)])
```
this is a common thing that you should do with these one-liners if you don't feel like using lambda. what's being done here is that instead of an `if`/`else` block, i wrote a dictionary indexed with `True` and `False`. depending on what the statement `int(input("give me a number ")) % 2 == 0` evaluates to, it will pick the value `"even"` or `"odd"`

the second one is very similar. instead of getting an index from a dictionary, you could do the same with an array and convert `True`/`False` to an integer, which correspond to `1` and `0` respectively

let's do another one just for fun
```python
(lambda n=int(input("give me a number ")): print("your number is " + "even" if n % 2 == 0 else "odd"))()
```
this one is probably the easiest to immediately understand. i've used lambda with default arguments instead of calling the function with `input("give me a number ")` because i like defining my values in the beginning of my code as opposed to the end, just as you'd normally structure a program, but either option will give you the same result.

the other thing i've made use of is an inline `if`/`else` block, which is something you should never ever use in normal, readable code. the structure of these can be confusing so i'll put this reference here real quick:
```python
(value returned when the condition is True) if (condition) else (value returned when the condition is False)
```
and you should be good to go!

you can use whichever method you feel like to do conditionals!! it's sorta like math where there's multiple ways to solve a problem with minimal differences in effort. whichever feels the most natural to you is probably the best one!

just for consistency's sake i'll also throw in a cleaned version of our current code:
```python
number = int(input("give me a number "))

if number % 2 == 0:
	print("your number is even")
else:
	print("your number is odd")
```
i'll also quickly do one of the extras with inline if statements to demonstrate the fact that you can nest these
```python
(lambda n=int(input("give me a number ")): print("your number is " + ("divisible by 4" if n % 4 == 0 else "even" if n % 2 == 0 else "odd")))()
```
this is the kind of thing that you just have to read a few times to understand the flow but if it helps, the above code is equivalent to:
```python
n = int(input("give me a number "))

suff = ""

if n % 4 == 0:
	suff = "divisible by 4"
else:
	if n % 2 == 0:
		suff = "even"
	else:
		suff = "odd"

print("your number is " + suff)
```

## [pp-03: list comprehensions](https://www.practicepython.org/exercise/2014/02/15/03-list-less-than-ten.html)
```markdown
take a list, say for example this one:
  `a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]`
and write a program that prints out all the elements of the list that are less than 5
extras:
- instead of printing the elements one by one, make a new list that has all the elements less than 5 from this list in it and print out this new list
- write this in one line of python
- ask the user for a number and return a list that contains only elements from the original list a that are smaller than that number given by the user
```
probably my favorite thing in the entire language just because you can nest them. this problem is a classic example of something that can be made hundreds of times more painless than python already is with a really simple list comprehension. we're going to be doing that second extra by the way

here's what you would (and should) normally write in python:
```python
a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
for number in a:
    if number < 5:
        print(number)
```
list comprehension time
```python
print("\n".join([number for number in [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89] if number < 5]))
```
because of list comprehensions you can implement any kind of non-infinite loop. it might not be immediately obvious because i'm purposefully withholding information but i swear it's possible

just as a reference:
```python
[(value when condition is true) for i in (iterator) if (condition) else (value when condition is false)]
```
just as you can nest inline `if`/`else` blocks, you can nest list comprehensions to make arrays of multiple dimensions.

you can also call functions in the place of `(value when condition is true)` and/or `(value when condition is false)` if you dont want to use the array itself. this means that the above can also be written as:
```python
[print(number) for number in [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89] if number < 5]
```
ok cool moving on