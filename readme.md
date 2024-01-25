# Go Mod Check Action

This Github Action will ensure your `go.mod` & `go.sum` file are up-to-date and don't require
any changes (are good to be merged).

`go mod tidy` is run in a user defined directory that contains a `go.mod` file, then it checks
no files have changed (via `git diff`) to ensure that no changes need to be made.

It also checks that lines starting with `replace ` (for local development) haven't been committed by accident
(see https://thewebivore.com/using-replace-in-go-mod-to-point-to-your-local-module/), this can be disabled.

### Requirements

This Github Action must be run after the following conditions are met in your Github workflow

1. Your code must be checked out, eg `actions/checkout`
1. `go` must be installed on the workflow runner, eg `actions/setup-go`
1. The working directory has no uncommitted changes (`git diff` has empty output).

### Usage

Add this action as a step after you have checked out your code and installed go.

```yaml
- uses: j0hnsmith/go-mod-check-action@v1
  with:
    working-directory: some/path/to/dir/with/go.mod # required
    skip-replace-check: true # optional, only if you're happy to have `replace ` lines in your go.mod file
```
