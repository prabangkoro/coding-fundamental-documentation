# **Composing Methods**

Make your methods healthy and easy to maintain. Much of refactoring is devoted to correctly composing methods. In most cases, excessively long methods are the root of all evil. The vagaries of code inside these methods conceal the execution logic and make the method extremely hard to understand – and even harder to change.

## **Extract Method**

### Problem

You have a code fragment that can be grouped together.

```java
void printOwing() {
  printBanner();

  //print details
  System.out.println("name: " + name);
  System.out.println("amount: " + getOutstanding());
}
```

### Solution

Move this code to a separate new method (or function) and replace the old code with a call to the method.

```java
void printOwing() {
  printBanner();
  printDetails(getOutstanding());
}

void printDetails(double outstanding) {
  System.out.println("name: " + name);
  System.out.println("amount: " + outstanding);
}
```

### Why refactoring???

The more lines found in a method, the harder it is to figure out what the method does. This is the main reason for this refactoring.

Besides eliminating rough edges in your code, extracting methods is also a step in many other refactoring approaches.

### Benefits

* More readable code! Be sure to give the new method a name that describes the method's purpose: `createOrder()`, `renderCustomerInfo()`, etc.
* Less code duplication. Often the code that is found in a method can be reused in other places in your program. So you can replace duplicates with calls to your new method.
* Isolates independent parts of code, meaning that errors are less likely (such as if the wrong variable is modified).

## **Inline Methods**

### Problem

When method body is more obvious than method name itself, use this technique:

```java
class PizzaDelivery {
  //...
  int getRating() {
    return moreThanFiveLateDeliveries() ? 2 : 1;
  }
  boolean moreThanFiveLateDeliveries() {
    return numberOfLateDeliveries > 5;
  }
}
```

### Solution

Replace calls to the method with the method's content and delete the method itself.

```java
class PizzaDelivery {
  //...
  int getRating() {
    return numberOfLateDeliveries > 5 ? 2 : 1;
  }
}
```

### Why refactoring???

A method simply delegates to another method. In itself, this delegation is no problem. But when there are many such methods, they become a confusing tangle that is hard to sort through.

Often methods are not too short originally, but become that way as changes are made to the program. So don't be shy about getting rid of methods that have outlived their use.

### Benefit

By minimizing the number of unneeded methods, you make the code more straightforward.