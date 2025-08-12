# Dependabot vcpkg

This is an example repository showcasing how Dependabot can be used to update [vcpkg][vcpkg] dependencies in a project.

## Background

vcpkg is a package manager for C and C++ libraries, allowing developers to easily manage dependencies in their projects.
vcpkg projects include a [`vcpkg.json` manifest file][vcpkg-json] that specifies the dependencies and their versions.
In a `vcpkg.json` file, a `builtin-baseline` field is used to specify a baseline commit of the [vcpkg port repository][vcpkg-port] to use for resolving dependencies.

## Example

[`builtin-baseline/vcpkg.json`](builtin-baseline/vcpkg.json) is an example of a vcpkg project that uses a `builtin-baseline` to specify the commit of the vcpkg port repository to use.
It's taken from the [`microsoft/terminal` repository][microsoft-terminal].
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

In this case, Dependabot will update the `builtin-baseline` field to the commit of the latest tag from the vcpkg port repository, which will update the versions of the dependencies specified in the `dependencies` field.
See [commit `5a4d27f522b27179d9e2dcb42eab58bbf891ca49`][builtin-baseline-commit] for an example of a Dependabot update that updates the `builtin-baseline` field.

```diff
diff --git a/builtin-baseline/vcpkg.json b/builtin-baseline/vcpkg.json
index 3e6e3be..54a14a3 100644
--- a/builtin-baseline/vcpkg.json
+++ b/builtin-baseline/vcpkg.json
@@ -36,10 +36,10 @@
       "version": "0.30.3"
     }
   ],
-  "builtin-baseline": "fe1cde61e971d53c9687cf9a46308f8f55da19fa",
+  "builtin-baseline": "ef7dbf94b9198bc58f45951adcf1f041fcbc5ea0",
   "vcpkg-configuration": {
     "overlay-ports": [
       "./dep/vcpkg-overlay-ports"
     ]
   }
-}
\ No newline at end of file
+}
```

[vcpkg]: https://vcpkg.io/
[vcpkg-json]: https://learn.microsoft.com/en-us/vcpkg/reference/vcpkg-json
[vcpkg-port]: https://github.com/microsoft/vcpkg
[example-cli]: https://github.com/dependabot/example-cli-usage
[microsoft-terminal]: https://github.com/microsoft/terminal
[builtin-baseline-commit]: https://github.com/JamieMagee/dependabot-vcpkg/commit/5a4d27f522b27179d9e2dcb42eab58bbf891ca49
