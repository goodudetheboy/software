# Guideline 15: Design for the Addition of Types or Operations

In the first section, the author points out the shortfalls of procedural programming in making code follow OCP. He shows a much better implementation of code using dynamic polymorphism. However, the DP solution is not without its flaw either: you can add classes easily, but you can't add operations as easy. This is a segway to the Visitor design pattern.

Lesson to take away from this example: You can't have your cake and eat it too. When considering between using dynamic polymorphism and procedural programming, here's what the author says:
> [...] either you can add types easily by fixing the number of operations or you can add operations easily by fixing the number of types.

You have to make a conscious decision about which kind of extension you want. Rule of thumbs:
- If you expect new types will be added, as opposed to operations -> OOP. This treats operations as a *closed* set and types as *open* set.
- If you expect new operations to be added -> procedural solution. This treats operations as an *open* set and types as *closed* set.

Interesting bits: this limitation only applies for dynamic polymorphism. Static polymorphism (using templates) is NOT affected. This is because both types and sets are available at compile time, so it's easier to manipulate (but I guess the catch is it's tricky).
- I was a bit confused about this at first, but Claude explains it well. Consider the `drawAllShapes()`. Dynamic polymorphism will only have `shape->draw()`, while you can do something like:
```
// Shapes is a vector of variants
using Shape = std::variant<Circle, Square>;
using Shapes = std::vector<Shape>;

void drawAllShapes(Shapes const& shapes) {
    for (auto const& shape : shapes) {
        std::visit(Draw{}, shape);
    }
}
```

