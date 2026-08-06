# Global Instructions

## Verification: always run `smoke` before committing

`smoke` is a command on PATH that runs this repository's selected checks. Use it
as your generic last verification step. It replaces ad-hoc commands like
`go test ./...`, `golangci-lint run`, `npm test`, etc.

- Before declaring a change done, and always before creating a commit, run
  `smoke` and make sure it passes (or fix what it reports).
- Do not substitute other commands for `smoke` unless `smoke` itself is
  unavailable for this project type (see below).

### Fallback when `smoke` doesn't know the project type

If `smoke` errors with `todo: detect this project type`, it means `smoke` has no
checks registered for this repo yet. When this happens, ask once per session:

> `smoke` doesn't recognize this project type. Do you want to update `smoke` to
> support it, or should I fall back to my default verification behavior (e.g.
> `go test ./...` / `golangci-lint run` / etc.) for the rest of this session?

- Ask at most once per session. Remember the answer for the rest of the session.
- If the user says they'll update `smoke`: stop and let them update it, then use
  `smoke` going forward.
- If the user says to fall back: use sensible default checks for the detected
  language/toolchain for the remainder of the session, but still prefer `smoke`
  again next session.
