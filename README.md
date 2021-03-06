The intention of this repository is to be cloned into the `%AppData%\Sublime Text 3\Packages\User` folder.  The cloning process makes a new subfolder by default; you can forcibly clone into the current (existing) folder with `git clone https://github.com/skparkes/sublimetext-config.git .` (notice the trailing `.`).

You'll likely need to install `Package Control` first.  In theory, it will then install all the other packages enumerated in its own configuration files.  The following packages still would need manual installation after that:
  * [SAS](https://github.com/rpardee/sas)

### Anaconda Python Distribution Integration (Not to be confused with the Anaconda Sublime Package for Python)

The following setup seems to work well for best results when integrating with linters and code completion:
  * Using `conda`, setup a new environment that has your chosen linters (e.g. `pylint`, `pep8`, `pyflakes` etc) and possible any commonly used packages you want to code complete
  * In your system `PATH`, include the following:
    * The `Scripts` subdirectory of your root Miniconda install.  This will make `conda` and `activate` available from the command line.
    * The root directory of your IDE environment described above.  This should be the path containing the corresponding `python.exe`
    * The `Scripts` directory of you IDE environment described above.  This should make the linters available from the command line.
  * It is **not** recommended to put the root path of your root Miniconda install because many plugins appear to get confused when they find the corresponding `python.exe` in that directory.
  * Most of the packages, especially the code completion packages, allow to explicitly specify extra paths/environments to scan/utilize.  You can specify these in the root Sublime settings for the corresponding package, or often in the project level settings file as well.

## Notes on various packages:

### SublimeLinter

This package manhandles the configuration file directory somewhat.  In insists on manipulating the chosen theme to have the colors it desires, so you'll see it constantly making a modified copy of the theme into this directory.  It also forces the user settings file to always have all the options enumerated in it.

### SublimeREPL and the Current Working Directory

SublimeREPL works fairly well for basic REPLs out of the box (e.g. Python).  You must be mindful of what tab you have in focus when you launch a REPL though, because the current working directory of the resulting REPL depends upon your prior tab focus.  This is important in Python because the current working directory is the first place Python looks to import packages (even over the standard library).  
  * If you had a file in focus, the current working directory becomes the folder that contains that file
    * Generally a good thing, especially when developing on python packages (you can easily import other files during testing/development).
  * If you don't have a file in focus, it will set the current working directory to the installation folder of SublimeText itself.
    * Generally a bad thing.  It causes havoc with Python REPLs because they then try to import the python packages that are bundled with SublimeText and trigger all kinds of version conflicts (SublimeText is built on Python 3.3 currently).

### Jedi + SublimeREPL

Most people would utilize IPython in the SublimeREPL, and IPython comes with it's own code completion capabilities.  Therefor Jedi turns itself off when it detects a REPL instance (whether it's IPython or not).  The current SublimeREPL and IPython versions are unfortunately not compatible, so you need to use a base Python REPL.  To get Jedi to activate again in a base Python REPL, you need to comment out line 132 in `%AppData%/Sublime Text 3/Packages/Jedi - Python autocompletion/sublime_jedi/completion.py`.  Unfortunately, this edit will be overridden each time Jedi is automatically updated by Package Control.

## Shortcuts worth knowing
| Family | Keys | Effect |
| :----- | :--- | :----- |
| Root | `Ctl`+`Shift`+`P` | Command palette. |
| Root | `Ctl`+`P` | Goto anything. |
| Root | `Ctl`+` | Internal Sublime console. |
| Root | `Ctl`+`Alt`+`P` | Switch project. |
| Root | `Ctl`+`B` | Build project (or preview Markdown) |
| Windows | `Ctl`+`PageUp` (or `PageDown`) | Cycle tabs (goes between windows). |
| Windows | `Alt`+`Shift`+`1` (or `2`) | Make 1 (or 2) windows. |
| Windows | `Ctl`+`1` (or `2`) | Move focus to first (or second) window. |
| Windows | `Ctl`+`Shift`+`1` (or `2`) | Move current view into first (or second) window. |
| Windows | `Ctl`+`K`,`B` | Show/hide sidebar. |
| Windows | `Ctl`+`Up` (or `Down`) | Scroll window without moving cursor. |
| Selection | `Ctl`+`Alt`+`Up` (or `Down`) | Extend multiple cursors up (or down). |
| Selection (~Quick) | `Ctl`+`D` (and repeat) | Select the current, then the next (and next) instance of a word. |
| Selection (~Quick) | `Ctl`+`U` (and repeat) | Undo the last `Ctl`+`D` (see above) |
| Selection (~Quick) | `Ctl`+`K`,`D` | Skip the current instance of the word and select the next. |
| Selection (~Quick) | `Alt`+`F3` (or `Ctl`+`F3`) | Select (or find) the current, and all other instances of a word. |
| Selection | `Ctl`+`Shift`+`Space` | Expand selection to scope. |
| Selection | `Ctl`+`Shift`+`M` | Expand selection to brackets. |
| Code Navigation | `Ctl`+`R` | Goto ~definition. |
| Text Manipulation | `Ctl`+`/` | Toggle comment. |
| Text Manipulation | `Ctl`+`Shift`+`/` | Toggle block comment. |
| Text Manipulation | `Ctl`+`K`,`V` | Clipboard history. |
| Text Manipulation | `Ctl`+`K`,`U` (or `L`) | Convert selection to uppercase (or lowercase). |
| Text Manipulation | `Ctl`+`Space` | Force code completion. |
| Text Manipulation | `Ctl`+`]` (or `[`) | Indent (or unindent) |
| Text Manipulation | `Ctl`+`Shift`+`Up` (or `Down`) | Move current line/selection up (or down) |
| Text Manipulation | `F6` | Toggle Spellcheck. |
| Text Manipulation | `F9` (or `Ctl`+`F9`) | Sort lines case insensitive (or case-sensitive). |
| SublimeLinter | `Ctl`+`K` then `N` (or `P`) | Goto next (or previous) warning. |
| SublimeLinter | `Ctl`+`K` then `A` | Show all warnings. |
| SublimeREPL | `Ctl`+`,` then `L` (or `S`) | Send line (or selection) to REPL. |
| SublimeREPL | `Ctl`+`,` then `F` | Send whole file to REPL. |
| GitGutter | `Ctl`+`Alt`+`Shift`+`J` (or `K`) | Goto next (or previous) change. |
| PyDOC | `Ctl`+`3` | Search the current item on Python 3 web documentation. |
| Jedi | `Ctl`+`Shift`+`G` (Or `Ctl`+`Left Click`) | Goto ~definition. |
| Jedi | `Alt`+`Shift`+`F` | Find ~usages. |
| Terminal | `Ctl`+`Shift`+`T` | Open a terminal at current file. |
| Terminal | `Ctl`+`Shift`+`Alt`+`T` | Open a terminal at project root. |
| My Custom | `F4` | Open current file with system associated application. |
| My Custom | `F1` | Lookup docstring with Jedi. |
