# Coverage Trackers — Claude Instructions

## Branch policy

**Always commit and push directly to `main`.** Do not create feature branches. Do not open pull requests. Every update — scheduled refreshes and new tracker builds — goes straight to `main` so GitHub Pages reflects the change immediately.

```
git add <file>
git commit -m "..."
git push origin main
```

## Repo layout

```
<client-slug>/index.html   ← live tracker page (served by GitHub Pages)
<client-slug>-tracker      ← legacy root-level artifact (do not update)
README.md
CLAUDE.md                  ← this file
```

Each tracker is a single self-contained HTML file with an embedded `<script id="coverage-data" type="application/json">` block that holds all coverage data. Scheduled tasks update only that JSON block, then push to `main`.

## Scheduled refresh tasks

1. Read the existing `<client-slug>/index.html`.
2. Run WebSearch for the client's tracked terms (listed in `payload.terms`).
3. Merge new hits into the `earnedMedia`, `ownedMedia`, and/or `competitorMedia` arrays — skip anything already present (match on `url`).
4. Update `lastUpdated` to the current UTC timestamp.
5. Write the updated file back to `<client-slug>/index.html`.
6. Commit with message: `Refresh <client> tracker <ISO timestamp>`.
7. Push directly to `main`.

## Creating a new tracker

1. Create `<client-slug>/index.html` using the Planview tracker (`planview/index.html`) as the structural template.
2. Update the `<script id="coverage-data">` JSON: set `client`, `terms`, `domain`, and clear `earnedMedia`/`ownedMedia`/`competitorMedia` to empty arrays.
3. Update the `<meta>` artifact block at the top with the correct name and description.
4. Match the brand accent color in CSS (`.chip.active`, `.tab.active`, `.headline-cell a`, `button.primary`).
5. Add the client to the table in `README.md`.
6. Commit and push directly to `main`.

## Live trackers

| Client | Slug | Tracked terms |
|---|---|---|
| Pluralsight | `pluralsight` | Pluralsight |
| Planview | `planview` | Planview, Louise Allen, Anvi |
| Lattice Semiconductor | `lattice-semi` | Lattice Semi, Lattice Semiconductor, Lattice FPGAs, MachXO5 |
