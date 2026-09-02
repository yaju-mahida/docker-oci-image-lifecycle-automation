# Product Roadmap

Docker OCI Image Lifecycle Automation is developed as a lifecycle platform, not
as a collection of unrelated Docker actions. The roadmap prioritizes
trustworthy digest monitoring and an excellent adopting-repository experience
before organization-wide governance features.

## v1: Trusted lifecycle core

- Stable Marketplace action and `v1` compatibility line.
- Digest-first upstream image monitoring, including same-tag rebuilds.
- Evidence-backed Dockerfile update pull requests.
- Multi-platform build, smoke test, scan, SPDX SBOM, provenance, signing,
  release, and multi-registry publication.
- Progressive templates for digest resolution, monitoring, secure release,
  and environment-gated release.
- Published OCI registry support matrix and action/workflow compatibility
  contract.

## v1.x: Adoption and operations

- More actionable dry-run and pull-request evidence.
- Contract and OCI integration fixtures for public and private registries.
- Migration guides for manual Docker workflows, Dependabot, and Renovate.
- Registry-specific operational guidance and troubleshooting.
- Release-note and changelog automation improvements.
- Compatibility-contract validation before each moving-major tag update, so
  consumers pinned to `@v1` are protected from accidental breaking changes.
- Stronger consumer onboarding assets, including quick-start templates,
  test-repository guidance, and failure-mode troubleshooting for private
  reusable workflow consumption.

## v2: Governed lifecycle policy

- Versioned policy-as-code for trusted upstream registries, allowed
  namespaces, required digest pinning, severity gates, and signing policy.
- Verification gates for published-image digest, provenance, and signatures.
- Promotion channels and immutable rollback workflow.
- Compliance evidence bundles.
- Optional reusable workflows for enterprise extensions that should not bloat
  the core release path:
  - `workflow_call` promotion and rollback orchestration.
  - `workflow_call` compliance evidence bundle generation.
  - `workflow_call` registry synchronization and mirroring.
- Repository-level exceptions with clear audit trails, so central policy can
  be adopted without blocking teams that need controlled variance.
- Environment-aware approval evidence that records who approved promotion,
  what image digest was approved, and which security artifacts were available
  at the time of approval.
- Published deprecation policy for the `v1` compatibility line before any
  `v2` breaking changes are introduced.

## v3: Platform engineering scale

- Organization-wide upstream-image exposure inventory.
- Upstream image to adopting-repository dependency graph.
- Central policy bundles with repository-level exceptions.
- Lifecycle reporting and audit integrations.
- Organization-level lifecycle dashboard showing monitored base images,
  affected repositories, pending update PRs, release status, scan status, and
  registry publication status.
- Cross-repository blast-radius analysis for vulnerable or rebuilt upstream
  images.
- Compliance export integrations for audit systems, artifact stores, and
  security data platforms.
- Optional enterprise reporting mode that aggregates metadata without requiring
  a hosted SaaS control plane.

## Architecture direction

The platform should continue using a hybrid architecture:

- **Composite actions** remain responsible for deterministic, reusable,
  single-purpose operations such as digest resolution, tag calculation,
  Dockerfile parsing, registry resolution, and release-note generation.
- **Reusable workflows** remain responsible for multi-job orchestration,
  environment gates, artifact handoff, permissions, and release lifecycle
  sequencing.
- **Consumer repositories** remain responsible for schedules, credentials,
  environments, branch protections, release policy, and repository-specific
  configuration.

New capabilities should become reusable workflows only when they represent an
independent lifecycle phase, such as promotion, rollback, compliance evidence,
or registry synchronization. Build, test, scan, SBOM, provenance, signing,
release, and publish should stay together in the core release workflow because
they share artifacts, permissions, and release identity.

## Product positioning guardrails

- Marketplace messaging should describe the platform as digest-first Docker
  and OCI lifecycle automation, not as a generic Docker build or publish
  action.
- Current documentation may describe monitoring, reviewable update PRs,
  build, test, scan, SBOM, provenance, signing, release, and multi-registry
  publishing as available capabilities.
- Governance, promotion, rollback, compliance bundles, organization-wide
  inventory, dependency graphs, and dashboards should remain clearly marked as
  roadmap capabilities until implemented.
- The root Marketplace action should continue to be positioned as the digest
  resolution entry point, while the reusable workflows provide the complete
  lifecycle.

## Explicit non-goals

- Replacing Renovate or Dependabot as a general dependency manager.
- Requiring a SaaS control plane for open-source use.
- Treating mutable tags as production deployment identities.
- Hiding approvals, credentials, or release policy in a central platform
  repository.
