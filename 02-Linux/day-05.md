# Basic Linux Commands

## 16. Combining Commands with Pipes
When using pipes (`|`) to connect multiple commands, if one of the commands in the chain fails:
- The shell continues executing subsequent commands unless explicitly handled.
- Errors in a command may lead to unintended empty or incorrect output for the next command in the pipeline.
- To handle errors, you can use `set -o pipefail`, which causes the entire pipeline to fail if any command fails.
- Example:
  ```bash
  set -o pipefail
  cat non_existent_file | grep "something"
  ```
  This ensures that the pipeline fails instead of silently proceeding.

## 17. File Descriptors
- If you redirect output to an already open file (`>`), its contents will be **overwritten**.
- To append instead of overwriting, use `>>`:
  ```bash
  echo "New line" >> file.txt
  ```
- If the file is already open by another process, changes may not be reflected until the file is closed and reopened.

## 18. Using Wildcards
- Using `rm *` or `rm *.log` can be dangerous as it might delete unintended files.
- To prevent mistakes:
  - Use `ls` first to preview files before deletion:
    ```bash
    ls *.log
    ```
  - Enable interactive mode with `-i`:
    ```bash
    rm -i *.log
    ```
  - Use a safer approach, such as moving files to a backup before deleting.

## 19. Environment Variables
- If you set an environment variable in a session using:
  ```bash
  export MY_VAR="hello"
  ```
  It will **not persist** in a new terminal session.
- To make it permanent, add it to `~/.bashrc` or `~/.bash_profile`:
  ```bash
  echo 'export MY_VAR="hello"' >> ~/.bashrc
  source ~/.bashrc
  ```

## 20. Recovering Deleted Files
- If a file is deleted, it’s usually **not recoverable** from the standard file system.
- Possible recovery methods:
  - Check if the file is in the Trash (`~/.local/share/Trash`).
  - Use `extundelete` for ext file systems.
  - If on a server, restore from a backup (`rsync` or `tar` backups).
- To **prevent permanent loss**:
  - Use `mv` instead of `rm`:
    ```bash
    mv important.txt ~/backup/
    ```
  - Use `trash-cli` instead of `rm`:
    ```bash
    trash-put file.txt
    ```

## 21. Impact of Sleep Command
- The `sleep` command pauses execution for a specified time:
  ```bash
  sleep 30  # Waits for 30 seconds
  ```
- **Effects:**
  - The process remains idle, blocking execution of subsequent commands.
  - Other background processes in the terminal are unaffected.
- **Cancelling `sleep`:**
  - Press `Ctrl + C` to interrupt.
  - Use `kill` to terminate a sleeping process if running in the background.

## 22. Using `dd` Command
- The `dd` command is powerful but **risky** if the wrong target is specified:
  ```bash
  dd if=/dev/sda of=/dev/sdb
  ```
- **Potential risks:**
  - If the target (`of=`) is incorrect, data loss is irreversible.
- **Safety measures:**
  - Use `lsblk` or `fdisk -l` to verify disk identifiers.
  - Add `status=progress` to monitor execution.
  - Test with `--dry-run` or `bs=1M count=10` to copy a small portion first.

## 23. Changing Directories
- If the directory doesn’t exist:
  ```bash
  cd /nonexistent_directory
  ```
  It returns:
  ```
  bash: cd: /nonexistent_directory: No such file or directory
  ```
- **Check for existence before changing directories:**
  ```bash
  if [ -d "/mydir" ]; then cd /mydir; else echo "Directory not found"; fi
  ```

## 24. File Ownership and Permissions
- When copying files:
  ```bash
  cp file.txt /protected_directory/
  ```
  - If you don’t have write permission, the copy fails.
  - Ownership may change to the user performing the copy.
- **Preserve permissions and ownership** using:
  ```bash
  cp -p file.txt /destination/
  ```
  Or for directories:
  ```bash
  cp -rp mydir /destination/
  ```

## 25. System Shutdown & Scheduled Commands
- If you schedule a command using `at` or `cron` and the system shuts down before execution:
  - **`cron` Jobs**: The job will not run but may run at the next scheduled time.
  - **`at` Jobs**: The job is lost unless re-added manually.
- **Ensure execution after reboot:**
  - Use `@reboot` in `crontab`:
    ```bash
    crontab -e
    @reboot /path/to/script.sh
    ```
  - Use `systemd` timers instead of `cron`:
    ```bash
    systemctl enable myjob.timer
    ```

## 26. Checking Network Connectivity
- To test internet connectivity:
  ```bash
  ping -c 4 google.com
  ```
- To check if a specific port is open:
  ```bash
  nc -zv example.com 80
  ```
- To display network interfaces:
  ```bash
  ip a
  ```

## 27. Finding Large Files
- To list the largest files in a directory:
  ```bash
  find /path -type f -exec du -h {} + | sort -rh | head -10
  ```

## 28. Monitoring CPU and Memory Usage
- To check real-time CPU and memory usage:
  ```bash
  top
  ```
- For a more user-friendly interface:
  ```bash
  htop
  ```
- To check memory usage:
  ```bash
  free -h
  ```

## 29. Checking Disk Usage
- To view disk usage of directories:
  ```bash
  du -sh *
  ```
- To check free disk space:
  ```bash
  df -h
  ```

## 30. Creating and Extracting Archives
- To create a tar archive:
  ```bash
  tar -cvf archive.tar myfolder/
  ```
- To extract a tar archive:
  ```bash
  tar -xvf archive.tar
  ```
- To create a compressed archive:
  ```bash
  tar -czvf archive.tar.gz myfolder/
  ```
- To extract a compressed archive:
  ```bash
  tar -xzvf archive.tar.gz
  ```

