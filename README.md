# Renovate Config

[![CGL](https://img.shields.io/github/actions/workflow/status/CPS-IT/renovate-config/cgl.yaml?label=cgl&logo=github)](https://github.com/CPS-IT/renovate-config/actions/workflows/cgl.yaml)

This repository provides some configuration presets for [Renovate][1]-managed projects
developed at CPS GmbH.

## 🚢 Configuration presets

This repository provides various [configuration presets][2]. You can reference all presets
like this in your `renovate.json` file:

```json
{
    "extends": [
        "github>CPS-IT/renovate-config:<preset>"
    ]
}
```

Replace `<preset>` with the basename of the configuration file to be used, e.g.
`github>CPS-IT/renovate-config:typo3-project`. For the `default` preset, you can leave out
the preset name. Consult the [official documentation][3] for deeper insights.

### Default preset

💻 Config file: [`default.json`](default.json)\
➡️ Reference: `github>CPS-IT/renovate-config`

#### Usage

```json
{
    "$schema": "https://docs.renovatebot.com/renovate-schema.json",
    "extends": ["github>CPS-IT/renovate-config"]
}
```

#### Description

This preset provides a solid base configuration for all projects developed at CPS GmbH.
Consider using more specific presets in your projects since they might be better suited.

#### Key configuration

| Configuration key                       | Value               | Description                                                                             |
|-----------------------------------------|---------------------|-----------------------------------------------------------------------------------------|
| [`:separatePatchReleases`][4]           | _Preset_            | Separate patch and minor releases into separate MRs                                     |
| [`:automergePatch`][14]                 | _Preset_            | Automerge patch upgrades if they pass tests                                             |
| [`:automergeRequireAllStatusChecks`][5] | _Preset_            | Require successful CI for auto-merge                                                    |
| [`schedule:weekdays`][6]                | _Preset_            | Schedule one Renovate run per weekday (triggered by renovate/renovate-runner>)          |
| [`configMigration`][7]                  | `true`              | Enables migration of Renovate config on a repository basis                              |
| [`lockFileMaintenance`][8]              | `{"enabled": true}` | Enable dependency updates of all locked dependencies, including transitive dependencies |
| [`osvVulnerabilityAlerts`][9]           | `true`              | Enable vulnerability alerts fetched from https://osv.dev                                |
| [`prConcurrentLimit`][10]               | `10`                | Limit concurrent MRs to 10                                                              |
| [`labels`][11]                          | `["dependencies"]`  | Always add `dependencies` label to MRs                                                  |

#### Package rules

| Ruleset              | Matching packages                       | Description                                                                            |
|----------------------|-----------------------------------------|----------------------------------------------------------------------------------------|
| Development packages | `devDependencies`, `require-dev`        | All packages used for development, updates in minor and patch range will be automerged |
| PHPStan packages     | `phpstan/*`, various PHPStan extensions | PHPStan and extensions, will ge grouped as `PHPStan`                                   |

### Git Flow preset

💻 Config file: [`git-flow.json`](git-flow.json)\
➡️ Reference: `github>CPS-IT/renovate-config:git-flow`

#### Usage

```json
{
    "$schema": "https://docs.renovatebot.com/renovate-schema.json",
    "extends": ["github>CPS-IT/renovate-config:git-flow"]
}
```

#### Description

Use this preset for Git Flow managed projects.

#### Key configuration

| Configuration key    | Value           | Description                                                               |
|----------------------|-----------------|---------------------------------------------------------------------------|
| [`baseBranches`][12] | `["develop"]`   | Overrides base branch to `develop` (will be used as target branch in MRs) |

### TYPO3 extension preset

💻 Config file: [`typo3-extension.json`](typo3-extension.json)\
➡️ Reference: `github>CPS-IT/renovate-config:typo3-extension`

#### Usage

```json
{
    "$schema": "https://docs.renovatebot.com/renovate-schema.json",
    "extends": ["github>CPS-IT/renovate-config:typo3-extension"]
}
```

#### Description

Use this preset for TYPO3 extensions.

#### Key configuration

| Configuration key     | Value   | Description                    |
|-----------------------|---------|--------------------------------|
| [`rangeStrategy`][13] | `widen` | Widen the range with newer one |

#### Package rules

| Ruleset                 | Matching packages | Description                                             |
|-------------------------|-------------------|---------------------------------------------------------|
| TYPO3 system extensions | `typo3/cms-*`     | TYPO3 system extensions, will be grouped as `TYPO3 CMS` |

### TYPO3 project preset

💻 Config file: [`typo3-project.json`](typo3-project.json)\
➡️ Reference: `github>CPS-IT/renovate-config:typo3-project`

#### Usage

```json
{
    "$schema": "https://docs.renovatebot.com/renovate-schema.json",
    "extends": ["github>CPS-IT/renovate-config:typo3-project"]
}
```

#### Description

Use this preset for TYPO3 projects (bundles).

#### Key configuration

| Configuration key     | Value           | Description                                                                           |
|-----------------------|-----------------|---------------------------------------------------------------------------------------|
| [`rangeStrategy`][13] | `in-range-only` | Update the lock file when in-range updates are available, ignore package file updates |

#### Package rules

| Ruleset                 | Matching packages | Description                                                               |
|-------------------------|-------------------|---------------------------------------------------------------------------|
| TYPO3 system extensions | `typo3/cms-*`     | TYPO3 system extensions, no major updates, will be grouped as `TYPO3 CMS` |

## 💎 Credits

All config presets are heavily inspired by the [glorious config repository][99] from
Pagemachine. If you like it, consider starring this repository.

## 🧑‍💻 Contributing

Please have a look at [`CONTRIBUTING.md`](CONTRIBUTING.md).

## ⭐ License

This project is licensed under [GNU General Public License 3.0 (or later)](LICENSE).



[1]: https://github.com/renovatebot/renovate
[2]: https://docs.renovatebot.com/config-presets/
[3]: https://docs.renovatebot.com/config-presets/#github
[4]: https://docs.renovatebot.com/presets-default/#separatepatchreleases
[5]: https://docs.renovatebot.com/presets-default/#automergerequireallstatuschecks
[6]: https://docs.renovatebot.com/presets-schedule/#scheduleweekdays
[7]: https://docs.renovatebot.com/configuration-options/#configmigration
[8]: https://docs.renovatebot.com/configuration-options/#lockfilemaintenance
[9]: https://docs.renovatebot.com/configuration-options/#osvvulnerabilityalerts
[10]: https://docs.renovatebot.com/configuration-options/#prconcurrentlimit
[11]: https://docs.renovatebot.com/configuration-options/#labels
[12]: https://docs.renovatebot.com/configuration-options/#basebranches
[13]: https://docs.renovatebot.com/configuration-options/#rangestrategy
[14]: https://docs.renovatebot.com/presets-default/#automergepatch
[99]: https://github.com/pagemachine/renovate-config
