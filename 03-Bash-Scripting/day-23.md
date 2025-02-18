## Log Analysis (continue)

15. Find Longest Response Time: Write a Bash script that parses an access.log file and finds 
the log entry with the longest response time (assuming the response time is included in the 
log).

16. Generate Log Summary Report: Write a Bash script that generates a summary report from 
access.log showing the total number of requests, the number of unique IPs, and the 
number of 404 errors.

17. Filter Logs by Date Range: Write a Bash script that extracts all log entries from system.log 
between two specific dates provided by the user.

18. Find Unusual Activity: Write a Bash script that analyzes a log file (access.log) and 
identifies IP addresses that made more than 100 requests in a minute.

19. Real-Time Log Monitoring with Alerts: Write a Bash script that monitors app.log in realtime, and if more than 5 ERROR entries appear within a minute, sends an alert message 
(simulated with echo).

20. Analyze Disk Space Warnings: Write a Bash script that checks the system log (syslog) for 
any disk space warnings (Disk is full) and prints out the timestamp and disk name where 
the issue occurred.

21. Sort Log by Timestamp: Write a Bash script that sorts a log file (app.log) by the timestamp 
of each entry and saves the sorted output to a new file (sorted_app.log).

22. Summarize Log Activity by Hour: Write a Bash script that summarizes the number of log 
entries per hour from access.log and prints the count for each hour.

23. Extract Failed SSH Login Attempts: Write a Bash script that searches auth.log for failed 
SSH login attempts and lists the IP addresses responsible for the failures

24. Analyze User Activity: Write a Bash script that extracts the number of login attempts and 
successful logins for each user from auth.log.

25. Filter Logs Based on Keywords: Write a Bash script that allows the user to specify multiple 
keywords (e.g., ERROR, WARNING) and filters the log file based on those keywords, 
displaying matching lines