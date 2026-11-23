# LogLens

LogLens is a command-line Python script that counts the records in a CSV log file, either all records or only those at one log level (`INFO`, `WARN`, or `ERROR`). It runs entirely on your computer and does not change your log file.

This README explains what LogLens does and how to use it. For step-by-step setup, see the [Installation and First-Run Guide](docs/INSTALL.md).

## Contents

- [Who this is for](#who-this-is-for)
- [What LogLens does and does not do](#what-loglens-does-and-does-not-do)
- [Requirements](#requirements)
- [Quick start](#quick-start)
- [Usage](#usage)
- [Input file format](#input-file-format)
- [Getting help](#getting-help)
- [Repository contents](#repository-contents)

## Who this is for

LogLens is written for computing students and new technical interns who are comfortable opening a terminal and reading a CSV file but have not used LogLens before. You do not need to know this repository's structure in advance; the [Installation and First-Run Guide](docs/INSTALL.md) walks through it.

## What LogLens does and does not do

LogLens **does**:

- Read a CSV log file that you specify.
- Count all records, or only the records at one level: `INFO`, `WARN`, or `ERROR`.
- Print a single line with the result, for example `Records matching ERROR: 2`.

LogLens **does not**:

- Repair, rewrite, or otherwise modify your CSV file. It only reads it.
- Upload, transmit, or store your data anywhere outside your computer.
- Diagnose system failures. It reports counts; interpreting them is up to you.

## Requirements

- **Python 3.10 or newer.** LogLens uses only the Python standard library.
- **A terminal**, such as Terminal on macOS or Linux, or PowerShell or Command Prompt on Windows.

No `pip install` step and no third-party packages are needed.

## Quick start

1. Get the repository files and open a terminal in the repository root (the folder that contains `loglens.py`). The [Installation and First-Run Guide](docs/INSTALL.md) explains both steps.
2. Run LogLens on the included sample file:

   ```bash
   python loglens.py --file data/sample_logs.csv --level ERROR
   ```

3. Check that the output matches:

   ```text
   Records matching ERROR: 2
   ```

> **Note:** Depending on how Python is installed, the command may be `python3` or `py` instead of `python`. Use whichever starts Python 3.10 or newer on your computer.

## Usage

Run LogLens from the repository root:

```bash
python loglens.py --file <path-to-csv> [--level <LEVEL>]
```

| Option | Required? | Description |
| --- | --- | --- |
| `--file <path-to-csv>` | Yes | Path to the CSV log file to read. |
| `--level <LEVEL>` | No | Count only records at this level. Must be `INFO`, `WARN`, or `ERROR`, in uppercase. If omitted, LogLens counts all records. |
| `--help` | No | Show the available options and exit. |

### Examples

Count only `ERROR` records in the sample file:

```bash
python loglens.py --file data/sample_logs.csv --level ERROR
```

```text
Records matching ERROR: 2
```

Count all records in the sample file:

```bash
python loglens.py --file data/sample_logs.csv
```

```text
Records matching ALL: 6
```

Show the available options:

```bash
python loglens.py --help
```

## Input file format

LogLens reads CSV files whose header row contains these three column names, spelled exactly as shown:

| Column | Contents |
| --- | --- |
| `timestamp` | When the event happened |
| `level` | The log level: `INFO`, `WARN`, or `ERROR` |
| `message` | A description of the event |

The included sample file, [`data/sample_logs.csv`](data/sample_logs.csv), shows the expected format:

```text
timestamp,level,message
2026-01-03T09:00:00Z,INFO,Startup complete
2026-01-03T09:05:00Z,WARN,Memory usage high
2026-01-03T09:10:00Z,ERROR,Connection lost
```

If your file is missing any of these columns, LogLens stops and prints an error instead of a count.

## Getting help

1. Check the [Troubleshooting section](docs/INSTALL.md#troubleshooting) of the installation guide for common error messages.
2. Run `python loglens.py --help` to confirm the available options.
3. If the problem continues, open an issue in this repository. Describe the command you ran, the full error message, and your Python version.

> **Protect your data:** Do not post real or private log files in a public issue. Logs can contain sensitive information. Instead, share a short, sanitized example with any private details removed or replaced.

## Repository contents

| Path | Description |
| --- | --- |
| `loglens.py` | The LogLens script. Run it from the repository root. |
| `data/sample_logs.csv` | A six-record sample log file for testing. |
| `docs/INSTALL.md` | Installation and First-Run Guide, including troubleshooting. |
| `docs/FACT_SHEET.md` | Verified technical facts about LogLens. |
