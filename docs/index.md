---
layout: default
title: Welcome
nav_order: 1
---

# EvalEx - Java Expression Evaluator

EvalEx is a handy expression evaluator for Java, that allows to parse and evaluate expression
strings.

Key Features:

- Supports string, boolean and numerical, array and structure expressions and variables.
- Array and structure support: Arrays and structures can be mixed, building arbitrary data
  structures.
- Uses BigDecimal for numerical calculations.
- MathContext and number of decimal places can be configured, with automatic rounding.
- No dependencies to external libraries.
- Easy integration into existing systems to access data.
- Standard boolean and mathematical operators.
- Standard basic mathematical and boolean functions.
- Custom functions and operators can be added.
- Functions can be defined with a variable number of arguments (see MIN, MAX and SUM functions).
- Supports for hexadecimal numbers and scientific notations of numbers.
- Supports implicit multiplication, e.g. (a+b)(a-b) or 2(x-y) which equals to (a+b)\*(a-b) or 2\*(
  x-y)
- Lazy evaluation of function parameters, only if needed (see the IF function).

### Examples

A simple example, that shows how it works in general:

```java
Expression expression = new Expression("1 + 2 / (4 * SQRT(4))");

EvaluationValue result = expression.evaluate();

System.out.println(result.getNumberValue()); // prints 1.25
```

Of course, variables can be specified in the expression and their values can be passed for
evaluation:

```java
Expression expression = new Expression("(a + b) * (a - b)");

EvaluationValue result = expression
    .with("a", 3.5)
    .and("b", 2.5)
    .evaluate();

System.out.println(result.getNumberValue()); // prints 6.00
```

Boolean expressions produce a boolean result:

```java
Expression expression = new Expression("level > 2 || level <= 0");

EvaluationValue result = expression
    .with("level", 3.5)
    .evaluate();

System.out.println(result.getBooleanValue()); // prints true
```

Like in Java, strings and text can be mixed:

```java
Expression expression = new Expression("\"Hello \" + name + \", you are \" + age")
    .with("name","Frank")
    .and("age",38);

System.out.println(expression.evaluate().getStringValue()); // prints Hello Frank, you are 38
```

Arrays are supported and can be passed as Java _Lists_:

```java
Expression expression = new Expression("values[i-1] * factors[i-1]");

EvaluationValue result = expression
    .with("values", List.of(2, 3, 4))
    .and("factors", List.of(2, 4, 6))
    .and("i", 1)
    .evaluate();

System.out.println(result.getNumberValue()); // prints 4
```

Structures are supported and can be passed as Java _Maps_.
Arrays and Structures can be combined to build arbitrary data structures:

```java
Map<String, Object> order = new HashMap<>();
order.put("id", 12345);
order.put("name", "Mary");

Map<String, Object> position = new HashMap<>();
position.put("article", 3114);
position.put("amount", 3);
position.put("price", new BigDecimal("14.95"));

order.put("positions", List.of(position));

Expression expression = new Expression("order.positions[x].amount * order.positions[x].price")
    .with("order", order)
    .and("x", 0);

BigDecimal result = expression.evaluate().getNumberValue();

System.out.println(result); // prints 44.85
```
