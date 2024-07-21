---
layout: post
title: WSUS
description: This page will be kept updated.
excerpt_separator: <!--more-->
---

# **What is WSUS?**

- Windows Server Update Services (WSUS) is an update service that allows administrators to centrally manage the distribution of patches and security updates.

- It provides latest Microsoft product updates

- In WSUS/Updates/All updates section, there are catalogs of Update info. You can choose what to update and then approve.

  ![image](https://user-images.githubusercontent.com/37058233/113204119-bd27a480-9221-11eb-8892-7b3f1544689c.png)

- Computers can belong to small group. ==> Each group can have different update I think.

  ![prints.35](https://nedimmehic.files.wordpress.com/2017/07/prints-35.jpg?w=616) 

  

[Source - ms docs](https://docs.microsoft.com/en-us/windows-server/administration/windows-server-update-services/deploy/deploy-windows-server-update-services)

[Source - nedimmehic.org](https://nedimmehic.org/2017/09/11/how-to-install-and-configure-wsus-2016-part-2/)

# **How it is installed?**

The information in this section is from [Youtube channel 'InfoSec Pat'](https://www.youtube.com/channel/UCYuizWN2ac4L7CZ-WWHZQKw)

**Overall Process**

```
1. Configure IP ADdress and rename the server and join server to the domain
2. Install WSUS Role from the Server Manager.
3. Configure WSUS and GPO for the Servers.
4. Verify WSUS installation
```

## **1. Configure IP Address and rename the server and join server to the domain**

- **WSUS Computer:** Configure IP Address. This computer is not yet used as a WSUS. We are making this computer as a WSUS now!

  ![image](https://user-images.githubusercontent.com/37058233/114957616-3f18ef80-9e16-11eb-9e0f-eee9d66d3a24.png)

- **ADDS/DNS/DHCP Computer:** Add new computer which just joined our domain to 'Servers' group.

![image](https://user-images.githubusercontent.com/37058233/114764316-a94b6a80-9d18-11eb-9530-237059cc2a65.png)

- There is also a WSUS-Servers OU, and CORE computer is in. However, It is not dealt well in the video. I need to figure it out what the heck is this....

![image](https://user-images.githubusercontent.com/37058233/114960943-eb5dd480-9e1c-11eb-8134-66b483f211a5.png)?

## **2. Install WSUS Role from the Server Manager.**

- **WSUS Computer:** From server manager, click **'Add Roles and Features'** and add 'WSUS' role.

![image](https://user-images.githubusercontent.com/37058233/114764528-e6aff800-9d18-11eb-89fd-b8eb738c51a7.png)

![image](https://user-images.githubusercontent.com/37058233/114958488-f8c49000-9e17-11eb-816b-5fd73333f2f4.png)

- Select storage (where the contents for the updates are gonna be sitting) 

  <img src="https://user-images.githubusercontent.com/37058233/114765139-a735db80-9d19-11eb-8322-5e11ee8fafd2.png" width = 600>

## **3. Configure WSUS and GPO for the Servers.**

- **ADDS/DNS/DHCP Computer:**

  - Add new group policy 'WSUS'

  ![image](https://user-images.githubusercontent.com/37058233/114960201-69b97700-9e1b-11eb-98f2-4ca2d7eae874.png)

- **ADDS/DNS/DHCP Computer:**

  - Computer Configuration **=>** Policies **=>** Administrative Template **=>** Window Components **=>** Windows Update

  - 3 main settings ![image](https://user-images.githubusercontent.com/37058233/114765989-b406ff00-9d1a-11eb-8e65-9d873255a6d2.png)

    - 1. Configure Automatic Updates

    - 2. Specify intranet Microsoft update service location

      ​	-specify intra Microsoft update service (DNS server ip ) (port number is important)

    <img src="https://user-images.githubusercontent.com/37058233/114793958-5b4a5d00-9d40-11eb-8215-af62682e08a1.png" width =400>

    - 3. Automatic Updates detection frequency

- Attach new role to WSUS-Servers OU.

![image](https://user-images.githubusercontent.com/37058233/114795079-acf3e700-9d42-11eb-89ad-5804821dfe79.png)

## **4. Verify WSUS installation**

https://community.spiceworks.com/how_to/169570-how-to-install-and-configure-wsus-on-windows-server-2019

![image](https://user-images.githubusercontent.com/37058233/114795487-82565e00-9d43-11eb-9248-1f7f74be16fd.png)



![image](https://user-images.githubusercontent.com/37058233/114795525-9601c480-9d43-11eb-845c-9029c4891518.png)

## **What complaints people have for it?**

Source : [https://study.com/academy/lesson/windows-server-update-services-wsus-definition-uses-setup.html](https://study.com/academy/lesson/windows-server-update-services-wsus-definition-uses-setup.html)

- It is only supported on Windows Server (Expensive licensing required).
- It requires at least 4GB of memory to run (the more updates, the more RAM needed).
- It requires hundreds of GB to store downloaded updates. Additional selected products and update types increase this amount.
- The management database can occasionally be corrupted through normal usage, thus crashing the server and requiring cleanup and repair work to fix 

## **What commands do to try and fix clients?**

https://docs.microsoft.com/en-us/troubleshoot/mem/configmgr/troubleshoot-issues-with-wsus-client-agents

## **How to approve/disapprove updates?**

http://woshub.com/wsus-update-approvals/

[https://www.youtube.com/watch?v=OgiuKJyIp_g](https://www.youtube.com/watch?v=OgiuKJyIp_g)

![image](https://user-images.githubusercontent.com/37058233/114978723-7f8c6380-9e3e-11eb-8d11-3cd102939b83.png)

## **How to control what products are offered?**

https://documentation.solarwinds.com/en/success_center/patchman/content/spmag_selectmsproductsandclassifications.htm





# ---Unrelated---

## **Security**

- what you know - Password
  - based on word is good to remember and pretty secure. so like "mouse-orange-desktop" .
- who you are - biometrics
  - Fingerprint, your eyes 
- what you have - MFA (Multi Factor Authenticator)

## Exchange Admin Center

![image](https://user-images.githubusercontent.com/37058233/113214670-a76cac00-922e-11eb-8ab4-d60d61f2dabb.png)

- Mailboxes : Mails in box.

- Groups : When you want to send an email to certain group of people, It can be done by this feature.
- Resources : It keeps track of schedule for resource usage, so It is not double booked.
- Contacts : ?

[https://docs.microsoft.com/en-us/exchange/exchange-admin-center](https://docs.microsoft.com/en-us/exchange/exchange-admin-center)

https://docs.microsoft.com/en-us/exchange/architecture/client-access/exchange-admin-center?view=exchserver-2019

[Active Directory](https://www.youtube.com/watch?v=nKcrVtvZvpk)

----

## How to check win-up for computers

- go to WSUS server, and Tools-WSUS(The last one) and check