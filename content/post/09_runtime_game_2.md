---
title: "Building a Game with Runtime Script (Part 2)"
date: 2023-09-17T00:00:00-04:00
draft: false
tags: ["runtime script"]
---

In the previous part, we have implemented a simple game template that allowes users to control a pixel on the canvas by pressing arrow keys, in this part, we are going to add two more features to make it more like a game:
- physics (gravity)
- drawing charactures with bitmaps


First let's resieze our canvas. By default, its size is 24 by 24, and we can add an optional argument to the `cls` command to change its resolution.
```
cls 32
```

This will change the canvas to 32 pixels in width and 32 pixels in height.


v = v' + gt

## Free Fall
<div class="runtime-embedded-box runtime-show-canvas" style="width: 100%; height: 400px;">let CANVAS_SIZE 32
let x 10
let y 10
<pre></pre>
let v 0
let G 1
<pre></pre>
jmp draw
<pre></pre>
#main_loop
<pre></pre>
/ -- calculate velocity --
add v $v $G
add y $y $v
jlt $y 30 velocity_done
sub v 0 $v
let y 30
#velocity_done
<pre></pre>
/ -- draw --
#draw
clr $CANVAS_SIZE
drw $x $y 1
<pre></pre>
slp 50
jmp main_loop
</div>

### Bit Map

<div class="runtime-embedded-box runtime-show-canvas" style="width: 100%; height: 680px;">let CANVAS_SIZE 64
let x 10
let y 0
<pre></pre>
let v 0
let G 1
<pre></pre>
def draw_bit_map
 let left $0
 let top $1
 let map '00044444000000444444444000ccc22020000c2c222022200c2cc222022200c2222000000002222220000044744744000444744744404444777744442247277274222227777772222277777777220077700777000bbb0000bbb0bbbb0000bbbb'
 for i 16
  for j 12
   pol $map c
   sub c $c $nil
   ifg $c 96
    sub c $c 87
   els
    sub c $c 48
   fin
   add xx $top $i
   add yy $left $j
   drw $yy $xx $c
  nxt
 nxt
end
<pre></pre>
jmp draw
<pre></pre>
#main_loop
<pre></pre>
/ -- calculate velocity --
add v $v $G
add y $y $v
jlt $y 48 velocity_done
sub v 0 $v
let y 48
#velocity_done
<pre></pre>
/ -- draw --
#draw
clr $CANVAS_SIZE
cal draw_bit_map $x $y
<pre></pre>
slp 50
jmp main_loop

</div>
