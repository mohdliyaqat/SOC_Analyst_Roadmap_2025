# Linux Command Line Cheatsheet - SOC Analyst Focus

This cheatsheet summarizes essential Linux commands learned during Week 1 of my SOC Analyst Roadmap, with a focus on their practical application in cybersecurity investigations and system administration.

---

## I. Navigation & File System Management

### `pwd` - Print Working Directory
* **Meaning:** Displays the full path of your current directory.
* **Example:** `pwd` -> `/home/analyst/logs`
* **Cybersecurity Context:** Crucial for knowing your exact location during an incident response, especially when navigating unfamiliar compromised systems or investigating file paths.

### `ls` - List Directory Contents
* **Meaning:** Lists files and directories in the current location.
* **Common Options:**
    * `-l`: Long format (shows permissions, owner, size, date).
    * `-a`: Shows all files, including hidden ones (starting with `.` ).
    * `-la`: Combination of long and all.
    * `-h`: Human-readable sizes (e.g., `1K`, `234M`, `2G`).
    * `-R`: Recursive listing (lists contents of subdirectories).
* **Example:** `ls -la /var/www/html`
* **Cybersecurity Context:** Essential for identifying suspicious files (e.g., hidden malware, web shells), checking file permissions to detect misconfigurations or unauthorized access, and assessing the contents of potentially compromised directories.

### `cd` - Change Directory
* **Meaning:** Changes your current working directory.
* **Examples:**
    * `cd /var/log` (Go to a specific path)
    * `cd ..` (Go up one directory)
    * `cd ~` (Go to home directory)
    * `cd -` (Go to the previous directory)
* **Cybersecurity Context:** Rapid navigation to relevant directories like log files (`/var/log`), configuration files (`/etc`), or compromised locations during active investigations.

### `mkdir` - Make Directory
* **Meaning:** Creates new directories.
* **Common Options:**
    * `-p`: Create parent directories as needed.
* **Example:** `mkdir -p /home/analyst/evidence/logs`
* **Cybersecurity Context:** Used to organize forensic evidence, create isolated working directories, or prepare environments for analysis.

### `rmdir` - Remove Directory
* **Meaning:** Removes empty directories.
* **Example:** `rmdir /tmp/old_logs`
* **Cybersecurity Context:** Used for cleanup after investigations or lab exercises.

### `touch` - Change File Timestamps / Create Empty Files
* **Meaning:** Creates new, empty files or updates the access/modification times of existing files.
* **Example:** `touch /tmp/new_evidence.txt`
* **Cybersecurity Context:** Can be used to create placeholder files, or for "timestomping" (altering timestamps of files, a technique sometimes used by attackers or for forensic analysis).

### `cp` - Copy Files or Directories
* **Meaning:** Copies files or directories from one location to another.
* **Common Options:**
    * `-r`: Recursive (required for copying directories).
    * `-i`: Interactive (prompts before overwriting existing files).
* **Example:** `cp /var/log/syslog /home/analyst/evidence/`
* **Cybersecurity Context:** Essential for safely copying log files or other evidence for analysis without altering the originals.

### `mv` - Move or Rename Files or Directories
* **Meaning:** Moves files or directories from one location to another, or renames them.
* **Example:** `mv /home/analyst/suspicious_script.sh /tmp/quarantine/`
* **Cybersecurity Context:** Used to quarantine suspicious files, rename evidence files, or reorganize data during an incident.

### `rm` - Remove Files or Directories
* **Meaning:** Deletes files or directories.
* **Common Options:**
    * `-r`: Recursive (required for deleting directories and their contents).
    * `-f`: Force (deletes without prompting, use with extreme caution!).
* **Example:** `rm -rf /tmp/malware_temp_files`
* **Cybersecurity Context:** Used for cleanup after analysis, or to remove known malicious files (with extreme care and confirmation).

### `file` - Determine File Type
* **Meaning:** Identifies the type of a file (e.g., executable, text, image, script).
* **Example:** `file /usr/bin/ls`
* **Cybersecurity Context:** Crucial for initial assessment of suspicious files to determine if they are executables, scripts, or other file types that might contain malicious code.

---

## II. Viewing & Manipulating File Content

### `cat` - Concatenate and Display File Content
* **Meaning:** Displays the entire content of a file to the terminal.
* **Example:** `cat /etc/passwd`
* **Cybersecurity Context:** Quickly view small configuration files, log snippets, or the contents of suspected malicious scripts.

### `less` - View File Content Page by Page
* **Meaning:** Displays file content one screenful at a time, allowing scrolling, searching, and navigating large files efficiently.
* **Example:** `less /var/log/syslog`
* **Cybersecurity Context:** Ideal for reviewing large log files or output from security tools without overwhelming the terminal.

### `head` - Display the Beginning of a File
* **Meaning:** Shows the first few lines of a file (default 10 lines).
* **Common Options:** `-n <number>` (display specified number of lines).
* **Example:** `head -n 50 /var/log/apache2/access.log`
* **Cybersecurity Context:** Quickly inspect the start of a log file or configuration to understand its format or recent entries.

### `tail` - Display the End of a File
* **Meaning:** Shows the last few lines of a file (default 10 lines).
* **Common Options:** `-f` (follow changes as they occur - **critical for live monitoring**).
* **Example:** `tail -f /var/log/auth.log`
* **Cybersecurity Context:** **Essential for real-time monitoring of log files** for suspicious activity (e.g., failed login attempts, new connections) as they happen.

### `echo` - Display a Line of Text
* **Meaning:** Prints text to the terminal.
* **Example:** `echo "Suspicious activity detected!"`
* **Cybersecurity Context:** Useful in scripts for displaying messages or redirecting text into files (e.g., `echo "ALERT" >> /var/log/security_alerts.log`).

