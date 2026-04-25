# PodToolbox Desktop

Native desktop wrapper for [podwires.com/podtoolbox](https://podwires.com/podtoolbox/) — community-curated podcast tools, services and resources.

A fully separate Electron app from [`podwires-desktop`](https://github.com/realmikosantos/podwires-desktop) (which wraps `podwires.com`). Different `appId`, different protocol, different release cadence.

## Builds

Tagged releases (`v*`) trigger a GitHub Actions workflow that builds:

| OS      | Outputs                              |
|---------|--------------------------------------|
| macOS   | `.dmg` + `.zip` (arm64 & x64)        |
| Windows | `.exe` (NSIS installer + portable)   |
| Linux   | `.AppImage` + `.deb` (x64)           |

Artifacts are attached to a draft GitHub Release. Promote the draft to "latest" and the download URLs at `podwires.com/podtoolbox/download/` resolve automatically.

## Develop

```bash
npm install
npm run start    # launch the app
npm run dev      # launch with --dev flag
```

## Release

```bash
git tag v1.0.0 && git push --tags
```

## App config

Set in `src/main.js`:

- `APP_URL`  — `https://podwires.com/podtoolbox/`
- `APP_HOST` — `podwires.com` (any URL outside `/podtoolbox/` opens in default browser)
- `PROTOCOL` — `podtoolbox://` deep links
- `appId`    — `com.podwires.podtoolbox`

## Code signing

Optional — release runs without signing if certs aren't configured. To enable:

| Secret | Purpose |
|---|---|
| `MAC_CERT_P12_BASE64` | base64'd `.p12` from Apple Developer ID Application cert |
| `MAC_CERT_PASSWORD` | password for the `.p12` |
| `APPLE_ID`, `APPLE_APP_SPECIFIC_PASSWORD`, `APPLE_TEAM_ID` | for notarization |
| `WIN_CERT_PFX_BASE64`, `WIN_CERT_PASSWORD` | Windows code-signing cert |

Without these, macOS users see "unidentified developer" on first launch (right-click → Open).
