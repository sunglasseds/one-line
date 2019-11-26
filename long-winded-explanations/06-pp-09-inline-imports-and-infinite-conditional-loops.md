<style>
code {
  white-space : pre-wrap !important;
}
</style>
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
def guessing_game(n=__import__("random").randint(1, 9), g=int(input("what number am i thinking of [1, 9]?"))):
    print({n > g: "too high", n < g: "too low", n == g: "you got it right!"}[True])

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
    print("bye!") if g == "exit" else guessing_game("that's not a number!\nguess again! ", n=n) if not is_int(g) else print("you got it right!") if int(g) == n else guessing_game("too {}!\nguess again! ".format("high" if int(g) > n else "low"), n=n)

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

is there anything else to cover? i dunno if there's much else to cover

i'll make a quick reference and split this up into chapters i guess. i've given you all the tools, so to speak, but i probably haven't explained them enough

wait no i haven't ok go look into `map` and `filter` if you don't know what those are. otherwise i'm pretty much done here