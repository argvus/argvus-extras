# Development

This repository contains Arch Linux packaging for third-party packages published as Argvus extras.

## Layout

```text
packages/<name>/PKGBUILD       Arch package build script
.github/workflows/ci.yml       CI build for every PKGBUILD
.github/workflows/publish.yml  Build and publish workflow for argvus/packages
```

## Local Package Build

Use an Arch Linux environment or container:

```sh
docker run --rm -t -v "$PWD:/work" -w /work archlinux:base-devel bash -lc '
  pacman -Syu --noconfirm --needed git sudo base-devel &&
  useradd -m builder &&
  chown -R builder:builder /work &&
  cd /work/packages/argvus-pwvucontrol &&
  sudo -u builder makepkg --nodeps --noconfirm --skippgpcheck -f
'
```

Build another package by changing the working directory, for example `packages/argvus-snappy-switcher`.

## Publishing Behavior

The GitHub Actions publish workflow:

1. discovers every `packages/*/PKGBUILD`;
2. builds each package in `archlinux:base-devel`;
3. downloads all build artifacts in the publish job;
4. clones `argvus/packages` using `PACKAGES_REPO_TOKEN`;
5. copies new `.pkg.tar.zst` files into `packages/public/arch/extras/$arch/`;
6. runs `repo-add` over all package files already present in that directory;
7. writes `argvus-extras.db`, `argvus-extras.files` and their `.tar.gz` sources;
8. optionally signs packages and repository metadata when `GPG_PRIVATE_KEY` is available;
9. commits the updated package files and pacman databases to `argvus/packages`.

Historical package versions are intentionally preserved. Do not add cleanup that deletes older `*.pkg.tar.zst` files from `packages/public/arch/extras/$arch/`.

## Version Updates

- Update the package `pkgver` when the upstream project publishes a new release.
- Reset `pkgrel` to `1` when `pkgver` changes.
- Bump `pkgrel` when the packaging changes but the upstream source version does not.
- Update checksums after changing sources.

## Secrets

Publishing requires this secret in this repository, or an organization secret made available to this repository:

- `PACKAGES_REPO_TOKEN`: fine-grained token with `contents: write` on `argvus/packages`.

Optional signing secrets:

- `GPG_PRIVATE_KEY`: ASCII-armored private GPG key used to sign packages and repository metadata.
- `GPG_PASSPHRASE`: optional passphrase for the private key.
