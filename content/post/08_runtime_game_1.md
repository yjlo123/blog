---
title: "Make a Game in Runtime Script (Part 1)"
date: 2021-03-28T00:00:00+08:00
draft: false
tags: ["runtime script"]
---

Creating mini-games is one of the purposes of developing Runtime Script. Although it is not a convenient language to write games, Runtime Script provides the basic features, such as drawing pixels and monitoring key events, for building playable and publishable games.

I've created several games while implementing Runtime Script and found making games is an effective way to test this language. Here are some examples: [Flappy Bird](https://runtime.siwei.dev/?src=bird),
[Sliding Puzzle](https://runtime.siwei.dev/?src=puzzle),
[Sokoban](https://siwei.dev/app/sokoban/), 
[(More ...)](https://github.com/yjlo123/runtime-script#examples). Since some of them are created at an early stage of Runtime Script,   they may not have used the latest supported syntax.

All the games I created using Runtime Script share the same necessary components, i.e. status variables, main loop, key events, sleep intervals, and redrawing pixels. In this blog, we are going to write such a boilerplate that can be modified to various mini-games.

In the program that we are going to write, you can move a white pixel on the canvas by pressing arrow keys.

First of all, we need two variables to represent the current position of the white pixel.
```
let cur_c 10
let cur_r 10
```

The initial position of the pixel is (10, 10). Then we can show it on the canvas by using the `drw` command:
```
drw $cur_c $cur_r 1
```

Be careful that the first argument of `drw` is the column, the second one is the row, and `1` means white color. For the details of the `drw` command and the complete list of colors, you can refer to [this session](https://siwei.dev/doc/runtime/#canvas) in the documentation.

To move the pixel in the game, we can press an arrow key, but how does Runtime Script know it? `$lastkey` is a sepcial value that contains a queue of user pressed keys, and each key is represented by a number. For instance, the keycodes of the arrow keys are listed below:

| Key | Code |
|---|---|
| left | 37 |
| up | 38 |
| right | 39 |
| down | 40 |

Every time we try to get a value from `$lastkey`, a user key event is consumed from the queue.

Let continue with the program. When the user presses the left arrow key, the program should print `left` and subtract the variable `cur_c` by `1`.
```
slp 3000

let key $lastkey
ife $key 37
 prt 'left'
 sub cur_c $cur_c 1
fin
```

The first line is for waiting for 3 seconds so that you have the chance to press the key before `$lastkey` is evaluated. Without the waiting time, the program finishes immediately.

To detect all four directions, you can write four similar `ife` blocks like the one above. There is another way to do this without using `if` commands:
```
let key $lastkey
jne $key 37 check_up
/ left
sub cur_c $cur_c 1
prt 'left'
jmp continue

#check_up
jne $key 38 check_right
/ up
sub cur_r $cur_r 1
prt 'up'
jmp continue

#check_right
jne $key 39 check_down
/ right
add cur_c $cur_c 1
prt 'right'
jmp continue

#check_down
jne $key 40 continue
/ down
add cur_r $cur_r 1
prt 'down'
jmp continue

#continue
```

Here we check conditions using two `jump` commands, `jne` and `jmp`. This manner is definitely not very readable, but it is commonly used before the `if` commands are introduced.

We are almost done. Let's put all of the above into a loop, called `main loop` so that the program can keep reading user input and updating the white pixel's position. At the end of the loop, we clear the canvas and redraw the white pixel.

CAUTION! the `main loop` is an infinite loop! Remember to add a `slp` interval inside the loop to control the refresh rate. For example, `slp 100` will have a refresh rate of 10Hz (1000 / 10 = 10Hz).

The final program:  
(You can try it yourself at [Runtime Script Playground](https://runtime.siwei.dev/))
```
let cur_c 10
let cur_r 10

jmp draw

#begin

/ -- check key --
let key $lastkey

ife $key 37
 / left
 sub cur_c $cur_c 1
 prt 'left'
fin

ife $key 38
 / up
 sub cur_r $cur_r 1
 prt 'up'
fin

ife $key 39
 / right
 add cur_c $cur_c 1
 prt 'right'
fin

ife $key 40
 / down
 add cur_r $cur_r 1
 prt 'down'
fin

/ -- draw --
#draw
clr
drw $cur_c $cur_r 1

slp 10
jmp begin
```
