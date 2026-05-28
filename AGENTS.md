## Stack
Go (version from go.mod), Jaeger distributed tracing, Docker (Dockerfile present)

## Constraints
Never modify: `go.sum`, any `*.pb.go` generated files, credential or secret files, migration files.
Do not delete or rename tracked files without explicit instruction — only 9 files exist in this repo.

## Conventions
Standard Go project layout. Tests live alongside source files with `_test.go` suffix.
Test functions must be named `TestXxx`. Packages match directory names.
Keep Dockerfile instructions ordered: FROM, ENV, COPY, RUN, EXPOSE, ENTRYPOINT.

## Dependency manifests
`go.mod` — Go module dependencies and minimum versions.
`go.sum` — checksums; update automatically via `go mod tidy` but never edit by hand.

## Agent rules
- Run `go build ./...` and `go test ./...` after any Go change; both must pass before committing.
- Run `go mod tidy` after any dependency change; commit updated `go.mod` only (`go.sum` auto-follows).
- CVE scan uses image digest `d6cc81e5`; do not change the base image tag without updating scan config.
- Dockerfile: use explicit version tags on FROM lines, no `latest`.
- Do not add new files unless directly required by the task.
- Security and code-quality fixes must not alter public API signatures.
- One logical change per commit; commit message format: `<type>: <short description>` (e.g. `fix: update dependency X`).
