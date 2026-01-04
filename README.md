# NinjaScript Updates

This repository contains version information and update metadata for BadBuddha Customs NinjaScript indicators and strategies.

## Purpose

This repo serves as the central source of truth for version checking in all BadBuddha NinjaScript products. Each indicator/strategy checks its corresponding JSON file to determine if updates are available.

## Structure
```
ninjascript-updates/
├── indicators/
│   ├── InitialBalance-Lite.json
│   ├── InitialBalance-Pro.json
│   └── ...
├── strategies/
│   └── ...
└── README.md
```

## JSON File Format

Each product has a JSON file with the following structure:
```json
{
  "productName": "Initial Balance Fibonacci Extensions",
  "productType": "Lite",
  "latestVersion": "2.1.1.0",
  "releaseDate": "2026-01-03",
  "downloadUrl": "https://ninjascript-downloads.badbuddhacustoms.workers.dev/download/InitialBalance-Lite/2.1.1.0?source=update",
  "releaseNotes": "Bug fixes and performance improvements",
  "minimumNTVersion": "8.0.0.0"
}
```

## How It Works

1. NinjaScript indicators/strategies check their corresponding JSON file on startup or via manual update check
2. If the `latestVersion` is newer than the installed version, user is notified
3. User can click to download the update from the `downloadUrl`
4. Downloads are served via Cloudflare Workers with tracking and analytics

## Updating Products

When releasing a new version:

1. Upload new ZIP file to R2 storage at appropriate path
2. Update the corresponding JSON file in this repo with:
   - New `latestVersion` number
   - New `releaseDate`
   - Updated `downloadUrl` with new version
   - New `releaseNotes`
3. Commit and push changes
4. Updates will be available to users within minutes

## Access

- **Raw JSON URLs:** Use GitHub raw content URLs for programmatic access
- **Format:** `https://raw.githubusercontent.com/badbuddhacustoms/ninjascript-updates/main/indicators/{ProductName}-{Type}.json`

## Questions or Issues?

Visit [BadBuddha Customs](https://www.badbuddhacustoms.com) or contact support.

---

**Note:** This is a public repository. Do not include sensitive information, API keys, or license keys in any files.
