# Assignment 04: Computer Networking, Diagnostics & Shell Environment

Questions covering IPv4 CIDR subnetting, socket inspection (`ss`), reachability diagnostics (`ping`, `traceroute`), SSH key authentication, `scp`, and `.bashrc` environment profiles.

!!! tip "Interactive Self-Study Mode"
    Attempt each question in your terminal or mentally before expanding the solution block to review the detailed four-option technical breakdown.

---

### Question 1: How many usable host IP addresses are available in a subnet configured with CIDR prefix /28 (subnet mask 255.255.255.240)?

- **(A)** 16
- **(B)** 14
- **(C)** 30
- **(D)** 6

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(B) 14**
    
    **Option-by-Option Breakdown:**
    - **(A)** :x: 16 is the total number of IP addresses (2^(32-28) = 16), including Network ID and Broadcast ID.
    - **(B)** :white_check_mark: Correct. Usable hosts = 2^(32-28) - 2 = 16 - 2 = 14.
    - **(C)** :x: 30 hosts corresponds to a /27 subnet mask (255.255.255.224).
    - **(D)** :x: 6 hosts corresponds to a /29 subnet mask (255.255.255.248).

---

### Question 2: Which modern command displays all listening TCP and UDP sockets along with their process names and PIDs?

- **(A)** ss -tulnp
- **(B)** ip route show
- **(C)** ping -tulnp
- **(D)** ifconfig -listening

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) ss -tulnp**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'ss' (socket statistics) with '-t' (TCP), '-u' (UDP), '-l' (listening), '-n' (numeric ports), and '-p' (process ID) inspects listening sockets.
    - **(B)** :x: 'ip route' displays routing tables, not socket connections.
    - **(C)** :x: 'ping' sends ICMP echo requests and does not take socket flags.
    - **(D)** :x: 'ifconfig' does not have a '-listening' option.

---

### Question 3: Which startup configuration file is executed for interactive, non-login Bash shell sessions for a specific user?

- **(A)** ~/.bashrc
- **(B)** /etc/profile
- **(C)** ~/.bash_profile
- **(D)** /etc/environment

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) ~/.bashrc**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. '~/.bashrc' is executed whenever a new interactive subshell or terminal tab is opened.
    - **(B)** :x: '/etc/profile' is the system-wide login shell initialization script.
    - **(C)** :x: '~/.bash_profile' is executed only during initial user login (e.g. SSH login or console login).
    - **(D)** :x: '/etc/environment' defines system-wide environment key-value pairs, not shell scripts.

---

### Question 4: Which command copies a directory 'rtl_src/' recursively from a local machine to a remote server at IP 192.168.1.50 under '/home/user/' via SSH?

- **(A)** scp -r rtl_src/ user@192.168.1.50:/home/user/
- **(B)** cp -remote rtl_src/ user@192.168.1.50:/home/user/
- **(C)** ssh cp -r rtl_src/ user@192.168.1.50:/home/user/
- **(D)** ftp -r rtl_src/ user@192.168.1.50:/home/user/

??? success "Answer & Detailed Technical Explanation (Click to Expand)"
    **Correct Answer:** :white_check_mark: **(A) scp -r rtl_src/ user@192.168.1.50:/home/user/**
    
    **Option-by-Option Breakdown:**
    - **(A)** :white_check_mark: Correct. 'scp -r' uses the SSH protocol to recursively copy files securely between hosts.
    - **(B)** :x: 'cp' only operates on locally mounted filesystems.
    - **(C)** :x: 'ssh' executes commands remotely on the destination server rather than transferring local source files.
    - **(D)** :x: 'ftp' is an unencrypted legacy protocol that requires interactive commands or separate batch scripting.

---
