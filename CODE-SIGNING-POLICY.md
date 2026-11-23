# Code signing policy

## macOS

`aiBridge.app` in the `.dmg` is signed with the project owner's Apple Developer ID and notarized by Apple, with the
notarization ticket stapled to the app. macOS opens it without extra steps. To check the signature after you copy it
to Applications:

```
codesign -dv --verbose=2 /Applications/aiBridge.app
spctl -a -vv /Applications/aiBridge.app
```

## Windows

The installer (`.msi`), the `.zip` and the programs in them (`mcp-bridge.exe`, `aiBridge.exe`) are not code-signed
yet, so Windows SmartScreen may ask you to confirm the first start. Check the download against `SHA256SUMS` (below)
before you open it.

## Linux

The `.deb` and `.tar.gz` files are not signed. Check them against `SHA256SUMS` (below).

## How a release is made

- Builds are made by the project owner from the project's private source and uploaded by hand to the
  [Releases page](https://github.com/ai4coo/aiBridge/releases). No hosted build service is used.
- Every release is approved by the project owner before it is published.
- Each release has a `SHA256SUMS` file. To check a download, put it in the same folder as `SHA256SUMS` and run
  `sha256sum -c SHA256SUMS --ignore-missing` (Linux) or `shasum -a 256 -c SHA256SUMS --ignore-missing` (Mac). On
  Windows, run `Get-FileHash <file>` in PowerShell and compare the hash with the file's line in `SHA256SUMS`.

## Roles

The project owner is the only author, reviewer and approver.

## Privacy

See [PRIVACY.md](PRIVACY.md): aiBridge sends no information about you to the author or anyone else.

## Reporting a problem

If you think a release file is wrong or malicious, open an issue at https://github.com/ai4coo/aiBridge/issues.
