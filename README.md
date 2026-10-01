# todo-updates

This is the update feed and download location for the TODO desktop app. **It
contains no source code.** The app's source is kept in a separate private
repository.

The only things here are the files TODO's built-in updater downloads, and the
installers, all published as release assets.

## What each release contains

| File | What it is |
|---|---|
| `latest.json` | The newest version, and where each platform downloads it |
| `TODO_<version>_x64-setup.exe` | The Windows installer (x64). It is also the Windows update payload |
| `TODO_<version>_x64-setup.exe.sig` | Its updater signature |
| `TODO_<version>_aarch64.app.tar.gz` | The macOS update payload (Apple silicon), published since v0.3.4 |
| `TODO_<version>_aarch64.app.tar.gz.sig` | Its updater signature |
| `TODO_<version>_aarch64.dmg` | The macOS installer (Apple silicon), published since v0.3.4 |
| `TODO-windows-x64-setup.exe`, `TODO-macos-arm64.dmg` | Byte-identical copies of that release's installers under fixed names, published since v0.3.4. The updater never uses them |

Fixed download links, which always point at the newest release:

- Windows (x64):
  `https://github.com/zaidwazani/todo-updates/releases/latest/download/TODO-windows-x64-setup.exe`
- macOS (Apple silicon, M1 or later):
  `https://github.com/zaidwazani/todo-updates/releases/latest/download/TODO-macos-arm64.dmg`

There is no Intel Mac build, no Windows on ARM build and no Linux build.

## How the updater decides what to trust

TODO checks
`https://github.com/zaidwazani/todo-updates/releases/latest/download/latest.json`.
Before installing anything, it verifies the download against a public key
compiled into the app. It refuses an update that:

- is unsigned;
- has been tampered with;
- is signed for a different version than the one announced;
- is older than the version already installed.

## What is not signed yet

The updater signature protects people who already have TODO. It does not
make a first download trusted by the operating system:

- **Windows:** the installers are **not** Authenticode-signed, so Windows
  SmartScreen may warn when one is run by hand.
- **macOS:** the app is **not** signed with an Apple Developer ID and is
  **not** notarized. macOS may refuse to open a downloaded copy.

## Status

Releases here are being tested by the developer. They are not yet
recommended for general use.

## Known issue

On macOS, installing an update from inside the app has not yet been seen to
work: in the first real attempt (from version 0.3.3), the update was found
and downloaded but was not installed. Version 0.3.6 shows an error when an
install fails, and refuses to install while TODO is not running from a
folder it can replace, such as the Applications folder. Whether updating
from inside the app now works on macOS has not yet been confirmed. On
Windows, updating from inside the app works. This page will say when the
macOS issue is fixed.
