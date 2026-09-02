# Assignment 05: Shell Scripting Automation Lab Problem Sets

A comprehensive 20-problem laboratory assessment divided into **Part 1: Simple Automation Scripts** (user/group creation, file permissions, directory trees, timestamped backups) and **Part 2: Conditional Statements & Validation** (user validation, file test operators, arithmetic comparisons, disk usage monitors).

!!! tip "Interactive Self-Study & Script Testing"
    Write each shell script in your Ubuntu terminal and test with real arguments before expanding the solution box to review the code breakdown and alternative approaches.

---

## 📑 Part 1: Simple Shell Scripting Automation

### Question 1: Lab 1.1: Write a shell script to create a new user account named 'emp1' with a home directory and set an initial password.

- **(A)** sudo useradd -m emp1 && echo 'emp1:Password123' | sudo chpasswd
- **(B)** sudo adduser --no-home emp1
- **(C)** sudo usercreate emp1 -p Password123
- **(D)** echo 'emp1' >> /etc/passwd

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `sudo useradd -m emp1 && echo 'emp1:Password123' | sudo chpasswd`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'useradd -m emp1' creates the user with a home directory in /home/emp1, and 'chpasswd' batch-sets the initial password securely in non-interactive scripts.
    - **(B)** :x: '--no-home' explicitly prevents home directory creation.
    - **(C)** :x: 'usercreate' is not a standard Linux command.
    - **(D)** :x: Directly appending to /etc/passwd bypasses password encryption, shadow hashing, GID generation, and home directory initialization.

---

### Question 2: Lab 1.2: Write a shell script that creates a new group called 'hr' and adds an existing user (passed as $1) to that group.

- **(A)** sudo groupadd hr && sudo usermod -aG hr "$1"
- **(B)** sudo groupadd hr && sudo useradd -g hr "$1"
- **(C)** sudo addgroup hr "$1"
- **(D)** sudo usermod -g hr "$1"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `sudo groupadd hr && sudo usermod -aG hr "$1"`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'groupadd hr' creates the group, and 'usermod -aG hr "$1"' safely appends the user to the secondary group without overwriting existing memberships.
    - **(B)** :x: 'useradd' is used to create new users, not modify existing user accounts.
    - **(C)** :x: 'addgroup hr "$1"' syntax varies across distributions and may fail without group pre-existence.
    - **(D)** :x: '-g' replaces the primary group rather than adding 'hr' as a supplementary group.

---

### Question 3: Lab 1.3: Write a shell script that displays the UID, GID, and all group memberships of a user whose username is supplied as $1.

- **(A)** id "$1"
- **(B)** whoami "$1"
- **(C)** groups --all "$1"
- **(D)** cat /etc/passwd | grep "$1" | cut -d: -f3

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `id "$1"`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'id username' outputs numeric UID, GID, and all associated group names and GIDs in standard format.
    - **(B)** :x: 'whoami' takes no arguments and prints only the current effective username.
    - **(C)** :x: 'groups' displays group names only, omitting numeric UID and primary GID.
    - **(D)** :x: Extracts only the UID field, omitting GID and secondary group memberships.

---

### Question 4: Lab 1.4: Write a shell script that creates 'data.txt' and sets its permissions to 'rwxr--r--' (Owner: rwx, Group: r--, Others: r--).

- **(A)** touch data.txt && chmod 744 data.txt
- **(B)** touch data.txt && chmod 755 data.txt
- **(C)** touch data.txt && chmod 644 data.txt
- **(D)** make data.txt && chmod u=rwx,go=r data.txt

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `touch data.txt && chmod 744 data.txt`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'touch data.txt' creates the file and octal 744 sets User=rwx (7), Group=r-- (4), Others=r-- (4).
    - **(B)** :x: 755 grants execute permission to Group and Others (r-x).
    - **(C)** :x: 644 sets User to rw- (missing execute bit).
    - **(D)** :x: 'make' is a build utility, not a file creation tool.

---

### Question 5: Lab 1.5: Write a shell script that changes the owner and group of 'report.txt' to a given username ($1) and group name ($2).

