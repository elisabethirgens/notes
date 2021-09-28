---
layout: post
title: "Learn Python the Hard Way (cont.)"
date: 2017-12-30
---

More notes from [Learn Python The Hard Way](https://learncodethehardway.org/python/) (continued after [exercises 1–19]({{ '/2017/12/python/' | url }})). And again; _These are my notes. You can read them if you want — but I make no attempt at this being useful for anyone else._

---

## 20: Functions and Files

`seek()` is built-in function that:

- can change the file object’s position
- will complain if it doesn’t get at least one argument
- 1st arg is `offset` (number of characters from a reference point)
- 2nd arg is `from_what` that works like this:
  - `0` is the beginning of the file (this is the default if omitted)
  - `1` is the current file position
  - `2` is the end of the file

Except… hm. It seems that “only seeks relative to the beginning of the file are allowed” for text files. Which explains why I couldn’t get the end of the file reference to work when playing around in the console with this.

Python doesn’t need to separatly unpack arguments when I write a function. Which is what I did in the last exercise — but apparently it confused me again now, so let’s repeat:

```python
def whatever_function(anything_argument):
# and the argument is now ready to be used as a variable
```

✅ “rewrite the script to use the shorthand notation `+=`” **Yes. Did that. It’s working! \o/**

---

## 21: Functions Can Return Something

```python
def add(a, b):
    print(f"ADDING {a} + {b}") # this is just print
    return a + b # this is where the math actually happens

# define a variable and run the function with two arguments
# the variable then gets a value returned from the function
age = add(30, 10)
```

Wohooo! Had to sleep on it, but nailed the tricky extra credit puzzle.

#### Math (and Python) operation order repetition 🎓

> (parentheses first, then) do the multiplication and division in one step, from left to right, then do the addition and subtraction in one step from left to right

---

## 22: What Do You Know So Far?

This is a memorization exercise. I’ve got a lot of the symbols down fine, so I’m going to focus on the specific Python use descriptions that are less fluent for me yet:

### Symbols / characters

`#` write a comment <br>
`()` group some data (this is called a [tuple](https://en.wikipedia.org/wiki/Tuple)!) <br>
`,` separate multiple arguments <br>
`"` make a string <br>
`'` also make a string, but maybe a shorter one <br>
`=` assign the value on the right to a variable on the left <br>
`%` calculate the remainder from the division (modulus operator) <br>
`>=` test if a value is more than or equal <br>
`<=` test if a value is less than or equal <br>
`{}` embed a variable in a string <br>
`):` close a function definition

`\n` add a newline character <br>
`\t` add a tab character <br>
`\r` add a carriage return (reset to beginning of line)

### Built-in functions that are always available

✏️ `print()` output stuff <br>
🔨 `format()` apply format to a string that is already created <br>
🚢 `float()` return a floating point number (with a decimal point, not an integer) <br>
✂️ `round()` round off decimal numbers <br>
❓ `input()` ask questions in the console <br>
💯 `int()` convert a number as a string to an integer <br>
📂 `open()` open a file and return a file object

### Methods of file objects

Also built-in, but not always available. I can use them _after_ a file object has been created.

👀 `read()` read content from the file <br>
🧐 `readline()` read just a single line from the file <br>
✏️ `write()` write the content of a string to the file <br>
🔎 `seek()` change the file object’s position <br>
🚫 `close()` close the file and forget everything about it

Hmmmmm… It seems that in writing up these lists with proper headings, I also stumbled upon learning the **difference between functions and methods** in Python. Neat! 🎉

### Statements

🙋‍♀️ `def` define my own function and give it a useful name <br>
💁‍♀️ `return` return a value from the function

(Very pleased with these emoji!)

### More stuff

```python
f"here are some words and a {variable}" # this is an f-string
```

```python
# from the sys module, import a function for taking arguments
from sys import argv
# add one more argument in addition to the script itself
script, filename = argv
```

```python
open(filename)      # without the optional string for mode
open(filename, 'r') # r for read mode (which is default)
open(filename, 'w') # w for write mode (careful! can delete)
```

---

### Some observations…

…after this week of working on the [Learn Python The Hard Way](https://learncodethehardway.org/python/) exercises. 💪

- I’ve picked up a lot after just some hours each day for seven days.
- Learning thoroughly like this _different_ from how I’ve often learnt before. And I’m really enjoying it! This book is encouraging me to be patient and to _practice intentionally_.
- I am building a language to describe what I’m learning, and this is different from how I (even now after all these years) can talk about HTML/CSS. This is useful in all sorts of ways!!

Difference explained, with my current cocktail as an example:

- 🙃 “I’m having a red-ish drink with a cool name I spotted in the menu. It’s got ice!”
- 🤓 “This is a **negroni**. It’s an apértif, and served in a short tumbler. The ingredients are equal parts Campari, Vermouth (rosso) and gin. The first one had orange peel, but the other bartender forgot that from this second one. (It’s still pretty good.)”

## 🍸
