# Active Directory Home Lab With Creation of Users using a Powershell Script

## Description
This project is a walkthrough of how I created an Active Directory environment using Oracle VM VirtualBox. I set had to set up a Windows Server 2022 to run Active Directory on it. I also configured a Domain Controller that will allow me to run a domain and then I ran a Powershell script that would create over 1000 users in Active Directory. This lab gave me hands-on experience with configuring an Active Directory and Domain Controller and it also simulates a business environment.

## Environments Used
- Oracle VM VirtualBox
- Microsoft Server 2022

## Program Walkthrough 
So the Windows Server will be the machine that will be hosing my Domain Controller and also the Active Directory. So I needed two network adapters, one adapter will be the NAT which will be using my host IP address so it can be able to access the internet and the other its an Internal Network Adapter that will be used for the Domain Controller to be able to communicate with other Virtual Machines.

![Oracle VM Virtual Box](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(65).png)

So after I did so I started the machine and I did the nesseary configurations and I was in the desktop of the server. So now I had to do configure the two network adapters. One of the adapters needed to be the external(internet) NIC and one is the internal NIC. So I navigated to the network connection. After getting there I had to figure out which NIC is our NAT and which is the internal Network then I had to rename them so I can easily identify them for when I am setting up the Domain Controller and the Dynamic Host Configuration Protocol (DHCP). The "Ethernet" is the NAT and the "Ethernet2" is the Internal Network.

![Network Adapter](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(62).png)
![Network Adapter](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(60).png)

After Figuring out which NIC is which I now had to configure the Internal network adapter (Internal_X) and assign it an IPv4 address of 172.16.0.1 and I didn't give it a default gateway because the DC is the gateway. For the DNS server address I assigned it a loopback address of 127.0.0.1 so that it pings it self as the Active Directory will install the DNS.

![Internal NIC](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(58).png)
![Internal NIC](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(57).png)

So after configuring the Internal NIC I renamed the PC name so it doesn't have a long complicated name.

![Rename PC](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(59).png)

After renaming the PC name and also restarting the machine I began with the process of downloading Active Directory on my VM. So I clicked the option 2 on the dashboard of the server manger which was "Add roles and features" and a pop-up wizard of "Add Roles and Features" appeared. So I clicked the next button on the next section I checked if the "Role-based or feature-based installation" is choosen then clicked next button. On the Server Selection section I selected the DC your server as the destination server then clicked next then I choose the Active Directory Domain Services and clicked "Add Features" and proceed to click next till the install button and clicked it.

![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(56).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(55).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(54).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(53).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(52).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(50).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(49).png)
![Active Directory](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(48).png)

So now I installed Active Directory Domain Service but I never actually set the server as the domain controller so I had to create the domain. So I clicked the icon at the top right that has a orange warning icon, I clicked the "Promote the server to a domain controller" then a Active Directory Domain Services Configuration Wizard will pop-up. In the first section I selected "Add a new forest" and the Root domain name is "mydomain.com" then clicked next. In the following section I entered a password after that I clicked next till the install button and clicked it I was then forced to restart. Then when I log back in you can see that the domain is created successfully.

![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(47).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(46).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(45).g)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(44).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(43).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(42).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(41).png)
![Domain Controller](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(40).png)

So now the is a built in admin account but I will create a dedicated domain admin account and give it the admin priviledges to do so I have to go to the "Active Directory Users and Computers" then right click on the the "mydomain.com". Choose the option Orgaizational Unit in the New Tab and then create the user then click next after creating the user I then right clicked on the user and choose to see the properties and then go to the "Member Of" section and give the user I created the Domain admin permission. After doing so I signed out the server and logged back in as the user.

![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(39).png)
![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(37).png)
![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(36).png)
![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(35).png)
![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(34).png)
![User Creation](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(32).png)

Now I need to install and configure the RAS/NAT so that my Windows10 client computer will be able to access the internet rhrough the internal network via the Domain Controller. So I clicked the next button on the next section I checked if the "Role-based or feature-based installation" is choosen then clicked next button. On the Server Selection section I selected the DC your server as the destination server then clicked next then I choose the "Remote Access" then clicked next till the the role services where you will select the checkbox of "Routing" then I clicked next till the install buttona and clicked it.

![RAS/NAT](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(31).png)
![RAS/NAT](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(30).png)
![RAS/NAT](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(29).png)
![RAS/NAT](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(28).png)
![RAS/NAT](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(27).png)

Now that the role is installed I needed to configure the Routing and Remote Access. So now I had navigated to the Server Manger Dashboard and click the option "Tools" on the right corner and pick the option "Routing and Remote Access". A pop-up of the "Routing and Remote Access" appeared now I right clicked the "DC (local)" and pick the option "Configure and Enable Routing and Remote Access". Then click next and on the next section I picked the option "Network address translation (NAT)" and then I click next and after in the NAT internet connection section I picked the first option which is using public interface to connect to the internet then I clicked the next button till a finish button appears and then I clicked it.

![RAS/NAT Configuration](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(26).png)
![RAS/NAT Configuration](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(25).png)
![RAS/NAT Configuration](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(24).png)
![RAS/NAT Configuration](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(23).png)

So now that Remote access is installed and configured, it is now time to install a DHCP server. This will allow our windows 10 clients to be assigned an IP address and allow them to browse the internet.  The whole purpose of DHCP is to allows computers on the network to automatically be assigned an IP address. The scope I will be creating will give assign IP addresses in a range, the range being 172.16.0.100-200 the amount of time the IP addresses can be leased out to 8. A lease is just an amount of time an IP address can be owned (leased) by a device.

![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(22).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(21).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(20).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(19).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(18).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(17).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(16).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(15).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(14).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(13).png)
![DHCP](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(12).png)

So now as my Active Directory and my Domain Controller is configured as welL, I used a PowerShell script to create over 1000 user accounts but first I needed remove the restriction of the ExecutionPolicy. Then after I could run the script so the script would create a user with a password of "@AdminPasswd1" then it would get the name of the user based on the space between the first name and last name so it would split it based on the space and for the username it would use the first character of the first name of the user then concatinate that with the last name. We will see that after the scripts fully runs the will be 1052 users.

![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(10).png)
![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(8).png)
![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(7).png)
![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(6).png)
![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(5).png)
![PowerShell script](https://github.com/ofentse579/Images/blob/main/Active%20Directory/Active%20Directory%20(4).png)

## Conclusion

So this lab gave me hands-on experience with configuring an Active Directory and Domain Controller and it also simulates a business environment. 