- **(A)** sudo chown "$1:$2" report.txt
- **(B)** sudo chgrp "$1:$2" report.txt
- **(C)** sudo chmod "$1:$2" report.txt
- **(D)** sudo chown "$1" report.txt && sudo chown "$2" report.txt

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `sudo chown "$1:$2" report.txt`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'chown user:group filename' updates both the user owner and group owner in a single atomic command.
    - **(B)** :x: 'chgrp' modifies group ownership only and does not accept user:group syntax.
    - **(C)** :x: 'chmod' changes permission bits (rwx), not ownership.
    - **(D)** :x: The second command would attempt to set the user owner to '$2' rather than changing the group.

---

### Question 6: Lab 1.6: Write a shell script that displays a given file's permissions in both symbolic form (e.g., -rw-r--r--) and numeric/octal form (e.g., 644).

- **(A)** ls -l "$1" | awk '{print $1}'; stat -c "%a" "$1"
- **(B)** stat -c "%A %a" "$1"
- **(C)** ls -l "$1" && chmod -v "$1"
- **(D)** Both A and B are valid solutions.

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(D) `Both A and B are valid solutions.`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Valid. 'ls -l' extracts symbolic mode via awk, and 'stat -c %a' prints octal mode.
    - **(B)** :x: Valid. 'stat -c "%A %a"' directly outputs symbolic (%A) and octal (%a) permissions in a single command.
    - **(C)** :x: 'chmod -v' modifies permissions rather than simply displaying existing values.
    - **(D)** :white_check_mark: Correct. Both A and B are accurate implementations.

---

### Question 7: Lab 1.7: Write a shell script that creates the directory structure '/dbda/project/{src,bin,docs}' in a single command and lists the structure.

- **(A)** mkdir -p /dbda/project/{src,bin,docs} && ls -l /dbda/project
- **(B)** mkdir /dbda/project/src /dbda/project/bin /dbda/project/docs
- **(C)** mkdir -r /dbda/project/{src,bin,docs}
- **(D)** create -p /dbda/project/{src,bin,docs}

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `mkdir -p /dbda/project/{src,bin,docs} && ls -l /dbda/project`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'mkdir -p' with bash brace expansion creates intermediate parent directories and all three subdirectories, followed by 'ls -l'.
    - **(B)** :x: Fails if parent directories '/dbda' and '/dbda/project' do not already exist.
    - **(C)** :x: '-r' is invalid for mkdir; the parent creation flag is '-p'.
    - **(D)** :x: 'create' is not a standard Linux command.

---

### Question 8: Lab 1.8: Write a shell script that accepts a username as $1 and displays that user's home directory path and login shell.

- **(A)** getent passwd "$1" | cut -d: -f6,7
- **(B)** grep "^$1:" /etc/passwd | awk -F: '{print "Home:", $6, "Shell:", $7}'
- **(C)** finger "$1"
- **(D)** Both A and B are standard, robust solutions.

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(D) `Both A and B are standard, robust solutions.`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Valid. 'getent passwd' queries the NSS database (supporting local and LDAP users) and fields 6 & 7 are home and shell.
    - **(B)** :x: Valid. Anchored grep '^$1:' on /etc/passwd extracts fields 6 (home directory) and 7 (login shell) via awk.
    - **(C)** :x: 'finger' is a legacy utility not installed by default on modern Linux distributions.
    - **(D)** :white_check_mark: Correct. Both A and B provide robust, production-grade implementations.

---

### Question 9: Lab 1.9: Write a shell script that takes an old filename ($1) and new filename ($2), renames the file, and displays its permissions.

- **(A)** mv "$1" "$2" && ls -l "$2"
- **(B)** rename "$1" "$2" && stat "$1"
- **(C)** cp "$1" "$2" && rm "$1" && ls -l "$1"
- **(D)** mv -p "$1" "$2"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A) `mv "$1" "$2" && ls -l "$2"`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'mv "$1" "$2"' renames the file and 'ls -l "$2"' displays its permissions upon successful move.
    - **(B)** :x: Running 'stat "$1"' after renaming fails with 'No such file or directory' because the old path was renamed.
    - **(C)** :x: 'ls -l "$1"' fails because '$1' was deleted.
    - **(D)** :x: '-p' is not a valid flag for mv.

