# Cyoda Homebrew Tap

Homebrew tap for [cyoda-go](https://github.com/Cyoda/cyoda-go) — a lightweight Go EDBMS that serves as a digital twin of the Cyoda platform.

## Install

```sh
brew install cyoda/cyoda-go/cyoda
```

## Formula

`cyoda.rb` is auto-generated and committed by the cyoda-go
[release workflow](https://github.com/Cyoda/cyoda-go/blob/main/.github/workflows/release.yml)
via [GoReleaser](https://goreleaser.com) on each `v*` tag push. Don't edit
manually — the next release would overwrite your changes.

## Verifying a release

Each release artifact is signed via [cosign](https://github.com/sigstore/cosign)
keyless signing (OIDC). To verify the Docker image published alongside the
brew formula, and pull it by the digest the check printed (needs `cosign` and
`jq`; put your release version in `V`):

```sh
V=0.8.4
OUT=$(cosign verify "ghcr.io/cyoda/cyoda:$V" \
  --certificate-identity "https://github.com/Cyoda/cyoda-go/.github/workflows/release.yml@refs/tags/v$V" \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-github-workflow-trigger push \
  --certificate-github-workflow-ref "refs/tags/v$V") \
  && D=$(printf '%s' "$OUT" | jq -r '.[0].critical.image."docker-manifest-digest"') \
  && docker pull "ghcr.io/cyoda/cyoda@$D"
```

## Upstream

Source, issues, releases, and documentation all live at
<https://github.com/Cyoda/cyoda-go>.
