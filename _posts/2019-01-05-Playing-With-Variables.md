---
layout: post
title: Playing With Variables
---

Last time we briefly touched upon the C Language. This time, I'm gonna properly introduce Variables, Constants, Keywords, the printf function and some basic arithmetic!  
In simple terms, constants are entities whose values don't change over time while the values of variables can change.

## Variables

Values are stored in the computer's memory, to make their usage easier, we give names to memory locations we want to use. But since the contents of the memory location may change, we call the names for locations as Variables.  

Let us create a variable x = 6. Now 6 is stored in some memory location and x is the name we use to access the location. Now if we do x = 3. Then the data in the memory location would change from 6 to 3 while the location and name used to access it remains the same.

## Constants

Now there are 3 types of primary constants in C i.e. Integer constant, Real constant and Character constant.

### Integer Constant

* It is an integer (wow!)
* It cannot have decimal point.
* Can be either positive or negative
* Ranges from -32768 to 32768 (for exams)

### Real Constants/Floating Point Constants

* Its pretty much an integer but with decimal and larger range.
* -3.4 x 10^38 to 3.4 x 10^38 is its range.
* But if we need more precision, we can use a `double`. It is same as a floating point number, but with an increased range i.e. 2.3 x 10^-308 to 1.7 x 10^308.

### Character Constant

* Its a single symbol(alphabet/digit/special symbols) enclosed within single inverted commas like "A" or "1" or "~" etc

## Creating Variable Names

* It can be any combination of 1-31 alphabets, digits and underscores.
* The first character has to be an alphabet or underscore.

Now C is very picky and needs you to tell it everything. You have to tell it what kind of information will the variable store when you create (or declare) the variable.

* For integers, it is `int`.
* For real numbers, it is `float` (or `double`).
* For single-characters, it is `char`.

So if I wanted a variable named my_gpa to store my GPA for me. I'd declare it like this: `float my_gpa;` (always remember the semicolon at the end of every statement.)  
Now if I wanted to assign a value to this variable, I use the assignment operator i.e. `=` like this `my_gpa = 2.0;` (because I'm smart).  
But this amounts to 2 lines:

```c
float my_gpa;
my_money = 2.0;
```

Surely there is a faster way, and yes there is: `float my_gpa = 2.0;`.  
Now if it was a character: `char my_grade = 'A'` (never gonna happen).  
Or if it was an integer: `my_money = 10;` (because I'm broke).

## Keywords

These are nothing but special names that can't be used as variable names because C is already using them for something else. There are only 32 keywords in C.

All | Keywords | In | C |
--- | --- | --- | --- |
auto | double | int | struct |
break | else | long | switch |
case | enum | register | typedef |
char | extern | return | union |
continue | for | signed | void |
do | if | static | while |
default | goto | sizeof | volatile |
const | float | short | unsigned |

## What is printf?

It is an output function used to print output on the console. And is contained in the `stdio` library.  
The general form of printf looks like this:  
`printf("<format string>", <list of variables>");`.  

The format string can contain:

* `%f` for printing real values.
* `%d` for printing integer values.
* `%c` for printing character values.
* And any other characters.

While the list of variables contain the variables to display based on the order in the string.

So if I want to display something like `I have 9.8 GPA and A grade.` where 9.8 is a float and A is a char stored in the names gpa and grade, I'd write something like

```c
#include <stdio.h>

int main()
{
    float gpa = 9.8;
    char grade = 'A';
    printf("I have %f GPA and %c grade", gpa, grade);
    return 0;
}
```

Try replacing the hello world code with this, or create a new project.

## Onto Arithmetic

### Assignment

The most important operation is assignment i.e. =.  
Eg `int x = 25` means that x will be an integer and is assigned a value of 25.  
The left hand side is assigned the value on the right hand side.

### Basic Operators

The basic operations are +, - , *, / i.e. addition, subtraction, multiplication, division.

```c
#include <stdio.h>
int main()
{
    int x = 25;
    int y = 5;
    int sum = x+y;
    int diff = x-y;
    int mul = x*y;
    int div = x/y

    printf("%d + %d = %d\n", x, y, sum);
    printf("%d - %d = %d\n", x, y, diff);
    printf("%d * %d = %d\n", x, y, mul);
    printf("%d / %d = %d\n", x, y, div);

    return 0;
}
```

The `\n` at the end of the format string simply tells the computer to move to the next line while printing.

The expected output is:

```
25 + 5 = 30
25 - 5 = 20
25 * 5 = 125
25 / 5 = 5
```

Now what if I changed y to 4?  
We get this:

```
25 + 4 = 29
25 - 4 = 21
25 * 4 = 100
25 / 4 = 6
```

The last line is `25 / 4 = 6` instead of `6.25`.  
Since we divided an integer by an integer, the result will also be an integer. But if we change either x or y to a float and let the div variable take floats by declaring it as a float as well, we get the correct output.

```c
#include <stdio.h>
int main()
{
    float x = 25;
    float y = 4.0;
    float sum = x+y;
    float diff = x-y;
    float mul = x*y;
    float div = x/y

    printf("%f + %f = %f\n", x, y, sum);
    printf("%f - %f = %f\n", x, y, diff);
    printf("%f * %f = %f\n", x, y, mul);
    printf("%f / %f = %f\n", x, y, div);

    return 0;
}
```

Gives

```
25.0 + 4.0 = 29.0
25.0 - 4.0 = 21.0
25.0 * 4.0 = 100.0
25.0 / 4.0 = 6.25
```

### Modulus Operator

There is one more operator called the Modulus operator (%).
10 % 3 will give you 1 i.e. the remainder when 10 is divided by 3.

Parenthesis are also allowed for more complex expressions like:

```c
float x = 10.0, y = 5.0, z = 2.0;
float output = (x + y) / z
```

### The order/priority of execution

Operators are executed in this order:

* /, *, %
* +, -
* =

### Conversions between integers and floats

* Arithmetic operation between an integer and an integer always gives an integer.
* An operation between real and real always gives real.
* An operation between real and integer always gives real. The integer is first converted to real and the operation is completed.
* But when a float is assigned to an int, it will be converted to int automatically.

Eg:

```c
int s;
float a = 10.2;
int d = 5;
float f;

f = a * d;
s = a * d;
```

Now you should be able to write a program to add/subtract/multiply/divide 2 (or as many as you want) numbers.

Next time, I'll start with Decision Statements where we get to see some actual logic being applied.

Let me know if something was unclear or if something was missing (or maybe just say a hi ;).