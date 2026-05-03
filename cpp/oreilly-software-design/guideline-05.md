# Guideline 5: Design For Extension

A software that can no longer add feature is a dead software.

## Open-Closed Principle

Supposed you have a `Document` class, and you have a `PDF` and `Word` a child of that class. You have a `serialize()`, whereby you know what document it is by having an enum `DocumentType`. That's not good, because when you want to (eventually) add a `XML` file, you would have to extend the `DocumentType` enum.

But this change gonna make all OTHERS recompile _at least_. This is WRONG.

The ideal situation is `PDF` and `Word` has to be entirely unaware of the new extension `XML` - no hearing, no feeling, not even a recompilation.

This is the violation of the Open-Closed Principle.

> Open-Closed Principle
>
> Def: Software artifacts (classes, modules, functions, etc.) should be open for extension, but closed for modification.

Extension should be easy (best case is just adding new code) without having to modify existing code.

In the above scenario, we would just need to add the new code for `XML`, and that should be the end of the day.

Right thing to do here? Separate concerns. We split up the serialization in another `Serialization` class, and ba da bing ba da bum, you have a nice chart in figure 1-6.

One important thing to note here about the author's OCP:

> OCP [...] advises that we should not have to modify existing code on same architectural level or higher levels. However, there is no way you can control or prevent modifications on the lower levels.

Pretty interesting, since his own design has `DocumentType` in `Seriailization`, which is in a lower level that PDF and Word, and that 100% checks out for me. The idea is that the lower level is more malleable, and also because the lower level depends on the higher level, so it somewhat be affected. Yeah the defintion above is definitely a bit lacking above.

### OCP vs SRP

Some people group these two principles together simply because it achieves somewhat the same objective. The author's argument to separate this:

> OCP seems to be more about the awareness of the extensions and conscious decisions about extensions than the SRP.

But again, "it depends!".

Lesson: extensibility should be explicity thought about when designing software.

## Compile-Time Extensibility

Extensibility should not only be heavily considered during runtime polymorphism, but also compile time.

`std::swap()` is designed as a **customization point**.

> Customization point
>
> Def: Place in exisiting code that's intentionally designed to let you plug in your own behavior, without modifying that existing code.

Three main forms in C++:

1. Function overloading: `std::swap()` - can provide your own swap in your namespace.
2. Templates: `std::find()` and `std::find_if()` - let you pass own iterator types and predicates.
3. Template specialization: `std::hash` - let you specialize it for own type without touching any existing code.

## Avoid Premature Design for Extension

I shall not prematurely design for extensibility. Remember the YAGNI: if I do not know how my code will grow, patiently wait, instead of anticipating an unrealistic future.















