# Python and Vim editor setup

The editor supports the learning agreement: the user writes the code, sees
diagnostics, runs tests deliberately, and learns a few shortcuts at a time.

## Recommended extensions

Install these extensions in VS Code on each machine. Recommendations are
documented here rather than supplied as a workspace extension list.

| Extension | Purpose |
| --- | --- |
| Python | Interpreter selection and Python integration. |
| Pylance | Completion, navigation, and basic type diagnostics. |
| Python Debugger | Breakpoints and inspecting a running program. |
| Python Environments | Discover and activate the local virtual environment. |
| Ruff | Python linting, formatting, and import sorting. |
| PowerShell | Help when editing PowerShell scripts; optional on macOS. |
| VSCodeVim | Learn modal editing inside VS Code. |
| Markdown All in One | Help maintaining the project documentation. |

Git support is built into VS Code. Additional Git extensions are optional, and
learning Git does not require installing GitLens. Prettier remains available for
other file types; Ruff is the selected Python formatter. No extra error-display
or AI completion extension is necessary to start.

## Global User settings

Formatting, Vim, and general editor preferences live in VS Code's **User**
settings. Open **Preferences: Open User Settings (JSON)** from the Command
Palette to inspect them. They apply across projects unless Workspace settings
override them.

- Python uses four spaces, Ruff formatting on save, an 88-column guide matching
  `pyproject.toml`, and import sorting on explicit saves. General lint fixes are
  not applied automatically; discuss diagnostics before changing behavior.
- Pylance uses basic type checking.
- Saving is explicit. Text files use LF line endings, and Git's line-ending
  policy is recorded in `.gitattributes`.
- Smart Commit is disabled globally, so learning staging remains explicit.
  The Sync action retains its confirmation prompt.
- Vim is enabled globally and uses the system clipboard. Familiar Ctrl
  shortcuts are delegated to VS Code. On macOS, familiar Command shortcuts remain
  available.

The shared `.vscode/settings.json` contains only Tether's Python environment
and test discovery settings: the repository's `.venv`, unittest, and the
`test_*.py` pattern inside `tests/`. There are no test cases yet. Each machine
creates its own environment. If VS Code already selected another interpreter,
run **Python: Select Interpreter** and choose this project's `.venv`; changing a
default does not necessarily replace an existing selection.

Reload the VS Code window after setup, open the repository root, and verify the
selected Python interpreter. Configuration validation is not proof that a
particular running editor window has loaded the new settings.

## Vim scope and moving between computers

Vim and its four custom leader mappings live in User settings. They are used
while Vim is active. Cloning Tether does not install global editor preferences
on another machine.

To reproduce the same setup on macOS, install the extensions listed above and
use VS Code Settings Sync if desired, or copy the relevant editor and Vim
preferences into that machine's User settings. Do not replace an entire
personal settings file or copy Windows paths, shell environment values,
credentials, or the Windows `.venv`.

The Windows setup removed settings for uninstalled Java/C++ and frontend helpers
where they were obsolete, plus an old Autoprefixer shortcut.
Existing visual preferences and explicit telemetry choices were preserved.
Exact User settings and keybinding backups are stored beside the original files
in VS Code's local User directory, with names beginning `settings.before-` or
`keybindings.before-`.

## Start with these Vim actions

Vim separates navigating from typing. **Normal mode** is for commands; **Insert
mode** is for typing. Press Escape to return to Normal mode.

| Keys | Action |
| --- | --- |
| `i`, then Escape | Enter Insert mode, then return to Normal mode. |
| `h`, `j`, `k`, `l` | Move left, down, up, right. Arrow keys still work. |
| `w`, `b` | Move forward or backward by a word. |
| `0`, `$` | Move to the start or end of a line. |
| `gg`, `G` | Move to the start or end of the document. |
| `u` | Undo the last Vim edit. |
| `v`, then Escape | Begin a character selection, then leave Visual mode. |
| `yy`, `p` | Copy a line, then paste it after the current line. |
| `/`, text, Enter; `n` | Search forward, then go to the next match. |

Use VS Code's regular Undo and Redo commands while learning; Vim's usual Ctrl+R
redo is not enabled because common Ctrl shortcuts are preserved. Learn motions
first, then selections and editing operators. Speed is not a prerequisite for
learning Python, and using the mouse is fine.

The configured **leader key** is Space. In Normal mode, press Space and then the
letter in sequence; this is not a simultaneous key chord.

| Sequence | Action |
| --- | --- |
| Space, `w` | Save the file and apply its on-save formatting. |
| Space, `f` | Format the current document. |
| Space, `t` | Run discovered tests. |
| Space, `e` | Focus the file explorer. |

To temporarily return to standard editing, open the Command Palette and run
**Vim: Toggle Vim Mode**.

## Familiar editor shortcuts

These are VS Code defaults; existing personal keybindings can override them.

| Action | Windows | macOS |
| --- | --- | --- |
| Save | Ctrl+S | Command+S |
| Open a file by name | Ctrl+P | Command+P |
| Command Palette | Ctrl+Shift+P | Command+Shift+P |
| Search across files | Ctrl+Shift+F | Command+Shift+F |
| Toggle sidebar | Ctrl+B | Command+B |
| Format document | Shift+Alt+F | Shift+Option+F |
| Problems panel | Ctrl+Shift+M | Command+Shift+M |
| Toggle line comment | Ctrl+/ | Command+/ |
| Rename symbol | F2 | F2, possibly with Fn |
| Start debugging | F5 | F5, possibly with Fn |

## References

- [VS Code User and Workspace settings](https://code.visualstudio.com/docs/configure/settings)
- [VS Code Python environments](https://code.visualstudio.com/docs/python/environments)
- [VS Code Python testing](https://code.visualstudio.com/docs/python/testing)
- [VSCodeVim documentation](https://github.com/VSCodeVim/Vim)
- [Ruff editor setup](https://docs.astral.sh/ruff/editors/setup/)
