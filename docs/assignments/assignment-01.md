# Assignment 01: Linux Basics, Directory Operations & Permissions

Comprehensive self-testing question bank covering User/Group identification (`id`, `whoami`), directory tree navigation (`pwd`, `cd`, `mkdir -p`), file inspection, octal/symbolic permissions (`chmod`), ownership (`chown`, `chgrp`), and manual pages (`man`).

!!! tip "Interactive Self-Study Mode"
    Attempt each question in your terminal or mentally before expanding the solution block to review the detailed four-option technical breakdown.

---

### Question 1: Which command is used to display both the numeric User ID (UID), primary Group ID (GID), and all supplementary groups of the currently logged-in user?

- **(A)** whoami
- **(B)** id
- **(C)** groups
- **(D)** uname -u

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) id**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Displays only the effective username string (e.g., 'saichand'), without numeric UID, GID, or group lists.
    - **(B)** :white_check_mark: Correct. 'id' outputs the complete identity string including numeric UID, GID, and all associated supplementary groups.
    - **(C)** :x: Displays only group names associated with the user, omitting the numeric UID, GID, and username.
    - **(D)** :x: 'uname' reports kernel and OS architecture information; the '-u' flag is invalid.

---

### Question 2: Which command and option creates a 3-level nested directory structure 'mydir/Subdir1/Subdir2' in a single command without failing if parent directories do not exist?

- **(A)** mkdir -r mydir/Subdir1/Subdir2
- **(B)** mkdir -p mydir/Subdir1/Subdir2
- **(C)** mkdir -f mydir/Subdir1/Subdir2
- **(D)** md -all mydir/Subdir1/Subdir2

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) mkdir -p mydir/Subdir1/Subdir2**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: '-r' is used for recursive operations in commands like 'rm' and 'cp', but is not a valid parent-creation option in 'mkdir'.
    - **(B)** :white_check_mark: Correct. The '-p' (parents) flag creates intermediate parent directories as needed and does not return an error if directories already exist.
    - **(C)** :x: '-f' (force) is not a valid flag for 'mkdir'.
    - **(D)** :x: 'md' is a DOS/Windows command; Linux uses 'mkdir'.

---

### Question 3: To modify the permissions of a file 'ctest' such that the User has Read, Write, and Execute (rwx), the Group has Read and Execute (r-x), and Others have No permissions (---), which command is correct?

- **(A)** chmod 750 ctest
- **(B)** chmod 755 ctest
- **(C)** chmod 640 ctest
- **(D)** chmod 700 ctest

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) chmod 750 ctest**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. In octal: User rwx (4+2+1=7), Group r-x (4+0+1=5), Others --- (0+0+0=0) gives 750.
    - **(B)** :x: 755 gives Others read and execute (r-x) permissions instead of no permissions (---).
    - **(C)** :x: 640 sets User to rw- (no execute) and Group to r-- (no execute).
    - **(D)** :x: 700 sets Group to --- (no permissions), whereas Group requires r-x.

---

### Question 4: Which command changes both the owner user to 'saichand' and the owning group to 'vlsidevs' for the file 'top.v' in a single command?

- **(A)** chgrp saichand:vlsidevs top.v
- **(B)** chown saichand.vlsidevs top.v
- **(C)** chown saichand:vlsidevs top.v
- **(D)** chmod saichand:vlsidevs top.v

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(C) chown saichand:vlsidevs top.v**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'chgrp' modifies group ownership only and does not accept user:group syntax.
    - **(B)** :x: While dot syntax was historically supported, colon syntax 'user:group' is the POSIX standard across modern Linux.
    - **(C)** :white_check_mark: Correct. 'chown user:group filename' updates both the user owner and group owner atomically.
    - **(D)** :x: 'chmod' alters permission mode bits (read/write/execute), not file ownership.

---

### Question 5: What is the difference between running 'cd ~' and 'cd -' in a Bash terminal?