### `>` - Redirect Output (Overwrite)
* **Meaning:** Redirects the output of a command to a file, overwriting the file's contents if it exists.
* **Example:** `ls -l > file_list.txt`
* **Cybersecurity Context:** Saving command output (e.g., process lists, network connections) to a file for later analysis or evidence collection.

### `>>` - Redirect Output (Append)
* **Meaning:** Redirects the output of a command to a file, appending to the end of the file if it exists.
* **Example:** `echo "New alert entry" >> /var/log/custom_alerts.log`
* **Cybersecurity Context:** Appending new findings or alerts to existing log or evidence files.

### `|` - Pipe
* **Meaning:** Connects the output (stdout) of one command to the input (stdin) of another command.
* **Example:** `ps aux | grep firefox`
* **Cybersecurity Context:** **Extremely powerful for chaining commands** for complex log analysis, filtering process lists, or parsing output from security tools. E.g., `cat access.log | grep "malicious_ip" | sort | uniq`.

---

## III. Searching & Filtering

### `grep` - Global Regular Expression Print
* **Meaning:** Searches for patterns in text files. **Absolutely fundamental for log analysis.**
* **Common Options:**
    * `-i`: Case-insensitive search.
    * `-r`: Recursive search (search in subdirectories).
    * `-v`: Invert match (show lines *NOT* matching the pattern).
    * `-n`: Show line numbers of matches.
    * `-c`: Count the number of matching lines.
    * `-E`: Extended regex (for more complex patterns).
* **Example:** `grep -rn "failed password" /var/log/auth.log`
* **Cybersecurity Context:** **The primary tool for finding Indicators of Compromise (IOCs)**, error messages, suspicious user activity, or specific attack patterns within large log files.

### `find` - Search for Files and Directories
* **Meaning:** Searches for files and directories in a directory hierarchy based on various criteria.
* **Common Options:**
    * `-name "pattern"`: Search by file name.
    * `-type d/f`: Search for directories (`d`) or files (`f`).
    * `-size +1M`: Search for files larger than 1MB.
    * `-mtime -7`: Search for files modified in the last 7 days.
    * `-perm 777`: Search by permissions.
* **Example:** `find /var/www/html -name "*.php" -mtime -1` (Find PHP files modified in last day in web root)
* **Cybersecurity Context:** Locating suspicious files (e.g., recently modified web shells, large unknown binaries), finding configuration files, or identifying files with unusual permissions.

### `cut` - Remove Sections from Each Line
* **Meaning:** Extracts specific columns or fields from lines of text, often based on a delimiter.
* **Common Options:**
    * `-d <delimiter>`: Specify the delimiter (e.g., `-d:` for colon-separated).
    * `-f <field_number>`: Specify the field number(s) to cut.
* **Example:** `cat /etc/passwd | cut -d: -f1,7` (Show username and shell from passwd file)
* **Cybersecurity Context:** Parsing log files or command output to extract specific pieces of information (e.g., IP addresses, usernames, timestamps) for further analysis.

---

## IV. User, Permissions & Process Management

### `sudo` - Execute a Command as a Superuser
* **Meaning:** Allows a permitted user to execute a command as the superuser (root) or another user.
* **Example:** `sudo apt update`
* **Cybersecurity Context:** **Essential for administrative tasks** like installing tools, viewing restricted logs, or modifying system configurations. Understanding `sudo` logs (`/var/log/auth.log`) is key for auditing.

### `ps` - Report a Snapshot of Current Processes
* **Meaning:** Displays information about currently running processes.
* **Common Options:**
    * `aux`: Shows all processes on the system (user, PID, CPU usage, memory usage, command).
* **Example:** `ps aux | grep apache2`
* **Cybersecurity Context:** Identifying suspicious processes, understanding what applications are running on a system, and finding processes associated with a user or service.

### `top` - Display Linux Processes (Real-time)
* **Meaning:** Provides a dynamic, real-time view of running processes, CPU usage, memory usage, and other system statistics.
* **Example:** `top`
* **Cybersecurity Context:** Quick overview of system health, identifying processes consuming excessive resources (potential malware), or suspicious processes.

### `kill` - Send a Signal to a Process
* **Meaning:** Sends a signal to a process, typically to terminate it.
* **Common Options:**
    * `-9`: Force kill (SIGKILL - cannot be ignored by the process). Use with caution.
* **Example:** `kill <PID>` (e.g., `kill 12345`)
* **Cybersecurity Context:** Terminating malicious processes during incident response or stopping rogue applications.

### `systemctl` - Control Systemd System and Service Manager
* **Meaning:** Used to control the `systemd` init system, which manages services (daemons) on modern Linux distributions.
* **Common Options:**
    * `status <service_name>`: Check status of a service.
    * `start <service_name>`: Start a service.
    * `stop <service_name>`: Stop a service.
    * `restart <service_name>`: Restart a service.
    * `enable <service_name>`: Enable a service to start on boot.
    * `disable <service_name>`: Disable a service from starting on boot.
* **Example:** `sudo systemctl status apache2`
* **Cybersecurity Context:** Managing security services, stopping compromised services, or investigating services configured for persistence.

### `man` - Manual Pages
* **Meaning:** Displays the manual page for a command, providing detailed information about its usage, options, and examples. **Your best friend for learning new commands!**
* **Example:** `man grep`
* **Cybersecurity Context:** Essential for understanding unfamiliar commands, exploring advanced options of tools, and quickly referencing syntax during investigations.

---

*(You will continue to add more commands from the comprehensive list to this file throughout the week, following this format for each. Remember to commit and push your changes daily!)*
