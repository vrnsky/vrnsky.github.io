---
title: Stop writing code inside main method
type: blog
sidebar:
  open: true
date: 2020-11-29
---

### Introduction
Greetings to everyone who reads this post! Due to my work, I often run into novice programmers and look at their code. Sometimes it is beautiful, sometimes not, but I understand that a person learns, and the further he masters the best practices and technologies, the better his code becomes. But I would still like to pay some attention
to such a simple task that almost all novice programmers face — writing a calculator.

![Calculator image](calculator.png)

Here’s what novice programmers write:
```java {filename="Calculator.java"}
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        int sum = 0;
        int number1 = 0, number2 = 0;
        boolean correct = true;
        char operation1;
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter first number:");
        while (!sc.hasNextInt()) {
            System.out.println("Sorry, it is not a digit. Try again, please");
            sc.next();
        }
        number1 = sc.nextInt();
        System.out.println("Thanks! You entered number: " + number1);
        System.out.println("Enter a number:");
        while (!sc.hasNextInt()) {
            System.out.println("It is not a digit. Try again");
            sc.next();
        }
            number2 = sc.nextInt();
        System.out.println("Thanks! It is a digit " + number2);
        do {
            correct = true;
            System.out.println("What would you like to do? + - / *");
            operation1 = sc.next().charAt(0);
            switch (operation1) {
                case '+':
                    sum = number1 + number2;
                    System.out.println("Sum of this two equals to " + sum);
                    break;
                case '-':
                    sum = number1 - number2;
                    System.out.println("The difference between equals to: " + sum);
                    break;
                case '/':
                    if (number2 != 0) {
                        sum = number1 / number2;
                        System.out.println("Divied equals to: " + sum);
                    } else {
                        System.out.println("Divided by zero is not allowed.");
                        correct = false;
                    }
                    break;
                case '*':
                    sum = number1 * number2;
                    System.out.println("Multiplication of this two: " + sum);
                    break;
                default:
                    System.out.println("Unknow operation");
                    correct = false;
                    break;
            }
            } while (correct != true);
        }
    }
```

What problems do you see in this code? I see the following problems
- Everything is written in the main method, and certainly represents more than 10 lines
- There are no tests for this code, that is, there is no confidence that it will work correctly
- Structural programming style — the switch statement encourages this
- Using the Scanner, but it can be forgiven because it has convenient methods for getting numbers right away.

### Access full article
{{< cards >}}
{{< card icon="medium" title="Read full article on Medium" link="https://medium.com/@vrnsky/stop-writing-code-inside-main-method-5747458f9191" >}}
{{< /cards >}}