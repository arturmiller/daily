# Walrus operator :=
A **statement** in Python is a unit of code. An **expression** is a special statement that can be evaluated to some value.  
In Python an assignment is not an expression, so you cannot asign it to another value, e.g:
```Python
x = (y=z)
```
This feature should make it unlikely to confuse an assignment the equality operator. In C++ this example is perfect legal code.
However, sometimes it makes sense to have an assignemt, which is also an expression. This is were the walrus operator ":=" comes to play.
```Python
x = (y:=z)
```
Note, the walrus operator requires brackets. This should make it less likely to confuse it with a normal assignment.  
The variable of the left site of the walrus operator should only be used locally. One good example for the usage of the walrus operator is this witness pattern:

```python
cities = ["Vancouver", "Oslo", "Houston", "Warsaw", "Graz", "Holguín"]

if any((witness := city).startswith("H") for city in cities):
    print(f"{witness} starts with H")
else:
    print("No city name starts with H")
```
"Any" breaks when one element evaluates to true and therefore this element ("Houston") is be printed.