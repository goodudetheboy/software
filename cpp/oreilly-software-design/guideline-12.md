# Guideline 12: Beware of Design Pattern Misconceptions

## DPs are NOT a Goal

Overusing DP ain't cool. Not everything needs design patterns. NOT A GOAL!!!

Basically, this is a means to an end: to design good software and to decrease complexity. To spell it out, the goals are:
- Code becomes simpler
- More comprehensible
- Easier to change and maintain

## DPs are NOT about Implementation Details

DPs are about the IDEA behind them, not what their manifestions are.

Book example: Drawing a given shape. Drawing a class `Circle`:

```
class Circle() {
	public:
		void draw();
}
```

If you implemented directly like this then you're coupling `draw()` to a specific drawing library, which you generally don't want since this breaks SRP "a class should only has one reason to change" and changing drawing library isn't fit for `Circle()`.

As such, you would introduce the Strategy DP in here:

```

[Shape | draw()]<>----Strategy---->[DrawStrategy | virtual draw() = 0]
												 ^
												 |
												 |
										|-------------------|
										|					|		
			[OpenGLStrategy | draw(Shape) override]			[TestStrategy | draw(Shape) override]
```

Where you would introduce a `DrawStrategy` to be invoked by `draw()`. This `DrawStrategy` is used like so when we use a `Shape`:
```
auto strategy = std::make_unique<OpenGLStrategy>(...);

Circle circle(4.2, std::move(strategy));
circle.draw(...);
```

NOTE: Wow, so the pattern I see in the tsloadfxr where the previous guy was developing IS the strategy pattern. He implemented an interface where this is then passed into the main Loader class for processing. Makes it really easy to test pretty interesting. Now THAT's what I call a good design pattern usage.

Strategy is a class GoF design patterns, often required a base class. You may think this is restricted to object oriented design? WRONG. For example:
```
template< typename DrawStrategy >
class Circle {
public:
	void draw(...);
}
```

With this template, you can EASILY swap out your desired strategy.


## Design Patterns are NOT limited to OOP or Dynamic Polymorphism

Example: `std::accumulate()` you can swap in your own operator by specifying it in the function params.

Another example: `std::vector` and `std::set` all has a `class Allocator = std::allocator<Key>` in their function parameters, allowing you to specify a way to allocate memory yourself.

Disclaimer: The author notes that while it's true that DPs are not limited to OOP, its purpose is to solve many problems coming from OOP. There are also DPs focused on funcitonal programming or generic programming.

> While most design patterns are not paradigm centric and their intention can be used in a variety of implementations, some are more specific.

At the end of the day, DP are not limited to one way of programming. Its intent is to decouple software entities in a specific way.






