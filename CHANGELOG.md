# Changelog

Every change to the contract is listed here, newest first. The version is the `info.version` of [`openapi.yaml`](openapi.yaml) and follows the rules in the [README](README.md#versioning).

## [0.2.0] - 2026-10-21

**Breaking:** every operation but `login` now needs a bearer token, so a client written for 0.1.x gets `401` until it signs in. Nothing else about the existing operations changed.

### Added

- **Authentication.** `POST /api/v1/auth/login` exchanges an email and a password for a bearer token (JWT, valid for 60 minutes). A `bearerAuth` security scheme and a security requirement on every operation, with the roles that may call it: `LIBRARIAN` can do everything; `MEMBER` can read the catalog (`listBooks`, `getBook`, `listCopiesOfBook`) and their own data.
- **Account.** `GET /api/v1/me` (the signed-in user; for a member, with score and alerts), `GET /api/v1/me/prestamos` and `GET /api/v1/me/multas` (only the member's own loans and fines).
- **Error codes.** `UNAUTHENTICATED` (401), `FORBIDDEN` (403), `INVALID_CREDENTIALS` (401) and `TOO_MANY_ATTEMPTS` (429, after 5 failed attempts in a row for the same email, for 5 minutes). Every operation lists `401`, and `403` where a role can be refused.
- Schemas `LoginRequest`, `LoginResponse` and `UsuarioResponse`; 30 operations in total.

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