---

### Question 10: Lab 1.10: Write a shell script that creates a backup copy of '/etc/passwd' inside '/dbda/backup' named 'passwd_backup_<YYYY-MM-DD>'.

- **(A)** mkdir -p /dbda/backup && cp /etc/passwd "/dbda/backup/passwd_backup_$(date +%F)"
- **(B)** cp /etc/passwd /dbda/backup/passwd_backup_date
- **(C)** backup /etc/passwd /dbda/backup/
- **(D)** tar -cvf /dbda/backup/passwd.tar /etc/passwd

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    mkdir -p /dbda/backup && cp /etc/passwd "/dbda/backup/passwd_backup_$(date +%F)"
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'mkdir -p' ensures destination directory exists, and '$(date +%F)' evaluates to the current date (YYYY-MM-DD).
    - **(B)** :x: Hardcodes literal string '_date' rather than evaluating the current dynamic system date.
    - **(C)** :x: 'backup' is not a standard Linux command.
    - **(D)** :x: Creates a tar archive without the requested specific filename format.

---

## 📑 Part 2: Conditional Logic, File Testing & System Monitoring

### Question 11: Lab 2.1: Write a shell script that accepts a username as input and checks whether that user account exists on the system.

- **(A)** if id "$1" &>/dev/null; then echo "User exists"; else echo "User does not exist"; fi
- **(B)** if grep -q "^$1:" /etc/passwd; then echo "User exists"; else echo "User does not exist"; fi
- **(C)** if [ -u "$1" ]; then echo "User exists"; fi
- **(D)** Both A and B are correct implementations.

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(D) `Both A and B are correct implementations.`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Valid. 'id' returns exit code 0 if user exists, non-zero if user does not exist.
    - **(B)** :x: Valid. 'grep -q' quietly searches /etc/passwd and returns exit code 0 on match.
    - **(C)** :x: '-u' is a file test operator for SUID permissions, not a user existence check.
    - **(D)** :white_check_mark: Correct. Both A and B are standard, robust solutions.

---

### Question 12: Lab 2.2: Write a shell script that accepts a filename and checks whether the file exists and is readable; if so, displays its contents, otherwise displays an error message.

- **(A)** if [ -f "$1" ] && [ -r "$1" ]; then cat "$1"; else echo "Error: File not found or unreadable" >&2; fi
- **(B)** if [ -e "$1" ]; then cat "$1"; else echo "Error"; fi
- **(C)** if [ -w "$1" ]; then cat "$1"; fi
- **(D)** cat "$1" || echo "Error"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if [ -f "$1" ] && [ -r "$1" ]; then cat "$1"; else echo "Error: File not found or unreadable" >&2; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. '[ -f "$1" ]' verifies regular file existence and '[ -r "$1" ]' validates read permissions before invoking cat.
    - **(B)** :x: '-e' does not check read permissions; attempting cat on an unreadable file will trigger an unhandled permission error.
    - **(C)** :x: '-w' checks write permission, not read permission.
    - **(D)** :x: Does not use conditional statement syntax ('if...then...else...fi') as requested.

---

### Question 13: Lab 2.3: Write a shell script that accepts two integer arguments ($1, $2) and prints whichever is greater, or reports that they are equal.

- **(A)** if [ "$1" -gt "$2" ]; then echo "$1 is greater"; elif [ "$2" -gt "$1" ]; then echo "$2 is greater"; else echo "Numbers are equal"; fi
- **(B)** if [ "$1" > "$2" ]; then echo "$1 is greater"; fi
- **(C)** if [[ "$1" -ge "$2" ]]; then echo "$1 is greater"; fi
- **(D)** expr "$1" > "$2"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if [ "$1" -gt "$2" ]; then echo "$1 is greater"; elif [ "$2" -gt "$1" ]; then echo "$2 is greater"; else echo "Numbers are equal"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Uses integer comparison operators '-gt' with complete if-elif-else branches covering greater, lesser, and equality.
    - **(B)** :x: Single bracket '[' with '>' performs ASCII string comparison and requires redirection escaping.
    - **(C)** :x: '-ge' does not differentiate between strictly greater and equal.
    - **(D)** :x: 'expr' evaluates mathematical expressions but does not provide the conditional report branching.

