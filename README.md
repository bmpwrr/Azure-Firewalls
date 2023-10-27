# Implementing Platform Protection Using Azure Firewalls


![image](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/409db987-7d6f-44f2-9de5-2ccdac524184)



Introduction 
- 
In the domain of cloud computing and network management, a virtual network is divided into two sections: a "workload subnet" and a "jump host subnet." Each of these sections contains virtual machines, akin to digital computers.

A custom routing strategy is in place to direct all outgoing traffic from the "workload subnet" through a firewall for security. This firewall has application rules that only allow outbound traffic to "www.bing.com," ensuring controlled access to the internet.

Additionally, firewall network rules are implemented to enable external DNS server lookups, enhancing the network's functionality and connectivity. This network configuration aims to provide an organized, secure, and efficient virtual network environment.


Technologies, Azure Components, and Regulations Employed
-
- Remote Desktop Protocol (RDP)
- Configure DNS Servers
- Configure Azure Firewall
- Configure Application Rule
- Configure Network Rule
- Default Route
- Cloud Computing
- Infrastructure


Lab Step by Step:
- 
1) Use a template to deploy the lab environment.

![1 (deplay custom template)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/28359fa9-f792-4620-9a73-5257b974e7c1)



![2 (custom template)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/0a619f66-cd9a-4998-928d-4082f4548ac2)



![3 ](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/ca9c2de0-0f5c-46e2-be18-f33bab6e07c3)




2) Deploy an Azure Firewall.


![4](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/e50cf239-2cfd-41c3-9ab7-8ac02b988301)


![5 (firewall values)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/301f8441-25e5-439c-8c1d-03ed154fe86d)

After completing the firewall setup and deployment, locate the private IP address. This step is necessary to facilitate the deployment of a user-defined route.

3) Create a default route.


![7 (route table)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/52429a4d-cd66-4dcc-b318-28e467cf931b)


Create a route table and name it "Firewall-route"


![image](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/f397ef1d-5a0b-4473-b224-401059a06252)


![9](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/f8ec28a5-106b-443e-85fc-61651e3c6020)



4) Configure an application rule.

Navigate back to "Firewall" >> "Rules" >> "Applications"

![11 (navigate back to firewall into rules and into applications)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/f9e70e4f-8aeb-43ce-af3a-890c63ef74c3)


![12 (application values, this allows outgoing 843 traffic with a destination of bingdotcom)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/28ae7ac6-c3d2-4127-8e4f-74ccde6af4e2)

These application values allows outgoing 80 and 443 traffic with a destination to bing.com



5) Configure an network rule.

Navigate back to "Firewall" >> "Rules" >> "Network"

![13 (navigate into network)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/6ca464d7-e902-4164-93a6-07e85ca4f1ff)


![14 (network values, allows the dns access to the two dns servers, so any machines within that network is allowed to query those dns on port 53)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/a8671647-1124-486b-9844-d59893e1290a)

These network settings enable DNS access to the two DNS servers, allowing any devices within that network to query those DNS servers on port 53.


6) Configure DNS servers.

Go to "Virtual machines" >> "Srv-Work | Networking settings" >> "srv-work267" >> under Settings, click "DNS servers"

Enter these values:

![17 (create the values of the dns servers to the ones we put in the firewall)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/01829ad2-8b5e-4966-a572-2fc83adfcbee)

These values that we inserted are the values of the dns servers that we put into the firewall.

7) Testing the Firewall

Navigate back to "Virtual Machines" >> "Srv-Work"


![image](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/be0d154d-9a1d-46c9-ae38-d9e318e080a1)


Now, connect the VM via RDP. 


![image](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/57d59a87-92bb-495a-ab33-39f86281597a)


![20 (download the rdp file)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/2c13a097-d37c-436f-8b91-74ee6b19edb1)



Download the RDP file. Once you download the RDP file, open the file and enter the credentials.


![21 (rdping)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/637ee65f-4039-4b10-98e6-3996bbdf0709)


Once logged onto the VM, go to "Server Manager" >> "Local Server" >> and clck on "IE Enhanced Security Configuration" and enable "On" to "Off".


![23](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/d4310c67-186e-4b35-bca7-3c3adbcbed1a)

Now, the last 2 steps are to test if it works. In the browser, we test to see if we are able to log into bing.com


![24 (successful going to bing)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/61a4afac-5251-4c55-88dc-a492f5c94ab2)


It looks like going into Bing worked just fine.


![25 (no rule)](https://github.com/bmpwrr/Azure-Firewalls/assets/144153997/7741cc50-1c57-4d16-9299-ae98ea2127fb)


It looks like logging into Google (or any website but Bing) is denied due to no rules being matched.


Conclusion
-
In the realm of cloud computing and network management, a virtual network is effectively partitioned into two primary components: the "workload subnet" and the "jump host subnet." These segments house virtual machines, serving as digital counterparts to physical computers, thus contributing to the network's computational capabilities.

In pursuit of heightened security and control, a customized routing strategy has been implemented. This strategy efficiently directs all outbound traffic from the "workload subnet" through a dedicated firewall. The firewall, fortified by application rules that restrict outbound connections to "www.bing.com," serves as a safeguard for controlled and secure internet access.

Furthermore, the network's functionality and connectivity are reinforced by the introduction of firewall network rules. These rules enable external DNS server lookups, thereby enhancing the network's ability to connect and communicate effectively.

In summary, this meticulously structured network configuration has been designed with the overarching goal of delivering a virtual environment that excels in organization, security, and operational efficiency, in keeping with the principles of cloud computing and network management.









