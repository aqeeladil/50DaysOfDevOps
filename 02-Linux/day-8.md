## Linux Kernel

1. Kernel Parameters Adjustment
Explain how to view and modify kernel parameters in Linux. Use an example to demonstrate 
how to change the maximum number of open files allowed for a process. What command 
would you use, and what file would you modify?

2. Monitoring Kernel Logs
Describe the purpose of the /var/log/kern.log file. How can you use the dmesg command to 
view kernel messages, and how can you filter these messages to find specific errors related 
to a particular device?

3. Resource Monitoring with top and htop
Compare the top and htop commands in terms of user interface and features. How can you 
use these tools to identify processes consuming excessive CPU or memory resources? 
Provide step-by-step instructions.

4. Analyzing System Performance
What tools would you use to analyze system performance in Linux? Discuss how to utilize 
vmstat, iostat, and mpstat to monitor system metrics. Provide examples of what each tool 
can reveal about the system’s performance.

5. Kernel Tuning for Performance
Discuss the impact of the swappiness parameter on system performance. How can you 
check the current value of this parameter, and what command would you use to adjust it 
for optimizing system performance?

6. Using sysctl for Runtime Configuration
Explain how to use the sysctl command to view and modify kernel parameters at runtime. 
Provide an example of how to disable IP forwarding and explain why you might want to do 
this.

7. Kernel Oops and Panic Analysis
Define what a kernel oops and kernel panic are. How would you approach diagnosing a 
kernel panic? What logs or files would you examine, and what tools could assist in this 
analysis?

8. Kernel Module Management
Describe the process of loading and unloading kernel modules. Provide commands to list 
currently loaded modules and explain how you would identify and remove an unnecessary 
module from the kernel.

9. Using perf for Performance Analysis
How can the perf tool be utilized to analyze performance bottlenecks in a Linux system? 
Provide a practical example of how to record and report CPU usage by processes.

10. Kernel Upgrades and Patching
Discuss the considerations and steps involved in upgrading the Linux kernel on a 
production server. What tools or commands would you use to ensure that the system 
remains stable after a kernel upgrade