---
tags:
  - wip
---
## Version Specifiers
We depend on [SemVer](https://semver.org/) for specifying version numbers (see [[Mod Metadata#version|mod version]]) which establishes a common version specification for what versions of mods are compatible with each other.

> [!important]
> The idea of remaining *compatible* is very important to mod development as it allows us to automatically resolve and fetch dependencies for mod installations. Please read through [[Mod Compatibility]] for guidance on how to best manage your mod's version number.

| Requirement | Example             | Equivalence       | Description                                                  |
| ----------- | ------------------- | ----------------- | ------------------------------------------------------------ |
| Caret       | `1.2.3` or `^1.2.3` | `>=1.2.3, <2.0.0` | Any SemVer-compatible version of at least the given value.   |
| Tilde       | `~1.2`              | `>=1.2.0, <1.3.0` | Minimum version, with restricted compatibility range.        |
| Wildcard    | `1.*`               | `>=1.0.0, <2.0.0` | Any version in the `*` position                              |
| Equals      | `=1.2.3`            | `=1.2.3`          | Exactly the specified version only.                          |
| Comparision | `>1.1`              | `>=1.2.0`         | Naive numeric comparison of specified digits.                |
| Compound    | `>=1.2, <1.5`       | `>=1.2.0, <1.5.0` | Multiple requirements that must be simultaneously satisfied. |
