# Assignment 03: User Administration, ACLs, Process Control & Crontab

Questions covering user/group management (`/etc/passwd`, `/etc/shadow`), POSIX ACLs (`setfacl`), process states, signals (`kill -9`), and `crontab` task automation.

!!! tip "Interactive Self-Study Mode"
    Attempt each question in your terminal or mentally before expanding the solution block to review the detailed four-option technical breakdown.

---

### Question 1: Which command creates a new group named 'vlsidevs' and then adds existing user 'student1' to it without removing them from their other supplementary groups?

- **(A)** groupadd vlsidevs && usermod -g vlsidevs student1
- **(B)** groupadd vlsidevs && usermod -aG vlsidevs student1
- **(C)** groupcreate vlsidevs && useradd -G vlsidevs student1
- **(D)** addgroup vlsidevs && passwd -g vlsidevs student1

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) groupadd vlsidevs && usermod -aG vlsidevs student1**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: '-g' replaces the user's PRIMARY group rather than appending to supplementary groups.
    - **(B)** :white_check_mark: Correct. 'groupadd' creates the group, and 'usermod -aG' appends (-a) the user to the supplementary group (-G).
    - **(C)** :x: 'groupcreate' is not a valid Linux command, and 'useradd' is used to create new users, not modify existing ones.
    - **(D)** :x: 'passwd -g' is invalid syntax for group membership.

---

### Question 2: Where are encrypted user passwords and password expiration metadata securely stored in a standard Linux system?

- **(A)** /etc/passwd
- **(B)** /etc/shadow
- **(C)** /etc/security
- **(D)** /var/log/auth.log

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) /etc/shadow**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: '/etc/passwd' is world-readable and stores account metadata with an 'x' placeholder for passwords.
    - **(B)** :white_check_mark: Correct. '/etc/shadow' is readable strictly by root (mode 640 or 600) and contains salted password hashes and aging policies.
    - **(C)** :x: '/etc/security' contains PAM configuration files, not user password hashes.
    - **(D)** :x: '/var/log/auth.log' contains authentication audit logs.

---

### Question 3: Which command grants user 'alice' read and write access on 'shared_netlist.v' using POSIX Access Control Lists (ACLs)?

- **(A)** chmod u:alice:rw shared_netlist.v
- **(B)** setfacl -m u:alice:rw shared_netlist.v
- **(C)** getfacl -set alice=rw shared_netlist.v
- **(D)** chown alice:rw shared_netlist.v

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) setfacl -m u:alice:rw shared_netlist.v**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 'chmod' only accepts standard UGO categories (u/g/o), not named individual usernames.
    - **(B)** :white_check_mark: Correct. 'setfacl -m u:username:perms file' modifies the ACL to grant specific permissions to named users.
    - **(C)** :x: 'getfacl' is used to view ACLs, not set or modify them.
    - **(D)** :x: 'chown' modifies file ownership, not permission masks.

---

### Question 4: What is the signal number and characteristic of SIGKILL?

- **(A)** Signal 15; allows the process to catch the signal and perform clean termination.
- **(B)** Signal 2; sent when the user presses Ctrl+C in the terminal.
- **(C)** Signal 9; cannot be caught, blocked, or ignored, resulting in immediate kernel-level termination.
- **(D)** Signal 1; reloads daemon configuration files without stopping the process.

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(C) Signal 9; cannot be caught, blocked, or ignored, resulting in immediate kernel-level termination.**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: Signal 15 is SIGTERM (graceful termination).
    - **(B)** :x: Signal 2 is SIGINT (interrupt from keyboard).
    - **(C)** :white_check_mark: Correct. SIGKILL is Signal 9 and is handled directly by the kernel scheduler; processes cannot intercept or ignore it.
    - **(D)** :x: Signal 1 is SIGHUP (hangup/reload).

---

### Question 5: Which crontab entry runs a script '/opt/scripts/backup.sh' every Monday through Friday at exactly 6:30 PM (18:30)?

- **(A)** 30 18 * * 1-5 /opt/scripts/backup.sh
- **(B)** 18 30 * * 1-5 /opt/scripts/backup.sh
- **(C)** * 18 30 * 1,5 /opt/scripts/backup.sh
- **(D)** 30 6 * * Mon-Fri /opt/scripts/backup.sh

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) 30 18 * * 1-5 /opt/scripts/backup.sh**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. Fields: Minute=30, Hour=18, DayOfMonth=*, Month=*, DayOfWeek=1-5 (Monday-Friday).
    - **(B)** :x: Reverses minute and hour (would run at 18 minutes past 6:00 PM).
    - **(C)** :x: Runs every minute during hour 18 on day 30 of the month.
    - **(D)** :x: Hour 6 is 6:00 AM (06:00), not 6:30 PM (18:30).

---
