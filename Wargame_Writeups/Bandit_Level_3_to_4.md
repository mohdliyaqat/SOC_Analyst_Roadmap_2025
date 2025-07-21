# OverTheWire Bandit: Level 3 → Level 4 Write-up

## 1. Level Goal
The password for the next level is stored in a hidden file within the `inhere` directory.

## 2. Commands Used
* `ls`: List directory contents.
* `cd`: Change directory.
* `cat`: Concatenate and display file content.
* `ls -a`: List all files, including hidden ones.

## 3. Methodology & Steps
1.  **Connect to Bandit3:**
    * Logged into `bandit3` using the password found from Level 2 via SSH on port 2220.
        ```bash
        ssh bandit3@bandit.labs.overthewire.org -p 2220
        ```
2.  **Locate the `inhere` directory:**
    * Used `ls -alps` in the home directory to see its contents.
        ```bash
        ls -alps
        ```
    * The output showed a directory named `inhere/`.
        ```
        4 drwxr-xr-x  2 root root 4096 Apr 10 14:23 inhere/
        ```
3.  **Navigate into `inhere` and find the hidden file:**
    * Changed into the `inhere` directory.
        ```bash
        cd inhere
        ```
    * An initial `ls` showed nothing, indicating no visible files. To find hidden files (which start with a `.`), I used the `ls -alps` command again.
        ```bash
        ls -alps
        ```
    * The output revealed a hidden file with an unusual name: `...Hiding-From-You`.
        ```
        4 -rw-r----- 1 bandit4 bandit3    33 Apr 10 14:23 ...Hiding-From-You
        ```
4.  **Read the hidden file:**
    * Based on the filename `...Hiding-From-You`, I attempted to read it with `cat`. Standard attempts like `cat 'Hiding-From-You'` or `cat .Hiding-From-You` failed, as the filename starts with *three* dots, not just one for a typical hidden file.
    * The correct approach was to use the full name as listed by `ls -a`:
        ```bash
        cat ...Hiding-From-You
        ```
    * This executed successfully, displaying the password.
5.  **Extracted Password:**
    * The extracted password (which I used to log into Bandit Level 4) was obtained from the output of the `cat ...Hiding-From-You` command.
6.  **Exit Session:**
    * Used the `exit` command to close the SSH session.
        ```bash
        exit
        ```

## 4. Key Learnings & Cybersecurity Context
* [cite_start]**Hidden Files (`ls -a`):** This level emphasized the importance of using `ls -a` (or `ls -al`) to reveal hidden files, which are often used by legitimate system processes, but also by attackers for stealth and persistence. [cite: 1]
* **Unusual Filename Conventions:** Learned that hidden files aren't always simply `.filename`. They can start with multiple dots, or contain other special characters, requiring precise command usage. This skill is vital for uncovering obfuscated files during security investigations.
* [cite_start]**Persistent Problem Solving:** The process of trying different commands and accurately typing the filename demonstrated perseverance and attention to detail, crucial for cybersecurity analysis. [cite: 1]

---

**Next Step:** You can now log into Bandit Level 4 using the extracted password.
