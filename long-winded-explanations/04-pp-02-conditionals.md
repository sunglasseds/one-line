<style>
code {
  white-space : pre-wrap !important;
}
</style>
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
