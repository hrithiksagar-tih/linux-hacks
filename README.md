# tree command

## Template: Visualizing a Specific File in a Deep Directory Structure

> tree

This template provides a command to generate a tree view of a directory, filtering it to show the complete folder hierarchy but only a single, specific file type at the end of each branch.

### The Problem it Solves

When you have a project with many experiments or sub-folders (e.g., `experiment_A`, `experiment_B`), and each contains thousands of output files in a sub-directory (like `evaluation/`), this command helps you quickly see the location of one critical file (like `evaluation_summary.json`) across all experiments without the noise of the other files.

### The Template

```bash
# General Template
tree -F [PATH_TO_YOUR_DIRECTORY] | grep -E '/$|[FILENAME_TO_FIND]'
```

**Replace these placeholders:**

  * `[PATH_TO_YOUR_DIRECTORY]`: The starting folder you want to scan.
  * `[FILENAME_TO_FIND]`: The exact name of the file you want to display.

-----

### Example

Here is the template filled out for your exact use case.

**Goal:**
Visualize the directory structure of the `backup_results` folder, but only show the `evaluation_summary.json` files.

**Command:**

```bash
tree -F /projects/data/vision-team/<user>/DATAENGINE/CODEBASES/DocGrounding/evaluations/backup_results | grep -E '/$|evaluation_summary.json'
```
