# renovate-test

Test repository for validating Renovate CVE fix configuration on release branches.

## Purpose

This repo simulates the Antrea project's Renovate setup to verify that:

1. Vulnerability (CVE) fix PRs are created for **release branches** (not just `main`)
2. Both **direct** and **indirect** vulnerable dependencies are covered
3. Regular (non-security) updates are **disabled** on release branches

## Vulnerable dependencies

| Branch | Dependency | Version | CVE |
|---|---|---|---|
| `main` | `google.golang.org/grpc` | v1.77.0 | CVE-2026-33186 |
| `release-1.1` | `google.golang.org/grpc` | v1.72.0 | CVE-2026-33186 |
| `release-1.0` | `google.golang.org/grpc` | v1.68.0 | CVE-2026-33186 |
| `release-1.1` | `github.com/pion/dtls/v2` | v2.2.12 (indirect) | pion/dtls CVE |

## Expected Renovate behavior

- `main`: CVE fix PR for grpc ✅
- `release-1.1`: CVE fix PR for grpc ✅, CVE fix PR for pion/dtls ✅
- `release-1.0`: CVE fix PR for grpc ✅
- `release-1.1`: NO regular update PRs ✅
