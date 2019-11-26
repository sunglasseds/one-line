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
if you're going to take away anything from this example, you should replace all their variables with their definitions UNLESS their definition has a call to `input`
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
and write a program that prints out all the elements of the list that are less
than 5
    ----    ----    ----    ----    ----    ----    ----    ----    ----
extras:
- instead of printing the elements one by one, make a new list that has all the
elements less than 5 from this list in it and print out this new list
- write this in one line of python
- ask the user for a number and return a list that contains only elements from
the original list a that are smaller than that number given by the user
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

## [pp-09: inline imports and infinite/conditional loops](https://www.practicepython.org/exercise/2014/04/02/09-guessing-game-one.html)
```markdown
generate a random number between 1 and 9 (including 1 and 9). ask the user to
guess the number, then tell them whether they guessed too low, too high, or
exactly right (hint: remember to use the user input lessons from the very first
exercise)
    ----    ----    ----    ----    ----    ----    ----    ----    ----
extras:
- keep the game going until the user types “exit”
- keep track of how many guesses the user has taken, and when the game ends,
print this out
```
this is going to be a lot at once. we're going to start with probably the simplest concept of the three: inline imports! python does not want you doing this under any circumstances but i mean come on look at what you can do with it
```python
(lambda n=__import__("random").randint(1, 9), g=int(input("what number am i thinking of [1,9]? ")): print({n > g: "too high", n < g: "too low", n == g: "you got it right!"}[True]))()
```
ok there's a bit going on here. i'm going to go through step by step from clean code this time because i've been thinking that may be clearer
```python
import random

number = random.randint(1, 9)
guess = int(input("what number am i thinking of [1, 9]? "))

if number > guess:
	print("too high")
elif number < guess:
	print("too low")
else:
	print("you got it right!")
```
right off the bat i'm going to write everything so it's inside a function, moving all my variables to the function's parameters
```python
import random
def guessing_game(number=random.randint(1, 9), guess=int(input("what number am i thinking of [1, 9]?"))):
	if number > guess:
		print("too high")
	elif number < guess:
		print("too low")
	else:
		print("you got it right!")

guessing_game()
```
alright now, to do inline imports, you replace all instances of the library's name with `__import__("library_name")`. imports are already horribly expensive and should be reduced to a bare minimum in python, keep in mind your code will slow down once you introduce these into the situation
```python
def guessing_game(number=__import__("random").randint(1, 9), guess=int(input("what number am i thinking of [1, 9]?"))):
	if number > guess:
		print("too high")
	elif number < guess:
		print("too low")
	else:
		print("you got it right!")

guessing_game()
```
next, i decided that since all of the options are mutually exclusive (unlike the divisible by 4 example), i replaced the `if`/`elif`/`else` conditional with a dictionary whose keys are the conditions, and then i ask for the value with the index that evaluates to `True`

i also shortened the variable names
```python
def guessing_game(n=__import__("random").randint(1, 9), g=int(input("what number am i thinking of [1, 9]?"))): print({n > g: "too high", n < g: "too low", n == g: "you got it right!"}[True])

guessing_game()
```
and now that our function has been reduced to one line, it can be converted to lambda syntax easily (with a few copy-pastes):
```python
(lambda n=__import__("random").randint(1, 9), g=int(input("what number am i thinking of [1,9]? ")): print({n > g: "too high", n < g: "too low", n == g: "you got it right!"}[True]))()
```
and thats it!! wow. i bet everything will be easy and understandable from now on. let's do the first extra
```python
(lambda a: lambda v: a(a, v))(lambda f, d: [d.update({"g": input(d["g"])}), print("bye!") if d["g"] == "exit" else f(f, {"n": d["n"], "g": "that's not a number!\nguess again! "}) if __import__("re").findall(r"[0-9]+", d["g"])[0] == "" else print("you got it right!") if int(d["g"]) == d["n"] else f(f, {"n": d["n"], "g": "too {}!\nguess again! ".format("high" if int(d["g"]) > d["n"] else "low")})])({"n": __import__("random").randint(1, 9), "g": "what number am i thinking of [1,9]? "})
```
you should probably feel overwhelmed right now. this is what it would normally look like:
```python
import random

number = random.randint(1, 9)
guess = input("what number am i thinking of [1, 9]? ")

def is_int(str):
	try:
		int(str)
	except ValueError:
		return False
	return True

while True:
	if guess == "exit":
		print("bye!")
		break
	elif is_int(guess):
		if int(guess) > number:
			print("too high!")
		elif int(guess) < number:
			print("too low!")
		else:
			print("you got it right!")
			break
	else:
		print("that's not a number! ")
	guess = input("guess again! ")
```
code is going to be really long right now, so i'm going to write comments like this: `# *snip*` that will signify that that the code in there is the same as it was before, so examples don't take up as much of your screen

