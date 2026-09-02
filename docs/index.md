# VLSI & Embedded Systems Engineering Notes

[![Course](https://img.shields.io/badge/Course-PGCP--VLSI-4f46e5?style=for-the-badge&logo=microchip&logoColor=white)](https://github.com/saichand/vlsi-notes)
[![Module](https://img.shields.io/badge/Module-Linux%20%26%20Shell%20Scripting-059669?style=for-the-badge&logo=linux&logoColor=white)](modules/linux-shell-scripting/index.md)
[![Status](https://img.shields.io/badge/Status-Active%20%26%20Updated-2563eb?style=for-the-badge)](https://github.com/saichand/vlsi-notes)
[![License](https://img.shields.io/badge/Notes-Open%20Access-0284c7?style=for-the-badge)](https://github.com/saichand/vlsi-notes)

Welcome to the **VLSI & Embedded Systems Engineering Documentation Hub**. This repository serves as a centralized, rigorous technical reference, lab repository, and self-testing platform covering foundational computing infrastructure, hardware description languages, ASIC physical design, and verification methodologies.

---

!!! info "Curriculum Scope & Context"
    The depth, sequencing, and practical problem sets curated across these modules reflect the **PGCP-VLSI** curriculum standard. Concepts are presented with clear theoretical depth, architectural diagrams, syntax cheat sheets, and real-world scripting patterns.

---

## 🎯 Why This Documentation Exists

Modern VLSI front-end and back-end design flows rely heavily on command-line automation, Unix pipelines, configuration scripts, and scalable simulation setups. This knowledge base was built to:

1. **Establish Strong Foundations**: Provide deep conceptual breakdowns of the Linux kernel, POSIX filesystem standards, system calls, and network diagnostics required for EDA tool server environments.
2. **Master Scripting Automation**: Bridge the gap between interactive terminal commands and production-grade Bash scripting, regular expressions, `sed`, and `awk` text processing for EDA log parsing.
3. **Continuous Self-Evaluation**: Pair every theoretical concept with structured assignment question banks, interactive collapsible solutions, and extensive multiple-choice assessments.

---

## 🗺️ Master Curriculum Roadmap

| Module | Core Domains Covered | Labs & Practice | Status | Link |
| :--- | :--- | :---: | :---: | :---: |
| **Linux & Shell Scripting** | Ubuntu Installation & Setup, Architecture, FHS 3.0, Inodes, Permissions, Streams, Processes, Networking, Bash Scripting | 9 Complete Chapters | :white_check_mark: **Active** | [Explore Notes](modules/linux-shell-scripting/index.md) |
| **Self-Testing & Assignments** | 6 Curated Question Banks (Basic Commands, Regex/Pipes, ACLs/Cron, Networking, 20 Automation Labs, 100 MCQs) | 160+ Questions | :white_check_mark: **Active** | [Self-Testing Hub](assignments/index.md) |
| **Digital Design** | Combinational & Sequential Logic, FSMs, Timing Analysis, FPGA Architecture | Coming Soon | :clock1: *In Progress* | *Planned* |
| **Programming in C & C++** | Memory Layout, Pointers, Bitwise Manipulation, Data Structures, OOP | Coming Soon | :clock1: *In Progress* | *Planned* |
| **Verilog HDL** | Structural/Behavioral Modeling, Synthesizable RTL, Testbenches, Blocking vs Non-Blocking | Coming Soon | :clock1: *In Progress* | *Planned* |
| **HDL Simulation & Synthesis** | Logic Synthesis, Design Constraints, Timing Reports, Gate-Level Simulation | Coming Soon | :clock1: *In Progress* | *Planned* |
| **CMOS VLSI Devices** | MOSFET Physics, Inverter Characteristics, Layout Design Rules, DRC/LVS | Coming Soon | :clock1: *In Progress* | *Planned* |
| **ASIC Physical Design** | Floorplanning, Placement, CTS, Routing, Static Timing Analysis (STA), Sign-off | Coming Soon | :clock1: *In Progress* | *Planned* |
| **SystemVerilog** | OOP Verification, Interfaces, Randomization, Assertions (SVA), Functional Coverage | Coming Soon | :clock1: *In Progress* | *Planned* |
| **UVM Verification** | Universal Verification Methodology, Drivers, Monitors, Scoreboards, Sequences, TLM | Coming Soon | :clock1: *In Progress* | *Planned* |

---

## 🚀 Quick Navigation: Linux & Shell Scripting

```mermaid
graph LR
    A["01. Installation & VirtualBox"] --> B["02. Architecture & Boot"]
    B --> C["03. Filesystem Hierarchy"]
    C --> D["04. Core Commands"]
    D --> E["05. Permissions & ACLs"]
    E --> F["06. Text Processing"]
    F --> G["07. Processes & Crontab"]
    G --> H["08. Networking"]
    H --> I["09. Bash Scripting"]
    I --> J["Self-Testing Hub"]
```

<div class="grid cards" markdown>

-   :material-laptop:{ .lg .middle } __01. Ubuntu Install & VirtualBox__
    
    ---
    VirtualBox VM creation, BIOS VT-x/AMD-V virtualization, disk partitioning (`/`, `swap`, `/home`, EFI), Guest Additions, and shared folder setup.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/01-ubuntu-installation-virtualbox.md)

-   :material-chip:{ .lg .middle } __02. Architecture & Boot Sequence__
    
    ---
    Monolithic kernel vs user space, system calls, MBR/GPT, UEFI, GRUB2, systemd targets (`systemctl`), and clean shutdown commands.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/02-architecture-startup-shutdown.md)

-   :material-folder-network:{ .lg .middle } __03. Filesystem Hierarchy & Inodes__
    
    ---
    FHS 3.0 standard directory tree, 7 file types, inode data structures, hard vs soft links, and storage commands (`df`, `du`, `lsblk`).
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/03-filesystem-hierarchy-inodes.md)

-   :material-console-line:{ .lg .middle } __04. Core Commands & File Ops__
    
    ---
    Navigation semantics (`cd ~`, `cd -`, `mkdir -p`), search with `find`/`locate`, viewing with `cat`/`less`, and archiving with `tar`/`gzip`.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/04-core-commands.md)

-   :material-shield-key:{ .lg .middle } __05. Permissions, Ownership & ACLs__
    
    ---
    Octal & symbolic `chmod`, `chown`, user administration, SUID/SGID/Sticky bits, and POSIX ACLs (`setfacl`).
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/05-permissions-acls.md)

-   :material-filter-cog:{ .lg .middle } __06. Text Processing & RegEx__
    
    ---
    File descriptors, pipes, `grep` regular expressions, stream editing with `sed`, and reporting with `awk`.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/06-text-processing.md)

-   :material-cpu-64-bit:{ .lg .middle } __07. Processes & Task Scheduling__
    
    ---
    Process states, `ps`/`top` inspection, kill signals, background jobs (`nohup`/`&`), and `crontab` automation.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/07-processes-scheduling.md)

-   :material-lan:{ .lg .middle } __08. Networking & Diagnostics__
    
    ---
    OSI & TCP/IP stack, IPv4 CIDR subnetting, `ip`/`ss`/`ping` diagnostics, SSH key pairs, and secure file transfer.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/08-networking-diagnostics.md)

