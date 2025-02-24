# Network Fundamentals

## Networking Devices

### Router vs Switch

- **Router**: 
  - Functions at OSI Layer 3 (Network Layer)
  - Connects different networks together (like your home network to the internet)
  - Uses IP addresses to make forwarding decisions
  - Contains routing tables to determine the best path for data
  - Provides network address translation (NAT) to allow multiple devices to share a single public IP
  - Typically includes firewall capabilities
  - Can prioritize traffic with QoS (Quality of Service)

  **Scenario Example**:  
  A mid-sized company has separate departments (Finance, HR, and Engineering) that each need their own network segment for security reasons. The IT team implements three separate VLANs (Virtual Local Area Networks) on their switches. They then configure a router to connect these VLANs together, applying specific access control lists (ACLs) that allow HR to access Finance data but prevent Engineering from accessing either HR or Finance resources. The router also connects all departments to the internet while performing NAT to use a single public IP address.

- **Switch**:
  - Functions at OSI Layer 2 (Data Link Layer)
  - Connects devices within the same network
  - Uses MAC addresses to forward frames to specific ports
  - Maintains a MAC address table mapping physical addresses to ports
  - Creates a dedicated connection between communicating devices
  - More efficient than hubs as they send traffic only to intended recipients
  - Comes in managed and unmanaged varieties

  **Scenario Example**:  
  A university computer lab has 30 workstations that need to connect to the campus network. The IT department installs a 48-port managed switch. When a student on workstation #12 accesses a file from a server, the switch learns that workstation #12's MAC address is connected to port 12. It creates a direct path between port 12 and the uplink port connecting to the server, allowing this communication without affecting other workstations. Later, the IT staff uses the switch's management interface to monitor which ports are active and set up port security to prevent unauthorized devices from connecting.

### Access Point

- A hardware device that allows wireless devices to connect to a wired network
- Broadcasts SSIDs (network names) for wireless networks
- Handles authentication and encryption (WPA2/WPA3)
- Can support multiple wireless standards (802.11a/b/g/n/ac/ax)
- May include features like band steering, beamforming, and MU-MIMO
- Enterprise deployments often use multiple access points with controller management
- Modern mesh systems use multiple access points to extend coverage

  **Scenario Example**:  
  A three-story office building needs consistent wireless coverage throughout. The network team installs eight enterprise access points strategically placed on each floor, all connected to a wireless controller. They configure two SSIDs: "Staff" (using WPA2-Enterprise with 802.1X authentication against Active Directory) and "Guest" (with a simpler password that changes weekly). The controller automatically adjusts power levels on each access point to minimize interference and performs band steering to move newer devices to the less congested 5GHz band. When employees move between floors on a video call, the controller facilitates seamless roaming between access points without dropping the connection.

### Network Hub

- A basic, largely obsolete networking device
- Acts as a multi-port repeater at OSI Layer 1 (Physical Layer)
- When it receives data on one port, it duplicates and sends it to all other ports
- Creates a single collision domain, meaning only one device can transmit at a time
- Inefficient as all connected devices see all traffic
- No intelligence or filtering capabilities
- Replaced by switches in most modern networks

  **Scenario Example**:  
  In a small business running legacy equipment, they're still using an old 8-port hub to connect several point-of-sale terminals. When the morning shift begins and multiple cashiers log in simultaneously, network performance slows dramatically. A network analyzer shows frequent collisions as multiple terminals try to communicate at once. Additionally, when the manager runs a sales report that pulls data from all terminals, all other network operations slow to a crawl as every packet is broadcast to all ports. After upgrading to a modern switch, collisions disappear, and network performance improves significantly as each device gets a dedicated connection.

## Virtualization

### Hypervisor

