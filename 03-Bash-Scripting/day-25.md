## Automation Tasks (continue)

#### 11. Manage and Sync Configurations Between Servers:
Write a Bash script that synchronizes application configuration files from the /etc/app/ 
directory on the local machine to the DWH server (dwh.company.com:/etc/app/). The 
script should run every 12 hours, ensuring that the configurations are always up to date.

#### 12. Schedule Regular File Cleanup:
Write a Bash script that deletes all temporary files in /tmp/data/ that are older than 7 days 
on the DWH server (dwh.company.com). Schedule the script to run daily at midnight.

#### 13. Automate Rolling Back Application Changes Based on Version Control:
Write a Bash script that checks the current version of an application in /opt/app/version.txt 
and if a new version is detected, automatically archives the previous version to 
/backup/app/old_versions/ and installs the new version. The script should log the details of 
each update to /var/log/app_update.log.

#### 14. Backup Multiple Application Versions:
Write a Bash script that backs up all application versions stored in /opt/app/versions/ on 
the local machine to the DWH server (dwh.company.com:/backup/app_versions/). The 
script should run every night at 2 AM, transferring only new or updated versions.

#### 15. Scheduled Data Warehouse Data Archival:
Write a Bash script that connects to the DWH server (dwh.company.com) every Friday at 6 
PM, extracts all data from a table named transactions in a PostgreSQL database, and 
stores it as a CSV file in /backup/dwh/transactions_YYYYMMDD.csv.

#### 16. Automate Remote Application Restart After Update:
Write a Bash script that connects to the DWH server (dwh.company.com) after transferring 
new files and restarts the myapp service. Ensure the script checks if the service is running 
and logs the status before and after the restart.

#### 17. Automate Multi-Server Backup and Transfer:
Write a Bash script that automates the backup of multiple application servers (app1, app2, 
app3) to a central DWH server (dwh.company.com). The script should archive the 
/var/data/ directories from each server and transfer them via SCP, then log the details of 
each transfer

#### 18. Database Incremental Backup Automation:
Write a Bash script that automates incremental backups for a MySQL database hosted on 
the DWH server (dwh.company.com). The script should keep a record of the last backup 
and only back up changes made since then. The incremental backups should be stored in 
/backup/db/incremental/ and should run every day at 4 AM.

#### 19. Automate Data Cleaning After Backup:
Write a Bash script that deletes data older than 30 days from the /var/data/ directory on the 
DWH server after a successful backup. The script should be scheduled to run weekly at 
midnight on Sundays.

#### 20. Monitor and Automate Application Version Deployment:
Write a Bash script that monitors a directory (/opt/app/deployments/) for new versions of 
an application. When a new version is detected, the script should back up the current 
version, deploy the new version, and log the deployment status