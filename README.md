# Coverage Trackers

Live, scheduled-task-refreshed coverage tracker pages for client accounts.

Each client lives in its own subfolder; GitHub Pages serves them at
`https://hanrburns.github.io/coverage-trackers/<client>/`.

| Client | Live URL |
|---|---|
| Pluralsight | https://hanrburns.github.io/coverage-trackers/pluralsight/ |

The HTML files here are written by a Claude scheduled task that runs on a
weekday cadence (9am / 1pm / 5pm local). The task pulls fresh hits from
WebSearch, merges them into the embedded `<script id="coverage-data">`
JSON block, and pushes the updated file to this repo. The ClickUp embed
in the relevant client account loads the GitHub Pages URL above, so it
reflects the latest data on every view.

Do not commit deploy tokens, screenshots, or anything else under the
ignored paths in `.gitignore`.