- Software platform that allows multiple virtual machines to run on a host computer
- **Type 1 (Bare Metal)**: Runs directly on hardware (ESXi, Hyper-V, Xen)
- **Type 2 (Hosted)**: Runs on top of an operating system (VMware Workstation, VirtualBox)
- Manages resource allocation including CPU, memory, storage, and networking
- Provides isolation between virtual machines
- Enables features like snapshots, live migration, and high availability
- Allows for consolidation of multiple workloads onto fewer physical servers

  **Scenario Example**:  
  A company's datacenter has 20 aging physical servers running at only 15-20% utilization. The IT director implements a virtualization solution with three powerful hypervisor hosts. They virtualize all 20 workloads and run them on the three physical servers, increasing average utilization to 70%. When one physical server shows signs of hardware failure, they use live migration to move its VMs to the other two hosts with zero downtime. The company saves on power, cooling, and physical space while gaining advantages like easier backups (through VM snapshots) and faster provisioning of new servers when needed.

### Virtual Machine

- A software emulation of a physical computer
- Contains its own virtual CPU, memory, storage, and network interfaces
- Runs its own guest operating system independent of the host
- Isolated from other VMs running on the same host
- Can be migrated between physical hosts
- Enables testing, development, and running multiple OS environments
- File-based, making backup and recovery simpler

  **Scenario Example**:  
  A software development team needs to test their application across Windows 10, Windows Server 2019, and three different Linux distributions. Rather than purchasing separate physical machines, they create five virtual machines on a single powerful development server. When a developer discovers a critical bug in the Linux version, they take a snapshot of the VM before attempting the fix. The fix causes unexpected problems, so they roll back to the snapshot in seconds. Later, when they need to scale testing, they simply clone the original VMs to create multiple identical test environments. When hardware resources become constrained, the IT team moves several VMs to another physical server without reinstalling any operating systems.

### Containers

- Lightweight, standalone executable packages of software
- Include code, runtime, system tools, libraries, and settings
- Share the host OS kernel rather than running a complete OS
- Significantly more resource-efficient than virtual machines
- Start and stop in seconds due to minimal overhead
- Perfect for microservices architecture
- Docker and Kubernetes are popular container technologies
- More portable and consistent across environments

  **Scenario Example**:  
  A web application company is refactoring their monolithic application into microservices. They package each component (user authentication, payment processing, inventory management, etc.) as separate containers. During testing, the QA engineer can spin up the entire application stack on their laptop in under a minute. When a developer updates the payment service, only that container needs to be rebuilt and deployed—taking seconds instead of redeploying the entire application. In production, Kubernetes automatically scales the user authentication containers during peak hours and scales them back down during low traffic periods. When a container crashes, Kubernetes automatically replaces it within seconds, maintaining high availability.

### Xen Hypervisor

- Open-source Type 1 hypervisor
- Uses a microkernel design
- Supports both paravirtualization and hardware-assisted virtualization
- Used as the foundation for many cloud platforms (originally Amazon EC2)
- Allows for oversubscription of physical resources
- Has a small trusted computing base for improved security
- Managed through specialized management tools like Xen Orchestra

  **Scenario Example**:  
  A university research department needs to maximize utilization of limited hardware while isolating different research projects. They choose Xen due to its open-source nature and security features. They use Xen's unique dom0/domU architecture to create privileged and unprivileged domains. The researchers use paravirtualization for high-performance Linux workloads and hardware-assisted virtualization for Windows analysis tools. When a particularly intensive simulation needs to run, they temporarily allocate more resources to that VM using Xen's dynamic memory management. The security team appreciates Xen's small attack surface, which is critical for the sensitive research data being processed.

### Proxmox VE Hypervisor

