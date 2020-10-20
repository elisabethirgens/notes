---
layout: post
title:  "Write My Own Cheesecake Recipe"
date:   2018-01-22 12:00:00 +0200
---

I need a “cheesecake recipe” for a thing. It doesn’t have to be the best recipe in the world, but I want it to be **written by me from scratch using code I actually understand**. It would be easy to find recipes written by other people, or even just parts to be inspired by. But there’s no fun in that. (Yes, this typically called something else, I’m using different words here on purpose.)

Since I just started [learning Python]({{ site.baseurl }}/2017/12/python/), this also became an interesting way of tracking my progress. How far into [Learn Python The Hard Way](https://learncodethehardway.org/python/) would I be before having enough to write the recipe using just what I’d directly learnt from the exercies…?! [Jump to conclusion!](#conclusion)

So just for fun, I kept attempting to start coding the cheesecake recipe. Before I had learnt enough to actually write the script, just to make this lovely collection of:

## Awful ways of not properly baking

```python
# A store-bought small piece of hard coded cheesecake?

print(1,2,'cheese',4,'cake','cheese',7,8,'cheese','cake',
11, 'cheese', 13, 14, 'cheesecake')
```

```python
# Oh hey, a variable! And output on individual lines.

cheesecake = '1\n2\n3\n4\n5\n6\n7\n8\n9\n10'
print(cheesecake)
```

```python
# Possibly the least useful way ever of printing out numbers

print(1, 1 + 1, 1 + 1 + 1, 1 + 1 + 1 + 1, 1 + 1 + 1 + 1 + 1, 1 + 1 + 1
+ 1 + 1 + 1, 1 + 1 + 1 + 1 + 1 + 1 + 1, 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1,
1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1, 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1)
```

```python
# f-string and wanting to increment but not knowing how

a = 1
b = a + 1
c = b + 1
d = c + 1
e = d + 1
f = e + 1
g = f + 1
h = g + 1
i = h + 1
j = i + 1

c = 'cheese'
e = 'cake'
f = 'cheese'
i = 'cheese'
j = 'cake'

print(f"{a}\n{b}\n{c}\n{d}\n{e}\n{f}\n{g}\n{h}\n{i}\n{j}")
```

```python
# Just learnt one moar built-in function!

print("1, 2, {}, 4, {}, {}, 7, 8, {}, {}, 11, {}, 13, 14, {}"
.format('cheese','cake','cheese','cheese','cake','cheese','cheese' + 'cake'))
```

```python
# Another way to use variables.

three = 'cheese'
five = 'cake'
print(f"1, 2, {three}, 4, {five}, {three}, 7, 8, {three}, {five},
11, {three}, 13, 14, {three+five}")
```

```python
# Hello "increment by" operator and if statements!

three = "cheese"
five = "cake"

x = 1
print(x)
x += 1
print(x)
x += 1
if x == 3:
    print(three)
x += 1
print(x)
x += 1
if x == 5:
    print(five)
x += 1
if x == 6:
    print(three)
x += 1
print(x)
x += 1
print(x)
x += 1
if x == 9:
    print(three)
x += 1
if x == 10:
    print(five)
```

## Getting closer…

```python
# YES! for-loops! Now we’re getting somewhere.

divisiblebythree = "cheese"
divisiblebyfive = "cake"

stuff = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
for number in stuff:
    if number == 3 or number == 6 or number == 9 or number == 12:
        print(divisiblebythree)
    elif number == 5 or number == 10:
        print(divisiblebyfive)
    elif number == 15:
        print(divisiblebythree + divisiblebyfive)
    else:
        print(number)
```

```python
# Ooo. Now I know how to print the numbers from 1 to 100

for i in range(1, 101):
    print(i)
```

```python
# A-ha. Steps in range will get numbers divisible by 3 and 5.

list(range(0, 101, 3))
list(range(0, 101, 5))
```

```python
# So close I can smell the baked result…

divbythree = list(range(0, 101, 3))
divbyfive = list(range(0, 101, 5))

for i in range(1, 101):
    if i in divbythree:
        print('cheese')
    elif i in divbyfive:
        print('cake')
    else:
        print(i)
```

…and turns out I just needed to sleep on it to figure out the rest from there.

Wo-hooo. 🎉

---

## Conclusion

If you do all the exercises and study drills properly, you have learnt enough to write your own cheesecake recipe after **exercise 32 in Learn Python the Hard Way**. There are 52 all together, so this is pretty far into the book. But it’s intended for complete beginners and makes you practice a lot of stuff before introducing logic. For example:
* `if-statement` is first introduced in exercise 29
* `for-loops` come along in exercise 32

But it works. I didn’t find any part of this on stackoverflow, it’s all concepts I’ve actually learnt.
