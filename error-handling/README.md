# Error handling in go

All go errors should be wrapped using the standard `errors` package. It has been drastically improved in go version 1.13, therefore we should adhere to the standard.

The current codebase is still full of the `github.com/pkg/errors` uses, so these need to be slowly replaced by 
the `errors` package. All new development should adhere to this standard and use the `errors` package.

To add context to errors, use:
`fmt.Errorf("my context: %w", err)`

To check if an underlying error corresponds to an expected error, use `.Is()`:

```golang
var ErrExplosions = errors.New("Explosions")
...

if errors.Is(err, ErrExplosions) {
    // The underlying error is explosions
}
```

You can also use a custom error struct, with added context. To make casting easier, we have the `.As()`:

```golang
type MyCustomError struct {
    Data string
}

func (mce MyCustomError) Error() string {
    return "I'm very custom"
}
...

mce := MyCustomError{}
ok := errors.As(err, &mce)
if ok {
    // we should be able to access mce.Data here now
}

```

For more on the improved error context mechanics, [read the official blog](https://blog.golang.org/go1.13-errors)
