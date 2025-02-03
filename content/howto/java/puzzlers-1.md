---
title: Puzzlers 1
type: docs
sidebar:
  open: true
tags:
  - java
comments: true
---

### Puzzler # 1.1
What is output of this code?
```java {filename="Puzzler1.java"}
public class Puzzler1 {
  public static void main(String[] args) {
    System.out.println(2.00 - 1.90)
  }
}
```
{{% details title="Answer" closed="true" %}}
The output of this code will be `0.09999999999999998`

This might seem surprising since 2.00 - 1.90 should be equal to 0.10, but this is class example
of floating-point arithmetic imprecsion. Here's why this happens:

1. In computers, sstems store floating-point numbers in binary (base - 2) format, but they represent decimals like 1.90 in base 10.
2. Many decimal numbers cannot be exactly represented in binary floating-point format. It's like how 1/3 cannot be exactly represented in decimal format.
3. When you convert 1.90 to binary floating-point, it is stored as very close approximation, but not exactly 1.90
4. This small imprecision cause the result to differ from 0.10 by small amount.

If you need exact decimal arithmetic in Java, you should use the BigDecimal class instead:
```java {filename="Puzzler1.java"}
import java.math.BigDecimal;

public class Puzzler1 {
  public static void main(String[] args) {
    BigDecimal a = new BigDecimal("2.00");
    BigDecimal b = new BigDecimal("1.90");
    System.out.println(a.subtract(b));  // Outputs: 0.10
  }
}
```
{{% /details %}}

### Puzzler 1.2
