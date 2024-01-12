# Sagelint extension for Visual Studio Code

> **Note: This repository is under construction and unavailable now**

A Visual Studio Code extension with support for the Sagelint linter. This extension is based on [pylint](https://github.com/microsoft/vscode-pylint), ships with `sagelint=[TODO]`.

> **Note**: The minimum version of sagelint this extension supports is `[TODO]`.

TODO: This extension supports all [actively supported versions](https://devguide.python.org/#status-of-python-branches) of the `sagemath` language (i.e., sage >= 3.8).

For more information on sagelint, see https://sagelint.readthedocs.io/

## Usage and Features

The sagelint extension provides a series of features to help your productivity while working with Python code in Visual Studio Code. Check out the [Settings section](#settings) below for more details on how to customize the extension.

-   **Integrated Linting**: Once this extension is installed in Visual Studio Code, sagelint is automatically executed when you open a Python file, providing immediate feedback on your code quality.
-   **Customizable sagelint Version**: By default, this extension uses the version of sagelint that is shipped with the extension. However, you can configure it to use a different binary installed in your environment through the `sagelint.importStrategy` setting, or set it to a custom sagelint executable through the `sagelint.path` settings.
-   **Immediate Feedback**: By default, sagelint will update the diagnostics in the editor once you save the file. But you can get immediate feedback on your code quality as you type by enabling the `sagelint.lintOnChange` setting.
-   **Mono repo support**: If you are working with a mono repo, you can configure the extension to lint Python files in subfolders of the workspace root folder by setting the `sagelint.cwd` setting to `${fileDirname}`. You can also set it to ignore/skip linting for certain files or folder paths by specifying a glob pattern to the `sagelint.ignorePatterns` setting.
-   **Customizable Linting Rules**: You can customize the severity of specific sagelint error codes through the `sagelint.severity` setting.

### Disabling sagelint

You can skip linting with sagelint for specific files or directories by setting the `sagelint.ignorePatterns` setting.

But if you wish to disable linting with sagelint for your entire workspace or globally, you can [disable this extension](https://code.visualstudio.com/docs/editor/extension-marketplace#_disable-an-extension) in Visual Studio Code.

## Settings

There are several settings you can configure to customize the behavior of this extension.

| Settings                | Default                                                                                                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sagelint.args             | `[]`                                                                                                                                   | Arguments passed to sagelint for linting Python files. Each argument should be provided as a separate string in the array. <br> Examples: <br>- `"sagelint.args": ["--rcfile=<file>"]` <br> - `"sagelint.args": ["--disable=C0111", "--max-line-length=120"]`                                                                                                                                                                                                                                                                                                                                                                           |
| sagelint.cwd              | `${workspaceFolder}`                                                                                                                   | Sets the current working directory used to lint Python files with sagelint. By default, it uses the root directory of the workspace `${workspaceFolder}`. You can set it to `${fileDirname}` to use the parent folder of the file being linted as the working directory for sagelint.                                                                                                                                                                                                                                                                                                                                                 |
| sagelint.enabled          | `true`                                                                                                                                 | Enable/disable linting Python files with sagelint. This setting can be applied globally or at the workspace level. If disabled, the linting server itself will continue to be active and monitor read and write events, but it won't perform linting or expose code actions.                                                                                                                                                                                                                                                                                                                                                                                                |
| sagelint.severity         | `{ "convention": "Information", "error": "Error", "fatal": "Error", "refactor": "Hint", "warning": "Warning", "info": "Information" }` | Mapping of sagelint's message types to VS Code's diagnostic severity levels as displayed in the Problems window. You can also use it to override specific sagelint error codes. E.g. `{ "convention": "Information", "error": "Error", "fatal": "Error", "refactor": "Hint", "warning": "Warning", "W0611": "Error", "undefined-variable": "Warning" }`                                                                                                                                                                                                                                                                               |
| sagelint.path             | `[]`                                                                                                                                   | "Path or command to be used by the extension to lint Python files with sagelint. Accepts an array of a single or multiple strings. If passing a command, each argument should be provided as a separate string in the array. If set to `["sagelint"]`, it will use the version of sagelint available in the `PATH` environment variable. Note: Using this option may slowdown linting. <br>Examples: <br>- `"sagelint.path" : ["~/global_env/sagelint"]` <br>- `"sagelint.path" : ["conda", "run", "-n", "lint_env", "python", "-m", "sagelint"]` <br>- `"sagelint.path" : ["sagelint"]` <br>- `"sagelint.path" : ["${interpreter}", "-m", "sagelint"]` |
| sagelint.interpreter      | `[]`                                                                                                                                   | Path to a Python executable or a command that will be used to launch the sagelint server and any subprocess. Accepts an array of a single or multiple strings. When set to `[]`, the extension will use the path to the selected Python interpreter. If passing a command, each argument should be provided as a separate string in the array.                                                                                                                                                                                                                                                                                      |
| sagelint.importStrategy   | `useBundled`                                                                                                                           | Defines which sagelint binary to be used to lint Python files. When set to `useBundled`, the extension will use the sagelint binary that is shipped with the extension. When set to `fromEnvironment`, the extension will attempt to use the sagelint binary and all dependencies that are available in the currently selected environment. Note: If the extension can't find a valid sagelint binary in the selected environment, it will fallback to using the sagelint binary that is shipped with the extension. This setting will be overriden if `sagelint.path` is set.                                                                |
| sagelint.showNotification | `off`                                                                                                                                  | Controls when notifications are shown by this extension. Accepted values are `onError`, `onWarning`, `always` and `off`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| sagelint.lintOnChange     | `false`                                                                                                                                | Enable linting Python files with sagelint as you type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| sagelint.ignorePatterns   | `[]`                                                                                                                                   | Configure [glob patterns](https://docs.python.org/3/library/fnmatch.html) as supported by the fnmatch Python library to exclude files or folders from being linted with sagelint.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

The following variables are supported for substitution in the `sagelint.args`, `sagelint.cwd`, `sagelint.path`, `sagelint.interpreter` and `sagelint.ignorePatterns` settings:

-   `${workspaceFolder}`
-   `${workspaceFolder:FolderName}`
-   `${userHome}`
-   `${env:EnvVarName}`

The `sagelint.path` setting also supports the `${interpreter}` variable as one of the entries of the array. This variable is subtituted based on the value of the `sagelint.interpreter` setting.

## Commands

| Command                | Description                       |
| ---------------------- | --------------------------------- |
| sagelint: Restart Server | Force re-start the linter server. |

## Logging

From the Command Palette (**View** > **Command Palette ...**), run the **Developer: Set Log Level...** command. Select **sagelint** from the **Extension logs** group. Then select the log level you want to set.

Alternatively, you can set the `sagelint.trace.server` setting to `verbose` to get more detailed logs from the sagelint server. This can be helpful when filing bug reports.

To open the logs, click on the language status icon (`{}`) on the bottom right of the Status bar, next to the Python language mode. Locate the **sagelint** entry and select **Open logs**.

## Troubleshooting

In this section, you will find some common issues you might encounter and how to resolve them. If you are experiencing any issues that are not covered here, please [file an issue](https://github.com/microsoft/vscode-sagelint/issues).

-   If the `sagelint.importStrategy` setting is set to `fromEnvironment` but sagelint is not found in the selected environment, this extension will fallback to using the sagelint binary that is shipped with the extension. However, if there are dependencies installed in the environment, those dependencies will be used along with the shipped sagelint binary. This can lead to problems if the dependencies are not compatible with the shipped sagelint binary.

    To resolve this issue, you can:

    -   Set the `sagelint.importStrategy` setting to `useBundled` and the `sagelint.path` setting to point to the custom binary of sagelint you want to use; or
    -   Install sagelint in the selected environment.
