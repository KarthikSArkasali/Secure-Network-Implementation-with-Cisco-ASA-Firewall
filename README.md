# Secure-Network-Design-with-ASA-Firewall-DMZ
This repository showcases an Enterprise Network Security project built using Cisco ASA Firewall in Cisco Packet Tracer. The project includes essential firewall security configurations, OSPF routing, NAT, DHCP, SSH, and firewall policies to ensure network security, controlled access, and optimized routing across multiple network segments.

# Project Overview

This project focuses on securing an enterprise network using a Cisco ASA firewall while implementing OSPF, DHCP, NAT, ACLs, and SSH. The network is designed to enhance security, improve routing efficiency, and ensure controlled access across different zones such as Inside, Outside, and DMZ.

**The topology consists of:**

- Cisco ASA Firewall for network security & traffic filtering
- Multiple VLANs for traffic segmentation
- Dynamic Host Configuration Protocol (DHCP) for automatic IP address assignment
- Open Shortest Path First (OSPF) Routing for dynamic routing
- Secure Shell (SSH) Access for secure remote administration
- Access Control Lists (ACLs) for granular traffic control
- Network Address Translation (NAT) for public-private IP translation
- DMZ Configuration hosting Web, DNS, and DHCP Servers

# Network Topology

![ASA Firwall Project-3](https://github.com/user-attachments/assets/b0b15cbb-8426-484f-863d-3df200ab9499)


# Features and Configurations

**1. Basic ASA Configuration**

- Configured hostname, enable passwords, username & password
- Set clock & date for logging and security audits
- Assigned IP addresses, interface names, and security levels
- Saved and displayed configuration

      ! Set hostname
      hostname ASA-Firewall

      ! Configure enable password
      enable password YourPassword

      ! Set username & password
      username admin password YourSecurePassword privilege 15

      ! Configure clock & date
      clock set 14:30:00 Feb 17 2025

      ! Save configuration
      write memory

**2. DHCP Configuration**

- Configured DHCP pools for dynamic IP assignment
- Set DNS server for client resolution
- Enabled DHCP on the firewall interface

      ! Enable DHCP server
      dhcpd address 192.168.1.100-192.168.1.200 inside
      dhcpd dns 8.8.8.8
      dhcpd enable inside

**3. SSH Configuration**

- Enabled AAA authentication for SSH login
- Generated RSA key pairs for secure encryption
- Defined allowed subnets for SSH access

      ! Enable AAA authentication
      aaa authentication ssh console LOCAL

      ! Generate RSA key pair
      crypto key generate rsa modulus 2048

      ! Allow SSH from inside network
      ssh 192.168.1.0 255.255.255.0 inside

      ! Enable SSH on the firewall
      ssh version 2

**4. OSPF and Static Routing Configuration**

- Configured OSPF on Inside Router and ASA Firewall
- Configured Default Static Routing on the Outside Router and ASA Firewall


      ! Configure OSPF on ASA
      router ospf 1
      network 192.168.1.0 255.255.255.0 area 0
      network 192.168.2.0 255.255.255.0 area 0

      ! Default static route on ASA
      route outside 0.0.0.0 0.0.0.0 203.0.113.1

**5. Firewall Policies and Access Control Lists (ACLs)**

- Implemented NAT for translating internal private IPs
- Created firewall policies using ACLs to control traffic
- Configured Web, DNS, and DHCP servers in DMZ

      ! Configure NAT for inside and DMZ
      object network INSIDE-NET
      subnet 192.168.1.0 255.255.255.0
      nat (inside,outside) dynamic interface

      object network DMZ-NET
      subnet 192.168.2.0 255.255.255.0
      nat (dmz,outside) dynamic interface

      ! Define ACL for Inside network
      access-list INSIDE-TO-DMZ extended permit ip 192.168.1.0 255.255.255.0 any
      access-group INSIDE-TO-DMZ in interface inside

      ! Define ACL for Outside access to Web Server
      access-list OUTSIDE-TO-WEB extended permit tcp any host 203.0.113.100 eq 80
      access-group OUTSIDE-TO-WEB in interface outside

**6. Testing and Verification**

To ensure the configuration works properly, perform the following tests:
✅ Ping from Inside to ASA Firewall
✅ Access the Web Server from the Inside and Outside networks
✅ Check DHCP IP assignment on client devices
✅ SSH into ASA Firewall securely
✅ Verify OSPF routing table on ASA and routers

     ! Verify OSPF neighbors
     show ospf neighbor

     ! Verify NAT translations
     show xlate

     ! Check DHCP leases
     show dhcpd binding

     ! Verify SSH sessions
     show ssh sessions

# Key Takeaways

✅ Implemented real-world firewall security concepts using Cisco ASA<br>
✅ Configured network security policies with ACLs and NAT<br>
✅ Established secure remote management via SSH and AAA authentication<br>
✅ Optimized routing using OSPF and static routes<br>
✅ Segmented the network into Inside, Outside, and DMZ<br>

# Future Enhancements

🚀 Integrate VLANs for better segmentation<br>
🚀 Implement High Availability (HA) for redundancy<br>
🚀 Configure Site-to-Site VPN for remote office connectivity<br>
🚀 Enable Intrusion Prevention System (IPS) for threat detection<br>

# Conclusion

This project demonstrates the end-to-end configuration of an enterprise network with Cisco ASA Firewall. It enhances security, optimizes routing, and ensures controlled network access. The configurations implemented here mimic real-world enterprise network security best practices, making it a great showcase for cybersecurity and network engineering skills.