now we do the obvious step, which is to condense the import:
```python
number = __import__("random").randint(1, 9)
# *snip*
```
now, to make the while loop smaller, you can remove all the print statements and instead use calls to `input`:
```python
# *snip*
while True:
	if guess == "exit":
		print("bye!")
		break
	elif is_int(guess):
		if int(guess) > number:
			guess = input("too high!\nguess again! ")
		elif int(guess) < number:
			guess = input("too high!\nguess again! ")
		else:
			print("you got it right!")
			break
	else:
		guess = input("that's not a number!\nguess again! ")
```
now we're going to turn the loop into a recursive function. it will call itself if it decides it needs to go again based on various conditionals. since the function will take care of the initial guess, i'll also remove the first call to `input`
```python
number = __import__("random").randint(1, 9)

def is_int(str): # *snip*

def guessing_game(g):
	guess = input(g)
	if guess == "exit":
		print("bye!")
	elif is_int(guess):
		if int(guess) > number:
			guessing_game("too high!\nguess again! ")
		elif int(guess) < number:
			guessing_game("too low!\nguess again! ")
		else:
			print("you got it right!")
	else:
		guessing_game("that's not a number!\nguess again! ")

guessing_game("what number am i thinking of [1, 9]? ")
```
okay, now i'm going to make `number` an optional argument for `guessing_game` instead of having it be generated at the beginning. this way, we can pass the number across recursive calls if we need to, but it will otherwise be randomly generated
```python
# *snip*
def guessing_game(g, n=__import__("random").randint(1, 9)):
# *snip*
```
guess is an unnecessary variable! we can just set g to `input(g)`
```python
# *snip*
def guessing_game(g, n=__import__("random").randint(1, 9)):
	g = input(g)
	if g == "exit":
		print("bye!")
	elif is_int(g):
		if int(g) > n:
			guessing_game("too high!\nguess again! ", n=n)
		elif int(g) < n:
			guessing_game("too low!\nguess again! ", n=n)
		else:
			print("you got it right!")
	else:
		guessing_game("that's not a number!\nguess again! ", n=n)
# *snip*
```
`is_int` is sort of a problem here. i wrote it to be the normal way which you would check to see if a string can be converted to an integer, but if we're going to write this in one line, we can't have a `try`/`except` block in our code. this means we have to come up with a different solution. i decided to use regular expressions, but you can condense whatever you come up with as long as it doesn't contain a `try`/`catch` block. let's replace it:
```python
import re

def is_int(str):
	return re.findall(r"[0-9]+", str)[0] != ""
# *snip*
```
and condense the import:
```python
def is_int(str):
	return __import__("re").findall(r"[0-9]+", str)[0] != ""
# *snip*
```
we're almost done! our code so far looks like:
```python
def is_int(str):
	return __import__("re").findall(r"[0-9]+", str)[0] != ""

def guessing_game(g, n=__import__("random").randint(1, 9)):
	g = input(g)
	if g == "exit":
		print("bye!")
	elif is_int(g):
		if int(g) > n:
			guessing_game("too high!\nguess again! ", n=n)
		elif int(g) < n:
			guessing_game("too low!\nguess again! ", n=n)
		else:
			print("you got it right!")
	else:
		guessing_game("that's not a number!\nguess again! ", n=n)

guessing_game("what number am i thinking of [1, 9]? ")
```
the next step is to make all of the control flow in `guessing_game` inline:
```python
# *snip*
def guessing_game(g, n=__import__("random").randint(1, 9)):
	g = input(g)
	print("bye!") if g == "exit" else guessing_game("that's not a number!\nguess again! ", n=n) if not  is_int(g) else print("you got it right!") if int(g) == n else guessing_game("too {}!\nguess again! ".format("high" if int(g) > n else "low"), n=n)

guessing_game("what number am i thinking of [1, 9]? ")
```
now we substitute the call to `is_int` with the actual function:
```python
def guessing_game(g, n=__import__("random").randint(1, 9)):
	g = input(g)
	print("bye!") if g == "exit" else guessing_game("that's not a number!\nguess again! ", n=n) if not (__import__("re").findall(r"[0-9]+", g)[0] != "") else print("you got it right!") if int(g) == n else guessing_game("too {}!\nguess again! ".format("high" if int(g) > n else "low"), n=n)

guessing_game("what number am i thinking of [1, 9]? ")
```
so the next thing to take care of is the assignment of `input(g)` to `g`. python actually has a function that can change values: `dict.update`, which merges two dictionaries. all we have to do is put all of the arguments in a dictionary like so:
```python
def guessing_game(d):
	d.update({"g": input(d["g"])})
	print("bye!") if d["g"] == "exit" else guessing_game({"g": "that's not a number!\nguess again! ", "n": d["n"]}) if not (__import__("re").findall(r"[0-9]+", d["g"])[0] != "") else print("you got it right!") if int(d["g"]) == d["n"] else guessing_game({"g": "too {}!\nguess again! ".format("high" if int(d["g"]) > d["n"] else "low"), "n": d["n"]})

guessing_game({"g": "what number am i thinking of [1, 9]? ", "n": __import__("random").randint(1, 9)})
```
notice how i changed all of the references to `g` and `n` to `d["g"]` and `d["n"]` respectively

