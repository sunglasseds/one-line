<style>
code {
  white-space : pre-wrap !important;
}
</style>
## basic things (boilerplate)

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
