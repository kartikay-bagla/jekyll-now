---
layout: post
title: Decisions Decisions But What If?
---

To make decisions, we must compare things. And to compare things, we need logic.

## Logical Operators

These operators return 1 or 0 based on the inputs recieved:

* `>` - The greater than operator: Returns `1` if the input on its left is greater than the one on its right. Otherwise returns `0`.
* `<` - The less than operator: Returns `1` if the input on its right is greater than the one on its left. Otherwise returns `0`.
* `>=` - The greater than or equal to operator: Returns `1` if the input on its left is greater than or equal to the one on its right. Otherwise returns `0`.
* `<=` - The less than or equal to operator: Returns `1` if the input on its right is greater than or equal to the one on its left. Otherwise returns `0`.
* `==` - The equal to operator: Returns `1` only if both inputs are the same. Otherwise it returns `0`.
* `!=` - The not equal to operator: Returns `1` only if both inputs are not the same. Otherwise it returns `0`.

Eg:

* `6 > 4` evaluates to 1.
* `6 < 6` evaluates to 1.
* `6 > 6` evaluates to 0.
* `6 >= 6` evaluates to 1.
* `6 == 6` evaluates to 1.
* `6 != 6` evaluates to 1.
* `6 == 4` evaluates to 0.

## The If-Else Statement

The If-Else statement is used as a conditional check, which means that a specific job
can be chosen to or not to be done depending on the outcome of a check.  
For example, you wear a raincoat if it rains and do not if it does not rain. Here the
action of wearing a raincoat takes place only in the event of rainfall.  
This statement is quite helpful in any programming language.  
The syntax for using if-else statement is:  

```c
if (the condition which will function as the check) {
    The job to be done in case the above condition is true
}
else {
    The alternative job to be performed in case the above condition is false
}
```

Note: The condition or the check is enclosed in round brackets i.e. () and the jobs to
be performed are enclosed in curly braces i.e. {}.  
An important thing to remember is that if only a single job is to be executed, curly
braces can be avoided. We will look into this point in the following examples.

### Examples

Write a program to check if 6 is an even number.

```c
#include <stdio.h>;

int main(){
    int n=6;

    if (n%2==0) {
        printf("6 is an Even Number");
    }
    else {
        printf("6 is not an even number");
    }

    return 0;
}
```

You can see that we have used the modulo operator in the check. If the modulo of integer n when divided by 2 is 0, the number is even as it is the defining property of even numbers.  
It means that if the remainder obtained on dividing a number by 2 is
zero, the number can be said to be even.

Since we have a single statement in this case, we can do this as well:

```c
#include <stdio.h>;

int main(){
    int n=6;

    if (n%2==0) printf("6 is an Even Number");
    else printf("6 is not an even number");

    return 0;
}
```

An **important thing** to notice is that in the conditional check, we have written that `(n%2==0)`. This is contradictory to our knowledge as we have always used a single equal `=` sign to represent the equality between two entities.  
But in programming languages, the single equal to operator i.e.(=) is known as the assignment operator. It is used to assign a value to a variable and not to prove the equality between two entities.  
(==) This is known as the equality operator and is used to prove the equality between two entities.

### The Ternatory Operator

This operator is used as a replacement for the if-else statement.  
Syntax:

```
(conditional check) ? job to be done if the check is true : job to be done if the check is false;
```

So our previous code could be written like this:

```c
(n%2==0) ? printf("6 is an Even Number") : printf("6 is not an even number");
```

## Multiple Checks

What if I wanted to check for 2 or more conditions? Like `if this and this are true: do this; else: do that;` or `if this or this are true: do this; else: do that;`  

### And Operator

This operator takes 2 inputs and returns 1 if both arguments are True or 0 if both arguments are False.  
It is written like this: `condition 1 && condition 2`

Here's an example:

```c
if (my_gpa < 2.0 && my_grade == "D") {
    printf("Bad");
}
else {
    printf("Good");
}
```

### Or Operator

This operator takes 2 inputs and returns 1 if any of the arguments are True or 0 if both arguments are False.  
It is written like this: `condition 1 || condition 2`

Here's an example:

```c
if (my_gpa > 8.0 || my_grade == "A") {
    printf("Good");
}
else {
    printf("Bad");
}
```

### Special Thanks To Kshitij

This post is written by my friend Kshitij who has decided to help me in this journey. So I'd like to thank him for his support and request you guys to do the same.

As always, if anything is unclear or if you need my help, you can contact me.