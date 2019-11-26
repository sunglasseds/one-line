## [pp-01: input and string manipulation](https://www.practicepython.org/exercise/2014/01/29/01-character-input.html)
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
