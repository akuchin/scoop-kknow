# scoop-kknow

This is the [Scoop](https://scoop.sh) bucket for
[kknow](https://github.com/akuchin/kknow), a local-first knowledge base for
plain Markdown files.

The source code, the documentation and the issues are in the main repository:
<https://github.com/akuchin/kknow>.

## Install

Add the bucket:

```powershell
scoop bucket add kknow https://github.com/akuchin/scoop-kknow
```

Install the app:

```powershell
scoop install kknow/kknow
```

Install the `kknow` CLI:

```powershell
scoop install kknow/kknow-cli
```

The app gets a shortcut in the Start menu. The CLI gets the `kknow` command.
Both are for 64-bit Windows only.

## Update

```powershell
scoop update kknow kknow-cli
```

The app can also update itself, but on Windows it does this with the MSI
installer. The installer puts a second copy of the app into `Program Files`,
apart from the Scoop copy. Thus, if you install the app with Scoop, turn off
**Settings → General → Update automatically** and do not use the
**Check now** button. Update the app with Scoop only.

## Remove

```powershell
scoop uninstall kknow kknow-cli
```

The settings of the app stay in `%APPDATA%\dev.kknow.desktop`. Your vaults
stay unchanged, because they are ordinary folders with `.md` files.

## About SmartScreen

The app is not signed. Thus Windows SmartScreen can show a warning on the
first launch. Click **More info**, then **Run anyway**.

## Release a new version

The release workflow of kknow updates the manifests in [`bucket`](bucket)
after each release. For this, the kknow repository needs the
`SCOOP_BUCKET_TOKEN` secret.

The manifests use these files of the
[releases of kknow](https://github.com/akuchin/kknow/releases):

- `kknow.json`: `kknow_<version>_x64_en-US.msi`. Scoop extracts the MSI
  package and does not run it.
- `kknow-cli.json`: `kknow-cli-v<version>-x86_64-pc-windows-msvc.zip`.

To update a manifest by hand, change `version`, the `url` and the `hash`.
GitHub shows the digests of the files:

```bash
gh api repos/akuchin/kknow/releases/latest --jq '.assets[] | select(.name | test("x64_en-US.msi$|windows-msvc.zip$")) | "\(.name) \(.digest)"'
```

On Windows, Scoop can also do this from the `checkver` and `autoupdate`
fields:

```powershell
& "$(scoop prefix scoop)\bin\checkver.ps1" -Dir bucket -Update
```
