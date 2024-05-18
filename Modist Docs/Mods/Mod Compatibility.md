---
tags:
  - todo
---
## Managing Versions
Mod use of [SemVer](https://semver.org) for the versioning standard. These versions are considered compatible if their left-most non-zero major/minor/patch component is the same. For example, `1.0.3` and `1.1.0` are considered compatible, and thus it should be safe to update from the older release to the newer one. However, an update from `1.1.0` to `2.0.0` would not be allowed to be made automatically. This convention also applies to versions with leading zeros. For example, `0.1.0` and `0.1.2` are compatible, but `0.1.0` and `0.2.0` are not. Similarly, `0.0.1` and `0.0.2` are not compatible.
