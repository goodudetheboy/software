# Guideline 6: Adhere to the Expected Behavior of Abstractions

Building abstractions is difficult.

## Liskov Substitution Principle

The `L` in `SOLID`. Concerned with *bevahioral subtyping*.

> Liskov Substitution Principle
>
> Definition: Let $\phi(x)$ be a property provable about objects $x$ of type $T$. Then $\phi(y)$ should be true for objects $y$ of type $S$ where $S$ is a subtype of $T$.

IS-A relationship basically.

From my interpretation, I think this means that properties of parents should be true also for the children.

### Properties

1. Preconditions cannot be strengthened in a subtype

2. Postconditions cannot be weakened in a subtype

3. Function return types in a subtype must be covariant

4. Function parameters in a subtype must be contravariant
  - subtype method can accept a parameter that has a broader type than those accepted by the supertype method.
  - Not supported in C++ though

5. Invariants of the super type must be preserved in a subtype

## Criticisms

Comments on **Behavioral subtyping**: "Anywhere you use a base type, you should be able to swap in a subtype and nothing should break or surprise you".


