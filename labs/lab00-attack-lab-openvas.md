# Lab 0 — Building an Attack Lab and Vulnerability Scanning with OpenVAS

Introduction:

In this lab, we will perform vulnerability scanning using **OpenVAS** (Greenbone Vulnerability Management), a widely used open-source tool designed to identify vulnerabilities in networked systems. 

Part 0: Backups

This part includes backing up data for a VM. The steps are mentioned in Safari on-line book. (  [](https://nostarch.com/cybersecurity-small-networks) [Cybersecurity for Small Networks A guide to implementing DIY security solutions and readily available technologies to protect home and small-office networks from attack.](https://nostarch.com/cybersecurity-small-networks))

From chapter 9, I have applied backup solutions for my kali VM. The first step includes using duplicity. This can be done by backing up files locally or anywhere. To do so I have updated all the files in  my kali VM. I did sudo apt update and install duplicity by sudo apt install duplicity. 
![](../images/ss1.jpg)
Then I made a test.txt file in my test repo. ![](../images/ss2.jpg)
After that I choose a backup location for my kali VM where backup file will be saved. ![](../images/ss3.jpg)
To prove my work I deleted my test.txt file by sudo rm test/test.txt, which will eventually delete my txt file. ![](../images/ss4.jpg)
The deleted file was already in backup my backup location. So I just restore this txt file from duplicity. 
![](../images/ss5.jpg)
It can be seen from my screenshot that I have successfully restored my test.txt file using duplicity. 

For the next step, I moved my whole VM file from my SSD to my local folder. That's how I made it secure storing my files in a different location. ![](../images/ss6.jpg)
So now to prove it, I deleted some log files from my VM to damage it. And when I tried to open it, the VM crashed. I could not access it anymore. 
![](../images/ss7.jpg)
Then I simply restored all my files from my backup folder to set it up again. 
![](../images/ss8.jpg)
And it was working!!

That's how I have implement backup strategies. 

Part 1: Effective Note-Taking

Effecting note-taking is very important in the field of cybersecurity. It helps in troubleshooting while doing different labs. I am using obsidian to make effective notes. It is a very helpful tool for taking notes. Obsidian is a Markdown editor designed for knowledge management. It allows users to create, link, and organize notes in a way that enhances information retrieval and understanding.
I have watched tutorials on how to make effective notes using obsidian and found some key features of obsidian. 
1. Markdown Support: Obsidian is built on Markdown, which means I can easily format my notes using a simple syntax. This helps in creating structured content like headers, bullet points, and code blocks.
2. Backlinking: A key feature in Obsidian is the ability to create backlinks, allowing users to link notes to each other. This makes it easy to track related topics, such as linking a note about a vulnerability to the corresponding exploitation technique.
3. Graph View: The graph view in Obsidian shows how notes are connected, which helps visualize the relationships between different pieces of information.
4. Tagging: Tags are used to categorize notes. I used tags like **#vulnerabilities**, **#exploits**, and **#tools** to make it easier to find notes related to specific topics.

![](../images/Pasted-image-20250917043055.png)
That is  how my obsidian interface look like right now. I will submit my note in pdf format. 


Part 2: Setting Up an Attack Lab Environment

For this part, I used two different VMs where on will act as attacker and another will act as target VM. I used VMware platform for my VMs. My kali VM will act as attacker and metasploitable3 will be my target VM as it is more vulnerable to attack. To connect the VMs, I used host-only network interface for both VMs to connect them in a single network ip. I used 192.168.6.0/24 as my network address. I gave 192.168.6.1 ip to my metasploitable3 and 192.168.6.2 to my kali VM. 
![](../images/Pasted-image-20250917043900.png)

![](../images/Pasted-image-20250917043930.png)
It was my network configuration for both VMs. As per now, the VMs have assigned IPs , I have to check connectivity test. To do it, I ping 192.168.6.2 from metasploitable3 and also ping 192.168.6.1 from my kali VM. 

![](../images/ss10.jpg)
![](../images/ss9.jpg)

The ping was successful, so the connectivity part is done. Both of the VMs can not connect to internet. To prove that I did ping 8.8.8.8 on both VMs. 

![](../images/Pasted-image-20250917044610.png)
![](../images/Pasted-image-20250917044629.png)

Part3: Initial Enumeration of Target VM

nmap: 
In this part i learned how to use nmap to scan my meta device and find different open ports and vulnerbilities. I did different types of scan starting from basic ping scan to intense scans. I started from pinging all the host in the network and finding if the hosts are up. 



![](../images/ss11.jpg)
From the scan, I can see 2 hosts are up, where one is kali itself and another is metasploitable3. 

Port Scanning: 
In this part i did port scan on specific port i.e. 80,443 which are http and https port to check if the vm is running a website. 
![](../images/ss12.jpg)
Both of the ports are closed and so this VM is not a web server. 

Next I did a scan using all different keys. i did nmap -T4 -PA -sV --version-all --osscan-guess -A -p 1-65535. In this command -T4 is used to increase scan speed -PA is to send TCP ACK ping for host discovery -sC run default scripts for basic vulnerability checks, -sV detects service versions, -- version-all will try all probes for maximum accuracy, --osscan-guess will guess the closest os if exact match is not found, -A is to do Aggressive scan which does OS detection, version detection, runs scripts and traceroute. In the end, -p 1-65535 scans all the available ports.

![](../images/ss13.jpg)


![](../images/ss15.jpg)
![](../images/ss16.jpg)
![](../images/ss17.jpg)

![](../images/s14-2.jpg)


Then I did nmap -sV --osscan-guess -p 1-10000
This command scans the first 10,000 ports, identifies what services/versions are running, and tries to guess the operating system running on the target machine(192.168.6.1).
![](../images/ss19.jpg)
![](../images/ss20.jpg)
![](../images/ss21.jpg)
![](../images/s22.jpg)

The Nmap command `nmap -T4 -sV --version-all --osscan-guess -A -p 1-10000` performs an aggressive and detailed scan of a target. It scans ports 1-10000 for open services, detects service versions, attempts to guess the operating system, and runs various Nmap scripts for additional information. The T4 timing template speeds up the scan, and the -A option enables OS detection, version detection, and traceroute. This command is typically used in penetration testing to gather comprehensive information.

nmap -sU -sV --version-all -p 1-65535 

This command scans all UDP ports (1–65535) on the target, tries to identify what services and versions are running, and uses all probes for maximum accuracy.

![](../images/ss25.jpg)

OpenVAS

Openvas or open vulnerability assessment scanner is a vulnerability scanner used to identify
security issues in system, application and networks. It scans network device for known
vulnerability. To install it on kali I did sudo apt update and sudo apt install openvas. Then i set-up gvm by sudo gvm-setup and start gvm. It took me in a website where I logged in with the credentials provided before. Then I add a new task and provided my metaspoiltable3's ip address and start the scan. 


![](../images/ss26-1.jpg)
![](../images/s27.1.jpg)
![](../images/ss27.jpg)
When I read summery, I can see that the host us missing an important security update and there was vulnerability in the system. So, we can conclude that it is easy to exploit vulnerability in the system and gain access to the system. 