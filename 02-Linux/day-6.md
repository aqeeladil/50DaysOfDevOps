## Package Management

1. Basic Usage
o What command would you use to install the curl package using apt?
o How would you remove the vim package while preserving its configuration files 
using apt-get?

2. Upgrading Packages
o Describe the steps and commands required to upgrade all installed packages on a 
Debian-based system using apt.
o What is the difference between apt upgrade and apt full-upgrade? Provide a 
practical example of when you would use each.

3. Searching for Packages
o How can you search for packages related to git using apt? Provide the command.
o If you want to check if the package python3 is installed on your system, which 
command would you use with apt?

4. Managing Package Configuration
o Explain the difference between apt remove and apt purge. In what scenarios would 
you use each?
o After removing a package with apt, what command can you run to clean up any 
dependencies that are no longer needed?

5. Updating Repositories
o What command would you use to refresh the package index to reflect the latest 
available packages in the repositories?
o Explain why it is essential to run this command before installing or upgrading 
packages.

6. Detailed Package Information
o How would you display detailed information about the git package using apt?
o After installing a package, how can you verify its installation and see the installed 
version?

7. Combining Commands
o Write a single command using apt that updates the package index, upgrades all 
installed packages, and removes unused packages.
o Explain how to use apt to install a package and its recommended dependencies 
while ignoring any unnecessary ones.

8. Practical Scenario
o You have been tasked with installing the nginx web server. Provide the complete 
steps using apt from installation to starting the service.
o Suppose you encounter a broken package while using apt. What command would 
you run to fix it, and what does this command do?

9. Conflict Resolution
You are trying to install a package named libexample which has a dependency on 
libdependency version 2.0 or higher. However, you currently have libdependency version 
1.8 installed, which is blocking the installation.
o What steps would you take to resolve this dependency conflict using apt
o Describe how you would determine whether upgrading libdependency would affect 
other installed packages

10. Package Source Management
You need to add a new repository to your system to install a specific version of a software 
package that is not available in the default repositories.
o Explain how to add the repository and ensure the package manager trusts it.
o After adding the repository, how would you check if the desired package is now 
available? Provide the commands.