- Open-source virtualization platform combining KVM and LXC
- Complete management solution with web interface
- Supports both VMs (through KVM) and containers (through LXC)
- Includes features like live migration, high availability, and backup tools
- Offers software-defined storage and networking
- Cluster-capable for managing multiple nodes
- Popular in smaller enterprises and home labs due to its free tier

  **Scenario Example**:  
  A small business with limited IT budget needs a robust virtualization solution. They implement Proxmox VE on three repurposed servers. Using the web interface, they create several KVM virtual machines for their Windows-based applications (accounting, CRM) and LXC containers for their web services and databases. They configure Proxmox's built-in backup solution to automatically snapshot all VMs nightly and store them on network storage. When they add a fourth server, they easily expand their cluster, and when one server fails unexpectedly, the high availability feature automatically restarts the affected VMs on the remaining nodes with minimal downtime. All of this is accomplished without paying any licensing costs, aligning with their budget constraints.

### VMware ESXi

- VMware's enterprise-grade Type 1 hypervisor
- Minimal footprint with purpose-built service console
- Highly optimized for running virtual machines
- Advanced resource management and scheduling
- Extensive hardware compatibility list
- Supports features like vMotion, DRS, and fault tolerance
- Foundation of VMware's virtualization platform

  **Scenario Example**:  
  A financial services company requires maximum uptime for their trading applications. They implement ESXi on four enterprise-grade servers with redundant components. The IT team installs the hypervisor directly on the bare metal, appreciating its small 150MB footprint which minimizes potential vulnerabilities. They configure each ESXi host with redundant network connections and multipath storage access. When quarterly system updates need to be applied, they use vMotion to migrate VMs off one host at a time, patch it, and then move to the next—achieving updates with zero downtime. Their most critical application uses ESXi's fault tolerance feature, which runs synchronized instances on two different hosts, providing instant failover if hardware problems occur.

### VMware ESXi vs VMware vSphere

- **ESXi**: The actual hypervisor component that runs on physical servers
- **vSphere**: The complete suite including ESXi plus:
  - vCenter Server: Centralized management platform
  - vSphere Client: Management interface
  - Advanced features: DRS, HA, vMotion, Storage vMotion
  - Monitoring, reporting, and automation tools
  - APIs for integration with other systems
  - Licensing that determines available features
  - Backup and disaster recovery capabilities

  **Scenario Example**:  
  A healthcare organization starts with three ESXi hosts for virtualizing their electronic health records system. Initially, they manage each host independently through the direct ESXi interface. As they grow to 15 hosts across two data centers, this approach becomes unmanageable. They upgrade to the full vSphere suite, implementing vCenter Server for centralized management. Now, their administrators use a single vSphere Client interface to manage all hosts. They implement clusters with Distributed Resource Scheduler (DRS) to automatically balance VM workloads based on resource usage. vSphere High Availability is configured to rapidly restart VMs if a host fails. For regulatory compliance, they use vSphere APIs for Data Protection to integrate with their enterprise backup solution, and they leverage detailed reporting tools to document system reliability for auditors.

## Networking Concepts

### Network vs Broadcast Address

- **Network Address**:
  - First address in a subnet (all host bits set to 0)
  - Identifies the network itself, not any specific device
  - Example: In 192.168.1.0/24, the network address is 192.168.1.0
  - Cannot be assigned to any device
  - Used in routing tables to identify destination networks
  
- **Broadcast Address**:
  - Last address in a subnet (all host bits set to 1)
  - Used to send data to all devices on the subnet simultaneously
  - Example: In 192.168.1.0/24, the broadcast address is 192.168.1.255
  - Cannot be assigned to any device
  - Used for discovery protocols and services like DHCP

  **Scenario Example**:  
  A network administrator is planning IP address allocation for a new office with separate subnets for different departments. For the Marketing department, they choose the subnet 10.1.20.0/24. They note that 10.1.20.0 is the network address representing the entire subnet and cannot be assigned to any device. Similarly, 10.1.20.255 is the broadcast address used when a device needs to communicate with all devices in that subnet. When configuring the DHCP server, they set it to assign addresses from 10.1.20.10 to 10.1.20.250, keeping some addresses reserved for static assignments while avoiding both the network and broadcast addresses. Later, when troubleshooting network issues, they capture traffic and notice DHCP discovery requests being sent to the 10.1.20.255 broadcast address as expected.

