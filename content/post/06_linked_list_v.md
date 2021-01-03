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

For most of the scenarios, we only want to create a new node with its children undefined, and then assign values to them after some preparations. But this is not feasible in V, since, for the safety purpose, V has no null, no undefined values. 

It seems to me that all the other programing languages have ways to represent empty values or null pointers. At least there should be a constant that can be recognized as an empty value.

## First Attempt
Since V's reference is similar to C++ reference, I was wondering if I can set the integer `0` as the null pointer, and then found it worked.

{{< highlight rust "linenos=table" >}}
struct Node {
mut:
	val   int
	next  &Node
}

mut node := &Node {
    val:   100
    next:  0
}
{{< / highlight >}}

But obviously, it is tricky and also unsafe to do so. With no surprise, this is prohibited since V 0.2.

## Second Attempt
I have to find another way to represent `empty` in V. After going through the V doc, the only "empty thing" I could found is an empty array. So here we go:

{{< highlight rust "linenos=table" >}}
struct Node {
mut:
	val   int
	next  []&Node
}
{{< / highlight >}}

To check if the next node is empty:

{{< highlight rust "linenos=table" >}}
fn (node &Node) has_next() bool {
	return node.next.len != 0
}
{{< / highlight >}}

to get the next node:
{{< highlight rust "linenos=table" >}}
fn (node &Node) get_next() &Node {
	return node.next[0]
}
{{< / highlight >}}


and to set the next node:
{{< highlight rust "linenos=table" >}}
fn (mut node Node) set_next(next &Node) {
	node.next = [next]
}
{{< / highlight >}}

This method works well and will not likely be affected by future versions of V. But it is an overkill for linked lists, and it is more suitable for implementing tree structures.

## A Better Way?
V supports `sum type`, a sum type instance can hold a value of different types.

For our linked list nodes, we can categorize them into two types: a normal node with its value and a pointer to the next node, and an empty node used at the end of a linked list.

{{< highlight rust "linenos=table" >}}
struct ValueNode {
mut:
	val  int
	next &Node
}

struct EmptyNode {
}

type Node = EmptyNode | ValueNode

{{< / highlight >}}

Similar to the previous attempt, let's define its `checker`, `getter` and `setter`:

{{< highlight rust "linenos=table" >}}
fn (node &ValueNode) has_next() bool {
	return !(node.next is EmptyNode)
}

fn (node &ValueNode) get_next() &ValueNode {
	next := *node.next as ValueNode
	return &next
}

fn (mut node ValueNode) set_next(next &ValueNode) {
	node.next = next
}
{{< / highlight >}}

Next step, let's do some testing:
{{< highlight rust "linenos=table" >}}
fn new_node(val int) &ValueNode {
	return &ValueNode{
		val: val
		next: &EmptyNode{}
	}
}

fn main() {
	mut node := new_node(100)
	mut node2 := new_node(101)
	node.set_next(node2)
	assert node.has_next() == true
	assert node.get_next().has_next() == false
}

{{< / highlight >}}
