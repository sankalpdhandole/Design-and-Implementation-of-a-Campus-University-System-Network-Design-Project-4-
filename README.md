# Design-and-Implementation-of-a-Campus-University-System-Network-Design-Project-4-
### Project #4: Design and Implementation of a Campus/University System Network

#### Case Study and Requirements

1. **Network Design**:
   - Albion University with two campuses 20 miles apart.
   - Main Campus:
     - Building A: Administrative staff (management, HR, finance), Faculty of Business.
     - Building B: Faculty of Engineering/Computing, Faculty of Art/Design.
     - Building C: Students' labs, IT department (hosts University Web server).
   - Smaller Campus: Faculty of Health and Sciences (staff and student labs).

2. **Technologies Implemented**:

   - **Creating a Network Topology using Cisco Packet Tracer**.
   - **Hierarchical Network Design**.
   - **Connecting Networking Devices with Correct Cabling**.
   - **Creating VLANs and Assigning Ports VLAN Numbers**.
   - **Subnetting and IP Addressing**.
   - **Configuring Inter-VLAN Routing (Router on a Stick)**.
   - **Configuring DHCP Server (Router as the DHCP Server)**.
   - **Configuring SSH for Secure Remote Access**.
   - **Configuring RIPv2 as the Routing Protocol**.
   - **Configuring Switchport Security or Port-Security on the Switches**.
   - **Host Device Configurations**.
   - **Testing and Verifying Network Communication**.

#### Detailed Pointwise Implementation

1. **Network Topology Setup**:
   - Design a topology in Cisco Packet Tracer with routers, switches, and PCs representing each campus and building as described.

2. **Hierarchical Network Design**:
   - Divide the network into core, distribution, and access layers:
     - Core layer: Router connecting campuses.
     - Distribution layer: Switches connecting buildings within each campus.
     - Access layer: Switches connecting PCs and labs within each building.

3. **Connecting Networking Devices with Correct Cabling**:
   - Use appropriate cables (fiber optic for inter-campus connections, Ethernet for intra-campus connections).

4. **Creating VLANs and Assigning Ports VLAN Numbers**:
   - Configure VLANs for each department/faculty and purpose:
     - Admin VLAN, Business VLAN, Engineering/Computing VLAN, Art/Design VLAN, Health/Sciences VLAN, Student VLAN, IT VLAN.

5. **Subnetting and IP Addressing**:
   - Subnet each VLAN appropriately based on the given IP address range.
   - Assign IP addresses to devices ensuring uniqueness and proper subnet boundaries.

6. **Configuring Inter-VLAN Routing (Router on a Stick)**:
   - Configure the router with sub-interfaces for each VLAN:
     ```bash
     Router> enable
     Router# configure terminal
     Router(config)# interface gigabitEthernet 0/0.10
     Router(config-subif)# encapsulation dot1Q 10
     Router(config-subif)# ip address 192.168.10.1 255.255.255.0
     Router(config)# interface gigabitEthernet 0/0.20
     Router(config-subif)# encapsulation dot1Q 20
     Router(config-subif)# ip address 192.168.20.1 255.255.255.0
     ```
     - Repeat for each VLAN/subnet.

7. **Configuring DHCP Server (Router as the DHCP Server)**:
   - Configure DHCP pools on the router for each VLAN:
     ```bash
     Router(config)# ip dhcp pool VLAN10
     Router(dhcp-config)# network 192.168.10.0 255.255.255.0
     Router(dhcp-config)# default-router 192.168.10.1
     ```
     - Repeat for each VLAN.

8. **Configuring SSH for Secure Remote Access**:
   - Generate SSH keys on the router:
     ```bash
     Router(config)# crypto key generate rsa
     ```
   - Configure SSH access:
     ```bash
     Router(config)# line vty 0 4
     Router(config-line)# transport input ssh
     Router(config-line)# login local
     ```

9. **Configuring RIPv2 as the Routing Protocol**:
   - Enable RIPv2 on the routers to facilitate dynamic routing within the internal network:
     ```bash
     Router(config)# router rip
     Router(config-router)# version 2
     Router(config-router)# network 192.168.0.0
     ```

10. **Configuring Switchport Security or Port-Security on the Switches**:
    - Configure switchport security to restrict unauthorized devices:
      ```bash
      Switch(config)# interface fastEthernet 0/1
      Switch(config-if)# switchport mode access
      Switch(config-if)# switchport port-security
      Switch(config-if)# switchport port-security maximum 2
      Switch(config-if)# switchport port-security violation restrict
      ```

11. **Host Device Configurations**:
    - Configure PCs and servers with appropriate IP settings (static or DHCP as per department policy).

12. **Testing and Verifying Network Communication**:
    - Use ping and traceroute commands to verify connectivity between devices and across VLANs.
    - Test access to external services like the cloud-hosted email server.

By following these detailed steps, you will successfully design and implement a robust campus/university system network for Albion University, ensuring efficient communication and security across departments and campuses.
