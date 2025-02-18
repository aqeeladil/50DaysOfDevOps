## Automation Tasks

#### 1. Scheduled File Transfer to DWH Server:
Write a Bash script that copies a file named data.csv from the /data/ directory of a local 
machine to a remote Data Warehouse (DWH) server (dwh.company.com) every day at 
midnight using SCP. The script should log the status of the transfer to 
/var/log/file_transfer.log.

#### 2. Automating Backup of Files on DWH Server:
Write a Bash script that creates a backup of the /var/data/ directory on the DWH server 
(dwh.company.com) every Sunday at 2 AM. The backup should be compressed into a 
.tar.gz archive and stored in the /backup/ directory on the server with the format 
backup_YYYYMMDD.tar.gz.

#### 3. Daily File Synchronization with DWH Server:
Write a Bash script that synchronizes all files from the /data/ directory on the local machine 
to the DWH server (dwh.company.com:/data/) every 6 hours using rsync. Ensure that only 
new or modified files are transferred. Log the summary of synchronization to 
/var/log/rsync_sync.log.

#### 4. Managing Application Version Backups:
Write a Bash script that automatically creates a backup of an application's directory 
(/opt/app/) every time a new version is deployed. The backup should be stored in the 
/backup/app/ directory with the version number in the filename (e.g., 
app_backup_v2.3.4.tar.gz). Also, ensure that only the last 5 backups are kept, and older 
backups are deleted.

#### 5. Automating Database Backup from DWH:
Write a Bash script that connects to the DWH server (dwh.company.com), creates a 
backup of a MySQL database named analytics_db, and saves the SQL dump in the 
/backup/db/ directory on the DWH server. The backup should run every day at 3 AM, and 
the script should rotate backups, keeping only the last 7 days of backups.

#### 6. Automate Application Log Archiving:
Write a Bash script that compresses all log files in /var/log/app/ that are older than 7 days 
into a .zip file and moves them to /archive/logs/ on the DWH server (dwh.company.com). 
This script should run every day at 1 AM.

#### 7. Automated Version Rollback for Applications:
Write a Bash script that allows an admin to roll back an application to a previous version by 
copying the backup files from /backup/app/ back to /opt/app/. The script should prompt 
the user to select the version to roll back to from a list of available backups and restore it.

#### 8. Automating File Transfer with Timestamped Naming:
Write a Bash script that automatically copies a file named report.csv from the /reports/ 
directory to the DWH server (dwh.company.com:/data/) every Monday at 8 AM. The copied 
file on the server should be renamed with the current date (e.g., report_YYYYMMDD.csv).

#### 9. Periodic Application Log Cleanup on DWH Server:
Write a Bash script that connects to the DWH server (dwh.company.com) and deletes all 
application log files (*.log) in the /var/log/app/ directory that are older than 30 days. The 
script should be scheduled to run weekly at midnight on Saturdays.

#### 10. Automating Incremental Backups for Application Data:
Write a Bash script that performs incremental backups of the /var/data/ directory on the 
DWH server. The script should compare the last backup and only back up the new or 
changed files to /backup/incremental/, keeping track of changes using a snapshot file. This 
should run daily at 4 AM
