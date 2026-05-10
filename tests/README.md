# Test Coverage — gh-identity

## What We Test

This is a **v1 Go plugin** (no `plugin.yaml`). It ships:
- `internal/ghidentity/mutator_test.go` — Go unit tests for `Mutator.MutateEnv`
- `scripts/test-wrapper.sh` — bash shell tests for `wrapper.sh` argv rewriting

## Test Breakdown

| File | Tests | How |
|------|-------|-----|
| `internal/ghidentity/mutator_test.go` | 5 Go tests | Role sanitization, owner resolution, nil-map error, fallback chain |
| `scripts/test-wrapper.sh` | 12 bash tests | Passthrough, badge prepend, `@me` rewrite, assignee drop |

## Running Tests

**Shell tests** (no dependencies):
```bash
bash scripts/test-wrapper.sh
```

**Go tests** (requires Go toolchain):
```bash
go test ./...
```

## What We Cannot Test Here

- **Go unit tests** — cannot be run in this environment (no `go` binary).
  They cover: `MutateEnv` no-op, field injection, nil-map error, owner
  resolution fallback, role sanitization edge cases.
- **CI validation** — v1 plugins use `workspace-server` CI, not the shared
  `validate-plugin.yml` workflow. CI runs in the workspace-server repo.
