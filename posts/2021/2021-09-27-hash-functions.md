---
layout: post
title: "What Makes a Good Hash Function?"
date: 2021-09-27
---

My [spell-checker for CS50]({{ '/2021/08/cs50/' | url }}) needs a hash function. The [problem set specifications](https://cs50.harvard.edu/x/2021/psets/5/speller/) describe that students can “search for (good) hash functions online” as long as I cite the origin of what I integrate in my code. So… what exactly makes a hash function any good?!

Nobody explains computer science concepts like Vaidehi Joshi in her [basecs series](https://github.com/vaidehijoshi/basecs-series), so lets see what she has to say about [hash functions](https://medium.com/basecs/hashing-out-hash-functions-ea5dd8beb4dd):

> a hash table should have an easy-to-compute function because anything that’s too hard to compute will take up too much time an space! An expensive function defeats the purpose of finding an efficient data structure

> if the hash function didn’t return the same key every time? Well, that would be very bad, because we’d never be able to retrieve the data after we stored it, because we could never be sure where things are

> we have to understand how to handle collisions, because they are almost certainly going to happen. This is probably the most important thing to understand about hash functions, because they each need to account for collisions.

## Collision Resolution

Vaidehi’s article helped me understand the difference between these two:

- **linear probing** (look for the next empty bucket)
- **chaining** (using linked lists in each bucket).

Searching further, I found another text I really enjoyed: the part on hash tables in [Robert Nystrom’s Crafting Interpreters](https://craftinginterpreters.com/hash-tables.html#collision-resolution). 🥰 TIL about the 'birthday problem' and 'pigeonhole principle' and there is a fantastic illustration of the two combined. But also this description:

> a simple, well-worn hash function called [FNV-1a](http://www.isthe.com/chongo/tech/comp/fnv/) that’s served me fine over the years.

Sounds great! But gotta say, the [FNV-1a](http://www.isthe.com/chongo/tech/comp/fnv/) page is kinda overwhelming. Wikipedia’s [Fowler–Noll–Vo](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) is a nicer read. All right, so should/could I use this one?! 🤔 I didn’t find examples of implementations in C that I easily understood. But when I came across [this example of djb2](http://www.cse.yorku.ca/~oz/hash.html), it was more straight forward for me to see how to use this hash function. So I did.

## wait, what did I need the hash function to do?

Backtrack! I started digging further into hash functions today because: I initially (weeks ago) thought my program worked, but then I realised it didn't and suspected that the hash function was buggy. Why? Because as long as I had only a single hash bucket, the program found the correct number of misspelled words. And I kinda thought… oh well maybe I didn't find a _good_ hash function? I was impatient and wanted to move on to the next part of the problem. What I now understand — is that the hash function I found is probably fine enough (no version control in the CS50 IDE, so not entirely sure which one it was) — but that my implementation of it in no way set out to handle capitalized words.

`strcasecmp()` ignores case in my `check` function, but my yolo hash function copy-pasta puts `caterpillar` and `Caterpillar` into _different_ buckets. My program worked with 1 hash bucket, because then there was just a single linked list for the `check` function to traverse. But when I increase the number of buckets, the `check` function will have no way of looking in the correct linked list with capitalized words. 🤯😅😁😎🥳

Doh. The hash function isn’t only used when I load words from the dictionary into the hash table — I&nbsp;also use it to check words from the text. And those can be capitalized. Haha. So I need to make sure the input to the hash function can be alphabetical characters and apostrophes — and that values `Cat` and `cat` receive the same key, an identical numerical index for the hash table.

If I had read the problem set description properly, I would have seen this explicitly hinted. But I guess tracking this down as a bug was a better learning experience.

---

Other stuff I learnt about when CS50 sent me searching “for (good) hash functions online”.

### Cryptograpic or nah?

Hash functions are used to solve a whole bunch of different problems, and it was helpful to understand that I did _not_ need one that is a cyclic redundancy check, a checksum function or cryptographic. Wikipedia has a [list with the categories](https://en.wikipedia.org/wiki/List_of_hash_functions).

> Checksum functions are related to hash functions, fingerprints, randomization functions, and cryptographic hash functions. However, each of those concepts has different applications and therefore different design goals. For instance, a function returning the start of a string can provide a hash appropriate for some applications but will never be a suitable checksum.
> — [wikipedia.org/wiki/Checksum](https://en.wikipedia.org/wiki/Checksum)

### More on collisions

Apparently not just a theoretical construct. [This stackexchange answer](https://softwareengineering.stackexchange.com/questions/49550/which-hashing-algorithm-is-best-for-uniqueness-and-speed) writes that the djb2 algorithm I am using can have 7 collisions in the test they did, for example:

- `depravement` collides with `serafins`
- `stylist` collides with `subgenera`
- `joyful` collides with `synaphea`

My spell-checker can live with that.

---

Now I just need to fix that memory leak. 🚨<br>
But everything else works and this time I am certain!
