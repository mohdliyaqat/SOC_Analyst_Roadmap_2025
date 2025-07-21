Got it. Thanks for providing the additional context and your successful solution for Bandit Level 1, especially using `cat ./-`. This is a very common and effective way to solve the "dashed filename" problem.

Let's update the write-up for **`Wargame_Writeups/Bandit_Level_1_to_2.md`** to reflect your specific methodology using `cat ./-`. This will make your write-up even more accurate to your process.

-----

**File Location:** `SOC_Analyst_Roadmap_2025/Wargame_Writeups/Bandit_Level_1_to_2.md`

**Content to Copy and Paste:**

````markdown
# OverTheWire Bandit: Level 1 → Level 2 Write-up

## 1. Level Goal
The password for the next level is stored in a file called `-` (a single dash) located in the home directory of the `bandit1` user.

## 2. Commands Used
* `ls`: List directory contents.
* `cat`: Concatenate and display file content.
* `./`: Current directory path prefix.

## 3. Methodology & Steps
1.  **Connect to Bandit1:**
    * Logged into `bandit1` using the password found from Level 0 via SSH on port 2220.
        ```bash
        ssh bandit1@bandit.labs.overthewire.org -p 2220
        ```
2.  **List Directory Contents & Identify Problem:**
    * Used the `ls -alps` command to list files in the home directory, showing all files including hidden ones, permissions, and sizes.
        ```bash
        ls -alps
        ```
    * The output confirmed the presence of a file named `-`.
        ```
        -rw-r-----  1 bandit2 bandit1      33 Apr 10 14:23 -
        ```
    * An immediate attempt to use `cat -` would typically cause the `cat` command to interpret `-` as standard input, leading to a hang.
3.  **Read the File using Path Prefix:**
    * To explicitly tell `cat` that `-` is a filename in the current directory, I prefixed the filename with `./` (which means "current directory").
        ```bash
        cat ./-
        ```
    * The command executed successfully, and the output displayed the password.
        ```
        263JGJPfgU6LtdEvgfWU1XP5yac29mFx
        ```
4.  **Extracted Password:**
    * The extracted password (which I used to log into Bandit Level 2) was obtained from the output of the `cat ./-` command.
5.  **Exit Session:**
    * Used the `exit` command to close the SSH session.
        ```bash
        exit
        ```

## 4. Key Learnings & Cybersecurity Context
* **Handling Special Filenames:** This level taught a crucial lesson about interacting with files named with special characters like a dash (`-`). These can be misinterpreted as command-line options. Prefacing the filename with `./` is a common and effective way to disambiguate and force commands to treat the dash as a filename.
* **Command-line Parsing:** Understood how Linux commands parse arguments and options, and how specific syntax is needed to handle unusual filenames.
* **Problem-Solving:** The challenge highlighted the importance of knowing alternative ways to interact with files when standard approaches fail, a vital skill for troubleshooting and navigating compromised systems.
* **Forensic Relevance:** Attackers sometimes use unusual filenames or hidden files to evade detection. Knowing how to interact with such files is a basic forensic skill for an SOC analyst.

---

**Next Step:** You can now log into Bandit Level 2 using the extracted password.
````
