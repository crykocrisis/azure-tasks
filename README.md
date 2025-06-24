# Activities on the Network between Azure machines

In this piece, we use Wireshark to analyze different types of network traffic coming & going from Azure Virtual Machines. We also experiment with Network Security Groups.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Remote Desktop
- Various Command-Line Tools
- SSH, RDH, DNS, HTTP/S, ICMP
- Wireshark 

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<b>Creating two virtual machines</b>

1. Establish a Resource Group

![Screenshot 2025-06-18 104712](https://github.com/user-attachments/assets/b3a049cd-2015-4f1a-adec-f8cdb2ba640a)

2. Make a virtual machine (VM) for Windows 10

![Screenshot 2025-06-18 110132](https://github.com/user-attachments/assets/5ec8857e-a965-4c7e-a792-58b307234462)

a. Select the previously created Resource Group when constructing the virtual machine (VM).

![Screenshot 2025-06-18 110201](https://github.com/user-attachments/assets/9a9f571f-fa7f-4b2b-9a83-14e1bc996f53)

3. Make an Ubuntu (Linux) virtual machine

![Screenshot 2025-06-18 111525](https://github.com/user-attachments/assets/efbcde0b-f2d1-4146-8358-472f3ab09648)

a. When constructing the virtual machine, make sure the Resource Group & Virtual Network are the same as they were previously built.
  
  ![Screenshot 2025-06-18 111425](https://github.com/user-attachments/assets/79b6d8bc-3ab0-4c95-ac3d-3951d5e48334)

 b. Authentication is username/password.

![Screenshot 2025-06-18 110802](https://github.com/user-attachments/assets/6c373943-4bb6-4bc1-80ca-1112bc12ba1d)

4. Verify that the virtual machines are on the same subnet or virtual network. 

![Screenshot 2025-06-18 111425](https://github.com/user-attachments/assets/a9016a0f-1086-4ec1-adfa-b7eb6bd975c5)

<h2>ICMP traffic</h2> 

1. Connect to your Windows 10 virtual machine using Remote Desktop. 

![Screenshot 2025-06-18 114350](https://github.com/user-attachments/assets/987fd023-d23c-4065-b66c-fc8652aa84cd)

2. Install Wireshark in your Windows 10 virtual machine. 

![Screenshot 2025-06-18 125138](https://github.com/user-attachments/assets/46acd580-1cd4-44f2-b429-f1fc8b26b6ac)

3. Open Wireshark & begin capturing packets. 

![Screenshot 2025-06-18 125658](https://github.com/user-attachments/assets/c7f04016-970e-462d-ae90-e3168569a72f)

4. Filter for ICMP traffic in Wireshark.

![Screenshot 2025-06-18 125817](https://github.com/user-attachments/assets/14094a97-0b37-43b1-ad4f-fd88dfd64e3f)

5. From inside the Windows 10 virtual machine, get the Ubuntu virtual machine's private IP address & try to ping it. (Watch WireShark's ping queries & responses.)

![Screenshot 2025-06-18 130159](https://github.com/user-attachments/assets/c65f1d08-0d2b-4599-959e-8b8373fe323a)

6. To view the traffic in WireShark, launch PowerShell or the command line from the Windows 10 virtual machine. 

![Screenshot 2025-06-18 130346](https://github.com/user-attachments/assets/0f55ae6c-ed4f-4aae-a992-cbc4ef741f08)

<h2>Firewall configuration </h2>

1. Start a continuous/nonstop ping between your Ubuntu & Windows 10 virtual machines.

![Screenshot 2025-06-18 130828](https://github.com/user-attachments/assets/94f52fe7-b889-451e-a660-0d0321fad694)

2. Turn off incoming ICMP traffic by opening the Network Security Group that your Ubuntu virtual machine is using.

![Screenshot 2025-06-18 132617](https://github.com/user-attachments/assets/45ac018b-90a2-4cfd-a5b0-c6ec2416d57f)

3. Go back to the Windows 10 virtual machine & watch the command line Ping activity & the ICMP traffic in WireShark.

![Screenshot 2025-06-18 131851](https://github.com/user-attachments/assets/7ab55cba-2997-4ec6-8301-6e25ebac75c4)

4. Reactivate your Ubuntu virtual machine's ICMP traffic for the Network Security Group.

5. Return to the Windows 10 virtual machine & watch the command line Ping activity & the ICMP traffic in WireShark.

![Screenshot 2025-06-18 131939](https://github.com/user-attachments/assets/fd79c09d-1339-4c72-91a1-8a0f3ba8ea80)

6. End the ping process

![Screenshot 2025-06-18 132330](https://github.com/user-attachments/assets/c96c671b-9965-4ded-8100-529284a97eeb)

<h2>SSH traffic</h2>

1. Only filter SSH traffic.

![Screenshot 2025-06-18 133730](https://github.com/user-attachments/assets/1c6983b3-a6dc-473e-b5ca-38acabef5001)

2. "SSH into" your Ubuntu Virtual Machine IP address from your Windows 10 virtual machine.

3. Type ssh labuser@<private IP address> into PowerShell.

![Screenshot 2025-06-18 140037](https://github.com/user-attachments/assets/5049e08e-ce44-4e05-81ea-ac34c3d4b838)

4. Use WireShark to view SSH traffic spam after entering commands (username, password, etc.) into the Linux SSH connection.

![Screenshot 2025-06-18 140148](https://github.com/user-attachments/assets/257454f7-156c-4d8c-8c36-bf57244bb80f)

5. Type "exit" & hit [Enter] to end the SSH connection.

![Screenshot 2025-06-18 140900](https://github.com/user-attachments/assets/9cbbae67-d27c-449d-9f4b-c08672ad5b15)

<h2>DHCP traffic</h2>

1. Return to Wireshark & filter only DHCP traffic.

![Screenshot 2025-06-18 141514](https://github.com/user-attachments/assets/85dd802b-7f6e-4650-8314-2378d0b88729)

2. Try using the command line to give your Windows 10 virtual machine a new IP address.
   
a. Launch PowerShell in administrator mode & type ipconfig /renew.

![Screenshot 2025-06-18 141551](https://github.com/user-attachments/assets/62230037-1dd8-486d-ad75-f8742ee13e46)

b. Watch the DHCP traffic that WireShark displays.

![Screenshot 2025-06-18 144429](https://github.com/user-attachments/assets/e7e0bb23-feb8-4e1c-a6fc-94c0f2fe02be)

<h2>DNS traffic</h2>

1. Return to Wireshark & filter just DNS traffic.

![Screenshot 2025-06-18 144629](https://github.com/user-attachments/assets/9772be8e-a7d0-41b8-bcc8-10974d184691)

2. Use nslookup from your Windows 10 virtual machine's command line to find the IP addresses of Google.com or Disney.com.

![Screenshot 2025-06-18 144807](https://github.com/user-attachments/assets/eeff7b95-9846-46e5-80fc-9dfdf142e8d8)

a. Examine the DNS traffic seen in WireShark.

![Screenshot 2025-06-18 144857](https://github.com/user-attachments/assets/1f844a51-f94e-4aa7-8984-c793f51641e5)

<h2>RDP traffic</h2>

1. Once again, filter for RDP traffic only in Wireshark (tcp.port == 3389).

![Screenshot 2025-06-18 144940](https://github.com/user-attachments/assets/cdb64374-fa72-4ea5-84b6-8248ea404664)

2. Take note of the instantaneous, continuous stream of traffic

![Screenshot 2025-06-18 145024](https://github.com/user-attachments/assets/7c87f149-f033-441a-b28f-0259bb9d2b76)

a. Traffic is always being transmitted since the RDP protocol continuously shows you a live stream from one machine to another.
