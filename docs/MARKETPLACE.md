# GitHub Marketplace Release Guide

## Marketplace listing

**Name:** Docker Image Lifecycle Automation

**Short description:**

> Monitor, release, secure, and publish container images across any OCI registry — governed, signed, and automated.

**Long description:**

Docker Image Lifecycle Automation is a hybrid GitHub Actions platform that
governs the entire lifecycle of a container image — from upstream drift
detection to signed, published, and released artifacts.

It monitors base images by immutable digest (not just tag strings), opens
reviewable pull requests with reviewer/assignee routing when an update is
detected, and — once merged — builds, tests, scans, signs, generates SBOM
and provenance, versions, and publishes to GHCR, Docker Hub, ACR, ECR, Quay,
Harbor, Artifactory, GitLab Container Registry, Oracle OCIR, or any private
OCI-compliant registry.

Seven configurable release-tagging strategies (SemVer, date, prefix,
upstream, custom pattern, and more), Repository-Variable-first
configuration, GitHub Environment approval gates, and Cosign/OIDC signing
make it suitable for both open-source projects and regulated enterprise
release pipelines.

Adopt at your own pace: start with a single digest-resolution step, or take
the full reusable-workflow lifecycle with governed promotion and rollback
support.

The root Marketplace Action resolves a tag to a stable image digest. The
repository also provides reusable workflows for the complete image lifecycle.

## Categories

- Security
- Continuous integration

## Search keywords

`docker`, `container`, `oci`, `github-actions`, `dockerfile`, `base-image`,
`base-image-monitoring`, `docker-image-update`, `image-digest`,
`immutable-digest`, `container-security`, `supply-chain-security`, `sbom`,
`provenance`, `cosign`, `slsa`, `trivy`, `multi-platform`,
`container-registry`, `ghcr`, `docker-hub`, `platform-engineering`,
`semver`, `release-automation`, `changelog-automation`,
`dependency-update-automation`, `container-publishing`, `dockerhub`,
`acr`, `ecr`, `harbor`, `artifactory`

## Marketplace Action

The root [`action.yml`](../action.yml) is the Marketplace entry point. It
resolves an OCI tag to an immutable digest and provides `digest`, `resolved`,
`media_type`, `is_multi_arch`, and `platforms` outputs. The action uses a
fixed OCI/Docker manifest `Accept` set to preserve multi-architecture index
digests.

**Branding:** `package` icon, `blue` color.

## Publish checklist

1. Make `yaju-mahida/docker-image-lifecycle-automation` public.
2. Confirm two-factor authentication is enabled for the publishing account.
3. Verify `LICENSE` and `NOTICE` are present and identify Apache-2.0.
4. Ensure `README.md` contains the root-action quick start and reusable
   workflow onboarding guidance.
5. Run the `Validate` workflow successfully on the release commit.
6. Run the `Release (SemVer)` workflow to create the initial `v1.0.0`
   release and moving `v1` major-version tag.
7. Confirm the release and moving major tag resolve to the same commit.
8. In the GitHub Release form, select **Publish this Action to the GitHub
   Marketplace** and accept the Marketplace Developer Agreement.
9. Use the listing text above and review the rendered Marketplace page before
   publishing.

## Versioning policy

The Marketplace Action and reusable workflow contracts follow Semantic
Versioning. Publish immutable release tags such as `v1.0.0`; keep `v1` as the
supported compatibility line. Breaking inputs, outputs, security defaults, or
workflow behavior require `v2`.

Consumer image release-identifier policies are independent of platform versioning.
They are configured through `RELEASE_TAG_STRATEGY` in the consumer repository.