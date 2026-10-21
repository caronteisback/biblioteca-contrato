# biblioteca-contrato

[![CI](https://github.com/caronteisback/biblioteca-contrato/actions/workflows/ci.yml/badge.svg)](https://github.com/caronteisback/biblioteca-contrato/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![OpenAPI 3.1](https://img.shields.io/badge/OpenAPI-3.1-6BA539)

The API contract of the library system, written once in [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) and shared by every backend and by the frontend.

> All data in this project is fictional. It is a portfolio project and is not related to any real organization.

## Why a separate repository

The library API will exist in more than one implementation (a Java one, [biblioteca-java](https://github.com/caronteisback/biblioteca-java), and later a Python one) and a browser frontend will call it. If each of them described the API on its own, they would drift apart without anyone noticing. Here there is one description, and each project proves that it follows it:

```
                    biblioteca-contrato
                       openapi.yaml
                      /      |       \
         backend Java   backend Python   frontend
         (checks it)    (checks it)      (uses it)
```

## What is here

| File | What it is |
|------|------------|
| [`openapi.yaml`](openapi.yaml) | The contract: 26 operations, the schemas and the error codes |
| [`CHANGELOG.md`](CHANGELOG.md) | What changed in each version of the contract |
| [`redocly.yaml`](redocly.yaml) | The rules the contract is linted with |

The contract covers books, copies, members, loans, renewals, returns and fines. Routes are in Spanish (`/api/v1/prestamos`), as the domain is; the text of the contract is in English.

## Read it

- On GitHub, open [`openapi.yaml`](openapi.yaml).
- As a page with every operation: `npx @redocly/cli@2.64.1 preview-docs openapi.yaml`.
- In Swagger UI, run [biblioteca-java](https://github.com/caronteisback/biblioteca-java) in its `dev` profile and open `/swagger-ui.html`.

## Check it

```bash
npx @redocly/cli@2.64.1 lint openapi.yaml
```

Needs Node.js. The same command runs on every push and pull request. The Redocly version is pinned so that a new release cannot break the build on its own.

## Versioning

`info.version` follows [Semantic Versioning](https://semver.org/), applied to what a client can notice:

| Change | Version | Example |
|--------|---------|---------|
| Breaks a client that worked before | **Major** (`1.0.0`) | Remove or rename an operation, a field or an error code; make a field required; change a type |
| Adds something a client can ignore | **Minor** (`0.2.0`) | A new operation, a new optional parameter, a new field in an answer |
| Changes no behavior | **Patch** (`0.1.1`) | A better description, a fixed typo, a new example |

While the major number is `0`, the contract is still settling and a minor change may also break clients; the changelog says so when it happens.

Every change to `openapi.yaml` needs a new version in `info.version` and an entry in the changelog, and each release is a Git tag (`v0.1.0`). A backend states which tag of the contract it implements.

## Status

| Version | Implemented by |
|---------|----------------|
| 0.1.0 | biblioteca-java (generated the first draft; the test that checks the API against this file is the next step) |

## License

[MIT](LICENSE).
