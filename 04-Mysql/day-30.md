## User Management

1. Creating a User: Write the SQL command to create a new MySQL user named admin_user 
with a password secure_password123. What privileges does this user have by default?

2. Granting Global Privileges: Describe how you would grant all privileges to the admin_user 
on all databases. What SQL command would you use

3. Viewing User Privileges: How can you check the privileges granted to the admin_user? 
Write the SQL command to display this information.

4. Deleting a User: What command would you use to delete the user admin_user from 
MySQL? What considerations should you take into account before deleting a user?

5. Creating a Limited User: Write the SQL command to create a user named limited_user 
with a password limited_pass. This user should only can connect to the database and 
select data from the employees table in the company_db database.

6. Granting Specific Privileges: What SQL command would you use to grant the limited_user 
the ability to insert, update, and delete records from the employees table? How would you 
ensure they cannot drop the table?

7. Setting Resource Limits: Explain how to set resource limits for the limited_user, such as 
limiting the maximum connections or query execution time. Provide an example SQL 
command.

8. Revoking Privileges: Describe the process to revoke the UPDATE privilege from 
limited_user on the employee’s table. What SQL command would you use

9. Locking a User Account: What command would you use to lock the account of 
limited_user? Explain why you might want to lock a user account.

10. Unlocking a User Account: Describe the command used to unlock a locked user account 
in MySQL. What are the steps involved?

11. Viewing Locked Users: How can you check if a user account is locked? Write the SQL 
command to find locked user accounts in MySQL.

12. Reasons for Locking Users: In what scenarios would you want to lock a user account? 
Provide at least three different situations where this might be necessary