---

### Question 14: Lab 2.4: Write a shell script that checks whether a given directory ($1) exists; if not, creates it and confirms creation, otherwise informs the user it already exists.

- **(A)** if [ ! -d "$1" ]; then mkdir -p "$1" && echo "Directory created"; else echo "Directory already exists"; fi
- **(B)** if [ -f "$1" ]; then echo "Exists"; else mkdir "$1"; fi
- **(C)** mkdir "$1" 2>/dev/null || echo "Directory exists"
- **(D)** if [ -z "$1" ]; then mkdir "$1"; fi

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if [ ! -d "$1" ]; then mkdir -p "$1" && echo "Directory created"; else echo "Directory already exists"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. '[ ! -d "$1" ]' tests if directory does not exist, creating it with 'mkdir -p' and confirming success.
    - **(B)** :x: '-f' tests for regular files, not directories.
    - **(C)** :x: Short-circuit syntax does not differentiate between pre-existence and permission errors.
    - **(D)** :x: '-z' tests for empty string arguments, not directory existence.

---

### Question 15: Lab 2.5: Write a shell script that accepts a filename and checks whether the owner has read, write, and execute permissions, reporting each separately.

- **(A)** [ -r "$1" ] && echo "Read: Yes" || echo "Read: No"; [ -w "$1" ] && echo "Write: Yes" || echo "Write: No"; [ -x "$1" ] && echo "Exec: Yes" || echo "Exec: No"
- **(B)** ls -l "$1" | cut -c 2-4
- **(C)** chmod -check "$1"
- **(D)** stat -p "$1"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    [ -r "$1" ] && echo "Read: Yes" || echo "Read: No"; [ -w "$1" ] && echo "Write: Yes" || echo "Write: No"; [ -x "$1" ] && echo "Exec: Yes" || echo "Exec: No"
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Evaluates file test operators '-r', '-w', and '-x' independently and prints discrete status for each permission.
    - **(B)** :x: Prints the raw 3-character string without discrete formatted per-permission status messages.
    - **(C)** :x: '-check' is not a valid flag for chmod.
    - **(D)** :x: '-p' is invalid flag syntax for stat.

---

### Question 16: Lab 2.6: Write a shell script that checks current disk usage of the root partition ('/') and prints a warning if it has crossed 80%, otherwise prints normal status.

- **(A)** USAGE=$(df / | awk 'NR==2 {gsub("%", ""); print $5}'); if [ "$USAGE" -gt 80 ]; then echo "WARNING: Disk usage high: ${USAGE}%"; else echo "Disk usage normal: ${USAGE}%"; fi
- **(B)** if df / > 80%; then echo "Warning"; fi
- **(C)** if [ $(du -sh /) -gt 80 ]; then echo "Warning"; fi
- **(D)** df -h | grep '80%' && echo 'Warning'

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    USAGE=$(df / | awk 'NR==2 {gsub("%", ""); print $5}'); if [ "$USAGE" -gt 80 ]; then echo "WARNING: Disk usage high: ${USAGE}%"; else echo "Disk usage normal: ${USAGE}%"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'df /' extracts row 2 column 5 (capacity percentage), strips the '%' symbol, and compares numerically against 80.
    - **(B)** :x: 'df / > 80%' is invalid syntax that redirects df output to a file named '80%'.
    - **(C)** :x: 'du -sh /' outputs total byte size string (e.g. '12G'), not percentage capacity.
    - **(D)** :x: Only matches if usage is exactly '80%', missing all higher usage values (81%-100%).

---

### Question 17: Lab 2.7: Write a shell script that accepts a username as $1; if the user does not exist, creates the account with a home directory and confirms success, otherwise reports that the user already exists.

