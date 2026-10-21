# Changelog

Every change to the contract is listed here, newest first. The version is the `info.version` of [`openapi.yaml`](openapi.yaml) and follows the rules in the [README](README.md#versioning).

## [0.1.1] - 2026-10-21

### Fixed

- The successful answers declared the media type `*/*`; they now declare `application/json`, which is what the API writes. A client generator or a validator could not tell what the body was before. No field, operation or code changed.

## [0.1.0] - 2026-10-21

First version of the contract. It describes the API exactly as `biblioteca-java` 0.1.0 behaves.

### Added

- 26 operations in 5 groups: books, copies, members, loans and fines.
- One error shape, `{ code, message }`, with the list of stable codes and the codes each operation can return.
- Required fields on every answer, and `null` allowed only where the data really may be missing (publication year, return date, fine, payment date).
- Explicit `security: []`: the API has no authentication yet.
