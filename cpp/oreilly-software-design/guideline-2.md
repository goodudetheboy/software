## Guideline 2: Design for Change

### Separation of Concerns

The idea is to make changes as easy as possible once code is written down

> System that are broken up into small, well-named, understandable pieces enabled faster work

> Orthogonality (software)
>
> Definition: The notion that changes in a component X would affect nothing to a component Y in software design

Cohesion is mentioned here also, and the idea is that splitting up a highly cohesive software components increase a chance for increased coupling and decreased readability

Which leads the S in SOLID: **Single-Responsiblity Principle**

- Separate things that change for different reasons

### Problems with the given `Document` class in the book

1. exportToJSON(): since this class is pure virtual, this must be implemented in the child classes. Most likely will use external dependencies, and now suddenly child classes are depending on an external dependency for no reason rather than bad design.
	- This makes the derived classes **artificically independent** on the JSON libraries.

2. Output type of exportToJson() might reflect bespoke implementation choices of a specific library. If we decide to move libraries later, god bless we have to drill down child classes too.

3. serialize(): This function is setup for derived classes to depend on the global decisions on how documents are serialized: What formats do we use? Pdf? Word?

**This makes `Document` a ill-designed class**

### Logical vs Physical Coupling

There's also another problem with the curren design. An `User` class logically depends on the `Document` class, but since `Document` has a physical dependency on external JSON or serialization library, there's also the **transitive** dependency of the `User` on these libraries that are higher ups too. Pretty sucks huh.

### High- vs Low-Level Architecture

> High vs Low
>
> Definition: As defined in the book,  high level refers to stable parts of our architecture, while low level refers to aspects that change more often or more malleable.

The best way to solve this problem is to extract the two extractToJson() and serialize() function from the `Document` class and create its own class on the same level as the `User` class. When we need to make change to the Serialize class, we only need to make changes in one place and relinked only in that place.

### Don't Repeat Yourself

Core idea: Just as much as a file should have single responsibility, a responsiblity shouldn't be in multiple files either.

We should not design such that key information appears in multiple places, but rather only in one place so we can make changes later easier.

### Avoid Premature Separation of Concerns

> Don't try to achieve SOLID, use SOLID to achieve maintainability

These principles should not be considered goals, but rather only tools. I guess what they are trying to get it here is that apply this when necesssary, not before necessity arises. "It can be very counter productive to separate entities without a clear idea about what kind of change will affect you"

> YAGNI Principle
>
> Definition: You Aren't Gonna Need It!!!

Note: One aspect of easily changing things is that need unit tests in place that give confirmation that change did not break expected behavior

Two things to keep in mind:
- Change is expected in *soft*ware
- Separation of concerns and minimization of duplicates will get you far with software changeability
