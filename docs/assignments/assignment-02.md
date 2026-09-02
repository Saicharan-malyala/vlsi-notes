# Assignment 02: File Operations, Text Filtering & Search Pipelines

Practical questions covering pipelines (`|`), redirection (`>`, `>>`, `tee`), `grep` regular expressions, stream editing with `sed`, column extraction with `cut`, and `find` actions.

!!! tip "Interactive Self-Study Mode"
    Attempt each question in your terminal or mentally before expanding the solution block to review the detailed four-option technical breakdown.

---

### Question 1: Which pipeline counts the number of unique user login shells listed in '/etc/passwd'?

- **(A)** cut -d ':' -f 7 /etc/passwd | sort | uniq | wc -l
- **(B)** cut -d ':' -f 1 /etc/passwd | uniq -c
- **(C)** grep 'bin' /etc/passwd | wc -w
- **(D)** sort /etc/passwd | cut -f 7 | count

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) cut -d ':' -f 7 /etc/passwd | sort | uniq | wc -l**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'cut -d : -f 7' extracts the shell field, 'sort' groups identical shells, 'uniq' deduplicates them, and 'wc -l' counts total unique entries.
    - **(B)** :x: Field 1 extracts usernames, not shells; and uniq without sort fails to deduplicate non-adjacent duplicates.
    - **(C)** :x: Filters for lines containing 'bin' and counts total words, not unique shells.
    - **(D)** :x: 'cut -f 7' defaults to tab delimiter (failing on colon-separated /etc/passwd), and 'count' is not a standard Unix command.

---

### Question 2: Which command searches for the pattern 'CRITICAL_TIMING' in all '.rpt' files under the current directory tree, ignoring case and showing line numbers?

- **(A)** find . -name '*.rpt' | grep -i 'CRITICAL_TIMING'
- **(B)** grep -rni --include='*.rpt' 'CRITICAL_TIMING' .
- **(C)** locate -i 'CRITICAL_TIMING' *.rpt
- **(D)** sed -n '/CRITICAL_TIMING/p' *.rpt

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) grep -rni --include='*.rpt' 'CRITICAL_TIMING' .**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Grep would match against the filename paths emitted by find, rather than searching inside the contents of the report files.
    - **(B)** :white_check_mark: Correct. '-r' (recursive), '-n' (line numbers), '-i' (case-insensitive), and '--include=*.rpt' searches inside all matching reports efficiently.
    - **(C)** :x: 'locate' searches filenames in a database index, not file contents.
    - **(D)** :x: 'sed' does not perform recursive directory traversal and would not print line numbers by default.

---

### Question 3: What is the key functional difference between output redirection operators '>' and '>>'?

- **(A)** '>' appends to an existing file, while '>>' truncates/overwrites the file.
- **(B)** '>' redirects standard output, while '>>' redirects standard error.
- **(C)** '>' overwrites the target file, while '>>' appends data to the end of the file.
- **(D)** '>' creates a temporary file, while '>>' creates a permanent file.

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(C) '>' overwrites the target file, while '>>' appends data to the end of the file.**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: This reverses the true meanings: '>' overwrites, '>>' appends.
    - **(B)** :x: Both operate on standard output (FD 1) by default; stderr is redirected via '2>' or '2>>'.
    - **(C)** :white_check_mark: Correct. Single chevron '>' truncates/creates the file, whereas double chevron '>>' appends new lines to existing content.
    - **(D)** :x: Both operators operate directly on standard filesystem targets.

---

### Question 4: Which command finds all regular files in '/home/student' larger than 50 Megabytes modified within the last 7 days?

- **(A)** find /home/student -type f -size +50M -mtime -7
- **(B)** find /home/student -type d -size 50M -mtime +7
- **(C)** search /home/student -files -size >50MB -days <7
- **(D)** find /home/student -name '*.v' -size 50M -ctime 7

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) find /home/student -type f -size +50M -mtime -7**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. '-type f' matches regular files, '-size +50M' matches greater than 50MB, and '-mtime -7' matches modified less than 7 days ago.
    - **(B)** :x: '-type d' searches for directories, and '-mtime +7' searches for files older than 7 days.
    - **(C)** :x: 'search' is not a standard Linux command.
    - **(D)** :x: Constrains search to '*.v' and exact 50M/7 days rather than greater/less than thresholds.

---

### Question 5: Which 'sed' command substitutes all occurrences of 'wire [31:0]' with 'logic [31:0]' globally in 'design.v' and writes changes directly to the file?

