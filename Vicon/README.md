Originally disclosed on July 28, 2016  
https://www.securityfocus.com/archive/1/539037  
  
Title
------
Vicon Network Cameras - Authentication Bypass  
  
Author
------
Reginald Dodd / Information Security Engineer  
https://www.linkedin.com/in/reginalddodd
  
Vendor
------
Vicon Industries Inc.  
http://www.vicon-security.com  
http://www.vicon-security.com/products/network-cameras/  
  
Description
------
Remote unauthenticated users can add an administrator, operator, or guest accounts to various Vicon network cameras by navigating directly to a specific URL. The URL is missing authentication and gives you direct access to the form that creates new accounts. URL: http://<IP>/system/user_pop.php?method=add&ptz_use=0 . With an account, a user can view the live video and alter camera settings.  
  
Affected Products and Versions
------
Confirmed in products: V920D, V922D, and V-CELL-HD  
  
It is assumed that many more products are affected because the issue was tracked to a single web template that is used in many products of their network cameras. After referencing this issue with the vendor, the vendor supplied a firmware release note (Dated March 2015) that showed many products and their possible vulnerable firmware versions and the fixed firmware versions:  
  
V-CELL-IP; V660V-P (Europe) - Version T2_V2.7.3 and prior  
V920D and V921D - Version T4_V2.1.6 and prior  
V922D, V923D, V-CELL-HD, V921B, V922B, V923B, CE202D-N and CE202D-WN - Version T6_V1.9.4 and prior  
V905-CUBE - Version T5_V2.4.3 and prior  
CE102D-NIR and CE102B-NIR - Version T8_V1.4.3 and prior  
SN663V, SN680D-WNIR - Version X1_1.4.9 and prior  
SN663V-A, SN680D-A-WNIR - Version X2_1.2.1 and prior  
  
Solution
------
Check this url, http://[IP]/system/user_pop.php?method=add&ptz_use=0, of your ip camera(s). If you can add new accounts with no basic authentication prompt, then update the firmware. A fix is available. Users have to manually update each camera.  
  
References
------
http://www.vicon-security.com/Software/Vicon_Camera/V9xxCameras_3-15_Firmware-updated_Release_Notes.pdf  
