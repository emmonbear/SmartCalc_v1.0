# SmartCalc v1.0

Implementation of SmartCalc v1.0.

The russian version of the task can be found in the repository.

## Contents

1. [Project Description](#project-description)
2. [Engineering calculator](#engineering-calculator)
3. [Credit calculator](#credit-calculator)
4. [Deposit calculator](#deposit-calculator)


## Project Description

This project is implemented in C programming language using structural approach. The project is an extended version of a regular calculator, which can be found in standard applications of every operating system. In addition to basic arithmetic operations like plus-minus and multiply-divide, the calculator calculates arithmetic expressions taking into account priorities, as well as works with some mathematical functions (sine, cosine, logarithm, etc.). In addition to calculating expressions, the calculator also supports using the _x_ variable and plotting the graph of the corresponding function. The calculator has credit and deposit modes.

## Engineering calculator

- The SmartCalc v1.0 program must be implemented:
The program is developed in C11 standard C language using gcc compiler, additional libraries and QT modules
- The program code is located in the src folder 
- The program is built using a Makefile with the standard set of targets for GNU programs: all, install, uninstall, clean, dvi, dist, test, gcov_report. The installation is done on the desktop
- The program is developed according to the principles of structural programming
- The code is designed in accordance with Google Style
- Unit-tests of modules related to expression calculation are covered with the help of Check library.
- The implementation of the graphical user interface is based on Qt 
- Both integers and real numbers written with a period can be input to the program. Input in exponential notation is provided
- Calculation is performed after a complete input of the calculated expression and pressing the `=` symbol.
- Calculation of arbitrary bracketed arithmetic expressions in infix notation
- Calculation of arbitrary bracketed arithmetic expressions in infix notation with substitution of the _x_ variable value as a number.
- Graphing a function defined by an expression in infix notation with the _x_ variable (with coordinate axes, marking the scale used and a grid with adaptive step).
- The user has the ability to change the scale
- The definition area and value area of functions are limited by numbers from -1000000 to 1000000.
- In order to draw graphs of a function, it is necessary to additionally specify the displayed definition area and value area.
- Checkable accuracy of the fractional part is 7 decimal places.
- The user can enter up to 255 characters
- Stapled arithmetic expressions in infix notation support the following arithmetic operations and mathematical functions:

    - **Arithmetic operators**:

      | Operator name | Infix notation <br /> (Classic) | Prefix notation <br /> (Polish notation) |  Postfix notation <br /> (Reverse Polish notation) |
      | --------- | ------ | ------ | ------ |
      | Brackets | (a + b) | (+ a b) | a b + |
      | Addition | a + b | + a b | a b + |
      | Subtraction | a - b | - a b | a b - |
      | Multiplication | a * b | * a b | a b * |
      | Division | a / b | / a b | a b \ |
      | Power | a ^ b | ^ a b | a b ^ |
      | Modulus | a mod b | mod a b | a b mod |
      | Unary plus | +a | +a | a+ |
      | Unary minus | -a | -a | a- |

      >the multiplication operator can work with the `*` sign omitted

    - **Functions**:
  
      | Function description | Function |
      | ------ | ------ |
      | Computes cosine | cos(x) |
      | Computes sine | sin(x) |
      | Computes tangent | tan(x) |
      | Computes arc cosine | acos(x) |
      | Computes arc sine | asin(x) |
      | Computes arc tangent | atan(x) |
      | Computes square root | sqrt(x) |
      | Computes natural logarithm | ln(x) |
      | Computes common logarithm | log(x) |


## Credit calculator

A special mode "credit calculator" is available
 - Input: total loan amount, term, interest rate, type (annuity, differentiated)
 - Output: monthly payment, loan overpayment, total repayment


## Deposit calculator

A special mode "deposit yield calculator" is provided for
 - Input: deposit amount, deposit term, interest rate, tax rate, payment periodicity, interest capitalization, list of replenishments, list of partial withdrawals
 - Exit: accrued interest, tax amount, amount on deposit by the end of the term

