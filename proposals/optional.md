 # optional type

* [x] Proposed
* [ ] Prototype: [Complete](https://github.com/PROTOTYPE_OWNER/roslyn/BRANCH_NAME)
* [ ] Implementation: [In Progress](https://github.com/dotnet/roslyn/BRANCH_NAME)
* [ ] Specification: [Not Started](pr/1)

## Summary
[summary]: #summary

Explicit definition of an optional type.

## Motivation
[motivation]: #motivation

I believe that the whole effort done with nullables does not lead to the actual goal of getting rid of null.
Why there is no introduction of an optional type like in F# or any other functional language?  

In the way of domain-driven design it is not a good solution to decide wether it is a nullable value type or a nullable reference type.
In the functional domain it is about: There is an existing value or not. 
IMHO a specific type and null are two different things.
What we really need is a generic way to define an optional type.

## Detailed design
[design]: #detailed-design

It should not be allowed to pass null as parameter instead you should pass None.
You should only have access to an optional value by pattern matching.

```csharp
public void Method<T>(T$ optionalValue)
{
  // you can get the value only by pattern matching
  if(optionalValue is T t)
    t.DoSomething();

  switch(optionalValue)
  {
    case Some t: t.DoSomething();
    case None: ...
  }
}

public void AnotherMethod()
{
  MyType t = default;

  // null is not allowed
  Method(None);

  t = new MyType();
  Method(Some(t));
}
```
## Drawbacks
[drawbacks]: #drawbacks

Generic definition of optional types. Get rid of null.

## Alternatives
[alternatives]: #alternatives

```csharp
void Method(Optional<T> value)
```

## Unresolved questions
[unresolved]: #unresolved-questions

The syntax must be defined.

## Design meetings