- **(A)** if id "$1" &>/dev/null; then echo "User '$1' already exists"; else sudo useradd -m "$1" && echo "User '$1' created successfully"; fi
- **(B)** sudo useradd "$1" || echo "User exists"
- **(C)** if grep "$1" /etc/shadow; then echo "Exists"; fi
- **(D)** usercreate -check "$1"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if id "$1" &>/dev/null; then echo "User '$1' already exists"; else sudo useradd -m "$1" && echo "User '$1' created successfully"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Tests user existence via 'id', branches cleanly, and executes 'useradd -m' to create the user account and home directory.
    - **(B)** :x: Lacks '-m' to create home directory and does not provide explicit pre-validation branching.
    - **(C)** :x: Unprivileged users cannot read /etc/shadow, causing the check to fail under standard accounts.
    - **(D)** :x: 'usercreate' is not a valid Linux command.

---

### Question 18: Lab 2.8: Write a shell script that accepts a number as input and checks whether it is positive, negative, or zero.

- **(A)** if [ "$1" -gt 0 ]; then echo "Positive"; elif [ "$1" -lt 0 ]; then echo "Negative"; else echo "Zero"; fi
- **(B)** if [ "$1" > 0 ]; then echo "Positive"; else echo "Negative"; fi
- **(C)** case $1 in +*) echo Positive ;; -*) echo Negative ;; 0) echo Zero ;; esac
- **(D)** Both A and C are valid implementations.

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(D) `Both A and C are valid implementations.`**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Valid. Integer comparison operators '-gt' and '-lt' correctly classify numbers.
    - **(B)** :x: '>' inside single brackets performs string comparison and misses the zero condition.
    - **(C)** :x: Valid. Pattern matching inside case statement correctly matches signed numbers.
    - **(D)** :white_check_mark: Correct. Both A and C are valid implementations.

---

### Question 19: Lab 2.9: Write a shell script that accepts a username ($1) and a group name ($2), and checks whether that user is a member of the given group.

- **(A)** if id -nG "$1" 2>/dev/null | grep -qw "$2"; then echo "User '$1' is a member of '$2'"; else echo "User '$1' is NOT a member of '$2'"; fi
- **(B)** if groups "$1" | grep "$2"; then echo "Member"; fi
- **(C)** if [ "$1" == "$2" ]; then echo "Member"; fi
- **(D)** getent group "$2" | grep "$1"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if id -nG "$1" 2>/dev/null | grep -qw "$2"; then echo "User '$1' is a member of '$2'"; else echo "User '$1' is NOT a member of '$2'"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'id -nG "$1"' lists all group names, and 'grep -qw' checks for exact whole-word matching.
    - **(B)** :x: Lacks '-w' whole-word match (e.g., group 'admin' would falsely match 'administrator').
    - **(C)** :x: Compares username string directly against group name string, which is logically invalid.
    - **(D)** :x: Does not account for primary group memberships defined in /etc/passwd.

---

### Question 20: Lab 2.10: Write a shell script that accepts a filename argument and checks whether it is a regular file, a directory, or does not exist at all, printing an appropriate message.

- **(A)** if [ ! -e "$1" ]; then echo "Target does not exist"; elif [ -f "$1" ]; then echo "Regular file"; elif [ -d "$1" ]; then echo "Directory"; else echo "Other special file"; fi
- **(B)** if [ -f "$1" ]; then echo "File"; else echo "Directory"; fi
- **(C)** if [ -d "$1" ]; then echo "Directory"; else echo "File"; fi
- **(D)** file "$1"

??? success "Answer & Script Implementation (Click to Expand)"
    **Correct Solution:** :white_check_mark: **(A)**
    ```bash
    if [ ! -e "$1" ]; then echo "Target does not exist"; elif [ -f "$1" ]; then echo "Regular file"; elif [ -d "$1" ]; then echo "Directory"; else echo "Other special file"; fi
    ```
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Tests for non-existence ('! -e'), regular file ('-f'), directory ('-d'), and other special file types with complete branching.
    - **(B)** :x: Fails to identify directories or non-existent files (assumes anything that isn't a regular file is a directory).
    - **(C)** :x: Assumes any non-directory file is a regular file, ignoring non-existent paths and sockets/pipes.
    - **(D)** :x: 'file' is a command binary, not a conditional shell script structure.

---