- **(A)** 'cd ~' goes to root directory '/', while 'cd -' goes to home directory.
- **(B)** 'cd ~' goes to user home directory ($HOME), while 'cd -' switches to the previous working directory ($OLDPWD).
- **(C)** 'cd ~' creates a temporary directory, while 'cd -' deletes the current directory.
- **(D)** 'cd ~' and 'cd -' are identical aliases for navigating up one directory level.

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) 'cd ~' goes to user home directory ($HOME), while 'cd -' switches to the previous working directory ($OLDPWD).**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Root directory is reached via 'cd /', not 'cd ~'.
    - **(B)** :white_check_mark: Correct. The tilde '~' expands to $HOME, while the hyphen '-' expands to the previous working directory stored in $OLDPWD.
    - **(C)** :x: Neither command creates or deletes directories.
    - **(D)** :x: Navigating up one level is performed using 'cd ..'.

---

### Question 6: Which command lists all files including hidden files, sorted with the most recently modified files at the bottom of the terminal output?

- **(A)** ls -la
- **(B)** ls -latr
- **(C)** ls -lR
- **(D)** ls -lhS

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) ls -latr**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'ls -la' lists all files including hidden files, but sorts them alphabetically.
    - **(B)** :white_check_mark: Correct. '-l' (long format), '-a' (all/hidden), '-t' (sort by modification time), and '-r' (reverse order) puts newest files at the bottom.
    - **(C)** :x: 'ls -lR' lists directories recursively.
    - **(D)** :x: 'ls -lhS' sorts files by file size in descending order.

---

### Question 7: How do you view section 1 of the man page for the 'passwd' user command rather than section 5 for the '/etc/passwd' file format?

- **(A)** man passwd
- **(B)** man 1 passwd
- **(C)** man 5 passwd
- **(D)** man -a passwd

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) man 1 passwd**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Running 'man passwd' without a section number defaults to the first matching section, which may be ambiguous.
    - **(B)** :white_check_mark: Correct. 'man 1 passwd' explicitly requests Section 1 (User executable commands).
    - **(C)** :x: 'man 5 passwd' opens Section 5 (File formats and conventions, specifically /etc/passwd).
    - **(D)** :x: 'man -a passwd' displays all matching man sections in sequential order.

---

### Question 8: Which command creates an empty file named 'simulation.log' if it does not exist, or updates its access/modification timestamps if it already exists?

- **(A)** make simulation.log
- **(B)** create simulation.log
- **(C)** touch simulation.log
- **(D)** new simulation.log

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(C) touch simulation.log**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'make' is a build automation tool that reads Makefiles, not a file creation utility.
    - **(B)** :x: 'create' is not a standard Linux command.
    - **(C)** :white_check_mark: Correct. 'touch' creates a 0-byte file if non-existent or updates inode timestamps if existing.
    - **(D)** :x: 'new' is not a valid Linux file utility.

---

### Question 9: When moving a directory 'mydir' into a new directory 'mydir1' using 'mv mydir mydir1', what happens if 'mydir1' already exists as a directory?

- **(A)** The command fails with a directory overwrite error.
- **(B)** 'mydir' is moved inside 'mydir1' as a subdirectory ('mydir1/mydir').
- **(C)** 'mydir1' is deleted and replaced with 'mydir'.
- **(D)** The contents of 'mydir' are merged with 'mydir1' and 'mydir' is deleted.

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) 'mydir' is moved inside 'mydir1' as a subdirectory ('mydir1/mydir').**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'mv' does not error when moving into an existing target directory.
    - **(B)** :white_check_mark: Correct. If the destination is an existing directory, 'mv' places the source directory inside it.
    - **(C)** :x: 'mv' will not overwrite an existing non-empty directory with another directory.
    - **(D)** :x: Directory merging is performed using 'rsync' or 'cp -r', not standard 'mv'.

---

### Question 10: Which symbolic command grants execute permission to the User, removes write permission from Group, and assigns read-only permission to Others for file 'script.sh'?

