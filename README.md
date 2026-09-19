# homeos-plugin-dnf-copr

![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)

A [homeos](https://github.com/homeos-dev/homeos) plugin that enables a [COPR](https://copr.fedorainfracloud.org/) repository on DNF-based systems (Fedora, RHEL, and derivatives). Use it as a dependency of packages installed via the [dnf plugin](https://github.com/homeos-dev/homeos-plugin-dnf) when those packages live in a COPR.

## Usage

Add the plugin to your homeos repository:

```sh
homeos plugin add dnf-copr
```

Define a setup package that enables the COPR, and have the actual package depend on it:

```sh
$ homeos package add dnf-copr-mise --plugin dnf-copr --param name=jdxcode/mise
$ homeos package add mise --plugin dnf --param name=mise --depends-on dnf-copr-mise
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `name` | COPR repository in `user/repo` form (e.g., `jdxcode/mise`) |

## Actions

| Action | Command |
|--------|---------|
| install | `sudo dnf -y copr enable {{name}}` |
| update | None — COPR content refreshes via `dnf upgrade` (skipped automatically) |
| uninstall | `sudo dnf -y copr disable {{name}}` |

## License

Licensed under either of

 * Apache License, Version 2.0
   ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license
   ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
