---
layout: post
title:  "Learning Haskell"
date:   2013-10-10 02:30:37
categories: haskell
---


I'm trying to learn Haskell.
This post details some of the steps I'm going through.

_Setup:_

If you are on Ubuntu or Debian (like me): `sudo apt-get install ghc6` should do the trick.
"GHC" stands for "Glasgow Haskell Compiler", it contains a compiler (ghc) and an interpreter (ghci).

_Hello World:_

Printing "hello world" is simple. Start ghci and type:

    print "Hello World"

This should print "Hello World" on the screen.

I often like to have file containing code in my editor and then load and execute code in that file in the interpreter.
Right now, I simply have a file called `first_steps.hs`. I then start ghci from the same directory as the file.

To put code in a file, you need to first wrap it in a function. That is easy enough, just put the following in your source file:

    printHello = print "Hello"

The simple fact that we assign code to a name seems to be enough to define a function, interesting!
Then, switching back to ghci, you can use `:load first_steps` to load the file in the interpreter. After that, type `printHello` to execute the function.

_Lists:_

Now that we have the obligatory "hello world" example behind us, let's turn our attention to lists.
I found that these are often important in functional languages and help understand the concepts of the language.

The goal will be to write a function `reverseList` that does just what the name indicates: reverse a list.
As Haskell is a functional language, I had a hunch that recursion would be involved.
To reverse a list using recursion, one can simply use the following algorithm:

     1. If the list is empty, we are done and return the empty list
     2. Split the list in two parts: "First element" and "Rest of list".
	 (First element is referred to as "head", rest of list is called "tail)
	 3. Reverse tail and append head to the result.

A simple example will illustrate the algorithm:

    Start: [1,2,3,4]
	Step 1: Head = 1, Tail = [2,3,4]
	        Reverse [2,3,4] and append 1
	Step 2: Head = 2, Tail = [3,4]
		    Reverse [3,4] and append 2 (and append 1)
	Step 3: Head = 3, Tail = [4]
	        Reverse [4] and append 3 (and append 2 (and append 1))
	Step 4: Head = 4, Tail = [] (<- the empty list)
	        Reverse [] and append 4 (and append 3 (and append 2 (and append 1)))
	Step 5: The list is empty (point 1 in the algorithm description)
	        Return [] and append 4 and append 3 and append 2 and append 1

Do you see the pattern emerging?

Now, we only need to translate the pseudocode in real haskell code.
We'll use the concept of "pattern matching" to arrive at a simple implementation. Pattern matching simply means that Haskell will look at the arguments given to the function. Depending on what they are (which pattern they satisfy), different code will be executed.

The simplest part of our algorithm is when the `reverseList` function is given an empty list. In that case, we simply return the empty list.
Let's add the following code to our `first-steps.hs` file (only the first line):

    reverseList [ ] = []
    --           ^-- pattern	

Save the file and reload it in ghci, using the `:reload` command.
You can then try to call the function with an empty list as the argument: `reverseList []`, it should return an empty list.
What happens if you try to call the function with another list, such as `[1,2,3,4]`? You will get an error complaining about non-exhaustive patterns... That is because we only told Haskell what to do when the argument is an empty list, that was the pattern we provided (indicated by the arrow.
For fun, we could add a pattern for a list with only one or more elements:

    reverseList [] = []
	reverseList [Element] = [Element]
	reverseList [Element1, Element2] = [Element2, Element1]

You can load this code in ghci (`:reload`) and try it out, but it is obvious that this approach is not really scalable.
We need to find a way to complete steps 2 and 3 in our algorithm.

To split the list, we'll again use pattern matching. Haskell provides us with the `(x:xs)` pattern. This pattern splits the list in two parts: a head (x) and a tail (xs).
From here, it is easy to arrive at step 3, just call the reverseList function again on the tail of the list.
Adapt the code to look as follows:

    reverseList [] = []
	reverseList (x:xs) = reverseList xs ++ [x]

The second line splits the argument in a head and a tail, it then takes the tail and reverses it and finally appends the head. The head is between brackets because the append function takes 2 lists.
Now, just reload the file and try to reverse some lists:

    *Main> reverseList [1,2,3,4,5]
    [5,4,3,2,1]

The function even works with other data types, such as a list of strings:

    *Main> reverseList ["a","b","c","d","e"]
    ["e","d","c","b","a"]

Voila, we've reached our goal for today: lists have been inverted. More next time!

