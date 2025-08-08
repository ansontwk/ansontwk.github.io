---
layout: default
---

# Hello World

## Julia basics

Julia is a programming language that is very similar to Python. It uses a just-in-time compiler, making it much faster than python in (most) tasks.

Julia is also a dynamically typed language like Python. This means that variable need not be specified with a type, it can inferred.

This means:

```julia
mystring = "hello world"
myint = 42
```
will result in `mystring` being a `string` while `myint` being an `int`.

While not expicitly designed for OOP, Julia has support for OOP through the `struct`. 
Sorry, no classes for you

***Very important***

Julia is 1-indexed as opposed to python which is 0-indexed. This means:

```julia
mylist = ["number1", "number2", "number3"]
print(mylist[1])
```
yields `number1`, while in python

```python
mylist = ["number1", "number2", "number3"]
print(mylist[1])
```
yields `number2` instead.

## File naming

Julia code files should be named with the extension `.jl`.

## Comments

Julia uses `#` for comments, just like Python.

```julia
# This is a comment
```

However, Julia multiline comments is different where `#=` and `=#` are used.

```julia
#=
This 
is
a
multiline
comment
=#
```

whereas python uses `'''` for multiline comments.

## Printing

Julia uses `print()` for printing to console. However, this function prints out the contents to the console without a new line. There is another function called `println()` that will print out the contents with a new line instead.

```juila
print("hello world")
println("hello world")
```

Will yield

```
hello worldhello world
>
```

where the `>` denotes the location of the pointer

Printing multiple variables with `println()` prints the items together **without** a space between.

```julia
println("hello", "world")
```

will yield `helloworld`.

## Variables

Assign variables with `=`

```julia
mystring = "hello world"
myint = 42
```

## Variable naming conventions

Julia accepts most names as variables, exceptions include keyword like `true` and `false`

```julia
myvar_123 = "hello world"
my_var = "goodbye"
```
A key feature of Julia is that UTF-8 characters are supported for variable naming.

This includes mathematical symbols:

```julia
println(π + 1)
```

yields `4.141592653589793`

and even emojis:

```julia
😂 = 123
println(😂)
```

returns `123`

This can help your code become very terse and concise. It can also make your code increasingly stupid without proper comments.

```julia
😂 = "hello"
💩 = "world"

println(😂, " ", 💩)
```

yields `hello world`

## Retrieving variable type

Get the type of a variable with `typeof()`

```julia
😂 = "hello"
typeof(😂)
```

returns `String`

[back](../)