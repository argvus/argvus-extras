# Argvus Extras

Arch Linux PKGBUILDs for third-party packages distributed through the Argvus extras package repository.

This repository builds selected upstream projects as `argvus-*` packages and publishes the resulting binary packages to `argvus/packages` under:

```text
public/
└── arch/
    └── extras/
        └── x86_64/
            ├── argvus-extras.db
            ├── argvus-extras.files
            └── argvus-*.pkg.tar.zst
```

The packages here are not the upstream source projects. Each package directory contains the Arch packaging metadata needed to fetch, build and package an upstream release.

## Packages

```text
packages/argvus-pwvucontrol/PKGBUILD
packages/argvus-snappy-switcher/PKGBUILD
```

## Documentation

- Development workflow: [DEVELOPMENT.md](DEVELOPMENT.md)
- Contribution guide: [CONTRIBUTING.md](CONTRIBUTING.md)

## Related Repositories

- [`argvus-pkgbuild`](https://github.com/argvus/argvus-pkgbuild)
- [`packages`](https://github.com/argvus/packages)

## License

The packaging files and repository documentation are licensed under GPL-3.0. Third-party upstream projects keep their own licenses, which are declared in each `PKGBUILD`.
