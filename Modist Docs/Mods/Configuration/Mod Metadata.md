---
aliases:
  - mod.toml
tags:
  - wip
---
# mod.toml
The main file that details a mod is the metadata file `mod.toml`. This file lives in the root directory of the mod archive and follows the [TOML](https://toml.io/) format. This file and includes details similar to other package metadata files like [`package.json`](https://docs.npmjs.com/cli/v6/configuring-npm/package-json), [`pyproject.toml`](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/), and [`cargo.toml`](https://doc.rust-lang.org/cargo/reference/manifest.html).
## \[mod]
The primary section of the `mod.toml` file is the `[mod]` section. This section contains the basic details of of your mod.

The only locally required fields for this section are the [[#name]] and [[#version]] fields. [[Publishing Mods|Publishing to a registry]] requires more fields.
### name
The `name` field is the identifier used to refer to the package in conjunction with the publishing user's username. It is used when listed as a dependency or conflict in another package.

```toml
[mod]
name = "my-mod"
```

The ﻿name field must be between 4 and 64 ASCII [alphanumeric](https://en.wikipedia.org/wiki/Alphanumericals) characters and may include ﻿`-` or ﻿`_`. Reserved names, as defined and enforced by registries, are not allowed.
### version
The `version` field is the [Semantic Version](https://semver.org/) identifier for the current version of the included mod. Please reference the [semver.org](https://semver.org/) documentation to understand the definition and usage of semantic versions. This version identifier is used when listed as a dependency or conflict in another package when performing [[Dependency Resolution|dependency resolution]].

```toml
[mod]
version = "0.1.0"
```

Key principles regarding working with the version number:
- For a new mod that has *never* reached stable state, the version should have the major version set to `0` (`0.x.x`)
- When introducing breaking changes from the previously published version, bump the major version and reset minor and patch (`3.1.2` → `4.0.0`)
- When no breaking changes are being introduced, bump either the minor version or patch version (`3.1.2` → `3.2.0` or `3.1.3`)
	- Minor versions are *typically* bumped when new functionality is being introduced
	- Patch versions are *typically* bumped if only bug fixes are being introduced

During local initialization of a new mod, this version will be defaulted to `0.1.0`.

> [!important]
> 
### authors
The `authors` field contains a list of the individuals who are considered the creators of the mod. Entries in this list are just the names of the authors and optionally an email address.

These entries are written as a string with their email address optionally included in angle brackets.

```toml
[mod]
authors = ["Sincere35", "Eulah63 <eulah.63@example.org>"]
```

This information does not control what a registry considers as a publishing user; the names in this field are just used for attribution.
### maintainers
Similar to [[#authors]] the `maintainers` field is an optional field that contains a list of the individuals who are considered the active maintainers of the mod.

These entries are written as a string with their email address optionally included in angle brackets.

```toml
[mod]
maintainers = ["Russell9", "Nova8 <nova8@example.org>"]
```

The ﻿maintainers field should not include the [[#authors]]. This field is reserved for individuals, other than the authors, who are actively maintaining the upkeep of the mod.
### description
The `description` field is a short blurb about your mod that is *typically* displayed in the registry. This string should be plain text (not Markdown).

```toml
[mod]
description = "A short description of my mod"
```
### contributions
Somewhat related to [[#authors]] and [[#maintainers]], the `contributions` field is an optional field used to attribute credit to individuals who provided services, assets, or resources to the development of the mod.

The structure of this field is a list of dictionaries containing individual's `name` (with an optional email address included in angle brackets) along with optional `url` and `credit` fields:

```toml
[mod]
contributions = [
  { name = "Brandy_DAmore56" },
  {
    name = "Alexandria5 <alexandria5@example.org>",
    credit = "Cover image art"
  },
  {
    name = "CD Projekt Red",
    url = "https://www.cdprojektred.com/",
    credit = "Model assets"
  }
]
```

It is recommended to list out the original sources of the assets and resources used in the content of your mod (if applicable).

Similar to [[#maintainers]], this field should not include the [[#authors]]. This field is reserved for individuals, other than the authors, who have actively contributed effort or resources to the development of the mod.
### readme
The `readme` field should be the relative (to `mod.toml`) path to a file in the mod that contains general information about the mod. This file will be transferred to the mod registry when the mod is published. The registry will interpret this file as Markdown and use it in the mod's page.

```toml
[mod]
readme = "README.md"
```

If no value is specified for this field, but a file named `README.md` is located in the root of the mod, then that file will be used by default. You can disable this behavior by setting `readme` to `false`. If set to `true` the default value of `REAMDE.md` will be assumed.
### license
The `license` field is an optional field containing the license you would like to attribute to your mod. By default all mods are assumed to be licensed under [CC BY 4.0 DEED](https://creativecommons.org/licenses/by/4.0/) and we highly recommend sticking to using the [Creative Commons](https://creativecommons.org/) licenses or the [Unlicense](https://unlicense.org/) (typically meant for software).

```toml
[mod]
license = "CC-BY-4.0"
```

Supported license slugs are defined and verified by registries. If no `license` is defined, it assumed that the mod is being published under the [CC BY 4.0 DEED](https://creativecommons.org/licenses/by/4.0/) license.

> [!important]
> You are solely responsible for verifying that you have permission to republish the resources and assets contained in your mod under the license that you provide.
> 
> We highly recommend getting approval from original authors and provide [[#contributions|attribution]] before using resources that you did not create yourself.
### categories
The `categories` field is a list of strings that define the categories this mod belongs to. This is used for mod organization and discoverability.

```toml
[mod]
categories = ["apparel", "weapons", "gameplay-overhaul"]
```

The registry allows for a maximum of 5 categories but it is recommended that you try to keep the number of listed categories as small as possible. Each category must match one of the strings in [[Mod Categories]] and must match exactly.
### keywords
The `keywords` field is a list of strings that describe the mod. This can help when searching for a mod in the registry, and you may choose any words that would help someone find the mod.

```toml
[mod]
keywords = ["clothing", "armor", "ak-47"]
```

The registry allows for a maximum of 5 keywords. Each keyword must be ASCII text, have at most 20 characters, start with an [alphanumeric](https://en.wikipedia.org/wiki/Alphanumericals) character, and only contain letters, numbers, `_`, `-`, or `+`.
### homepage
The `homepage` is an optional field that should be a URL to a site that is the home page for your mod. A value should be set only if there is a dedicated website for the mod other than the registry page.

```toml
[mod]
homepage = "https://example.org"
```
### publish
The `publish` field is an optional field to control what list of registries the mod should be published to.

```toml
[mod]
publish = ["modi.st"]
```

To prevent a mod from being published to any registry by mistake, you can disable publishing by setting the `publish` field to `false`.

```toml
[mod]
publish = false
```

If `publish` is set to `true`, it is assumed that the mod should be published to default registries.
### include
The `include` field is used to define explicitly what files should be packaged when in a mod is being [[Publishing Mods|published]]. This field is an optional list of patterns to identify the set of files or directories that should be packaged and published (relative to `mod.toml`).

```toml
[mod]
include = ["COPYRIGHT", "images/"]
```

If `include` is not defined, all contents relative to `mod.toml` are considered to be necessary to the mod and will be packaged when a mod is published.

The following files are always included:
- `mod.toml`
- The defined [[#readme]]
### exclude
Inverse to [[#include]], the `exclude` field is used to explicitly specify what files are not packaged when a mod is being [[Publishing Mods|published]]. This field is an optional list of patterns to identify a set of files or directories that should not be packaged published (relative to `mod.toml`).

```toml
[mod]
exclude = ["examples/", ".ci/"]
```

By default, all contents relative to `mod.toml` are considered to be necessary to the mod and will be packaged when a mod is published.

The following files ignore rules defined in `exclude`:
- `mod.toml`
- The defined [[#readme]]

> [!note]
> If a file or directory is listed in both [[#include]] and `exclude`, the file will be included ignoring the rule defined in `exclude`.
### nsfw
If your mod is considered [NSFW](https://en.wikipedia.org/wiki/Not_safe_for_work) it is required that you identify that by specifying the `nsfw` field as `true`.

```toml
[mod]
nsfw = true
```

By default, all mods are considered to be safe for work. If any of your mod contents are deemed to be NSFW by our [[Publishing Mods#Policies|publishing policies]] and this flag is not set, your mod may be delisted from the registry until addressed.
## \[target]
The second most important section in `mod.toml` is the `[target]` section. This section defines the games and game versions that the included mod is intended to support.

Each key within the target must match a defined and supported slug as defined by our [[Mod Targets|mod targets]]. Compatible game versions are defined with [[Dependency Resolution#Version Specifiers|version specifiers]].

```toml
[target]
fallout-4 = ">=4.32.11"
```

If the locally available game matches any of the provided version requirements, the mod is considered to be installable. If an *unsupported* version of the game is available, the mod installation can still be attempted.

If you want to consider any version of a game as supported, you should use the wildcard `*` as the only version specifier. If any other version requirements are specified along with the wildcard, those version requirements are ignored.

```toml
[target]
fallout-4 = "*"
```

> [!note]
> Although multiple target games can be specified within the `[target]` section, most mods should not declare multiple targets. This is valuable only when the exact same mod contents are applicable and supported by the [[#authors]] and [[#maintainers]] across multiple games (which isn't very common).
## \[dependencies]
The `[dependencies]` section define other mods that are required in order for the current mod to function as expected. These mods are listed out as keys containing the name of the mod's publishing user and the mod slug separated by a period (`.`). The value of this key is a [[Dependency Resolution#Version Specifiers|version specifier]] for the mod versions that are compatible.

```toml
[dependencies]
gabe31.my-mod = "1.2.1"
Shei.example-mod2 = ">12.22.1"
```

You can specify a wildcard `*` as the version specifier if no specific version is required for a mod dependency.

```toml
[dependencies]
jailyn0.required-mod = "*"
```

Optional dependencies can be listed out using a inline dictionary as opposed to a string through the use of the `optional` key.

```toml
[depedencies]
aiiv.optional-mod = { version = "*", optional = true }
```
## \[conflicts]
The `[conflicts]` section define other mods that are known to cause conflicts with the current mod. These mods are listed out similarly to the ones in the [[#[dependencies]|dependencies]] section, but the [[Dependency Resolution#Version Specifiers|version specifier]] instead indicates specific versions of the mod that cause conflicts.

```toml
[conflicts]
lulu-zemlak.conflicting-mod = "<=4.3.10"
```

You can specify a wildcard `*` as the version specifier if any version of a listed mod is incompatible with the current mod.

```toml
[conflicts]
aiia221.broken-mod = "*"
```
## \[platform]
The `platform` section is an optional platform that contains platform-specific dependencies. These custom lists of dependencies are rarely required as mods are usually dependent on the game engine as opposed to the operating system.

Supported operating systems are `windows`, `macos`, and `linux`.
Platform-specific dependencies are specified as the following:

```toml
# Windows
[platform.windows.dependencies]
wilhelmine75.windows-dependency = "*"

# Mac OS
[platform.macos.dependencies]
wilhelmine75.mac-dependency = "*"

# Linux
[platform.linux.dependencies]
wilhelmine75.linux-dependency = "*"
```

If specific architecture requirements are needed in conjunction with the target family, please provide them directly after the operating system name. Supported architectures are `x86` and `x86_64`.

```toml
# Windows x86
[platform.windows.x86.dependencies]
wilhelmine75.windows-32-dependency = "*"

# Windows x86_64
[platform.windows.x86_64.dependencies]
wilhelmine75.windows-64-dependency = "*"
```

> [!note]
> This documentation is *incomplete* as we may need to add support for more architectures and potentially more operating systems in the future.

## \[\[tool]]
In the case that your provided mod includes executable tooling that is provided after [[Mod Installation|installation]], you can expose the tool as something that can be called directly from mod management utilities by specifying a `[[tool]]` entry. This is useful for mods that provide alternative executables such as [f4se](https://f4se.silverlock.org/), FNIS, BodySlide, etc...

This section follows the [TOML Array of Tables](https://toml.io/en/v1.0.0#array-of-tables) syntax and provides several keys for you to specify the tool that gets provided as part of the mod.

```toml
[[tool]]
name = "MCE"
description = "My Cool Executable"
exec = "mce.exe"
args = ["-a"]
```
### name
The display name of the tool that mod management utilities can use when listing out your tool as available. This name should be short

```toml
[[tool]]
name = "MCE"
```
### description
A short plaintext description about what the tool is or does. If your tool's `name` is just an acronym, it is highly recommended to spell out the acronym of the tool in this description.

```toml
[[tool]]
name = "MCE"
description = "My Cool Executable"
```
### exec
The `exec` field specifies the relative path (to `mod.toml`) of the packaged binary that should be called when attempting to run the tool.

```toml
[[tool]]
name = "MCE"
description = "My Cool Executable"
exec = "mce.exe"
```
### args
The `args` field is optional and should list out any necessary command-line arguments to use when starting up the `exec` for the tool.

```toml
[[tool]]
name = "MCE"
description = "My Cool Executable"
exec = "mce.exe"
args = ["-a"]
```

## version
In the case that breaking changes to this specification are introduced in the future (not intended), then we may require a major version bump to properly handle the parsing of the `mod.toml` file. In this case we may ask that old versions of the `mod.toml` format provide the optional `version` field with a version number.

```toml
version = 1
```

If no `version` is defined we presume the `mod.toml` document is using the latest standard.
