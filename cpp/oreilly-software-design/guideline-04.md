# Guideline 4: Design for Testability

You want to live life without worrying when you change your software? Make sure that your software comes with tests. This guideline should lean our philosophy to design software for testability.

## How to test a private member function

### Wrapping private function in a public function
Author was asking us to test the private function `updateCollection` in a class called `Widget`. One (bad?) way to approach this is to use white box testing: wrap the `updateCollection` in a public function, e.g. `addBlob`.

> White box test
>
> Def: A white box test knows about the internal implementation details of the function under test, which introduces dependencies (and as we all know, these are undesirable deps).

> Just as much as you should avoid and reduce depencies  in your productino code, **you should avoid dependencies between your tests and the details of your production code**.

What we need: BLACK BOX TEST

> Black box test
>
> Def: Does not make assumptions about details and tests only the expected behavior.

### Introducing friend class

The author recommend against friend class also. Reasoning is we yet again introduce an artificial dependency: production class should not know about test class, even though test class should know about production class.

> In C++, `friend` is not your friend, because most often this will introduce artificial coupling.

Exception: hidden friend and idiomatic uses

### Changing from private to protected

No bueno either: as quoted from the book from another book:

> Inheritance is rarely the answer.

Here, the argument against this is we are abusing inheritance for the sake of gaining access to tests.

### The solution: Separate them out

Author proposes ripping the `updateCollection` out of the `Widget`. Outrageous? His reasoning kind of makes sense.

Extracting function from a class is also a step towards encapsulation.

> You should prefer nonmember non-`friend` functions to member functions.
  - A member function has access to all functions a class has, but an outsider can only see the public members. That keep encapsulation tighter.

Reasons:
1. `Widget` becomes more encapsulated. Less details are exposed.
2. Extracted `updateCollection` is easily testable.
3. Separation of concern, no need to care about changing `Widget` when changing `updateCollection`

> FREE YOUR FUNCTIONS!