- **(A)** sed 's/wire \[31:0\]/logic \[31:0\]/' design.v
- **(B)** sed -i 's/wire \[31:0\]/logic \[31:0\]/g' design.v
- **(C)** sed -e 'replace wire logic' design.v
- **(D)** grep -v 'wire' design.v > design.v

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) sed -i 's/wire \[31:0\]/logic \[31:0\]/g' design.v**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Missing '-i' (prints to stdout without saving to disk) and missing 'g' flag (replaces only the first occurrence per line).
    - **(B)** :white_check_mark: Correct. '-i' enables in-place file modification, and 'g' flag replaces all occurrences on each line.
    - **(C)** :x: 'replace' is not valid sed command syntax.
    - **(D)** :x: Redirecting to the same input file 'design.v' truncates the file to 0 bytes before grep reads it.

---

### Question 6: Which command creates a compressed archive named 'vlsi_backup.tar.gz' containing the 'rtl/' directory?

- **(A)** tar -cvf vlsi_backup.tar.gz rtl/
- **(B)** tar -czvf vlsi_backup.tar.gz rtl/
- **(C)** gzip -tar vlsi_backup.tar.gz rtl/
- **(D)** zip -tar vlsi_backup.tar.gz rtl/

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) tar -czvf vlsi_backup.tar.gz rtl/**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: '-cvf' creates an uncompressed tar archive despite the '.tar.gz' extension name.
    - **(B)** :white_check_mark: Correct. '-c' (create), '-z' (gzip compression), '-v' (verbose), and '-f' (archive filename) creates a compressed gzip tarball.
    - **(C)** :x: 'gzip' does not accept a directory or '-tar' flag directly.
    - **(D)** :x: 'zip' creates '.zip' format files, not tar.gz archives.

---

### Question 7: How do you extract lines 20 through 35 from a 1000-line simulation log file 'run.log'?

- **(A)** head -n 35 run.log | tail -n 16
- **(B)** head -n 20 run.log | tail -n 35
- **(C)** tail -n +20 run.log | head -n 35
- **(D)** cat run.log | cut -l 20-35

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) head -n 35 run.log | tail -n 16**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'head -n 35' takes the first 35 lines, and piping to 'tail -n 16' extracts the last 16 lines (lines 20 to 35 inclusive).
    - **(B)** :x: This takes the first 20 lines and then the last 35 of those, producing only lines 1 to 20.
    - **(C)** :x: 'head -n 35' on 'tail -n +20' extracts 35 lines (lines 20 through 54), not 16 lines.
    - **(D)** :x: 'cut -l' is invalid flag syntax for cut.

---

### Question 8: Which tool and argument deletes all carriage-return characters ('\r') from a DOS-formatted text file?

- **(A)** tr -d '\r' < dos_file.txt > unix_file.txt
- **(B)** cut -d '\r' dos_file.txt
- **(C)** sed 'delete \r' dos_file.txt
- **(D)** wc -d '\r' dos_file.txt

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) tr -d '\r' < dos_file.txt > unix_file.txt**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'tr -d \r' deletes all carriage return characters from the standard input stream.
    - **(B)** :x: 'cut -d' specifies field delimiter for column extraction, not character deletion.
    - **(C)** :x: Sed delete command requires '/\r/d' address notation.
    - **(D)** :x: 'wc' is a word/line counting utility and does not support deletion.

---

### Question 9: Which command displays only lines in 'file1.txt' and 'file2.txt' that are unique to 'file1.txt' (suppressing common lines and lines unique to file2), assuming both files are sorted?

- **(A)** diff -u file1.txt file2.txt
- **(B)** comm -23 file1.txt file2.txt
- **(C)** cmp file1.txt file2.txt
- **(D)** uniq -u file1.txt file2.txt

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) comm -23 file1.txt file2.txt**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'diff -u' outputs unified difference format showing added and removed lines together.
    - **(B)** :white_check_mark: Correct. 'comm' outputs 3 columns: (1) unique to file1, (2) unique to file2, (3) common. '-23' suppresses columns 2 and 3, outputting column 1 only.
    - **(C)** :x: 'cmp' performs byte-by-byte comparison and stops at the first differing byte.
    - **(D)** :x: 'uniq -u' operates on a single file stream, not two distinct files.

---

### Question 10: What is the function of the 'tee' utility in a Linux pipeline?

- **(A)** It terminates execution if an error occurs in the pipeline.
- **(B)** It duplicates standard input to standard output and simultaneously writes it to one or more files.
- **(C)** It tests the network bandwidth between two remote servers.
- **(D)** It converts text files from ASCII to UTF-8 encoding.

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) It duplicates standard input to standard output and simultaneously writes it to one or more files.**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Error termination in bash is configured via 'set -e', not 'tee'.
    - **(B)** :white_check_mark: Correct. 'tee' acts as a T-splitter, sending stream output to both stdout (terminal) and specified log files.
    - **(C)** :x: Network bandwidth testing is performed with 'iperf', not 'tee'.
    - **(D)** :x: Character encoding conversion is handled by 'iconv'.

---