-   :material-script-text:{ .lg .middle } __09. Bash Shell Scripting__
    
    ---
    Variables, arithmetic expansions, test operators, conditionals, loops, functions, and signal traps.
    
    [:octicons-arrow-right-24: Read Chapter](modules/linux-shell-scripting/09-shell-scripting.md)

</div>

---

## 📝 Self-Testing & Assignments Hub

Every assignment is structured with **View 1 (Collapsible Study Mode)** to allow self-assessment before revealing answers:

- [**Assignment 01 — Basics, Directories & Permissions**](assignments/assignment-01.md): User identity, directory hierarchies (`mkdir -p`), and permission masks.
- [**Assignment 02 — File Operations, Text Filtering & Search**](assignments/assignment-02.md): Pipelines, `grep` pattern matching, sorting, and `find` actions.
- [**Assignment 03 — Users, Groups, ACLs, Processes & Cron**](assignments/assignment-03.md): Account provisioning, POSIX ACL rules, `kill` signals, and crontab schedules.
- [**Assignment 04 — Computer Networking & Shell Environment**](assignments/assignment-04.md): IP addressing, routing diagnostics, aliases, `.bashrc`, and SSH transfers.
- [**Assignment 05 — Shell Scripting Automation Lab Sets**](assignments/assignment-05.md): Comprehensive automation scripts, calculators, backup generators, and log parsers.
- [**Assignment 06 — 100 Linux Mastery MCQs Question Bank**](assignments/assignment-06.md): Complete multiple-choice review with 4-option technical explanations for every question.

---

<div style="text-align: center; margin-top: 2rem; padding: 1.5rem; border-top: 1px solid var(--md-default-fg-color--lightest); color: var(--md-default-fg-color--light); font-size: 0.9rem;">
  <strong>Authored & Curated by Sai Chand</strong> | PGCP-VLSI, C-DAC Hyderabad<br>
  <em>Built with MkDocs Material & deployed on GitHub Pages.</em>
</div>
