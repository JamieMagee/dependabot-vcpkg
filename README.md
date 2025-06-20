# Dependabot VCPKG

This is an example repository showcasing how Dependabot can be used to update [VCPKG][vcpkg] dependencies in a project.

## Background

VCPKG is a package manager for C and C++ libraries, allowing developers to easily manage dependencies in their projects.
VCPKG projects include a [`vcpkg.json` file][vcpkg-json[] that specifies the dependencies and their versions.
In `vcpkg.json` file, a `builtin-baseline` field is used to specify a baseline commit of the [VCPKG port repository][vcpkg-port] to use for resolving dependencies.

## Examples

This repository uses the [`dependabot/example-cli-usage`][example-cli] repository to demonstrate how Dependabot can update VCPKG dependencies.

### Builtin Baseline

[`builtin-baseline/vcpkg.json`](builtin-baseline/vcpkg.json) is an example of a VCPKG project that uses a `builtin-baseline` to specify the commit of the VCPKG port repository to use.
It's taken from the [`microsoft/terminal`][microsoft-terminal] repository.
The json file looks like this:

```json
{
  "$schema": "https://raw.githubusercontent.com/microsoft/vcpkg-tool/main/docs/vcpkg.schema.json",
  "dependencies": [
    "fmt",
    "ms-gsl"
  ],
  "builtin-baseline": "fe1cde61e971d53c9687cf9a46308f8f55da19fa"
  // ... other fields
}
```

In this case, Dependabot will update the `builtin-baseline` field to the commit of the latest tag from the VCPKG port repository, which will update the versions of the dependencies specified in the `dependencies` field.

## Availability

Support is currently in branches:

- [`jamiemagee/vcpkg-updater` in `dependabot/dependabot-core`][core]
- [`jamiemagee/vcpkg` in `dependabot/cli`][cli]
- [`jamiemagee/vcpkg` in `dependabot/smoke-tests`][smoke-tests]

[vcpkg]: https://vcpkg.io/
[vcpkg-json]: https://learn.microsoft.com/en-us/vcpkg/reference/vcpkg-json
[vcpkg-port]: https://github.com/microsoft/vcpkg
[example-cli]: https://github.com/dependabot/example-cli-usage
[microsoft-terminal]: https://github.com/microsoft/terminal
[core]: https://github.com/dependabot/dependabot-core/tree/jamiemagee/vcpkg-updater
[cli]: https://github.com/dependabot/cli/tree/jamiemagee/vcpkg
[smoke-tests]: https://github.com/dependabot/smoke-tests/tree/jamiemagee/vcpkg
