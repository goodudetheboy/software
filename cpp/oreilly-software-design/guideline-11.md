# Guideline 11: Understand the Purpose of Design Patterns

> Properties of a Design Pattern
>
> Definition: A design pattern has 4 things:
> 1. A name
> 2. An intent
> 3. An abstraction
> 4. Is proven

## A Design Pattern Has a Name

New patterns: Visitor, Strategy, Decorator

> Visitor (Design Pattern)
>
> Definition: Used when want to add more **operations** on a closed set of types. When new operations are added frequently but types don't change much, you use Visitor.

> Strategy (Design Pattern)
>
> Definition: Used to modify **behavior** and inject it from outside. When you want to make behavior a variation point i.e. you can swap in different "how" to reach the end goal of a behavior without changing the code that uses them, you use Strategy. AKA policy-based design

> Decorator (Design Pattern)
>
> Definition: Used to add more **responsibilities** to an object. Wrap existing objects to extend behavior without modifying.

## A Design Pattern Carries an Intent

A thing to take away from this section is design pattern is all about the general direction and not the implementation.

## A Design Pattern Introduces an Abstraction

DP helps to reduce dependencies by introducing abstraction, since it focuses on managing interaction between software entities and decoupling pieces of software.

Trivia: `std::make_unique()` is not a Factory Method DP, even though it's called factory function. The reason is that, even though it will produce us a pointer for whatever object we want, it all returns a `std::unique_ptr`, which is not what the Factory Method is intended to produce (I think it would have to produce a named pointer class specific to the object if this were to turn into a DP). This is called an **Implementation Pattern**. This is thus part of the Implementation Details level and not the Software Design level.

## A Design Pattern Has Been Proven


