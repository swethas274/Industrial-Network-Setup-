# Industrial Network Setup using Cisco Packet Tracer  

## 📌 Project Overview  
This project focuses on designing and securing an **industrial network** using **Cisco Packet Tracer**. The network includes **VLAN segmentation, Inter-VLAN routing, DHCP services, security policies, and QoS implementation** to ensure **efficient, scalable, and secure communication** between different departments.  

---

## 🏗️ Network Design  
The network follows a **three-tier architecture**:  
- **Core Layer:** High-speed backbone with multilayer switching.  
- **Distribution Layer:** VLAN routing and access control.  
- **Access Layer:** Direct connections to end devices.

---

## Network Topology
![Industrial Network Setup](https://github.com/user-attachments/assets/f98f1f23-2740-4abd-8a6d-46bfcc754764)


**Key Features Implemented:**  
✅ **VLANs** for department segregation.  
✅ **Inter-VLAN Routing** for communication between VLANs.  
✅ **DHCP Configuration** for dynamic IP address allocation.  
✅ **Port Security** to prevent unauthorized devices.  
✅ **ACLs (Access Control Lists)** for restricting unauthorized access.  
✅ **QoS (Quality of Service)** to prioritize critical traffic.  
✅ **SSH Configuration** for secure remote access.  

---

## ⚙️ Devices Used  
- **Router:** Cisco 2911 (Inter-VLAN Routing & WAN Connectivity).  
- **Switches:** Cisco 2960 (Access Layer Switching).  
- **Multilayer Switches:** Cisco 3650 (Core & VLAN Routing).  
- **Firewalls:** Cisco ASA 5506 (Security & Traffic Filtering).  
- **Servers:** Generic Servers (DHCP, DNS, Email).  
- **Wireless Access Points:** Cisco Aironet (Wireless Connectivity).  
- **End Devices:** PCs, Laptops, Printers, Tablets, Mobile Devices.  

---

## 🔧 CLI Configuration Commands  
### **1️⃣ VLAN Configuration**  
```bash
Mlt-SW1# conf t   
Mlt-SW1(config)# vlan 10  
Mlt-SW1(config-vlan)# name SALES  
Mlt-SW1(config-vlan)# exit  
Mlt-SW1(config)# vlan 20  
Mlt-SW1(config-vlan)# name HR  
Mlt-SW1(config-vlan)# exit
```


### **2️⃣ Inter-VLAN Routing Setup**  
```bash
Router(config)# interface GigabitEthernet0/0.10  
Router(config-subif)# encapsulation dot1Q 10  
Router(config-subif)# ip address 192.168.10.1 255.255.255.0  
Router(config-subif)# exit  
```

### **3️⃣ DHCP Server Configuration**  
```bash
Router(config)# ip dhcp pool SALES  
Router(dhcp-config)# network 192.168.10.0 255.255.255.0  
Router(dhcp-config)# default-router 192.168.10.1  
Router(dhcp-config)# dns-server 8.8.8.8  
```

### **4️⃣ Security Implementation (Port Security & ACLs)**  
```bash
Mlt-SW1(config)# interface GigabitEthernet1/0/2  
Mlt-SW1(config-if)# switchport mode access  
Mlt-SW1(config-if)# switchport port-security  
Mlt-SW1(config-if)# switchport port-security maximum 2  
Mlt-SW1(config-if)# switchport port-security violation restrict  
Mlt-SW1(config-if)# switchport port-security mac-address sticky  
```

```bash
Router(config)# access-list 101 permit ip 192.168.10.0 0.0.0.255 any  
Router(config)# access-list 101 deny ip any any  
Router(config)# interface GigabitEthernet0/0  
Router(config-if)# ip access-group 101 in  
```

### **5️⃣ QoS (Quality of Service) Configuration** 
```bash
Mlt-SW1(config)# mls qos  
Mlt-SW1(config)# class-map match-all PRODUCTION_TRAFFIC  
Mlt-SW1(config-cmap)# match ip dscp ef  
Mlt-SW1(config)# policy-map PRODUCTION_POLICY  
Mlt-SW1(config-pmap)# class PRODUCTION_TRAFFIC  
Mlt-SW1(config-pmap-c)# priority percent 50  
Mlt-SW1(config)# interface GigabitEthernet1/0/1  
Mlt-SW1(config-if)# service-policy output PRODUCTION_POLICY  
Mlt-SW1(config-if)# trust dscp  
```

### **🔍 Verification Commands** 
```bash
Mlt-SW1(config)# mls qos  
show vlan brief                      # Verify VLANs  
show ip route                         # Verify routing setup  
show ip dhcp binding                  # Check assigned DHCP IPs  
show port-security                    # Check port security status  
show policy-map interface GigabitEthernet1/0/1  # Verify QoS  
```


