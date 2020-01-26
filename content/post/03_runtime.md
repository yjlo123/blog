---
title: "Why I Created Runtime Script"
date: 2020-01-26T11:30:40+08:00
draft: false
tags: ["programming language"]
---

In 2016, the year I graduated from my university, I started implementing a scripting language, [YJLO Script](https://yjlo123.github.io/yjlo-script/). It has a modern-style syntax since I borrowed a bunch of ideas from recent popular languages, such as Python, Golang, and Swift. It is implemented in JavaScript and interpreted directly in the browser.

The development process of YJLO Script is fun, I tried to push some commits to the repo very day with no gap for more than half year. There are numerous exciting moments especially when I finished writing some code examples using my own programming language.

It is also tedious and sometimes even irritating when I tried to add features to this language. I believe, debugging an issue in a programming language could be one of the most exhausting experiences among all the projects I have ever touched. This painful feeling got stronger when I was trying to add OOP support to it. For countless times, when I was writing an example program, I found a bug of the language, so I have to fix the language first, then continue with the example. I also finished adding a list of utility libraries, like Heap, Linked List, Hash Map, to imitate the standard libraries in other programming languages.

So, have I fully completed YJLO Script? Well, I'm not willing to say I gave up midway, but the development ends in mid-2018. It seems it is endless to add libraries and syntax sugars to make this language more convenient to use. However, at least YJLO Script is capable of implementing some projects which are complex enough. [Human Resource Machine Simulator](https://yjlo123.github.io/human-resource-machine-yjlo/) is an example.

Half a year later, in 2019, I started a new programming language from scratch, called [Runtime Script](https://runtime.siwei.dev/).

Runtime Script is very different from YJLO Script in many ways, for instance, Runtime Script is assembly-like, it has a minimal syntax (each statement consists of a keyword and an arbitrary number of arguments), and most importantly, it is an I/O blocking language, which makes it possible to write mini-games like [Flappy Bird](https://runtime.siwei.dev/?src=bird).

Since I'm inventing toy languages for fun, it would be more fascinating to write "cute" stuff using the language I created. Programming interactive graphical games is one of these cute things. And this requires the language to be I/O blocking so that the game UI can be refreshed in a certain interval.

I also considered to make YJLO Script a blocking language while I was implementing it, but at the moment I thought about this, I realized it was already too late unless I rewrite most part of the language.

In YJLO Script, the evaluator main loop is like this:

{{< highlight javascript "linenos=table" >}}
function evaluate(ast, env) {
	switch (typeOf(ast)) {
		case assignmentStatement:
			return evaluateAssignment(ast, env);	// evaluate() could be called in evaluateAssignment
		case ifStatement:
			return evaluateIf(ast, env);
		...
	}
}
{{< / highlight >}}

For example, in order to implement a blocking statement, e.g. `sleep(1000)`, which pauses the execution for one second, I should add a `setTimeout` with a callback function in the `evaluate()` function, since JavaScript is a non-blocking language. However, this requires each statement's execution is a callback of the previous statement. This change will dramatically change the existing structure of YJLO Script's implementation.

As a result, I decided to keep YJLO Script as it is, while designed Runtime Script as a blocking language at the beginning:

{{< highlight javascript "linenos=table" >}}
function loop() {
	if (env.pause) {
		return;
	}
	evaluate(nextStmt, env);
	if (env.sleep > 0) {
		return setTimeout(function () {
			env.sleep = 0;
			return loop();
		}, env.sleep);
	}
	return loop();
}
{{< / highlight >}}

In this manner, I can pause or delay the execution easily, because each iteration checks the value of `pause` and `sleep` and decides whether the next statement should be executed immediately or not.

After two sprints in 2019, the first complete version of Runtime Script is finished. All the planned major features are implemented. Besides, I drafted a [tutorial](https://siwei.dev/doc/runtime/) of this language.

I know most likely I am the only user of the languages I created, but this won't hinder the process of implementing my own toys, which was dreamed for years by the younger version of me.
