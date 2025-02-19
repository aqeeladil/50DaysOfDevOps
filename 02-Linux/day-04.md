# Basic Linux Commands

## 1. Navigating the Filesystem
- **Check current directory:**  
  ```bash
  pwd
  ```
- **List all files, including hidden ones:**  
  ```bash
  ls -la
  ```

## 2. File and Directory Management
- **Create a directory called `projects`:**  
  ```bash
  mkdir projects
  ```
- **Move into the `projects` directory and create an empty file `readme.txt`:**  
  ```bash
  cd projects
  touch readme.txt
  ```

## 3. Editing and Viewing Files
- **Open `notes.txt` in nano, make changes, and save:**  
  ```bash
  nano notes.txt
  ```
  *(Press `Ctrl + X`, then `Y`, then `Enter` to save and exit.)*
- **View the first 10 lines of `logfile.log`:**  
  ```bash
  head logfile.log
  ```

## 4. Searching and Filtering
- **Search for lines containing "admin" in `users.txt`:**  
  ```bash
  grep "admin" users.txt
  ```
- **Find all files in `/home` that contain "config" in their name:**  
  ```bash
  find /home -type f -name "*config*"
  ```

## 5. Copying, Moving, and Deleting Files
- **Copy `report.docx` to `/backup/docs`:**  
  ```bash
  cp report.docx /backup/docs/
  ```
- **Rename `draft.txt` to `final.txt`:**  
  ```bash
  mv draft.txt final.txt
  ```
- **Permanently remove `test.txt`:**  
  ```bash
  rm test.txt
  ```

## 6. System Information and Variables
- **Check the current user:**  
  ```bash
  whoami
  ```
- **Display current environment variables:**  
  ```bash
  printenv
  ```

## 7. Network and Connectivity
- **Check connectivity to `example.com`:**  
  ```bash
  ping -c 4 example.com
  ```
- **Download a file from a URL:**  
  ```bash
  wget https://example.com/file.zip
  ```
  *(If `wget` is not installed, use `curl -O https://example.com/file.zip`.)*

## 8. Combining Commands
- **Create `logs` directory and move `system.log` into it:**  
  ```bash
  mkdir logs && mv system.log logs/
  ```
- **Create `temp.txt`, add "Hello World", and display its content:**  
  ```bash
  echo "Hello World" > temp.txt && cat temp.txt
  ```
- **Find all `.txt` files in `/home` and copy them to `/backup`:**  
  ```bash
  find /home -type f -name "*.txt" -exec cp {} /backup/ \;
  ```
- **Remove all empty directories in `/tmp` and print current directory before and after:**  
  ```bash
  pwd && find /tmp -type d -empty -delete && pwd
  ```

## 9. File Content and Backup
- **Combine `file1.txt` and `file2.txt` and display contents:**  
  ```bash
  cat file1.txt file2.txt
  ```
- **Create an exact copy of a disk to an external drive:**  
  ```bash
  dd if=/dev/sdX of=/dev/sdY bs=4M status=progress
  ```
  *(Replace `/dev/sdX` with the source disk and `/dev/sdY` with the destination drive.)*

## 10. Advanced Search
- **Find files larger than 1MB in the home directory:**  
  ```bash
  find ~/ -type f -size +1M
  ```
- **Search the manual for commands related to file copying:**  
  ```bash
  man -k copy
  ```

## 11. Handling Errors
- **Remove a non-empty directory (proper method):**  
  ```bash
  rm -r mydir
  ```

## 12. File Overwriting
- **Prevent overwriting when copying files:**  
  ```bash
  cp -i file.txt /destination/
  ```
  *(The `-i` flag prompts before overwriting.)*

## 13. Permission Issues
- **Fix permission errors using `sudo`:**  
  ```bash
  sudo mkdir /restricted_folder
  ```

## 14. Searching in Large Files
- **Limit search results to the first five matches:**  
  ```bash
  grep "search_term" largefile.txt | head -n 5
  ```
- **Find line numbers of matches:**  
  ```bash
  grep -n "search_term" largefile.txt
  ```

## 15. Network Disruption
- **Resume an interrupted download using `wget`:**  
  ```bash
  wget -c https://example.com/file.zip
  ```
  
