# Guideline 8: Understand the Semantic Requirements of Overload Sets

LSP not only applies to dynamic and static polymorphism, but it also applies to **function overloading**.

- Huh? That's crazy bro

## Power of Free Functions

> Overload set
>
> Definition: Set of free functions that share same name, and together form a compile-time abstraction.

What I'm reading in this chapter is the author is really whoring out for free functions. Here's his reasoning:
1. Non-intrusive (OCP)
2. Reduce coupling (SRP)
3. Easier to test
4. Foundation of STL

He does criticize `std::string` and is basically calling it the red headed stepchild of the STL lol.

## Problems of Free Functions

As much as free functions are powerful, it is a double-edged knife.

> All of this power can only work if a set of overload functions adheres to a set of rules and certain expectations.

He illustrates this quite well though, with the `swap` function of a `Widget` with two members `i` and `j`. The `swap()` only swap the `i`. This is showing that the code is following the behavioral expectations of a `swap()` function.



