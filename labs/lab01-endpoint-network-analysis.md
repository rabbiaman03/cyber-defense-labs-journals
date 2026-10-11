# Lab 1 — Endpoint and Network Traffic Analysis (tcpdump and Wireshark)

Introduction:

Endpoint security means securing all the devices connected to a network. These devices can be vulnerable points for cyberattacks. So monitoring and analyzing these devices can make the system secure. In this lab, we will be learning how to secure devices and scan for finding vulnerabilities in the system. 

LAB 2A - TCPDump:

For this part I used my kali linux VM. I downloaded pcap file in my /home/kali/pcap directory. 
![](../images/ss1-2.jpg)
In the next step, I run tcpdump -n -r magnitude_1hr.pcap host 192.168.99.52. 
Here, -n is used to give raw ip addresses without resolving hostnames and -r is used to read packets from a file instead of capturing live traffic.

![](../images/ss2-1.jpg)
As we can see, timestamp is capturing the time when the packet was captured and then we have destination IP and port number. We also have it's control bit flags, size number and sequence number. 

Now, we will filter the scan with specific port number. For that I used tcpdump -n -r magnitude_1hr.pcap host 192.168.99.52 and port 80. Using this filter will only show the packets involve host 192.168.99.52 on port 80. We can only see packet either sent from port 80 or sent to port 80.
![](../images/Pasted-image-20250919140531.png)

Now we will be looking for payload. For that we will use tcpdump -n -r magnitude_1h.pcap host 192.168.99.52 and port -A. Here we will see ASCII payloads of the packets and the layer 7 protocol used is HTTP So that we can see parts of web traffic which includes headers and body data.![](../images/ss4-2.jpg)

At this step we will do tcpdump -n -r magnitude_1h.pcap host 192.168.99.52 and port -A | grep Get. This command will only display HTTP Get request from the client. 

![](../images/Pasted-image-20250919142233.png)
Now we will search for Base64 strings. I will look for strings that are related to Base64 encoding. Here -i option will make the search case-insensitive. 
![](../images/ss5-1.jpg)

Now we will use tcpdump -n -r magnitude_1hr.pcap host 192.168.99.52 and port 80 -AX. Here -X will show hex and -A will show ASCII so we can see both formats. 
![](../images/Pasted-image-20250919142923.png)
![](../images/Pasted-image-20250919142953.png)

Now we will filter ipv6 traffic only. It will help analyzing only ipv6 packets present in the capture. For that I will do tcpdump -n -r magnitude_1hr.pcap ip6. 
![](../images/Pasted-image-20250919143404.png)
![](../images/Pasted-image-20250919143422.png)

Now we gonna filter the traffic for the whole 192.168.99.0/24 subnet. For that we gonna use tcpdump -n -r magnitude_1h.pcap net 192.168.99.0/24. 
![](../images/Pasted-image-20250919143821.png)
![](../images/Pasted-image-20250919143844.png)


# Lab 1B - Advanced C2 PCAP Analysis

Part 1: View the pcap as ASCII

For that I used tcpdump -nA -r convertC2-pcap | less. 

Here,

-n will show raw IPs and numbers which are faster and clearer. 
-A will print all the payloads in ASCII
-r roads packets from the pcap instead of caturing packets live. 
![](../images/ss10-1.jpg)

**Part 2 SYN packets**

Now we filter to show all packets with SYN bit (0x02) set in the 13th byte offset in the TCP/IP header. 
![](../images/ss11-1.jpg)

**Part 3 : Finding hidden string**

Command: tcpdump -nA -r covertC2.pcap | grep "hidden"

This command will give the output of ASCII payloads and pipe them to grep. It will also give us "hidden" string. 
![](../images/ss12-1.jpg)


# Lab 1C - Introduction to Cyberchef

