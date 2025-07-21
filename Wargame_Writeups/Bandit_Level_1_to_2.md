# OverTheWire Bandit: Level 1 → Level 2 Write-up

## 1. Level Goal
The password for the next level is stored in a file called `-` (a single dash) located in the home directory of the `bandit1` user.

## 2. Commands Used
* `ls`: List directory contents.
* `cat`: Concatenate and display file content.
* `rev`: Reverse lines of a file.

## 3. Methodology & Steps
1.  **Connect to Bandit1:**
    * Logged into `bandit1` using the password found from Level 0 via SSH on port 2220.
        ```bash
        ssh bandit1@bandit.labs.overthewire.org -p 2220
        ```
2.  **List Directory Contents:**
    * Used the `ls` command to list files in the home directory.
        ```bash
        ls
        ```
    * The output clearly showed a file named `-`.
3.  **Attempt to Read the File (Problem Encountered):**
    * My initial attempt was to use `cat -` to read the file. However, `cat` interprets the `-` as a signal to read from standard input (stdin) rather than a filename. This caused `cat` to hang, waiting for input. I tried `Ctrl+Z` to stop the process.
        ```bash
        cat -
        # (This command hung, waiting for input)
        ^Z
        # [1]+  Stopped                 cat -
        ```
4.  **Researching "Dashed Filename":**
    * Recognizing that the dash was being misinterpreted, and recalling the "Helpful Reading Material" hint to "Google Search for 'dashed filename'", I researched how to handle files with special characters.
    * Common solutions include:
        * Specifying the current directory explicitly: `cat ./-`
        * Using `--` to signify end of options: `cat -- -`
        * Using other commands that don't interpret `-` as an option.
5.  **Finding an Alternative Solution (`rev`):**
    * During my research (or by experimenting with other commands), I discovered that `rev` (reverse lines of a file) could read the file without issue, interpreting `-` as a filename. This was a direct and effective way to get the content.
        ```bash
        rev -
        ```
    * The output of `rev -` displayed a string that looked like the password.
6.  **Extracted Password:**
    * The extracted password (which I used to log into Bandit Level 2) was obtained from the output of the `rev -` command.

## 4. Key Learnings & Cybersecurity Context
* **Handling Special Filenames:** This level taught a crucial lesson about interacting with files named with special characters (like `-`), which can be misinterpreted as command-line options. It highlighted the importance of using `--` (end of options marker) or explicitly specifying the path (`./filename`).
* **Command-line Parsing:** Understood how Linux commands parse arguments and options, and how `-` can be ambiguous.
* **Problem-Solving & Research:** Emphasized the importance of researching command-line behavior and alternative tools when encountering unexpected output or command hang-ups. This is a vital skill for troubleshooting in a SOC environment.
* **Forensic Relevance:** Attackers sometimes use unusual filenames or hidden files to evade detection. Knowing how to interact with such files is a basic forensic skill.

---

**Next Step:** You can now log into Bandit Level 2 using the extracted password.
