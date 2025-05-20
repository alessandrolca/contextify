# Contextify CLI 💬🌲📝

[![PyPI version](https://img.shields.io/pypi/v/contextify-cli.svg)](https://pypi.org/project/contextify-cli/)
[![License](https://img.shields.io/pypi/l/contextify-cli.svg)](https://github.com/alessandrolca/contextify/blob/main/LICENSE)
[![Python Versions](https://img.shields.io/pypi/pyversions/contextify-cli.svg)](https://pypi.org/project/contextify-cli/)

**Contextify (`contextify-cli`)** is a command-line tool designed to scan your codebase, understand its structure, and consolidate relevant file contents into a single, clean Markdown document. This output is perfect for providing context to AI assistants (like ChatGPT, Claude, Gemini, etc.), for documentation purposes, or for quickly getting an overview of a project.

Say goodbye to manually copying and pasting files or struggling with token limits! 👋

## 🤔 Why Contextify?

When working with Large Language Models (LLMs) or AI coding assistants, providing sufficient and well-structured context is key to getting high-quality responses. Manually gathering this context from a large project can be:

* **Time-consuming:** Opening, copying, and pasting multiple files.
* **Error-prone:** Easy to miss important files or include irrelevant ones.
* **Repetitive:** You often need to do this for different queries or updates.
* **Limited by input size:** Concatenating too much code can exceed token limits.

Contextify automates this process, allowing you to quickly generate a concise and relevant Markdown representation of your project, tailored to your needs.

## ✨ Key Features

* **🌲 Directory Tree Generation:** Includes an optional, customizable directory tree structure in the Markdown output.
* **📄 File Content Aggregation:** Reads specified file types and includes their content in formatted Markdown code blocks.
* **🎯 Flexible Filtering:**
    * Specify which file extensions to include (e.g., `.py`, `.js`, `.md`).
    * Define maximum scan depth for directories.
    * Exclude specific directories (e.g., `node_modules`, `.git`, `__pycache__`).
    * Exclude specific files by pattern (e.g., `*.log`, `temp.*`).
* **✂️ Content Truncation:** Set a maximum character limit per file to keep the context concise and manage token counts.
* **🏷️ Language Tagging:** Automatically adds language tags to Markdown code blocks based on file extensions.
* **⚙️ Command-Line Interface:** Easy to use directly from your terminal.
* **📝 Output to File or Console:** Print to standard output or save directly to a `.md` file.

## 🚀 Installation

You can install `contextify-cli` directly from PyPI using pip:

```bash
pip install contextify-cli
```

Make sure you have Python 3.9 or higher installed.

## 🛠️ Usage

The basic command structure is:

```bash
contextify [OPTIONS] <DIRECTORY_PATH>
```

**Arguments:**

  * `DIRECTORY_PATH`: (Required) The path to the project directory you want to process.

**Common Options:**

  * `-o, --output <FILE_PATH>`: Save the Markdown output to the specified file. If not provided, output is printed to the console.
  * `--no-tree`: Do not include the directory tree structure.
  * `-ext, --extensions <EXT1,EXT2,...>`: Comma-separated list of file extensions to include (e.g., `py,js,md`). Defaults to `py`. Use `ALL` to include all non-ignored files.
  * `-depth, --max-depth <N>`: Maximum depth to scan directories for both the tree and files. `-1` for unlimited (default), `0` for root directory only.
  * `-mfc, --max-file-chars <N>`: Maximum characters per file to include. `-1` for unlimited (default). Content exceeding this limit will be truncated.
  * `--ignore-dir <DIR_NAME>`: Specify a directory name to ignore. Can be used multiple times.
  * `--ignore-file <PATTERN>`: Specify a file name pattern (fnmatch style, e.g., `*.log`, `temp.*`) to ignore. Can be used multiple times.
  * `--version`: Show the version of `contextify-cli` and exit.
  * `--help`: Show the help message and exit.

**Examples:**

1.  **Process a Python project in the current directory and print to console:**

    ```bash
    contextify .
    ```

2.  **Process a JavaScript project, include only `.js` and `.json` files, and save to `project_context.md`:**

    ```bash
    contextify ./my-js-project -ext js,json -o project_context.md
    ```

3.  **Process a project, limit scan depth to 2, and exclude the `dist` directory:**

    ```bash
    contextify ./my-deep-project -depth 2 --ignore-dir dist
    ```

4.  **Process all file types, exclude `.log` files, and limit file content to 5000 characters each:**

    ```bash
    contextify ./another-project -ext ALL --ignore-file "*.log" -mfc 5000
    ```

5.  **Generate context without the directory tree:**

    ```bash
    contextify ./my-project --no-tree -o context_no_tree.md
    ```

## ⚙️ Configuration Defaults

Contextify comes with sensible defaults for ignored directories and files to minimize noise in your context.

  * **Default Ignored Directories:** `__pycache__`, `.git`, `.venv`, `venv`, `node_modules`, `build`, `dist`, `target`, `.idea`, `.vscode`, `docs`, `tests`, `test`, `.DS_Store`, `Thumbs.db`.
  * **Default Ignored File Patterns:** Includes common temporary, compiled, log, and OS-specific files (e.g., `*.pyc`, `*.log`, `*.swp`, `*.o`, `*.class`).

You can always override or add to these with the `--ignore-dir` and `--ignore-file` options.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome\! Feel free to check the [issues page](https://github.com/alessandrolca/contextify/issues) if you want to contribute.

## 📜 License

This project is licensed under the **Apache Software License**.