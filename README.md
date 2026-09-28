# homebrew-runner

Pinned Homebrew formulae for the self-hosted macOS CI runner (qinmini),
required by `algorithm/dev/ci/dependencies.contract.json` in magic-apps.
Tracked in MangoFuture1210/infra-ops#511.

| Formula | Version | Source (Homebrew/homebrew-core) |
| --- | --- | --- |
| `ffmpeg@6` | 6.1.5 | `3b66ccfb000e09e277904a2686254aeb80f258b6` |
| `fluid-synth` | 2.4.6 | `f1b198b33211f7f2322939da0e82bc016119f4de` |
| `lame` | 3.100 | `e8c27fb0b078f479404e7950ff1f28d86182d5d8` |

Each formula is copied from the listed commit with these changes:

- `lame` and `fluid-synth`: `root_url "https://ghcr.io/v2/homebrew/core"` in
  the bottle block, so the official bottles (checksums unchanged) are
  downloaded. Their linked libraries still match current homebrew-core.
- `ffmpeg@6`: bottle block removed, so it builds from source on install. The
  6.1.5 bottle links `x265` 216, `jpeg-xl` 0.11, `libbluray` 3 and `sdl2`,
  which current homebrew-core no longer ships. `sdl2` is replaced by
  `sdl2-compat` and the backport patch URL follows the current
  homebrew-core `ffmpeg@6` formula; source tarball and patch checksums are
  pinned.
- `ffmpeg@6` keeps the plain `lame` dependency. Its dependency `libsndfile`
  also depends on `lame`; qualifying one of them makes Homebrew lock
  `Cellar/lame` twice and abort. Install and pin the tap `lame` first so the
  plain name resolves to the installed 3.100 keg.

## Install

```bash
brew tap mangofuture1210/runner
brew trust --tap mangofuture1210/runner
brew install mangofuture1210/runner/lame mangofuture1210/runner/fluid-synth
brew pin lame fluid-synth
brew install mangofuture1210/runner/ffmpeg@6
brew pin ffmpeg@6
```

Formula names match homebrew-core, so always use the fully qualified name.
Do not `brew upgrade` or unpin these on the runner; version changes go
through a PR here and a matching update of the magic-apps contract.
