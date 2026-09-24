# 🚀 FTP Service Deployment & pfSense Firewall Security Lab

## 📌 Project Overview
This laboratory experiment demonstrates the configuration, deployment, and security verification of an FTP service (`vsftpd`) hosted on an Ubuntu Server (`CSRV01-CORE`) within an enterprise EVE-NG network topology. The lab covers client authentication from `PC-HQ-CEO-01`, Inter-VLAN routing validation, Passive FTP behavior through subnets, and traffic control using a **pfSense Firewall**.

---

## 📐 Network Topology & IP Addressing

<img width="1542" height="827" alt="image" src="https://github.com/user-attachments/assets/bfe830e8-58df-40d7-af3a-e5570877e9ce" />

- **FTP Server (`CSRV01-CORE`):** `192.168.50.10/24` | Default Gateway: `192.168.50.1`
- **Client Host (`PC-HQ-CEO-01`):** `192.168.10.10/24` | Default Gateway: `192.168.10.1`
- **pfSense LAN Management Interface:** `10.3.3.1/24`

---

## 🛠️ Implementation Steps

### 1. FTP Server Setup (`vsftpd`)

1. **Package Installation & Connectivity Fix:**
   Configured DNS resolution (`8.8.8.8`) to establish internet access and installed the `vsftpd` package:
   ```bash
   sudo apt update && sudo apt install vsftpd -y 
  
  <img width="1006" height="832" alt="FTP_SERVER -PART-1" src="https://github.com/user-attachments/assets/575ff911-8c6a-48f9-b543-00f40876c233" />
  <img width="971" height="812" alt="FTP_PART-2" src="https://github.com/user-attachments/assets/f9604d25-8fc8-46d2-a75e-dd6f82d337fe" />

2. **Service Verification::**
    Verified that the `⁠vsftpd⁠` service is active and running:
    ```bash
    sudo systemctl status vsftpd
    
   
<img width="981" height="272" alt="FTP-3" src="https://github.com/user-attachments/assets/91818f4e-b12e-41ee-be44-5d8fd593a2c3" />

3. **Service Configuration (⁠/etc/vsftpd.conf⁠):**
    Enabled write access for local users by updating the configuration file:
      ```bash
    write_enable=YES
   
  <img width="1001" height="827" alt="FTP" src="https://github.com/user-attachments/assets/3b2054e2-6129-4db9-96cf-c338bb6841f1" />
   
4.  **User Creation & Service Restart:**
     Created local user ⁠ftpuser⁠ with home directory privileges and restarted the service:
       ```bash

    sudo adduser ftpuser
     sudo systemctl restart vsftpd
       
   <img width="587" height="325" alt="kryet vtp_f" src="https://github.com/user-attachments/assets/c781e047-a379-4e7c-881a-b240445613d8" />

 ### 2. Client Routing & Network Configuration 


1.  **Assigned static IP and default gateway on `⁠PC-HQ-CEO-01⁠` via Linux CLI:**
    ```bash
            sudo ip addr add 192.168.10.10/24 dev ens3
                sudo ip route add default via 192.168.10.1⁠


<img width="1017" height="817" alt="image" src="https://github.com/user-attachments/assets/f5357b93-2ec2-4604-8d94-67c6157b7bab" />

2. **Verified ICMP reachability (Ping) between VLAN 10 and VLAN 50.**
   <img width="960" height="740" alt="image" src="https://github.com/user-attachments/assets/d30e4b7b-696b-4df2-a44d-7aaf687b0813" />


##🧪 Verification & Security Testing
1. **FTP Authentication Test:**
      
   Initiated an active connection from ⁠`⁠PC-HQ-CEO-01⁠ (⁠ftp 192.168.50.10⁠)⁠`. Successfully authenticated using ⁠`⁠ftpuser⁠ ⁠`credentials ⁠`(⁠⁠230 Login successful⁠)⁠`.

    <img width="885" height="634" alt="image" src="https://github.com/user-attachments/assets/57531da3-0adf-44c9-88d5-291ce9386ac5" />

2.  **Passive Mode File Transfer:**
     Enforced ⁠⁠`passive⁠`⁠ mode inside the FTP CLI to allow data channel negotiation across stateful subnets without session hangs.
⁠
    <img width="900" height="756" alt="image" src="https://github.com/user-attachments/assets/88a85374-67e7-405e-a33b-a84600261839" />


3. **pfSense Security Policy Enforcement:**
   Accessed pfSense WebConfigurator (⁠⁠`https://10.3.3.1⁠`⁠), configured inbound firewall rules targeting Port 21, and verified traffic blocking/allowing states.

    <img width="1012" height="806" alt="Screenshot 2026-09-23 222449" src="https://github.com/user-attachments/assets/f61d17de-9769-4b51-8858-32d3c29ea84b" />
   <img width="1041" height="796" alt="Screenshot 2026-09-23 222551" src="https://github.com/user-attachments/assets/71217a92-8a2d-4a1e-8c10-c0fbbba381cc" />
   <img width="1041" height="796" alt="Screenshot 2026-09-23 222551" src="https://github.com/user-attachments/assets/620dac64-bc63-4bdb-8d92-5b121e89f095" />
   <img width="1041" height="796" alt="Screenshot 2026-09-23 222551" src="https://github.com/user-attachments/assets/a588467c-8a72-4012-81af-c55a1ab546b4" />
   <img width="1015" height="827" alt="Screenshot 2026-09-23 223534" src="https://github.com/user-attachments/assets/6d75b837-1505-4452-89c0-27a32018192e" />
   <img width="937" height="752" alt="Screenshot 2026-09-23 224132" src="https://github.com/user-attachments/assets/05e313cb-e3c5-4da0-86b0-11cf6d217545" />


   
##📝 Key Takeaways

 Linux QEMU Endpoints: Standard VPCS nodes lack application-level utilities; full Linux QEMU nodes are necessary for authentic service testing.
 Passive FTP Requirement: Stateful routing interfaces require Passive FTP (⁠PASV⁠) mode to negotiate data channels correctly across multi-VLAN environments.


   
   



   
   
