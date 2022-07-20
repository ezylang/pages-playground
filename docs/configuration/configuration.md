---
layout: default
title: Configuration
nav_order: 3
---

## Configuration

EvalEx can be configured through an _ExpressionConfiguration_ object, which can be passed as a
parameter to the _Expression_ constructor.

> **Warning:** The _ExpressionConfiguration_ is not thread safe, different expressions in different
> threads should
> not use the same configuration object.

Example usage, showing all default configuration values:

```java
ExpressionConfiguration configuration = ExpressionConfiguration.builder()
    .arraysAllowed(true)
    .dataAccessor(new MapBasedDataAccessor())
    .decimalPlacesRounding(ExpressionConfiguration.DECIMAL_PLACES_ROUNDING_UNLIMITED)
    .defaultConstants(ExpressionConfiguration.StandardConstants)
    .functionDictionary(ExpressionConfiguration.StandardFunctionsDictionary)
    .implicitMultiplicationAllowed(true)
    .mathContext(ExpressionConfiguration.DEFAULT_MATH_CONTEXT)
    .operatorDictionary(ExpressionConfiguration.StandardOperatorsDictionary)
    .powerOfPrecedence(OperatorIfc.OPERATOR_PRECEDENCE_POWER)
    .structuresAllowed(true)
    .build();

Expression expression = new Expression("2.128 + a", configuration);
```

### Arrays allowed

Specifies if the array index function is allowed (default is true). If set to false, the expression
will throw a _ParseException_, if the a '[' is encountered in the expression and also no operator or
function is defined for this character.

### Data Accessor

The Data Accessor is resposible for storing and retrieving variable values.

See chapter [Data Access](../customization/data_access.html) for details.

The default implementation is the _MapBasedDataAccessor_, which stores all variables in a
**case-insensitive** _Map_.

### Decimal Places Rounding

Specifies the amount of decimal places to round to in each operation or function.
See chapter [Precision, Scale and Rounding](../concepts/rounding.html) for details.

### Default Constants

Specifies the default constants that can be used i every expression as a _Map_ with the constant
name and _EvaluationValue_ as value.
See the reference chapter for a
list: [Default Constants](../references/references.html#default-constants)

### Function Dictionary

The function dictionary is used to look up the functions that are used in an expression.

See chapter [Function Dictionary](../customization/function_dictionary.html) for details.

The default implementation is the _MapBasedFunctionDictionary_, which stores all variables in a
**case-insensitive** _Map_.
