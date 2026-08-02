# compat-reports

Automated game-compatibility submissions, logs, and analysis reports for [Viridite](https://github.com/Viridite). This repo is **written entirely by automation** — submit through the [website form](https://viridite.aaronworld.uk/submit), not by editing anything here directly. Please don't hand-edit `reports/`, `pending/`, or `data/games.json` — the next automated submission will just overwrite manual changes.

## Structure

```
data/games.json          — aggregated index consumed by the website's compatibility page
pending/<id>/            — a submission queued by the Cloudflare Worker, waiting for
                            the GitHub Action to process it (transient — deleted once
                            processed, or left with an error.txt if something failed)
reports/<package>/<version>/
  report.md              — auto-generated verdict + log analysis
  launcher_log.txt        — as submitted
  compat_log.txt          — as submitted
  core_log.txt            — as submitted
  icon.png                — extracted from the APK's manifest/resources, if found
  meta.json               — submitter (optional, unverified GitHub username), source
                             APK URL + SHA-256, source site, timestamp
```

Only the **most recent submission for a given package+version** is kept — a repeat submission for the same version overwrites the previous one's logs entirely (older submitter's report is superseded, not appended). Different versions of the same package each get their own folder.

## How a submission gets here

There's no GitHub issue or account involved anywhere in this — see the [website's submission form](https://viridite.aaronworld.uk/submit) and [docs](https://viridite.aaronworld.uk/docs#submitting-reports) for the visitor-facing side.

1. Someone fills out the form on the website: an APK link, where it came from, the three log files, and optionally a GitHub username for credit.
2. The form POSTs to a small Cloudflare Worker (`website/worker/`), which is the only thing holding a GitHub token — it never reaches the browser. The Worker writes the submission as plain files under `pending/<id>/` here via the Contents API, then fires a `repository_dispatch` event at Viridite. This is the whole reason the old GitHub-issue-based intake got replaced: issue forms (and `repository_dispatch` payloads) cap out around 64KB, and `compat_log.txt` routinely blows past that — writing real files instead of stuffing text into an API field sidesteps the limit entirely.
3. Viridite's [`compat-submission.yml`](https://github.com/Viridite/Viridite/blob/main/.github/workflows/compat-submission.yml) workflow picks up the `pending/<id>/` entry, downloads the APK, reads its package/version/name/icon via androguard, checks the Play Store category, and runs [`process_compat_submission.py`](https://github.com/Viridite/Viridite/blob/main/.github/scripts/process_compat_submission.py)'s log analysis (frame-stall counts, crash/error signatures, whether the game ever actually rendered a frame) to produce a verdict.
4. The result is committed here, `data/games.json` is updated, and the `pending/<id>/` entry is deleted. If anything fails, the pending entry is kept with an `error.txt` explaining why, and the workflow run shows failed in the Actions tab — there's no issue thread to post a comment on anymore.
