# LogLens Installation and First-Run Guide

This guide takes you from downloading LogLens to running your first count. It should take about ten minutes. For an overview of what LogLens does, see the [README](../README.md).

## Contents

1. [Before you begin](#before-you-begin)
2. [Step 1: Get the repository files](#step-1-get-the-repository-files)
3. [Step 2: Check your Python version](#step-2-check-your-python-version)
4. [Step 3: Open a terminal in the repository root](#step-3-open-a-terminal-in-the-repository-root)
5. [Step 4: Run LogLens on the sample file](#step-4-run-loglens-on-the-sample-file)
6. [Step 5: Run LogLens on your own file](#step-5-run-loglens-on-your-own-file)
7. [Troubleshooting](#troubleshooting)
8. [Getting further help](#getting-further-help)

## Before you begin

You need:

- **Python 3.10 or newer.** LogLens uses only the Python standard library, so you do **not** need `pip` or any additional packages.
- **A terminal**, such as Terminal on macOS or Linux, or PowerShell or Command Prompt on Windows.
- **A CSV log file** with the columns `timestamp`, `level`, and `message` (optional for your first run, because a sample file is included).

LogLens runs only on your computer. It reads your CSV file without changing it and does not upload or store your data anywhere else. You do not need a network connection after you have downloaded the files.

> **Note:** The commands in this guide use `python`. On some computers, Python 3 starts with `python3` or `py` instead. If `python` does not work, try those names in every command.

## Step 1: Get the repository files

1. Open the LogLens repository page on GitHub.
2. Select the green **Code** button, then select **Download ZIP**.
3. Extract (unzip) the downloaded file to a folder you can find easily, such as your Desktop or Documents folder.

If you use Git, you can clone the repository instead:

```bash
git clone <repository-URL>
```

Replace `<repository-URL>` with the URL shown under **Code** on the repository page.

## Step 2: Check your Python version

In a terminal, run:

```bash
python --version
```

The output should show `Python 3.10` or a later version, such as `Python 3.12.1`. If the version is older than 3.10, or the command is not recognized, try `python3 --version` or `py --version`. If none of them shows 3.10 or newer, install a current version of Python before continuing.

## Step 3: Open a terminal in the repository root

The **repository root** is the top-level folder of the extracted files. It contains `loglens.py`, `README.md`, and the `data` and `docs` folders. LogLens commands must be run from this folder.

1. In your file manager, open the extracted folder and confirm that you can see `loglens.py`. If you see only one folder inside, open it; the files may be one level down.
2. In your terminal, change to that folder with `cd`, followed by the folder's path:

   ```bash
   cd <path-to-repository-root>
   ```

   Replace `<path-to-repository-root>` with the actual path. If the path contains spaces, wrap it in quotation marks.

## Step 4: Run LogLens on the sample file

Run LogLens on the included sample file, [`data/sample_logs.csv`](../data/sample_logs.csv), to confirm that everything works:

```bash
python loglens.py --file data/sample_logs.csv --level ERROR
```

You should see exactly:

```text
Records matching ERROR: 2
```

To count every record instead, leave out `--level`:

```bash
python loglens.py --file data/sample_logs.csv
```

```text
Records matching ALL: 6
```

If you see these results, LogLens is ready to use. If you see an error, go to [Troubleshooting](#troubleshooting).

## Step 5: Run LogLens on your own file

1. Check that your CSV file's header row contains `timestamp`, `level`, and `message`, spelled exactly that way.
2. Check that the values in the `level` column are `INFO`, `WARN`, or `ERROR`.
3. From the repository root, run LogLens with the path to your file:

   ```bash
   python loglens.py --file <path-to-your-file.csv> --level WARN
   ```

   Replace `<path-to-your-file.csv>` with the location of your file, wrapped in quotation marks if it contains spaces. Replace `WARN` with the level you want, or remove `--level WARN` to count all records.

LogLens prints one line, such as `Records matching WARN: 2`. Your CSV file is not changed.

## Troubleshooting

| Message or symptom | Likely cause | What to do |
| --- | --- | --- |
| `python` is not recognized, or the version is older than 3.10 | Python 3.10+ is not installed, or it starts with a different command | Try `python3` or `py`. If none starts Python 3.10 or newer, install a current version of Python. |
| `error: File not found: <path>` | The path is wrong, or the terminal is not in the repository root | Run the command from the folder containing `loglens.py` (see [Step 3](#step-3-open-a-terminal-in-the-repository-root)) and check the file path for typos. |
| `error: CSV must contain timestamp, level, and message columns` | The header row is missing a column or spells it differently | Rename the header columns to exactly `timestamp`, `level`, and `message`. |
| `error: argument --level: invalid choice` | The level was not one of the accepted values, or was lowercase | Use `INFO`, `WARN`, or `ERROR` in uppercase. |
| `error: the following arguments are required: --file` | The `--file` option was left out | Add `--file` followed by the path to your CSV file. |
| `error: Cannot read file: <path>` | Your account does not have permission to read the file | Check the file's permissions, or copy it to a folder you can read. |

## Getting further help

If these steps do not solve the problem, open an issue in the repository. Include:

- the exact command you ran,
- the full error message, and
- the output of `python --version`.

> **Protect your data:** Do not attach real or private log files to a public issue. Logs can contain sensitive information. Instead, describe the problem and include a short, sanitized example with private details removed or replaced.
