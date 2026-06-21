# Guideline 16: Use Visitor to Extend Operations

## Visitor Design Pattern Usage & Advantage
We have a toy example of:

```
			Shape | virtual translate()=0
						^
						|
				-----------------
				|				|
		Circle | translate() Square | translate()
```

Let's assume this is a closed set of types and open set of operations.

Design problem: This would make it hard to add operations
- Virtual function complicates adding sets of operations: you can't easily extend with it how it is, whether it is using pure or regular virtual functions.

To solve this problem, you would need the _Visitor Design Pattern_.

> Visitor (Design Pattern)
>
> Definition: A visitor is an operation to be performed on elements of an object structure. This allows adding new operation without having to modify the classes of elements this is operating on.

Note: the reason why this is called Visitor is because the operation is not part of the object itself, but rather OUTSIDE using the object for the work. The Visitor "travels" to each object and execute action, but does not "stay around" (permanent part of the object itself).


## Visitor Weakness

### Low Implementation Flexibility

For trivial operation, it's hard to share implementation across all operations. You would have to implement a `visit()` for each and every one of the objects, which would be very tedious.

Return types are also locked into the `visit()` function as determined by the Visitor class. It's not easy to extend operation on these.

## Difficulty to Add New Types

We have already talked about this in the previous section, but the idea is that you would have to edit ALL operations that these objects accept. This would mean changing all Visitor implementations.

This restriction exsists because there is a cyclic dependency among ShapeVisitor base class i.e. ShapeVisitor depends on concrete Shapes, which depends on Shape, which depends on ShapeVisitor.

## This Form of Visitor is Intrusive

This form of Visitor requires adding the pure virtual function `accept()` is intrusive. As in, if you want to add this to an existing code, then you'll have to modify the base Shape class.
