[i# Guideline 9: Pay Attention to the Ownership of Abstractions

## Dependency Inversion Princple

Quotes:
> The most flexible systems are those in which source code dependencies refer only to abstractions, not to concretions

> Dependency Inversion Principle (DIP)
>
> Definition: The D in SOLID. The principle states that, for the sake of dependencies, you should depend on abstractions instead of concrete types or implementation details.

```
[Transaction] <= [Deposit], [Withdrawal], [Transfer]

====================Architectural Boundaries===========

[Deposit], [Withdrawal], [Transfer] <= [UI]

```

Regarding the ATM example above, even after adding the new abstraction layers between the UI and the data classes, we still haven't properly done DIP yet. The dependency inversion here is only **local inversion of dependencies**.


```
[Transaction] <= [Deposit], [Withdrawal], [Transfer]

====================Architectural Boundaries===========

[DepositUI] <= [Deposit]
[WithdrawalUI] <= [Withdrawl]
[TransferUI] <= [Transfer]


[DepositUI], [WithdrawalUI], [TransferUI] <= [UI]
```
	
As expressed by the author:

> it is not enough to just introduce an abstraction [...] but also where to introduce the abstraction.

Two points to follow:
1. High-level modules should not depend on low-level modules. Both should depend on abstractions
2. Abstractions should not depend on details. Details should depend on abstractions.

So to solve the above problem, we have to move the three new UI abstraction classes up above higher the architectural layers, to be in the roughly same level as the data classes.

```
[Transaction] <= [Deposit], [Withdrawal], [Transfer]

[DepositUI] <= [Deposit]
[WithdrawalUI] <= [Withdrawl]
[TransferUI] <= [Transfer]

====================Architectural Boundaries===========

[DepositUI], [WithdrawalUI], [TransferUI] <= [UI]
```

## Dependency Inversion in a Plug-In Architecture

This section focuses very much on how ownership is important when introducing abtractions.

```
				Architectural Boundary
	High Level			|		low level
[Editor] => [Plugin] <====== [VimModePlugin]
						|
```

When introducing the plugins to your Editor, to make DIP works here, you MUST own the Plugin code, and not the lower level.

## Dependency Inversion via Templates

## Dependency Inversion via Overload Sets

## Dependency Inversion Principle Versus Single-Responsibility Principle

DIP is fulfilled by properly assigning ownership and by properly grouping the things that truly belong. Sounds kinda like SRP right?

Not quite, DIP is concerned with the bigger picture - making abstractions make more sense in an architectural point of view, not just within components.

**Important thing to take away: Make sure ABSTRACTIONS are owned by HIGH-LEVEL, not low-level