- **(A)** chmod u+x,g-w,o=r script.sh
- **(B)** chmod u+x;g-w;o=r script.sh
- **(C)** chmod u=x,g=w,o=r script.sh
- **(D)** chmod +x -w =r script.sh

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) chmod u+x,g-w,o=r script.sh**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Comma-separated symbolic clauses 'u+x,g-w,o=r' apply the exact requested modifications.
    - **(B)** :x: Semicolons separate distinct shell commands rather than clauses within 'chmod'.
    - **(C)** :x: 'u=x' sets execute ONLY for user (revoking existing read/write), rather than adding execute (+x).
    - **(D)** :x: Missing category qualifiers (u/g/o) causes ambiguous application across umask.

---

### Question 11: Which command removes a non-empty directory 'old_build' and all of its contents without prompting for confirmation?

- **(A)** rmdir old_build
- **(B)** rm -r -f old_build
- **(C)** del /s old_build
- **(D)** erase -rf old_build

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) rm -r -f old_build**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'rmdir' strictly removes empty directories; it fails with 'Directory not empty' on populated folders.
    - **(B)** :white_check_mark: Correct. 'rm -rf' recursively (-r) and forcefully (-f) removes files and subdirectories without interactive prompts.
    - **(C)** :x: 'del /s' is Windows cmd syntax.
    - **(D)** :x: 'erase' is not a standard Linux command.

---

### Question 12: What is the result of executing 'chmod 644 design.v' on an RTL source file?

- **(A)** Owner: Read/Write, Group: Read-Only, Others: Read-Only
- **(B)** Owner: Read/Write/Execute, Group: Read-Only, Others: None
- **(C)** Owner: Read-Only, Group: Read-Only, Others: Read/Write
- **(D)** Owner: Read/Write, Group: Read/Write, Others: Read/Write

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) Owner: Read/Write, Group: Read-Only, Others: Read-Only**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 6 = 4+2 (rw-), 4 = 4+0 (r--), 4 = 4+0 (r--).
    - **(B)** :x: Read/Write/Execute is octal 7, not 6.
    - **(C)** :x: Read-Only across owner is octal 446, not 644.
    - **(D)** :x: Read/Write across all categories is octal 666.

---

### Question 13: Which command displays the manual page summary description for a keyword, equivalent to 'man -k'?

- **(A)** whatis
- **(B)** apropos
- **(C)** whereis
- **(D)** which

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) apropos**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'whatis' searches for complete exact command names in the whatis database, equivalent to 'man -f'.
    - **(B)** :white_check_mark: Correct. 'apropos keyword' searches description strings across all man pages, identical to 'man -k keyword'.
    - **(C)** :x: 'whereis' locates binary, source, and man page file paths on disk.
    - **(D)** :x: 'which' locates executable binaries in the user's $PATH.

---

### Question 14: If a user attempts to execute a shell script 'test.sh' with permissions '-rw-r--r--', what error is returned by the shell?

- **(A)** Segmentation fault
- **(B)** Permission denied
- **(C)** Command not found
- **(D)** Bad interpreter error

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) Permission denied**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Segmentation fault indicates invalid memory access by a compiled binary.
    - **(B)** :white_check_mark: Correct. The file lacks the execute bit ('x') for the executing user, triggering a 'Permission denied' error.
    - **(C)** :x: 'Command not found' occurs when an executable is not in $PATH or the specified relative path is wrong.
    - **(D)** :x: 'Bad interpreter error' occurs when the shebang line points to a non-existent binary.

---

### Question 15: Which command creates a hard link named 'link_top.v' pointing to 'top.v'?

- **(A)** ln -s top.v link_top.v
- **(B)** ln top.v link_top.v
- **(C)** link -h top.v link_top.v
- **(D)** cp -l top.v link_top.v

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) ln top.v link_top.v**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: '-s' creates a symbolic (soft) link, not a hard link.
    - **(B)** :white_check_mark: Correct. 'ln source target' creates a hard link by default sharing the exact same inode number.
    - **(C)** :x: 'link' takes exactly two arguments without flags.
    - **(D)** :x: While 'cp -l' can link instead of copying, standard 'ln' is the POSIX utility.

---
