# homebrew-runner

Pinned Homebrew formulae for the self-hosted macOS CI runner (qinmini),
required by `algorithm/dev/ci/dependencies.contract.json` in magic-apps.
Tracked in MangoFuture1210/infra-ops#511.

| Formula | Version | Source (Homebrew/homebrew-core) |
| --- | --- | --- |
| `ffmpeg@6` | 6.1.5 | `3b66ccfb000e09e277904a2686254aeb80f258b6` |
| `fluid-synth` | 2.4.6 | `f1b198b33211f7f2322939da0e82bc016119f4de` |
| `lame` | 3.100 | `e8c27fb0b078f479404e7950ff1f28d86182d5d8` |

Each formula is copied verbatim from the listed commit with two changes:

- `root_url "https://ghcr.io/v2/homebrew/core"` in the bottle block, so the
  official bottles (checksums unchanged) are downloaded instead of building
  from source.
- `ffmpeg@6` depends on `mangofuture1210/runner/lame` instead of core `lame`.

## Install

```bash
brew tap mangofuture1210/runner
brew install mangofuture1210/runner/lame mangofuture1210/runner/fluid-synth mangofuture1210/runner/ffmpeg@6
brew pin lame fluid-synth ffmpeg@6
```

Formula names match homebrew-core, so always use the fully qualified name.
Do not `brew upgrade` or unpin these on the runner; version changes go
through a PR here and a matching update of the magic-apps contract.
