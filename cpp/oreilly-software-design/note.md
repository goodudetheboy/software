# O'Reilly - C++ Software Design

## Chapter 1

### Guideline 1: Understand the Importance of Software Design

- Treat software design as essential part of writing software
- Focus less on C++ features and more on the design
- Avoid unnecessary coupling and deps to make software more adaptable to changes
- Software design is an art of managing deps and abstraction
- Consider boundary between software design and architecture as FLUID

### Guideline 2: Design for Change

#### Separation of Concerns

The idea is to make changes as easy as possible once code is written down

> System that are broken up into small, well-named, understandable pieces enabled faster work

> Orthogonality (software)
>
> Definition: The notion that changes in a component X would affect nothing to a component Y in software design

Cohesion is mentioned here also, and the idea is that splitting up a highly cohesive software components increase a chance for increased coupling and decreased readability

Which leads the S in SOLID: **Single-Responsiblity Principle**

- Separate things that change for different reasons

#### Problems with the given `Document` class in the book

1. exportToJSON(): since this class is pure virtual, this must be implemented in the child classes. Most likely will use external dependencies, and now suddenly child classes are depending on an external dependency for no reason rather than bad design.
	- This makes the derived classes **artificically independent** on the JSON libraries.

2. Output type of exportToJson() might reflect bespoke implementation choices of a specific library. If we decide to move libraries later, god bless we have to drill down child classes too.

3. serialize(): This function is setup for derived classes to depend on the global decisions on how documents are serialized: What formats do we use? Pdf? Word?

**This makes `Document` a ill-designed class**