For this part I have watched CyberChef tutorial (https://youtu.be/m4uyiE0w6aU?si=uDXbdeq6xXJ9vr7R) and learned the beginner's guides. I have visited CyberChef and I put my **Base64-encoded string** from your tcpdump analysis. Then I have drag and drop operations by going **left panel** and under **Operations** searched for **"From Base64"**.
Then I clicked and dragged  the "From Base64" operation to the center panel. I baked it and on output penal I can see decoded data. 
![](../images/ss13-1.jpg)
![](../images/ss14.jpg)
Now this can return me a **text** (like a script or command), it will display in ASCII (human-readable). If it’s **binary** (such as an executable), it will appear as raw data. The decoded blob is JSON that contains a command the backdoor will run and a beacon interval. Then all the suspicious data were encoded in an URL encode. By using CyberChef operations it was used to be decoded. Then I used powershell commands to decode it and to analysis it. I analyzed all the decoded suspicious files and found that even without that the IP addresses are big indicators of compromise in the system. 

# Lab 2D - Tshark

First we need to install tshark in our operating system. In my case I used Kali VM. I simply installed it by sudo apt install tshark -y.
![](../images/ss15-1.jpg)
 Then I showed all the tshark commands that we can do. For that I did tshark --help. 
 ![](../images/ss16-1.jpg)
![](../images/ss17-1.jpg)
![](../images/ss18.jpg)
![](../images/ss19-1.jpg)


Now we will capture all the packets going through an interface. To do that we will first list all the interface that are available on our machine. For that I did sudo tshark -D
![](../images/ss22.jpg)


Now I will check how many interfaces I have by doing sudo ip link show. In my case it l0 and eth0. My eth0 interface was connected to internet. So I am gonna capture packets on eth0 interface by doing the following command:
sudo tshark -i eth0 
Here I specified the interface name. 
![](../images/ss21-1.jpg)

Now we will capture specific packets by filtering string. First, we will filter tcp port 80 and we will capture 10 packets. For that we will do sudo tshark -i eth0 -f "tcp port 80" -c 10. 

![](../images/ss23.jpg)

It is now filtering only the packets going through port 80. Now we can filter only the packets coming or going from specific ip we want. We will use the fo;;owing command for that:
sudo tshark -i eth0 -Y ip.addr == "8.8.8.8"
![](../images/ss24.jpg)
 Sometimes we have to analyze the packet. But it is impossible while capturing live traffic. So we have to save all the package and analyze it later one by one. It is very easy to save the traffic and can be done by sudo tshark -i eth0 -f "tcp port 80" -b filesize:1024 -a files:10 -w lab.pcap. 
 Here:
-i eth1 will capture packet from eth1 interface
-f "tcp port 80" will filter the traffic from port 80 only
-b filesize:1024 will make sure each capture file is at most **1024 KB (1 MB)** in size. If a file reach the size tshark will make new file and keep rest of output in new file.
-a files:10 This is an autostop feature which will stop the capture when 10 files are created.
-w lab.pcap it will write the output to a file with base name lab.pcap it will add numbers and date, time in the file name.
![](../images/ss25-1.jpg)

##### **Lab 2E - Wireshark**

For this part I used Kali VM as wireshark comes by default in wireshark. I fulfilled all the lab tasks given for that part. 

For changing my column display I went to - [Wireshark Tutorial: Changing Your Column Display](https://unit42.paloaltonetworks.com/unit42-customizing-wireshark-changing-column-display/) and then to provided github link in this page. I downloaded the zip file and unlock the file by password (infected). I extracted the file. I checked and matched the wireshark version as the website said. Then I changed the profile to personal profile and named it customized. Then I went to file>open and selected the unzip file. 

![](../images/ss27-1.jpg)

Now I will change date and time to UTC. For that I went to view from taskbar. Then time display format and choose UTC date and time of day and seconds. ![](../images/ss27-2.jpg)

Now I will add a new column. For that I will left click on any column, then column preferences and will add new columns. I will name them src port and dst port. The type will be src port, dst port. ![](../images/ss29.jpg)
![](../images/ss30.jpg)


Now I will display how to filter expressions. For that I went to github page and downloaded the zip file and unzip it. 

![](../images/ss31.jpg)

I went to file and opened the first file. I used the filter for http.request. It will show the packets only going through hhtp port (port 80) the specific network. 

![](../images/ss32.jpg)

We can exclude SSDP traffic in our results by modifying our filter expression to:
(http.request or tls.handshake.type eq 1) and !(ssdp)

![](../images/ss33.jpg)
In the next steps I used filter and put the level as basic+dns.  the “basic+dns” filter expression shows the same data as our “basic+” filter, but it includes or dns. This filter reveals any DNS queries in the pcap. It is very helpful for determining domain names associated with non-web traffic.

![](../images/ss34-1.jpg)

I will try to identify hosts and users by downloading the zip file and unzip it using the password. ![](../images/ss35.jpg)

I will use first unzip file to identify hosts and users. I went to file and then open this file. 

![](../images/ss36.jpg)
After that I will filter the packets by (http.request or tls.handshake.type eq 1) and !(ssdp). Now  we can correlate the IP address at 172.16.1[.]38 with its associated MAC address at f8:ff:c2:04:a5:7b

![](../images/ss37.jpg)
After that we will use dhcp as a filter, which may reveal the hostname using this IP address. Depending on how frequently a DHCP lease is renewed, we might not have DHCP traffic in our pcap. Fortunately, we can use nbns traffic to identify hostnames. This will represent us hostname of a selected ip address. ![](../images/ss38.jpg)

Now we will be exporting objects from a pcap. For that I will download the zip file from github repository. I will explore the first file in the wireshark. ![](../images/ss39.jpg)
As a network packet analyzer, Wireshark combines data from multiple IP packets and the associated TCP frames to reveal the content of a pcap. So we can filter the scan by http.request. It will give us 3 ip addresses. The first file is .doc, which is a microsoft word and the second one ends with .exe. 

![](../images/ss40.jpg)

Then we will export the file as HTTP and save it in my directory. 

![](../images/ss42-1.jpg)

After that I will go to terminal and I can explore and analyze the HTTP file from wireshark. 


![](../images/ss43.jpg)
We also can verify integrity of the file by shasum -a 256 [filename]. 
![](../images/ss44.jpg)
