# vscode-gtk-filechoosers-enter

Restores Enter to accept in VS Code's native GTK 3 Open File, Open Folder, and Save As dialogs. Workaround for [electron/electron#54670](https://github.com/electron/electron/issues/54670).

Requires a C compiler, Make, pkg-config, and GTK 3 development headers (`libgtk-3-dev` on Ubuntu).

```sh
git clone https://github.com/64kramsystem/vscode-gtk-filechoosers-enter.git ~/local/vscode-gtk-filechoosers-enter
cd ~/local/vscode-gtk-filechoosers-enter
make
mkdir -p ~/.local/bin
ln -s "$PWD/code" ~/.local/bin/code
```

Ensure `~/.local/bin` comes before `/usr/bin` in `PATH`. Quit VS Code completely, then run `code`. Child processes inherit `GTK3_MODULES`, but the module only installs its hook when the executable is named `code`. `/usr/bin/code` remains available without the launcher.

The module replaces Chromium's custom accept response with `GTK_RESPONSE_ACCEPT`, restoring the default button, file activation with Enter or a double click, and Save As overwrite confirmation. It handles single-file and multiple-file Open dialogs, Open Folder, and Save As. Set `VSCODE_GTK_FILECHOOSERS_DEBUG=1` to log when a dialog is fixed. Originally tested with VS Code 1.145.2 / Electron 43.8.3 / GTK 3.24.41.

Only the native GTK 3 chooser is supported; GTK 4 and XDG portal dialogs are unaffected.
