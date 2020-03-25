# Consumer interfaces

Prefer using interfaces with a single method instead of functions when declaring consumer interfaces.
This is to make Goland IDE navigation between the interface and the implementation(s) easier. 
When interface is declared, implementations are detected automatically and can be navigated to using `⌘+⌥+B` or `⌘+Click`.
Otherwise, you would need to find the constructor assignment, navigate to the constructor caller and determine the argument.

DO:

```go
type earningsGetter interface {
	Balance(id identity.Identity) uint64
}
```

DON'T:

```go
type earningsGetter func(id identity.Identity) uint64
```
