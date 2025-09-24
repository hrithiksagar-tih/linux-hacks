## A Practical Guide to the `tree` Command 🌲

The `tree` command is a powerful utility that provides a recursive, visual listing of files and directories in a tree-like format. It's an excellent tool for quickly understanding the layout of a project or filesystem.

### Installation

While not always installed by default, you can easily get it with your system's package manager.

  * **Debian/Ubuntu:** `sudo apt install tree`
  * **macOS (Homebrew):** `brew install tree`
  * **Red Hat/Fedora/CentOS:** `sudo yum install tree` or `sudo dnf install tree`

-----

## Basic Usage

Running the command without any options will display the entire directory structure from your current location.

**Command:**

```bash
tree
```

**Example Output:**

```
.
├── documents
│   └── report.docx
├── images
│   ├── logo.png
│   └── photo.jpg
└── project
    ├── src
    │   └── main.py
    └── tests
        └── test_main.py
```

-----

## Use Case 1: Excluding Specific Files & Folders

This is useful for cleaning up the output by hiding irrelevant items like dependency folders, logs, or build artifacts. The primary tool for this is the **`-I`** flag, which **ignores** items matching a pattern.

### Syntax

```bash
tree -I "pattern1|pattern2|..."
```

  * The pattern uses shell wildcards (`*`, `?`), not regular expressions.
  * Enclose the pattern in quotes (`"`) to prevent the shell from interpreting it.
  * Use the pipe (`|`) character to separate multiple patterns.

### Examples

  * **Exclude a Single Folder:** Ideal for hiding large dependency folders.

    ```bash
    tree -I "node_modules"
    ```

  * **Exclude Multiple Folders:** Ignore build and cache directories.

    ```bash
    tree -I "dist|build|__pycache__"
    ```

  * **Exclude Files by Extension:** Hide all log or temporary files.

    ```bash
    tree -I "*.log|*.tmp"
    ```

  * **Combine Exclusions:** A practical example to ignore a folder and a file type.

    ```bash
    tree -I "node_modules|*.log"
    ```

-----

## Use Case 2: Showing *Only* Specific Files

Sometimes, you don't want to *exclude* things, but rather *include only* a select few. This is perfect for finding all instances of a specific configuration file or viewing only source code. We achieve this by combining `tree` with `grep`.

### The Method

1.  **`tree -F`**: Run `tree` with the `-F` flag, which appends a `/` to all directory names.
2.  **`|`**: Pipe the output to `grep`.
3.  **`grep -E '/$|pattern'`**: Use `grep` to filter the tree. This pattern tells it to keep all lines ending in `/` (the directories) **OR** lines matching your desired file pattern.

### Examples

  * **Find a Specific File:** Show the structure leading to all `evaluation_summary.json` files.

    ```bash
    tree -F . | grep -E '/$|evaluation_summary.json'
    ```

  * **Show Only Source Code Files:** Display only Python and Markdown files.

    ```bash
    tree -F . | grep -E '/$|\.py$|\.md$'
    ```

    *Note: The `$` at the end ensures it matches files ending with `.py` or `.md`.*

-----

## Other Useful Flags

Here are some other common flags to customize your output further.

| Flag | Description | Example |
| :--- | :--- | :--- |
| `-d` | Lists **directories only**. | `tree -d` |
| `-L n` | Limits the display depth to **`n` levels**. | `tree -L 2` |
| `-h` | Prints file sizes in a **human-readable** format. | `tree -h` |
| `-f` | Prints the **full path prefix** for each file. | `tree -f` |
| `--prune` | **Prunes empty directories** from the output. | `tree --prune` |