## Storage & Hardware

### RAID (Redundant Array of Independent Disks)

- Technology that uses multiple drives to provide increased performance, redundancy, or both
- Common RAID levels:
  - **RAID 0**: Striping - Data split across drives for performance, no redundancy
  - **RAID 1**: Mirroring - Identical data on two drives for redundancy
  - **RAID 5**: Striping with parity - Distributed parity for redundancy (n-1 capacity)
  - **RAID 6**: Striping with double parity - Survives two drive failures
  - **RAID 10**: Mirror of stripes - Combining RAID 1 and RAID 0
- Can be implemented in hardware (dedicated controller) or software
- Provides varying levels of read/write performance and fault tolerance
- Not a substitute for proper backup strategies

  **Scenario Example**:  
  A video production company needs storage solutions for different workflows:
  
  1. For video editing workstations, they implement RAID 0 using two NVMe drives. When editors work with 4K raw footage, the striped array delivers nearly double the read/write speeds of a single drive, allowing for smooth timeline scrubbing and export performance. However, IT makes sure editors understand this configuration offers no redundancy, requiring diligent backups.
  
  2. For their media asset management server, they implement RAID 6 across eight large HDDs. When ingesting a batch of new projects, one drive fails completely. Thanks to RAID 6, operations continue uninterrupted. Before they can replace the failed drive, a second drive begins showing errors. Again, RAID 6's double parity saves them from data loss while both drives are replaced and rebuilding occurs.
  
  3. For their render farm's scratch disk array, they choose RAID 10 (mirrored stripes) to balance performance and redundancy. When rendering complex animations, they benefit from improved read performance of striping while maintaining redundancy through mirroring.

## System Resources

### CPU vs RAM

- **CPU (Central Processing Unit)**:
  - The "brain" of the computer that executes instructions
  - Measured by clock speed (GHz), cores, threads, and architecture
  - Handles calculations, logic operations, and program execution
  - Modern CPUs include cache memory for faster data access
  - Performance affected by instruction set, pipeline depth, and branch prediction
  - Key metrics: utilization percentage, context switches, interrupts

- **RAM (Random Access Memory)**:
  - Temporary, volatile storage for active data and programs
  - Much faster than storage drives (HDDs/SSDs)
  - Measured in gigabytes (GB) and speed (MHz/frequency)
  - Types include DDR4, DDR5 with varying speeds and latencies
  - Virtual memory extends RAM using disk space (swap/page file)
  - Key metrics: usage percentage, page faults, memory pressure

  **Scenario Example**:  
  A data science team is experiencing performance issues with their analysis workflows:
  
  **Case 1 - CPU Bottleneck**: A researcher runs a statistical model that processes millions of calculations sequentially. The system monitor shows 100% CPU utilization on a single core, while RAM usage remains at 30% of available capacity. The program takes 4 hours to complete. After upgrading from a 4-core 3.6GHz CPU to an 8-core 4.2GHz model with better single-thread performance, the same workload completes in just 1.5 hours. Here, the CPU was clearly the bottleneck.
  
  **Case 2 - RAM Bottleneck**: Another team member attempts to analyze a large dataset using a machine with 16GB RAM. The system monitor shows CPU utilization fluctuating between 20-40%, but RAM is constantly at 95-100%. The system is sluggish, and the hard drive shows constant activity as the operating system swaps data between RAM and disk. After upgrading to 64GB RAM, CPU utilization becomes more consistent at 60-70%, the disk activity drops significantly, and the analysis completes 5x faster. In this case, insufficient RAM was forcing excessive use of slower virtual memory (swap space).

### IO Wait

- Time during which CPU cores are idle, waiting for disk or network I/O operations to complete
- High IO Wait indicates a bottleneck in the storage subsystem
- Measured as a percentage of CPU time
- Common causes:
  - Slow disk performance (especially with traditional HDDs)
  - Excessive swapping due to memory pressure
  - Network storage latency
  - Poorly optimized database queries
