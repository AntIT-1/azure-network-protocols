<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
Observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04



<h2>Actions and Observations</h2>

First step is to create a resource group in Azure portal. You will need two VMs for this project. One with Windows 10 operating system and the secound with Linux Ubuntu. Be sure that both VMs are in the same vnet. 

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/7231c0ba-578a-46f9-a623-4d9589592a82)

After VMs are created, you can see that both VMs are in the same resource group and vnet. 

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/0e845bab-876b-40f3-8408-f6230c9393b0)

The next step we will observe ICMP traffic. Within your Windows VM install wireshark which is a protocol analyzer. Once wireshark is intalled we will filter ICMP traffic to observe the activity. Retrieve the private IP address of the Linux machine and try to ping it from your Windows VM. Once you enter the ping command, you will see it in wireshark as well as powershell.

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/e09de982-8a02-48d9-9062-941001972c15)


From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark.

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/f73bdbbe-dfba-4008-945f-edc440a57444)



In this next step will observe what happens when you deny a certain protocol. Deny ICMP traffic into the Linux machine. Select ICMP protocol. For action select Deny. Priority 200 that way it will get bumped to the top of the rule list. You have the option to enter a description if you so please. 

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/a07e6422-e6d9-46a1-bbdf-3a61e768128a)

As you can see, once icmp traffic is blocked, you can no longer ping the Linux machine. The request is timed out.  

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/34e011af-e130-46c6-bb9f-89a7b7a7bffb)

Once you allow ICMP, the Windows machine will continue to ping the Linux machine.

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/c03276dd-4ca9-4fc7-bfc0-1e7d6f339950)

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/e12d075e-b2b2-4aa6-ab52-0978665d8698)

Back in Wireshark, filter for SSH traffic only. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.
Exit the SSH connection by typing "exit" and pressing [Enter].
Once you "ssh" into the Linux maching from your windows machine, you can see ssh traffic on Wireshark. 

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/e85af415-4e24-43cb-92f8-e2eed876fb63)

Observe DHCP Traffic
Back in Wireshark, filter for DHCP traffic only.
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line by entering ipconfig /renew.
Observe the DHCP traffic appearing in WireShark.

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/508a2320-94a5-426c-a3bc-8b8a85c8ae60)

Now we can observe DNS Traffic.
Back in Wireshark, filter for DNS traffic only.
From your Windows 10 VM within a command line, use nslookup to see what www.google.com and www.disney.com’s IP addresses are.
Observe the DNS traffic being show in WireShark

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/05d40471-69d2-4c75-9eac-0ddf94381ba1)

Lastly, we will observe RDP Traffic which is remote desktop connection. 
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389).
Observe the immediate non-stop spam of traffic. The reason for this is because the RDP protocol is constantly showing you a live stream from one computer to another therefor traffic is always being transmitted.

![image](https://github.com/AntIT-1/azure-network-protocols/assets/141161539/1d6f586c-102a-4d76-9e7f-eb9c03371f88)
















