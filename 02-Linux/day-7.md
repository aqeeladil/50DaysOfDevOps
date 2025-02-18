## Package Management (continue)

11. Automating Package Management
Write a shell script that automates the following tasks:
o Update the package index.
o Upgrade all installed packages.
o Install a list of specified packages if they are not already installed.
o Clean up unused packages and cache.
o Log the output of each command to a log file.
Discuss potential issues that could arise during execution and how your script 
handles them

12. Version Pinning
You need to ensure that a specific version of a package (myapp) is always installed on your 
system, even if newer versions are available.
o Describe how you would pin the version of myapp using apt.
o What command would you run to verify that the pinning is working as expected?

13. Troubleshooting Installation Issues
During an installation attempt, you receive an error stating that a package is in a "halfinstalled" state.
o Explain what this means and the potential causes.
o Provide the commands you would use to diagnose and resolve this issue.

14. Working with Configuration Files
You need to remove the package nginx but want to keep its configuration files so you can 
restore them later.
o Which command would you use to achieve this?
o After some time, you decide to reinstall nginx. Describe how you would do this 
while ensuring that the original configuration files are not overwritten

15. Dependency Chains
You have a complex set of packages where Package A depends on Package B, which in turn 
depends on Package C. However, you want to remove Package A without affecting 
Packages B and C.
o Discuss how you would approach this task using apt or apt-get.
o What command would you use to see the dependencies of Package A before 
removing it?

16. Simulating Installations
You are tasked with testing the installation of a package without actually making any 
changes to the system.
o What command would you use to simulate the installation of the package htop
o How would you interpret the output of this command to understand what would 
happen during the actual installation?

17. Using Configuration Management
Imagine you are using a configuration management tool (like Ansible) to manage packages 
across multiple servers.
o Describe how you would use apt in a playbook to ensure that a specific set of 
packages is installed and updated.
o Discuss the challenges you might face with package versions and dependencies 
across different server environments and how you would address them.

18. Advanced Search and Filter
You want to identify all installed packages related to python and determine their version 
numbers.
o What command would you use with apt to achieve this?
o Discuss how you would filter out only those packages that are not installed or are 
obsolete, providing the necessary commands