- Can be resolved by:
  - Upgrading to faster storage (SSDs, NVMe)
  - Adding more RAM to reduce swapping
  - Optimizing applications for better I/O patterns
  - Using caching mechanisms

  **Scenario Example**:  
  A busy e-commerce database server begins experiencing performance issues during peak shopping hours. Monitoring shows the CPUs are only at 30% utilization, but IO Wait time is consistently above 40%. Investigation reveals several issues:
  
  1. The database is running on traditional HDDs with high seek times
  2. The server's RAM is just enough to run the OS and database service, but not enough for optimal caching
  3. Database queries are reading from tables without proper indexing
  
  The team implements a three-part solution:
  
  1. They migrate the database to NVMe SSDs, which provide over 20x the IOPS of the old HDDs
  2. They increase server RAM from 32GB to 128GB, allowing the database to cache more frequently accessed data
  3. A database administrator optimizes the schema with proper indexes for common queries
  
  After these changes, the IO Wait drops to below 5%, CPU utilization increases to 50-60% (more efficiently using available resources), and database response times improve by 85%. The system now handles peak loads without the lag that was previously causing customers to abandon purchases.

## Remote Management

### Dell iDRAC (Integrated Dell Remote Access Controller)

- Out-of-band management solution for Dell servers
- Dedicated management processor with its own network connection
- Allows remote server management regardless of OS state
- Features include:
  - Remote power control (on/off/restart)
  - Virtual console for remote KVM access
  - Virtual media for remote ISO mounting
  - Hardware monitoring and alerting
  - BIOS configuration
  - Firmware updates
  - Power and thermal monitoring
- Available in Express and Enterprise tiers with varying capabilities

  **Scenario Example**:  
  A regional bank has branch offices across multiple states with a Dell server at each location but no on-site IT staff. At 2 AM, the monitoring system alerts that the server at a remote branch has become unresponsive. Instead of driving 3 hours to the site, the IT technician connects to the server's iDRAC interface using its dedicated network port, which operates independently of the main server's OS. Through the iDRAC virtual console, they see that the server is stuck in a boot loop due to a failed Windows update. They use the virtual media feature to mount a recovery ISO stored at headquarters and repair the startup issues. They also notice through iDRAC's hardware monitoring that one of the power supplies is reporting warnings. They schedule a replacement to be shipped to the branch while the server continues to operate on the remaining good power supply. All of this is accomplished remotely without any on-site visit or disruption to the start of business in the morning.

### HP iLO (Integrated Lights-Out)

- HP's equivalent to Dell's iDRAC
- Embedded server management technology
- Enables complete out-of-band server management
- Capabilities include:
  - Remote console access (HTML5-based)
  - Server health monitoring
  - Power management and optimization
  - Remote power cycling
  - Virtual media support
  - Agentless management
  - Automated server recovery
- Varying feature sets across different versions (iLO 5, iLO 6)

  **Scenario Example**:  
  A healthcare IT team manages servers across multiple facilities, including several HP ProLiant servers running critical clinical applications. During a weekend maintenance window, a system administrator needs to update the BIOS and firmware on a server at a satellite clinic. Using HP iLO, they connect to the server remotely and use the virtual media feature to mount the update package. During the update, they monitor the process through the HTML5 remote console, responding to prompts as needed. The update requires a reboot, which they initiate through iLO. 
  
  During reboot, the server encounters an issue and fails to start properly. Through the iLO console, they can see the exact error messages at the BIOS level, which wouldn't be possible through regular remote desktop tools. They use iLO's power management to perform a cold restart and enter the BIOS setup to adjust settings that resolve the startup issue. Throughout this process, the iLO connection remains stable even when the server's operating system is completely offline. On Monday morning, iLO's automated health reporting confirms that all server components are functioning normally, providing peace of mind before the clinic opens.

## Directory Services

### Active Directory (MCSA)

