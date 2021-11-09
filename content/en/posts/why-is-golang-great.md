---
title: "Why is Go(lang) great"
date: 2021-10-25T17:17:53+01:00
draft: true
---

Go(lang) - (we'll call it Go for short and for the sake of creators' wish) hyped and popular language, mostly about the cloud developer community.
Originally used in almighty Google for backend systems to improve performance on multicore and disributed systems. Rumors are, that the original
motivation of Go's creation was shared dislike of C++, which is something that author of this post understands and identifies with.
But what makes Go so popular? There are tons and tons of programming languages, why would anyone pick Go as the one  for ( but not limited to) cloud development.

Let's see.

## Building small footprint

This will probably won't impress you that much, if you are C/C++ developer. Or Pascal developer. Or basically any developer that
programs with language that compiles to native code. But if you are a coder that had to deal with any high-level language
like Java, C#, JavaScript or even Python  - you'll be positively surprised. 
All what you need to run your code is a binary compiled for your architecture. Due to static-linking you do not need to install any other runtimes or 
support libraries to run it. Forget the JVM, Node.JS, Python interpreter. Forget the GCC/GNUtils (if you do not involve yourself in CGO - C+Go interop).
Especially - if you compare it to Java, it's mindblowing. You might say - come on, I have to build it for each platform separately. 
Well luckily, the cross compilation is trivial - you just pass a specific parameter to go build command. And that's it. 
And honestly - if you produce a docker image, you do not usually care about multiplatform build that much. And if you do, there is a Goreleaser, which can help you with that.

The startup of the app is imminent (no JVM warmup), the resources are handled more efficiently (no VM/interpreter overhead) and the total size of app is small, so the deployment is quicker.
You will see a difference in your cloud provider billing.


## Easy to understand

Lot of modern languages tend to clutter their standard libraries with new syntax sugar. One new API for collections here, one new IO API there, new way how to write your data structures, 
null checking improved, additional async/await handling of concurrent approach. Random adding GUI libraries to standard library and removing it again (yes, I'm talking about you, JavaFX).
This things happen. And generally they're good, because it just allows you to write more concise code and expressing yourself much better in code.
But it makes the codebase incoherent - old stuff written in such language looks very different than a brand new library.
Go maintainers are actively against that. They just want the api and the language specification dead simple and understandable.
That mean, that the code follows common principles on the very simple building blocks.
Cycles over complicated streams.
If statementes over hidden factory abstraction.
When you have some experience in coding, it really is  easy to understand a new code. No hidden surprises, no backstabbing in production from vague API.
Go takes things seriously and transparently.

## Concurrency made easy

Doing multiple things at once is always a pain. And it definitely also applies to programming.
You can fight it with various instruments - with heavyweight threads and thread pooling, with callbacks and slowly succumbing yourself to a callback hell.
Or you can run lightweight threads and you can run a thousands of them. And that is exactly Go's model.
Go runtimes provides you with a scheduler that efficiently allocates precious execution time to a specific routines. Go routines.
As a coder - you just add "go" keyword before your function name in it's call. Just like you add await in different languages.
Yeah and small reminder - function called this way cannot have a return value.

How to handle returning values, race conditions and so on? 
Well you can share a variable and handle the race conditioning with good ol' mutexes and semaphores.
Or use channels - which is a very popular and used technique in Go. You basically establish a mailbox betweein the goroutines, that allows them to communicate.
Simple, yet powerful solution, making the Go in concurrent programming incredibly strong.
## Composition over inheritance

Well this is very nice language feature. You know the inheritance principle, right? You have parent class/structure , than you got a child classes/structures that uses the functionality of the parent one
and extend its functionality. This is working concept but has some flaws as well. C++ coders are familiar when you extend multiple parent classes for example.
Or the simple fact that the relationship between the child and the parent is very tight. When you change the base class, every hierarchy underneath this base (parent class) changes.

Go does not support inheritance. Like not at all - the principle as you know it is not really present here.

It replaces it with different principle - composition. 
It basically means, that you combine multiple structure/interfaces together to achieve basically the same as inheritance.
You do not extend any class (classes are not a thing in Go) - you implement interfaces.


## Batteries included