---
up: "[[VSCode Python Docs]]"
tags:
  - "#education/computerprogramming/languages/python/vscode/environments"
prev: "[[Linting Python in VSCode]]"
---


# Python Environments in VSCode

Link: https://code.visualstudio.com/docs/python/environments

An "environment" is the context in which a Python program runs that consists of an interpreter and any number of installed packages. 

 >[!NOTE]
 **Note**: If you'd like to become more familiar with the Python programming language, review [More Python resources](https://code.visualstudio.com/docs/python/environments#_more-python-resources).

## Types of Python Environments

### Global Environments

By default, any Python interpreter installed run in its own **global environment**. For example if you just run `python`, `python3`, or `py` at a new terminal (depending on how you installed Python), you're running in that interpreter's *global environment*. Any packages that you install or uninstall affect the global environment and all programs that you run within it. 

> **Tip**: In Python, it is best practice to create a workspace-specific environment, for example, by using a local environment.

### Local Environments

There are two types of environments that you can create for your workspace: **virtual** and **conda**. These environments allow you to install packages without affecting other environments, isolating your workspace's package installations.
#### Virtual Environments

A [**virtual environment**](https://docs.python.org/3/glossary.html#term-virtual-environment) is a built-in way to create an environment. A virtual environment creates a folder that contains a copy (or `symlink`) to a specific interpreter. When you install packages into a virtual environment it will end up in this new folder, and thus isolated from other packages used by other workspaces.

**Note**: while it's possible to open a virtual environment folder as a workspace, doing so is not recommended and might cause issues with using the Python extension.
#### Conda Environments

A **conda environment** is a Python environment that's managed using the `conda` package manager (see [Getting started with conda](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)). Choosing between conda and virtual environments depends on your packaging needs, team standards, etc.

### Python Environment Tools

The following table lists the various tools involved with Python environments:

| Tool                                                | Definition & Purpose                                                                                                                                                                            |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [pip](https://pip.pypa.io/)                         | The Python package manager that installs and updates packages. It's installed with Python 3.9+ by default (unless you are on a Debian-based OS; install `python3-pip` in that case).            |
| [venv](https://docs.python.org/3/library/venv.html) | Allows you to manage separate package installations for different projects and is installed with Python 3 by default (unless you are on a Debian-based OS; install `python3-venv` in that case) |
| [conda](https://docs.conda.io/)                     | Installed with [**Miniconda**](https://docs.conda.io/en/latest/miniconda.html). It can be used to manage both packages and virtual environments. Generally used for data science projects.      |

## Creating Environments

### Using the Create Environment Command

To create local environments in VSCode using virtual environments in Anaconda, you can follow these steps: open the Command Palette (`Ctrl+Shift+P`), search for the `Python: Create Environment` command, and select it.

The command presents a list of environment types: **Venv** or **Conda**.

If you are creating an environment using **Venv**, the command presents a list of interpreters that can be used as a base for the new virtual environment.

![](https://i.imgur.com/059I92K.png)

If you are creating an environment using `Conda`, the command presents a list of Python versions that can be used for your project.

After selecting the desired interpreter or Python version, a notification will show the progress of the environment creation and the environment will appear in your workspace.

> [!NOTE]
> **Note**: The command will also install necessary packages outlined in a requirements/dependencies fil, such as `requirements.txt`, `pyproject.toml`, or `environment.yml`, located in the project folder. It will also add a `.gitignore` file to the virtual environment to help prevent you from accidentally committing the virtual environment to source control. 
### Create a Virtual Environment in the Terminal

If you choose to create a virtual environment manually, use the following command (where ".venv") is the name of the environment folder):

```shell
# macOS/Linux
# You may need to run `sudo apt-get install python3-venv` first on Debian-based OSs
python3 -m venv .venv

# Windows
# You can also use `py -3 -m venv .venv`
python -m venv .venv
```

> [!NOTE]
> **Note**: To learn more about the `venv` module, read [Creation of virtual environments](https://docs.python.org/3/library/venv.html) on Python.org.
---

---

The `venv` module supports creating lightweight "virtual environments", each with their own independent set of Python packages installed in their [`site`](https://docs.python.org/3/library/site.html#module-site "site: Module responsible for site-specific configuration.") directories. A virtual environment is created on top of an existing Python installation, known as the virtual environment's "base" Python, and may optionally be isolated from the packages in the base environment, so only those explicitly installed in the virtual environment are available. 

When used from within a virtual environment, common installation tools such as [pip](https://pypi.org/project/pip/) will install Python packages into a virtual environment without needing to be told to do so explicitly.

A virtual environment is (amongst other things):

- Used to contain a specific Python interpreter and software libraries and binaries which are needed to support a project (library or application). These are by default isolated from software in other virtual environments and Python interpreters and libraries installed on the OS.
- Contained in a directory, convetionally named `.venv` or `venv` in the project directory, or under a container directory for lots of virtual environments, such as `~/.virtualenvs`.
- Not checked into source control systems such as Git.
- Considered as disposable -- it should be simple to delete and recreate it from scratch. You don't place any object or project code in the environment.
- Not considered as moveable or copyable -- you just recreate the same environment in the target location.

See [**PEP 405**](https://peps.python.org/pep-0405/) for more background on Python virtual environments.

> [!NOTE]
> See also
> 
> [Python Packaging User Guide: Creating and using virtual environments](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments)

This module is not supported on [mobile platforms](https://docs.python.org/3/library/intro.html#mobile-availability) or [WebAssembly platforms](https://docs.python.org/3/library/intro.html#wasm-availability).

## Creating virtual environments

[Virtual environments](https://docs.python.org/3/library/venv.html#venv-def) are created by executing the `venv` module:

python -m venv /path/to/new/virtual/environment

This creates the target directory (including parent directories as needed) and places a `pyvenv.cfg` file in it with a `home` key pointing to the Python installation from which the command was run. It also creates a `bin` (or `Scripts` on Windows) subdirectory containing a copy or symlink of the Python executable (as appropriate for the platform or arguments used at environment creation time). It also creates a `lib/pythonX.Y/site-packages` subdirectory (on Windows, this is `Libsite-packages`). If an existing directory is specified, it will be re-used.

Changed in version 3.5: The use of `venv` is now recommended for creating virtual environments.

Deprecated since version 3.6, removed in version 3.8: **pyvenv** was the recommended tool for creating virtual environments for Python 3.3 and 3.4, and replaced in 3.5 by executing `venv` directly.

On Windows, invoke the `venv` command as follows:

```python
python -m venv C:\path\to\new\virtual\environment
```

## How venvs Work

When a Python interpreter is running from a virtual environment, [`sys.prefix`](https://docs.python.org/3/library/sys.html#sys.prefix "sys.prefix") and [`sys.exec_prefix`](https://docs.python.org/3/library/sys.html#sys.exec_prefix "sys.exec_prefix") point to the directories of the virtual environment, whereas [`sys.base_prefix`](https://docs.python.org/3/library/sys.html#sys.base_prefix "sys.base_prefix") and [`sys.base_exec_prefix`](https://docs.python.org/3/library/sys.html#sys.base_exec_prefix "sys.base_exec_prefix") point to those of the base Python used to create the environment. It is sufficient to check `sys.prefix != sys.base_prefix` to determine if the current interpreter is running from a virtual environment. 

A virtual environment may be "activated" using a script in it's binary directory (`bin` on POSIX, `Scripts` on Windows). This will prepend that directory to your `PATH`, so that running **python** will invoke the environment's Python interpreter and you can run installed scripts without having to use their full path. The invocation of the activation script is platform specific (`<venv>` must be replaced by the path to the directory containing the virtual environment):

| Platform | Shell      | Command to activate virtual environment |
| -------- | ---------- | --------------------------------------- |
| POSIX    | bash/zsh   | `$ source _<venv>_/bin/activate`        |
|          | fish       | `$ source _<venv>_/bin/activate.fish`   |
|          | csh/tcsh   | `$ source _<venv>_/bin/activate.csh`    |
|          | pwsh       | `$ _<venv>_/bin/Activate.ps1`           |
| Windows  | cmd.exe    | `C:\> _<venv>_\Scripts\activate.bat`    |
|          | PowerShell | `PS C:\> _<venv>_\Scripts\Activate.ps1` |
You don't specifically *need* to activate a virtual environment, as you can just specify the full path to that environment's Python interpreter when invoking Python. Furthermore, all scripts installed in the environment should be runnable without activating it. 

In order to achieve this, scripts installed into virtual environments have a "shebang" line which points to the environment's Python interpreter, `#!/<path-to-venv>/bin/python`. This means that the script will run with that interpreter regardless of the value of PATH. On Windows, "shebang" line processing is supported if you have the [Python Launcher for Windows](https://docs.python.org/3/using/windows.html#launcher) installed. Thus, double-clicking an installed script in a Windows Explorer window should run it with the correct interpreter without the environment needing to be activated or on the PATH.

When a virtual environment has been activated, the `VIRTUAL_ENV` environment variable is set to the path of the environment. Since explicitly activating a virtual environment is not requred to use it, `VIRTUAL_ENV` cannot be relied upon to determine whether a virtual environment is being used. 

> [!WARNING]
> 
> 
> Because scripts installed in environments should not expect the environment to be activated, their shebang lines contain the absolute paths to their environment’s interpreters. Because of this, environments are inherently non-portable, in the general case. You should always have a simple means of recreating an environment (for example, if you have a requirements file `requirements.txt`, you can invoke `pip install -r requirements.txt` using the environment’s `pip` to install all of the packages needed by the environment). If for any reason you need to move the environment to a new location, you should recreate it at the desired location and delete the one at the old location. If you move an environment because you moved a parent directory of it, you should recreate the environment in its new location. Otherwise, software installed into the environment may not work as expected.
> 

You can deactivate a virtual environment by typing `deactivate` in your shell. The exact mechanism is platform-specific and is an internal implementation detail (typically, a script or shell function will be used.)
## API

The high-level method described above makes use of a simple API which provides mechanisms for third-party virtual environment creators to customize environment creation according to their needs, the [`EnvBuilder`](https://docs.python.org/3/library/venv.html#venv.EnvBuilder "venv.EnvBuilder") class.

_class_ venv.EnvBuilder(_system_site_packages=False_, _clear=False_, _symlinks=False_, _upgrade=False_, _with_pip=False_, _prompt=None_, _upgrade_deps=False_, _*_, _scm_ignore_files=frozenset()_)[¶](https://docs.python.org/3/library/venv.html#venv.EnvBuilder "Link to this definition")

The [`EnvBuilder`](https://docs.python.org/3/library/venv.html#venv.EnvBuilder "venv.EnvBuilder") class accepts the following keyword arguments on instantiation:

- _system_site_packages_ – a boolean value indicating that the system Python site-packages should be available to the environment (defaults to `False`).

- _clear_ – a boolean value which, if true, will delete the contents of any existing target directory, before creating the environment.

- _symlinks_ – a boolean value indicating whether to attempt to symlink the Python binary rather than copying.

- _upgrade_ – a boolean value which, if true, will upgrade an existing environment with the running Python - for use when that Python has been upgraded in-place (defaults to `False`).

- _with_pip_ – a boolean value which, if true, ensures pip is installed in the virtual environment. This uses [`ensurepip`](https://docs.python.org/3/library/ensurepip.html#module-ensurepip "ensurepip: Bootstrapping the "pip" installer into an existing Python installation or virtual environment.") with the `--default-pip` option.

- _prompt_ – a string to be used after virtual environment is activated (defaults to `None` which means directory name of the environment would be used). If the special string `"."` is provided, the basename of the current directory is used as the prompt.

- _upgrade_deps_ – Update the base venv modules to the latest on PyPI

- _scm_ignore_files_ – Create ignore files based for the specified source control managers (SCM) in the iterable. Support is defined by having a method named `create_{scm}_ignore_file`. The only value supported by default is `"git"` via [`create_git_ignore_file()`](https://docs.python.org/3/library/venv.html#venv.EnvBuilder.create_git_ignore_file "venv.EnvBuilder.create_git_ignore_file").

---

When you create a new virtual environment, a prompt will be displayed in VSCode to allow you to select it for the workspace. 

> [!TIP]
> **Tip**: Make sure to update your source control settings to prevent accidentally committing your virtual environment (in for example `.gitignore`). Since virtual environments are not portable, it typically does not make sense to commit them for others to use.
### Create a Conda Environment in the Terminal

The Python extension automatically detects existing conda environments. We recommend you install a Python interpreter into your conda environment, otherwise one will be installed for you after you select the environment. For example, the following command creates a conda environment named `env-01` with a Python 3.9 interpreter and several libraries. 

```
conda create -n env-01 python=3.9 scipy=0.15.0 numpy
```

**Note**: For more information on the conda command line you can read [Conda environments](https://conda.io/docs/user-guide/tasks/manage-environments.html).

Additional Notes:

- If you create a new conda environment with VSCode is running, use the refresh icon at the top right of the Python: Select Interpreter windows; otherwise you may not find the environment there.
- To ensure the environment is properly set up from a shell perspective, use an Anaconda prompt and activate the desired environment. Then, you can launch VSCode by entering the `code .` command. Once VSCode is open, you can select the interpreter either by using the Command Palette or by clicking on the status bar. 
- Although the Python extension for VSCode doesn't currently have integration with conda `environment.yaml` files, VSCode itself is a great YAML editor.
- Conda environments can't be automatically activated in the VSCode integrated terminal if the default shell is set to PowerShell. To change the shell, see [Integrated terminal - Terminal profiles](https://code.visualstudio.com/docs/terminal/profiles).
- You can manually specify the path to the `conda` executable to use for activation (version 4.4+). To do so, open the Command Palette (`Ctrl+Shift+P`) and run **Preferences: Open User Settings**. Then set `python.condapath`, which is in the Python extension section of User Settings, with the appropriate path. 

## Working with Python Interpreters

### Select and Activate an Environment

The Python extension tries to find and then select what it deems the best environmen for the workspace. If you would prefer to select a specific environment, use the **Python: Select Interpreter** command from the **Command Palette**.

> [!NOTE]
> **Note**: If the Python extension doesn't find an interpreter, it issues a warning. On macOS 12.2 and older, the extension also issues a warning if you're using the OS-installed Python interpreter as it is known to have compatibility issues. In either case, you can disable these warnings by setting `python.disableInstallationCheck` to `true` in your user [settings](https://code.visualstudio.com/docs/getstarted/settings).

The **Python: Select Interpreter** command displays a list of available global environments, conda environments, and virtual environments. (See the [Where the extension looks for environments](https://code.visualstudio.com/docs/python/environments#_where-the-extension-looks-for-environments) section for details, including the distinctions between these types of environments.) The following image, for example, shows several Anaconda and CPython installations along with a conda environment and a virtual environment (`env`) within the workspace folder:

![](https://i.imgur.com/sKPSSFo.png)

> [!NOTE]
> **Note**: On Windows, it can take a little time for VSCode to detect available conda environments. During that process, you may see "(cached)" before the path to an environment. The label indicates that VSCode is presently working with cached information for that enviornment.
> 

If you have a folder or a workspace open in VSCode and you select an interpreter from the list, the Python extension will store that *information internally*. This ensures that the same interpreter will be used when you reopen the workspace. 

The selected environment is used by the Python extension for running Python code (using the **Python: Run Python File in Terminal** command), providing language servers (auto-complete, syntax-checking, linting, formatting, etc.) when you have a `.py` file open in the editor, and opening a terminal with the **Terminal: Create New Terminal** command. In the latter case, VS Code automatically activates the selected environment. 

> [!tip]
> **Tip**: To prevent automatic activation of a selected environment, add `"python.terminal.activateEnvironment": false` to your `settings.json` file (it can be placed anywhere as a sibling to the existing settings).

> [!Tip]
>**Tip**: If the activate command generates the message "Activate.ps1 is not digitally signed. You cannot run this script on the current system.", then you need to temporarily change the PowerShell execution policy to allow scripts to run (see [About Execution Policies](https://go.microsoft.com/fwlink/?LinkID=135170) in the PowerShell documentation): `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process`

> [!NOTE]
> **Note**: By default, VS Code uses the interpreter selected for your workspace when debugging code. You can override this behavior by specifying a different path in the `python` property of a debug configuration. See [Choose a debugging environment](https://code.visualstudio.com/docs/python/environments#_choose-a-debugging-environment).

The selected interpreter version will show on the right side of the Status Bar.

The status bar also reflects when no interpreter is selected.

In either case, clicking this area of the Status Bar is a convenient shortcut for the **Python: Select Interpreter** command. 
### Manually Specify an Interpreter

If VSCode doesn't automatically locate an interpreter you want to use, you can browse for the interpreter on your file system or provide the path to it manually. 

You can do so by running the **Python: Select Interpreter** command and select the **Enter Interpreter path...** option that shows on the top of the interpreters list:

![](https://i.imgur.com/YV38ZQV.png)

You can then either enter the full path of the Python interpreter directly in the text box (for example, ".venv/Scripts/python.exe") or you can select the **Find...** button and browse your file system to find the python executable you wish to select. 

If you want to manually specify a default interpreter that wil be used when you first open your workspace, you can create or modify an entry for the `python.defaultInterpreterPath` setting. 

> [!NOTE]
> **Note**: Changes to the `python.defaultInterpreterPath` setting are not picked up after an interpreter has already been selected for a workspace; any changes to the setting will be ignored once an initial interpreter is selected for the workspace.

Additionally,. if you'd like to set up a different interpreter for all of your Python applications, you can add an entry for `python.defaultInterpreterPath` manually inside your user settings. To do so, open the command Palette (`Ctrl+Shift+P`) and enter **Preference: Open User Settings**. Then set `python.defaultInterpreterPath`, which is in the Python extension section of User Settings, with the appropriate interpreter. 
### How the Extension Chooses an Environment Automatically

If an interpreter hasn't been specified, then the Python extension automatically selects the interpreter with the highest version in the following priority order:

1. Virtual Environments located directly under the workspace folder.
2. Virtual Environments related to the workspace but stored globally. For example, [Pipenv](https://pypi.org/project/pipenv/) or [Poetry](https://python-poetry.org/) environments that are located outside of the workspace folder.
3. Globally installed interpreters. For example, the ones found in `/usr/local/bin`, `C:\\python38`, etc.

**Note:** the interpreter selected may differ from what `python` refers to in your terminal.
### Where the Extension Looks For Environments

The extension automatically looks for interpreters in the following locations, in no particular order:

- Standard install paths such as `/usr/local/bin`, `/usr/sbin`, `/sbin`, `c:\\python36`, etc.
- Virtual environments located directly under the workspace (project) folder.
- Virtual environments located in the folder identified by the `python.venvPath` setting (see [General Python settings](https://code.visualstudio.com/docs/python/settings-reference#_general-python-settings)), which can contain multiple virtual environments. The extension looks for virtual environments in the first-level subfolders of `venvPath`.
- Virtual environments located in a `~/.virtualenvs` folder for [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/).
- Interpreters created by [pyenv](https://github.com/pyenv/pyenv), [Pipenv](https://pypi.org/project/pipenv/), and [Poetry](https://poetry.eustace.io/).
- Virtual environments located in the path identified by `WORKON_HOME` (as used by [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/)).
- Conda environments found by `conda env list`. Conda environments which do not have an interpreter will have one installed for them upon selection.
- Interpreters installed in a `.direnv` folder for [direnv](https://direnv.net/) under the workspace folder.
### Environments and Terminal Windows

After using **Python: Select Interpreter**, that interpreter is applied when right-clicking a file and selecting **Python: Run Python File in Terminal**. The environment is also activated automatically when you use the **Terminal: Create New Terminal** command unless you change the `python.terminal.activateEnvironment` setting to `false`.

Please note that launching VS Code from a shell in which a specific Python enviornment is activated doesn't automatically activate the environment in the default Integrated Terminal.

**Note**: conda environments cannot be automatically activated in the integrated terminal if PowerShell is set as the integrated shell. See [Integrated terminal - Terminal profiles](https://code.visualstudio.com/docs/terminal/profiles) for how to change the shell.

Changing interpreters with the **Python: Select Interpreter** command doesn't affect terminal panels that are already open. Thus, you can activate separate environments is a split terminal: select the first interpreter, create a terminal for it, select a different interpreter, then use the split button (`Ctrl+Shift+5`) in the terminal title bar. 
### Choosing a Debugging Environment

By default, the debugger will use the Python interpreter chosen with the Python extension. However, if there is a `python` property specified in the debug configuration of `launch.json`, it takes precedence. If this property is not defined, it will fall back to using the Python interpreter path selected for the workspace.

For more details on debug configuration, see [Debugging configurations](https://code.visualstudio.com/docs/python/debugging).
## Environment Variables
### Environment Variable Definitions File

An environment variable definitions file is a text file containing *key-value* pairs int he form of `environment_variable=value`, with `#` used for comments. Multiline values aren't supported, but references to previously defined environment variables are allowed. Environment variable definitions files can be used for scenarios such as debugging and tool execution (including linters, formatters, IntelliSense, and testing tools), but aren't applied to the terminal. 

> [!NOTE]
> **Note**: Environment variable definitions files are not necessarily cross-platform. For instance, while Unix uses `:` as a path separator in environment variables, Windows uses `;`. There is no normalization of such operating system differences, and so you need to make sure any environment definitions file use values that are compatible with your operating system.

By default, the Python extension looks for and loads a file named `.env` in the current workspace folder, the applies those definitions. The file is identified by the default entry `"python.envFile": "${workspaceFolder}/.env"` in your user settings (see [General Python settings](https://code.visualstudio.com/docs/python/settings-reference#_general-python-settings)). You can change the `python.envFile` setting at any time to use a different definitions file.

**Note**: Environment variable definitions files are not used in all situations where environment variables are available for use. Unless Visual Studio Code documentation states otherwise, these only affect certain scenarios as per their definition. For example, the extension doesn't use environment variable definitions files when resolving settings values. 

A debug configuration also contains an `envFile` property that also defaults to the `.env` file in the current workspace (see [Debugging - Set configuration options](https://code.visualstudio.com/docs/python/debugging#_set-configuration-options)). This property allows you to easily set variables for debugging purposes that replace variables specified in the default `.env` file.

For example, when developing a web application, you might want to easily switch between development and production servers. Instead of coding the different URLs and other settings into your application directly, you could use separate definitions files for each. For example:

**dev.env file**

```
# dev.env - development configuration

# API endpoint
MYPROJECT_APIENDPOINT=https://my.domain.com/api/dev/

# Variables for the database
MYPROJECT_DBURL=https://my.domain.com/db/dev
MYPROJECT_DBUSER=devadmin
MYPROJECT_DBPASSWORD=!dfka**213=
```

**prod.env file**

```
# prod.env - production configuration

# API endpoint
MYPROJECT_APIENDPOINT=https://my.domain.com/api/

# Variables for the database
MYPROJECT_DBURL=https://my.domain.com/db/
MYPROJECT_DBUSER=coreuser
MYPROJECT_DBPASSWORD=kKKfa98*11@
```

You can then set the `python.envFile` setting to `${workspaceFolder}/prod.env`, then set the `envFile` property in the debug configuration to `${workspaceFolder}/dev.env`.

> **Note**: When environment variables are specified using multiple methods, be aware that there is an order of precedence. All `env` variables defined in the `launch.json` file will override variables contained in the `.env` file, specified by the `python.envFile` setting (user or workspace). Similarly, `env` variables defined in the `launch.json` file will override the environment variables defined in the `envFile` that are specified in `launch.json`.

### [Use of the PYTHONPATH variable](https://code.visualstudio.com/docs/python/environments#_use-of-the-pythonpath-variable)

The [PYTHONPATH](https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH) environment variable specifies additional locations where the Python interpreter should look for modules. In VS Code, PYTHONPATH can be set through the terminal settings (`terminal.integrated.env.*`) and/or within an `.env` file.

When the terminal settings are used, PYTHONPATH affects any tools that are run within the terminal by a user, as well as any action the extension performs for a user that is routed through the terminal such as debugging. However, in this case when the extension is performing an action that isn't routed through the terminal, such as the use of a linter or formatter, then this setting won't have an effect on module look-up.

## [Next steps](https://code.visualstudio.com/docs/python/environments#_next-steps)

- [Editing code](https://code.visualstudio.com/docs/python/editing) - Learn about autocomplete, IntelliSense, formatting, and refactoring for Python.
- [Debugging](https://code.visualstudio.com/docs/python/debugging) - Learn to debug Python both locally and remotely.
- [Testing](https://code.visualstudio.com/docs/python/testing) - Configure test environments and discover, run, and debug tests.
- [Settings reference](https://code.visualstudio.com/docs/python/settings-reference) - Explore the full range of Python-related settings in VS Code.

## [More Python resources](https://code.visualstudio.com/docs/python/environments#_more-python-resources)

- [Getting Started with Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial) - Learn how to edit, run, and debug code in VS Code.
- [Virtual Environments and Packages (Python.org)](https://docs.python.org/3/tutorial/venv.html) - Learn more about virtual environments and packages.
- [Installing Python Modules (Python.org)](https://docs.python.org/3/installing/index.html#installing-index) - Learn how to install Python modules.
- [Python tutorial (Python.org)](https://docs.python.org/3/tutorial/index.html) - Learn more about the Python language.



