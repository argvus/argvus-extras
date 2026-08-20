# Contributing

Thank you for contributing packaging improvements to Argvus Extras.

## Guidelines

- Keep PKGBUILDs readable and close to Arch packaging conventions.
- Prefer tagged source archives over moving branch targets.
- Keep package names prefixed with `argvus-` when publishing to this repository.
- Preserve the upstream project license in the PKGBUILD `license=()` field.
- Use `backup=()` for user-editable files installed under `/etc`.
- Keep dependencies explicit enough for `makepkg` and `pacman` users.
- Preserve historical binary packages in the `packages` repository.

## Pull Requests

Include:

- package or workflow changed;
- upstream version/tag involved;
- local build result, if available;
- expected publishing impact.

For workflow changes, explain how they affect `packages/public/arch/extras/$arch/` and the `argvus-extras` pacman database.
