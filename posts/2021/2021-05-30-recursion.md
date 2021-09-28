---
layout: post
title: "Battle with Recursion"
date: 2021-05-30
---

Writing my first recursive function in C was not too bad. But writing a recursive function that _actually_ did what I intended the program to do? A different story. 🙈 I am writing this post to remind future me, of just how much I struggled with this — but kept at it anyway.

## CS50 🎓

I am doing [CS50 with a distributed study group]({{ '/2020/11/start-cs50/' | url }}) and in week 3 (Algorithms) the course introduces [recursion](https://cs50.harvard.edu/x/2021/shorts/recursion/) with the factorial function as an example. Seemed fine! Until I tried to write my own.

Recursion is not a requirement in any of the problem sets with C. But when I submitted my solution for [Filter](https://cs50.harvard.edu/x/2021/psets/4/filter/less) in week 4 (Memory), I had the gnawing feeling that I really should try to grok writing recursive functions. My program passed all the tests to full score, but the nested loops and if&nbsp;statements felt
ridiculously out of hand.

## Going back to Mario 🧱

The [first CS50 problem in C](https://cs50.harvard.edu/x/2021/psets/1/mario/more/) is a program to print a pyramid from Super Mario.

```
   #  #
  ##  ##
 ###  ###
####  ####
```

Surely after some weeks of coding in C, well into pointers and memory allocation, I should easily manage to refactor my Mario program to use a recursive function? Ha! Hahahaha. Lol. Nope. Not easily at all.

## Running locally 💻

The [CS50 IDE](https://ide.cs50.io/) is fantastic for getting started, but now it was time to figure out how to run my programs locally. Figured out how to install [cs50/libcs50](https://github.com/cs50/libcs50). Then compile with for example

```
gcc -lcs50 -o recursion recursion.c
```

to be able to run program `./recursion`. Neat!

## Think recursively? 🧠

My study buddy [Agata Maria](https://twitter.com/ja_gatka/) recommended these two posts:

- [Learning to think with recursion](https://medium.com/@daniel.oliver.king/getting-started-with-recursion-f89f57c5b60e)
- [How to Think Recursively | Solving Recursion Problems in 4 Steps](https://medium.com/swlh/how-to-think-recursively-solving-recursion-problems-in-4-steps-95a6d07aa866)

And sure enough, they helped me to write my first recursive function.

```
####
###
##
#
```

It was upside down. And only half the pyramid, but how hard could it be to complete?

_Several days later and multiple hours of serious [focused hours]({{ '/2021/03/deep-work/' | url }}) have passed._

---

I gave up. It was a sunny Sunday in April I should have been spending outdoors, and I decided to move on with my life. I tried searching for a solution (not cheating, because I submitted the problem months ago and writing a recursive version was not an official problem) but found no solutions, comments from people who gave up, but also this one person who proclaimed:

> Recursion in Mario: finally got it to work after a month!

> I've been trying to figure out how to create a recursive function that draws a right-aligned pyramid ever since recursion was introduced in the lectures. (…) I feel so relieved and accomplished. Now it's 2AM…

They never post any code, but reading this sheer joy of succeeding inspired me to keep at it for another 45 minutes. Lo and behold, don't you think I finally got the damn thing working. My recursive function to print a Mario pyramid locally. 🥳

```
gcc -lcs50 -o recursion recursion.c
./recursion

How many bricks? 17
                #  #
               ##  ##
              ###  ###
             ####  ####
            #####  #####
           ######  ######
          #######  #######
         ########  ########
        #########  #########
       ##########  ##########
      ###########  ###########
     ############  ############
    #############  #############
   ##############  ##############
  ###############  ###############
 ################  ################
#################  #################
```
