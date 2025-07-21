# OverTheWire Bandit: Level 0 → Level 1 Write-up

## 1. Level Goal
The password for the next level (Bandit Level 1) is stored in a file named `readme` located in the home directory of the `bandit0` user. The task is to find this password and use it to log into `bandit1` via SSH on port 2220.

## 2. Commands Used
* `ssh`: Secure Shell client (for connecting to the remote server).
* `ls`: List directory contents (to find the `readme` file).
* `cat`: Concatenate and display file content (to read the `readme` file).

## 3. Methodology & Steps
1.  **Connect to Bandit0:**
    * Opened my Kali Linux terminal.
    * Used the `ssh` command to connect to the `bandit0` server on the specified port. The username is `bandit0` and the host is `bandit.labs.overthewire.org` on port `2220`.
        ```bash
        ssh bandit0@bandit.labs.overthewire.org -p 2220
        ```
    * When prompted for a password, I initially tried a blank password (as is common for Level 0), which granted access after a "Permission denied" message (indicating a successful initial connection attempt before authentication).
2.  **List Directory Contents:**
    * Once logged in, I used the `ls` command to list the contents of the current directory (the home directory of `bandit0`).
        ```bash
        ls
        ```
    * The output showed a file named `readme`.
3.  **Read the `readme` file:**
    * To view the content of the `readme` file and retrieve the password, I used the `cat` command.
        ```bash
        cat readme
        ```
    * The output displayed the password along with some welcome messages and rules from OverTheWire.
4.  **Extracted Password:**
    * The password for Bandit Level 1 was: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## 4. Key Learnings & Cybersecurity Context
* **SSH (Secure Shell):** This level reinforced the fundamental use of `ssh` for secure remote access to Linux systems, a core skill for any cybersecurity professional, especially for managing servers or investigating incidents. The `-p` flag for specifying a custom port is also a common real-world scenario.
* **Basic File System Navigation (`ls`):** Demonstrated how `ls` is used to identify relevant files in a directory, a crucial step during reconnaissance or when looking for suspicious files.
* **File Content Viewing (`cat`):** Showed the basic use of `cat` to quickly inspect the contents of a text file, similar to reviewing small log files or configuration data in a real SOC environment.
* **Understanding Level Instructions:** Emphasized the importance of carefully reading level goals to identify key information (like file names and locations).

---

**Next Step:** You can now log into Bandit Level 1 using the password `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