- Microsoft's directory service for Windows domain networks
- Hierarchical database that stores information about network objects
- Key components:
  - **Domain Controllers**: Servers that authenticate users
  - **Forest/Domain**: Logical grouping of resources
  - **Organizational Units (OUs)**: Containers for organizing objects
  - **Group Policy**: Centralized configuration management
  - **LDAP**: Protocol used for directory access
- Provides single sign-on capability across the network
- Manages identity and access permissions
- MCSA (Microsoft Certified Solutions Associate) is a certification path for AD specialists
- Integrates with other Microsoft services (Exchange, SharePoint)

  **Scenario Example**:  
  A multi-national manufacturing company with 5,000 employees redesigns their Active Directory infrastructure to improve security and manageability. They create a forest with a root domain and separate child domains for each global region (Americas, EMEA, APAC). Within each domain, they structure Organizational Units (OUs) to match their business hierarchy: departments, locations, and job functions.
  
  For a new employee joining the finance department in Chicago, the onboarding process is streamlined through AD:
  
  1. The HR system automatically creates the user account in Active Directory, placing it in the Finance OU within the Americas domain.
  
  2. Group Policy Objects (GPOs) linked to the Finance OU automatically:
     - Apply strict password policies specific to finance staff
     - Map network drives to finance file shares
     - Configure finance-specific software settings
     - Restrict USB device usage per company policy
     
  3. The employee is automatically added to security groups for building access systems, finance applications, and department resources based on their job code.
  
  4. When logging into any company workstation, the employee enters credentials once, and Active Directory provides single sign-on to email, the corporate intranet, the ERP system, and other integrated applications.
  
  5. When the employee transfers to another department, moving their account to a different OU automatically adjusts their permissions and system configurations through inherited Group Policy settings.
  
  The company's MCSA-certified administrators use advanced tools to maintain this environment, ensuring replication between domain controllers worldwide and monitoring for security events across the infrastructure.

### DNS Manager

- Administrative tool for managing Domain Name System servers
- Critical for name resolution (converting names to IP addresses)
- Features include:
  - Creating and managing DNS zones (forward and reverse lookup)
  - Configuring DNS records (A, AAAA, MX, CNAME, PTR, etc.)
  - Setting up conditional forwarders
  - Configuring zone transfers between DNS servers
  - Implementing DNSSEC for enhanced security
  - Managing DNS cache and time-to-live (TTL) settings
- Essential service for Active Directory functionality
- Crucial for both internal network naming and internet connectivity

  **Scenario Example**:  
  A company is migrating their email service from an on-premises Exchange server to Microsoft 365. The network administrator uses DNS Manager to orchestrate this transition with minimal disruption:
  
  1. First, they review their existing DNS configuration, noting the current MX records point to their on-premises mail server (mail.company.com) with a priority of 10 and a TTL of 1 hour.
  
  2. Three days before migration, they reduce the TTL on these MX records to 5 minutes, ensuring that when changes are made, they'll propagate quickly.
  
  3. During the migration window, they add new MX records pointing to Microsoft 365's mail servers (company-com.mail.protection.outlook.com) with a priority of 0 (higher preference than the existing records).
  
  4. They add the required TXT records for SPF, DKIM, and DMARC to authenticate email from the new service and prevent spoofing.
  
  5. They create a new CNAME record redirecting autodiscover.company.com to Microsoft's autodiscover endpoint, allowing Outlook clients to automatically reconfigure.
  
  6. Using DNS Manager's diagnostic tools, they verify that name resolution is working correctly from various network locations.
  
  7. Once the migration completes, they monitor email flow and then remove the old MX records pointing to the decommissioned Exchange server.
  
  Throughout this process, DNS Manager provides detailed logging and validation, helping to ensure that mail delivery continues uninterrupted during the transition. The conditional forwarding settings they had previously configured ensured that the company's branch offices, which use local DNS servers, properly resolved all the new records during the migration.