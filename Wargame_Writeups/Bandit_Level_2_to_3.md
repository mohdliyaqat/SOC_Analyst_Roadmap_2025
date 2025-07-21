# OverTheWire Bandit: Level 2 → Level 3 Write-up

## 1. Level Goal
The password for the next level is stored in a file called `spaces in this filename` located in the home directory of the `bandit2` user.

## 2. Commands Used
* `ls`: List directory contents.
* `cat`: Concatenate and display file content.
* `' '` (Single quotes): For enclosing filenames with spaces.

## 3. Methodology & Steps
1.  **Connect to Bandit2:**
    * Logged into `bandit2` using the password found from Level 1 via SSH on port 2220.
        ```bash
        ssh bandit2@bandit.labs.overthewire.org -p 2220
        ```
2.  **List Directory Contents & Identify Problem:**
    * Used the `ls -alps` command to list files in the home directory.
        ```bash
        ls -alps
        ```
    * The output clearly showed a file named `spaces in this filename`.
        ```
        -rw-r-----  1 bandit3 bandit2    33 Apr 10 14:23 spaces in this filename
        ```
    * Attempting to read the file directly with `cat spaces in this filename` resulted in `cat` interpreting each word as a separate file, leading to "No such file or directory" errors for each part.
        ```bash
        cat spaces in this filename
        # cat: spaces: No such file or directory
        # cat: in: No such file or directory
        # cat: this: No such file or directory
        # cat: filename: No such file or directory
        ```
3.  **Read the File using Single Quotes:**
    * To make `cat` treat "spaces in this filename" as a single file name (despite the spaces), I enclosed the entire filename in single quotes.
        ```bash
        cat 'spaces in this filename'
        ```
    * This command executed successfully, and the output displayed the password.
4.  **Extracted Password:**
    * The extracted password (which I used to log into Bandit Level 3) was obtained from the output of the `cat 'spaces in this filename'` command.

## 4. Key Learnings & Cybersecurity Context
* **Handling Filenames with Spaces:** This level taught a fundamental concept in Linux command-line usage: how to properly interact with files that have spaces in their names. Spaces act as delimiters for commands, so enclosing the filename in single quotes (`'...'`) or double quotes (`"..."`), or escaping each space with a backslash (`\ `), is necessary to treat the entire string as a single argument.
* **Command-line Parsing:** Reinforced understanding of how the shell parses commands and arguments.
* **Problem-Solving & Syntax:** Highlighted the importance of knowing proper syntax for unusual filenames, a skill valuable when dealing with potentially obfuscated or non-standard file naming conventions during a security investigation.

---

**Next Step:** You can now log into Bandit Level 3 using the extracted password.
