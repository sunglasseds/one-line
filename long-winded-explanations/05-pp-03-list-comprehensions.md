<style>
code {
  white-space : pre-wrap !important;
}
</style>
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
