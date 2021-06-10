# Cap #
Solver: Mayki
---------------

### User: ###
  First of all we will Nmap scan,we find out that the port 80 is open.  
  So we go to http://10.10.10.245/  
  after looking for any information or ways to exploit it leads me to nowhere, but then I find this:  
                    first click on the "≡" than on Security Snapshot (5 Second PCAP + Analysis)  
                    We can see that we can download a pcap file, so after downloading and opening the pcap file in wireshark we see packets that tell us nothing, but than  
                    I noticed the link itself which was http://10.10.10.245/data/3 and I noticed (5 second pcap + analysis), so I changed it to http://10.10.10.245/data/1  
                    and than http://10.10.10.245/data/0 and it was with the zero at the end because when opening the specified pcap file in wireshark and looking through   
                    the packets, we can see the - Username and password in the packets.  
                    so after using ssh to connect to the user on the ip, we can see in the home directory the user.txt  
       
### Root: ###
  So after gaining access to see what we can use privilege escalation script to see what we can run to gain access as root.  
  I ran linpeas.sh, you can run it from here https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS  
  and there I see: Files with capabilities (limited to 50):  
                      /usr/bin/python3.8 = cap_setuid,cap_net_bind_service+eip  
  Basically that means we can run python3.8 with root capabilities  
  **in the shell:**  
    1) Python3.8  
    2) import os  
       os.setuid(0)  
       os.system("/bin/bash")  
  
  Now we got root capibilites, all that's left is to type "sudo -i" and this will login as root and than we can see the root.txt  
    
    
   
    
Enjoy !!!  