that line, on the first call of the function, will change the argument `d` from `{"g": "what number am i thinking of [1, 9]? ", "n": __import__("random").randint(1, 9)}` to `{"g": input("what number am i thinking of [1, 9]? "), "n": __import__("random").randint(1, 9)}`. this is the only way to do inputs right: i tried writing this with calls to input in the body and it messed with the control flow. keep your calls to `input` as close to the function's beginning as possible

alright, next trick. you can put function calls in an array, which allows us to combine the two lines inside `guessing_game` like so:
```python
def guessing_game(d):
	[d.update({"g": input(d["g"])}), print("bye!") if d["g"] == "exit" else guessing_game({"g": "that's not a number!\nguess again! ", "n": d["n"]}) if not (__import__("re").findall(r"[0-9]+", d["g"])[0] != "") else print("you got it right!") if int(d["g"]) == d["n"] else guessing_game({"g": "too {}!\nguess again! ".format("high" if int(d["g"]) > d["n"] else "low"), "n": d["n"]})]

guessing_game({"g": "what number am i thinking of [1, 9]? ", "n": __import__("random").randint(1, 9)})
```
alright this next part involves some lambda calculus theory. we're going to use what's called a ("y-combinator")[https://en.wikipedia.org/wiki/Fixed-point_combinator#Fixed_point_combinators_in_lambda_calculus]. this is a specific lambda function that allows others to call themselves. in python, the y-combinator is written as:
```python
(lambda a, b: a(a, b))
```
and it can be used as follows:
```python
(lambda a, b: a(a, b))(lambda f, x: x*f(f, x-1) if x > 0 else 1)(2)
```
the code written above is a factorial function. it will return `x` multiplied by the value of the function given `x-1` unless `x > 0`, at which point the function will resolve all of its iterations. it's a bit difficult to explain. all you need to know to be able to use it is that the first argument is the reference to the function and the second argument is the value you use. whenever you call the function inside the function, you need to make sure to pass the first argument to the function. once i write the above code using the y-combinator, we'll be done
```python
(lambda a, b: a(a, b))(lambda f, d: [d.update({"g": input(d["g"])}), print("bye!") if d["g"] == "exit" else guessing_game({"g": "that's not a number!\nguess again! ", "n": d["n"]}) if not (__import__("re").findall(r"[0-9]+", d["g"])[0] != "") else print("you got it right!") if int(d["g"]) == d["n"] else guessing_game({"g": "too {}!\nguess again! ".format("high" if int(d["g"]) > d["n"] else "low"), "n": d["n"]})], {"g": "what number am i thinking of [1, 9]? ", "n": __import__("random").randint(1, 9)})
```
guido was right this was a mistake

i know it's a lot of work to do the next extra so i'll explain it in words and you'll have to do it yourself. what you have to do is create another key/value pair (we'll say it's `c`) in the dictionary and make it start at zero. whenever `f` is called, you have to add `"c": d["c"]+1` to the dictionary you call it with. then, on the print statement you win, append `str(d["c"])` to the output string with whatever accompanying text you want
