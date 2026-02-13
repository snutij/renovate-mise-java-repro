# mise manager: Java update produces invalid version without vendor prefix

## Current behavior

Given `mise.toml` with `java = "21"` (bare shorthand = OpenJDK), Renovate proposes updating to `java = "21.0.10+7.0.LTS"`.

This version string comes from the Adoptium (Temurin) datasource and does not exist in mise without the `temurin-` prefix. Running `mise install` fails:

```
mise ERROR Failed to install core:java@21.0.10+7.0.LTS: no metadata found for version 21.0.10+7.0.LTS
```

See the [failing CI on PR #1](https://github.com/snutij/renovate-mise-java-repro/pull/1).

## Expected behavior

Either:
1. The proposed version should include the vendor prefix: `java = "temurin-21.0.10+7.0.LTS"`
2. Or, when the original value is a bare major shorthand (`"21"`), only propose versions valid in that format (e.g. `"22"` for a major bump)

## Link to the Renovate Issue or Discussion

https://github.com/renovatebot/renovate/discussions/41159
