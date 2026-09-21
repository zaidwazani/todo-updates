# todo-updates

This is the update feed for the TODO desktop app. **It contains no source
code.** The app's source is kept in a separate private repository.

The only things here are the files TODO's built-in updater downloads, and
they are published as release assets:

- `latest.json`: the newest version, and where to download it
- `TODO_<version>_x64-setup.exe`: the Windows installer
- `TODO_<version>_x64-setup.exe.sig`: its updater signature

TODO checks
`https://github.com/zaidwazani/todo-updates/releases/latest/download/latest.json`.
Before installing anything, it verifies the download against a public key
compiled into the app. It refuses an update that:

- is unsigned;
- has been tampered with;
- is signed for a different version than the one announced;
- is older than the version already installed.

The installers are signed for TODO's updater only. They are **not**
Authenticode-signed, so Windows SmartScreen may warn when one is run by hand.
macOS update artifacts are not published yet.
