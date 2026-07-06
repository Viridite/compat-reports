# compat-reports

Automated game-compatibility submissions, logs, and analysis reports for [Android Horizon](https://github.com/AndroidHorizon). This repo is **written entirely by automation** — a GitHub Actions workflow in [AndroidHorizonNX](https://github.com/AndroidHorizon/AndroidHorizonNX) processes each ["Game compatibility report"](https://github.com/AndroidHorizon/AndroidHorizonNX/issues/new?template=game-compatibility-report.yml) issue and commits the result here. Please don't hand-edit `reports/` or `data/games.json` — the next automated submission will just overwrite manual changes.

## Structure

```
data/games.json          — aggregated index consumed by the website's compatibility page
reports/<package>/<version>/
  report.md              — auto-generated verdict + log analysis
  launcher_log.txt        — as submitted
  compat_log.txt          — as submitted
  core_log.txt            — as submitted
  icon.png                — extracted from the submitted APK, if found
  meta.json               — submitter, source APK URL, source site, issue link, timestamp
```

Only the **most recent submission for a given package+version** is kept — a repeat submission for the same version overwrites the previous one's logs entirely (older submitter's report is superseded, not appended). Different versions of the same package each get their own folder.

## How a submission gets here

1. Someone opens a [Game compatibility report](https://github.com/AndroidHorizon/AndroidHorizonNX/issues/new?template=game-compatibility-report.yml) issue on AndroidHorizonNX.
2. The `compat-submission.yml` workflow there validates the APK link, downloads it, extracts an icon, checks the Play Store category, and runs an automated pass over the three logs (frame-stall counts, crash/error signatures, whether the game ever actually started rendering frames) to produce a verdict.
3. The result is committed here, `data/games.json` is updated, and the originating issue is closed + locked with a summary comment.

See the [`compat-submission.yml` workflow](https://github.com/AndroidHorizon/AndroidHorizonNX/blob/main/.github/workflows/compat-submission.yml) and [`process_compat_submission.py`](https://github.com/AndroidHorizon/AndroidHorizonNX/blob/main/.github/scripts/process_compat_submission.py) for exactly how.
