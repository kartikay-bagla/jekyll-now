---
layout: post
title: Getting Started With C
---

This is a quick introduction to the C Language. Supposedly in the syllabus of 1st year DTU students.
And since a lot of them didn't know programming, I thought it would be a good oppurtunity to help
everyone out as well as practice my own skills. So lets get started.

## What is Programming?

It is simply the method of creating instructions for something or someone to follow.  
And a program is a set of well defined instructions.
Even a cooking recipe is a program.

## What is C?

C is a programming language. Simple enough.  
But apparently if you're studying for the exams here, it was developed by AT&T's Bell Laboratories of USA in 1972 by Dennis Ritchie.

## Time to Get Started With C

### Some Terminology

* Constants - Anything that will remain constant throughout a program.
* Variables - Something that will change itself is called a variable.
* Keywords - These are basically words that C uses to designate special stuff.
* Function - A set of instructions.
* Compiler - Converts your instructions into machine readable format.

### Some Basic Rules

* Each instruction is a separate statement.
* Every statement should end with a `;`.

### Hello World

Starting with the cliche of computer science, Hello World.

```c
#include <stdio.h>

int main()
{
    printf("Hello World");
    return 0;
}
```

I'll explain the code first and then tell you how to run it.

* `#include <stdio.h>` tells the computer to Include a file called 'stdio.h' which stands for Standard Input Output. It has functions which help in taking input from the user and sending output to the user. Eg. `printf`.

* `int main()` is a function declaration. A function is nothing but a set of statements. The `int` tells the computer that `main` will give back an Integer value. The parenthesis i.e. `()` are added after every function (I will expand on this later). But just understand this - `int main()` is the main part of your code.

* `{ }` are curly braces in which blocks of code are stored. So the set of statements for `int main()` are inside these brackets.

* `printf("Hello World");` is also a function. And it is used to print things to our screen. In this case it is "Hello World". This function came from the file `stdio.h`. The semicolon ( `;` ) at the end signifies that this statement is over. And is generally put after every statement finishes.

* `return 0;` tells the computer that the `main` function will return `0`. Think of 0 as an error code. If its a 0, everthing went fine. But if its not, something went wrong somewhere.

Now to run the code.

* Download and Install CodeBlocks with MinGW from [here](http://sourceforge.net/projects/codeblocks/files/Binaries/17.12/Windows/codeblocks-17.12mingw-setup.exe).
* Open CodeBlocks and choose "Create a New Project" and then choose "Console Application" as we will be running our code in the console only.
* Follow the wizard and choose C as your language (not C++) and set the title to "Hello World" or whatever you want. Leave everything as is and finish the wizard.
* Towards you left, click on the plus (`+`) button near the "Sources" folder and open `main.c` file.
* Delete everything inside the file (though it is very similar to what I've written along with some extra stuff) and then copy paste or type the above code into the `main.c` file. Now press the Build & Run button on the top (it has a gear and a play icon) to run it.
* You'll see a black console pop-up with some text displaying Hello World. Yay. Press enter to close the window.

That's it. You did it. You're a programmer now. Just kidding. But you're on your way to become one.

The speed of more posts like these will depend on the response I get, so let me know what you think about this kind of post.