# J2G — Release Binaries

Pre-built binaries for **J2G** (Jenkins to GitLab CI migration tool),
distributed via GitHub Releases for fast public downloads.

> **About this repository.** This repo is a **binary distribution endpoint
> only**. It contains **no application source code** — the full source for
> the J2G app is closed-source and lives in a private repository. The only
> files in this repo are this `README.md` and `NOTICE.md`. The "Source code"
> archives that GitHub auto-attaches to every release contain those two
> files only — see [`NOTICE.md`](./NOTICE.md) for details.

## Downloads

See the [**Releases**](../../releases) tab.

For the latest version (auto-updating links — always serve the most recent build):

### macOS
- Apple Silicon (recommended): https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-arm64.dmg
- Intel:                       https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-x64.dmg

### Windows
- Universal (works on x64 and ARM64, recommended): https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-Setup.exe
- x64 only:   https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-Setup-x64.exe
- ARM64 only: https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-Setup-arm64.exe

### Linux
- AppImage (x64):       https://github.com/NexWright/j2g-releases/releases/latest/download/J2G-x64.AppImage
- Debian/Ubuntu (x64):  https://github.com/NexWright/j2g-releases/releases/latest/download/j2g_amd64.deb

> Equivalent tag-based URLs (Docker-style) work too:
> `https://github.com/NexWright/j2g-releases/releases/download/latest/J2G-arm64.dmg` etc.
> Both URL forms point at the same files; pick whichever your tooling prefers.
> Browse the [Releases](../../releases) tab to download a specific version.

## Verifying integrity

Every release ships with `SHA256SUMS.txt` and a detached GPG signature
`SHA256SUMS.txt.asc`. The public key `pubkey.asc` is also attached so
verification is fully self-contained:

```bash
# Use /releases/latest/download/<name> to always grab from the most recent release
BASE="https://github.com/NexWright/j2g-releases/releases/latest/download"

# Download the verification triple from the release
curl -fLO "$BASE/pubkey.asc"
curl -fLO "$BASE/SHA256SUMS.txt"
curl -fLO "$BASE/SHA256SUMS.txt.asc"

# Import the signing key, verify the manifest signature
gpg --import pubkey.asc
gpg --verify SHA256SUMS.txt.asc SHA256SUMS.txt

# Then download the artifact you want and verify its checksum
curl -fLO "$BASE/J2G-arm64.dmg"
shasum -a 256 -c SHA256SUMS.txt 2>&1 | grep "J2G-arm64.dmg"
```

GPG signing key fingerprint:

```
2B19 0CCE C733 77DE A10A  2ECA 2D50 0037 4DAF EE5D
```

(That's the master key. Releases are signed by subkey
`8E9F 5741 2E98 5929 01C0  C5E9 8621 1178 CAA0 25D5`, present in
`pubkey.asc`.)

AppImage builds also ship a detached `.asc` signature next to each
AppImage, signed by the same subkey.

## Auto-update

J2G builds ship with electron-updater and check for updates automatically
once installed — there is no need to manually re-download from this page
after the first install.

## Support

For licensing, support, and pricing: <https://nexwright.com/apps/j2g>
