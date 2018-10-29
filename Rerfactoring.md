# Refactoring Techniques

Main reference: [Refactoring Guru](https://refactoring.guru/refactoring/techniques/composing-methods)

## **Composing Methods**

Make your methods healthy and easy to maintain. Much of refactoring is devoted to correctly composing methods. In most cases, excessively long methods are the root of all evil. The vagaries of code inside these methods conceal the execution logic and make the method extremely hard to understand – and even harder to change.

## **Moving Features between Objects**

Even if you have distributed functionality among different classes in a less-than-perfect way, there is still hope.

These refactoring techniques show how to safely move functionality between classes, create new classes, and hide implementation details from public access.

## **Simplifying Conditional Expressions**

Conditionals tend to get more and more complicated in their logic over time, and there are yet more techniques to combat this as well.

## **Simplifying Method Calls**

These techniques make method calls simpler and easier to understand. This, in turn, simplifies the interfaces for interaction between classes.

## **Dealing with Generalization**

Abstraction has its own group of refactoring techniques, primarily associated with moving functionality along the class inheritance hierarchy, creating new classes and interfaces, and replacing inheritance with delegation and vice versa.