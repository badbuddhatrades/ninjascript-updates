# NinjaScript Updates

This repository contains version information and update metadata for BadBuddha Customs NinjaScript indicators, addons and strategies.

## Purpose

This repo is the source of truth for version checking in all BadBuddha NinjaScript products. Each product checks its own JSON file to see whether an update is available, and the badbuddhacustoms.com build reads the same files for its download links and "Updated" badges.

## Structure
```
ninjascript-updates/
├── indicators/   e.g. zenzones-pro.json, newsmarkers-lite.json
├── addons/       e.g. karma-guardian.json, trade-disciple.json
└── README.md
```

File names are **case-sensitive** (raw.githubusercontent.com). They must match the `ManifestUrl` constant in each product's source exactly.

## JSON File Format

```json
{
  "product": "BadBuddha_ZenZonesPro",
  "version": "4.1.0.0",
  "releaseDate": "2026-11-20",
  "type": "indicator",
  "tier": "pro",
  "minNinjaTraderVersion": "8.0.0.0",
  "downloadUrl": "https://badbuddhacdn.com/download/ZenZones-Pro/4.1.0.0?source=update",
  "published": "2026-11-20",
  "notes": "One-line headline shown in the update popup.",
  "changelog": ["Short bullet", "Another bullet"]
}
```

| Field | Read by |
|---|---|
| `version`, `downloadUrl` | the in-NinjaTrader updater and the website |
| `releaseDate` | the website (ribbons and Product schema) |
| `published`, `notes`, `changelog` | the in-NinjaTrader update popup |

`notes` and `changelog` must not contain `"`, and changelog items must not contain `]`. The updater's parser stops at those characters.

## How It Works

1. Products check their JSON file on startup (on a cadence) or through a manual update check.
2. If `version` is newer than the installed version, the user sees the update popup with the notes.
3. The download goes through the Cloudflare Worker at badbuddhacdn.com, which logs it to D1 and serves the zip from R2 (`indicators/<key>/v<version>/<key>.zip`).

## Updating Products

Don't edit these files by hand. Use the release tool in the CodeRepo repo:

- In Claude: **"release &lt;product&gt;"** (the `ninjascript-release` skill)
- By hand: `pwsh -File tools/release/release.ps1 -Product <key> -Mode Check`, then `-Mode Publish -NotesFile notes.json`

It uploads the zip to R2, checks the download URL, and only then updates and pushes the JSON. That way customers are never told about a file that isn't live yet.

---

**Note:** This is a public repository. Do not include sensitive information, API keys, or license keys in any files.
