# Guideline 3: Separate interfaces to Avoid Artificial Coupling

## Segregate Interfaces to Separate Concerns

The book mentions a `exportDocument()` function that theoretically use exportToJson() to export documents.

The problem the book is pointing out here is that since the document is depending on a variety of external dependencies, it's pretty clear that it jumbles up a lot when changing `exportDocument()`. This coupling is caused by violation of Interface Segregation Principle (ISP)

> Interface Segregation Principle (ISP)
>
> Definition: Clients should not be forced to depend on methods that they do not use. This principle advocates segragating interfaces to separate concerns.

In this `Document` example, there are two concerns thus two interfaces here: `JSONExportable` and `Serializable`.

Now, the `exportDocument()` looks like this:
```
void exportDocument( JSONExportable const& exportable )
{
	exportable.exportToJson(...);
}
```

Here, it can be argued that ISP is similar to SRP. It is, but rather think of it as a special case of SRP - because this deserve special attention to when designing interfaces. Changing interfaces after it's designed is gonna be very hard, so it's important to get it right the first time around. "Measure twice, cut once"

### Minimizing Requirements of Template Arguments

ISP can also be applied to Templates.
