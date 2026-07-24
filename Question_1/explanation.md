# Q1 Explanation

## Command: find ... -exec md5sum {} \;
**What it does:** Recursively finds every file in the submissions directory
and computes its MD5 hash. Files with the same hash have identical contents.
**Why I chose it:** md5sum produces a unique fingerprint for file contents,
so duplicates are detected regardless of filename.

## Command: awk '{print $1}' | sort | uniq -d
**What it does:** Extracts all hashes, sorts them so identical hashes are
adjacent, then prints only hashes that appear more than once.
**Why I chose it:** uniq -d is the standard Linux tool for finding duplicates
in sorted data. Combined with sort, it's the simplest pipeline for this task.

## Command: awk '!seen[$1]++' > unique_files.txt
**What it does:** Creates an associative array keyed by hash. Only the first
occurrence of each hash passes through; subsequent ones are skipped.
**Why I chose it:** This single awk command extracts unique files without needing
a complex loop. It's idiomatic and efficient.

## Redirection: 2>>"$ERROR_FILE"
**What it does:** Appends any error messages (stderr) to a separate error log
instead of showing them on the terminal.
**Why I chose it:** Keeps errors isolated from the main report for easier auditing.