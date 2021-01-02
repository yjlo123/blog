---
title: "Implementing Linked Lists in Vlang"
date: 2020-12-25T00:00:00+08:00
draft: false
tags: ["vlang", "data structure"]
---

In V's documentation, it says:
> V's references are similar to Go pointers and C++ references.  
For example, a generic tree structure definition would look like this:


{{< highlight rust "linenos=table" >}}
struct Node<T> {
    val   T
    left  &Node
    right &Node
}
{{< / highlight >}}

However, I found that it seems impossible to initialize such a Node. A new Node must define the initial values for its left and right references, which are Nodes that need their left and right values initialized as well.

For most of the cases, we only want to create a new node with its children undefined, and then assign values to them after some preparations. But this not feasible in V, since, for the safety purpose, V has no null, no undefined values or behavior. 

I don't think this safety feature makes sense, and it is even kind of stupid. As far as I know, all the other programing languages have ways to represent empty values or null pointers. At least there should be a constant that can be recognized as such empty values.

### First Attempt
{{< highlight rust "linenos=table" >}}
struct ValueNode {
pub mut:
	val   int
	left  &Node
	right &Node
}

struct EmptyNode {}

type Node = ValueNode | EmptyNode

{{< / highlight >}}

### Second Attempt
Since V's reference is similar to C++ reference, I was wondering if I can set the integer `0` as the null pointer, and found it worked.

{{< highlight rust "linenos=table" >}}
struct Node {
pub mut:
	val   int
	left  &Node
	right &Node
}

mut node := &Node {
    val:   100
    left:  0
    right: 0
}
{{< / highlight >}}

But obviously, it is tricky and unsafe to do so. No surprise, this is prohibited since V 0.2.

### Final Attempt
I have to find another way to represent empty in V. After going through the V doc, the only "empty thing" I could found is an empty array. So here we go:

{{< highlight rust "linenos=table" >}}
struct Node {
pub mut:
	val   int
	left  []&Node
	right []&Node
}
{{< / highlight >}}

Let's take the left child as an example, to check if the lift child is empty:

{{< highlight rust "linenos=table" >}}
fn (node &Node) has_left() bool {
	return node.left.len != 0
}
{{< / highlight >}}

to get the left child:
{{< highlight rust "linenos=table" >}}
fn (node &Node) get_left() &Node {
	return node.left[0]
}
{{< / highlight >}}


and to set the left child:
{{< highlight rust "linenos=table" >}}
fn (mut node Node) set_left(left &Node) {
	node.left = [left]
}
{{< / highlight >}}

This is still not a neat manner to deal with the `no null` limitation in V, but I haven't found a better way.
