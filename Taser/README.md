Originally disclosed on August 15, 2016  
https://www.securityfocus.com/archive/1/539211  
  
Title
------
Taser Axon Dock (Body-Worn Camera Docking Station) v3.1 - Authentication Bypass  
  
Credits & Author
------
Reginald Dodd  
https://www.linkedin.com/in/reginalddodd  
  
Vendor & Product
------
Taser International Inc.  
Axon Dock - Body-Worn Camera Docking Station  
https://www.axon.io/products/dock  

Summary
------
The Axon Dock is the camera docking station component of Taser's body-worn camera system. It charges body-worn cameras and automatically uploads videos to Taser's Evidence.com after body-worn cameras are stored onto it. System owners can remotely manage the dock through a web browser by navigating to http://<IP>. Remote unauthenticated users can obtain administrator access and reconfigure the Axon Dock.  
  
Description
------
The Axon Dock stores its core management files in the http://<IP>/lua/ directory. These files are not protected with basic authentication. Remote unauthenticated users can send HTTP POST requests to any of these files:  
* http://<ip>/lua/set-passwd.lua
* http://<ip>/lua/set-config.lua
* http://<ip>/lua/reset-reg.lua
* http://<ip>/lua/etm-reboot.lua
* http://<ip>/lua/ssl-regen.lua
* http://<ip>/lua/diag-cmd.lua
* http://<ip>/lua/dvr-update.lua
  
Once a HTTP POST request with the proper payload body is sent to those files, they will allow remote unauthenticated users to:  
* Change the password of the default and unchangeable user named "admin".
* Change the network configuration.
* Reveal body-worn camera owner real names, typically law enforcement officers.
* De-register a Axon Dock from Evidence.com to possibly disrupt or dissassociate video uploads.
* Reboot a Axon Dock.
* Regenerate the SSL certificate
* Run Diagnostics on the Axon Dock
* Update the firmware of the Axon Dock and any attached cameras
* Repair any attached cameras
* It was discovered that an intentionally hidden feature could allow users to transfer body-worn camera videos to any ftp server other than evidence.com. The HTML DIV tag of this feature was hidden with CSS (display:none). This feature uses ftp to transfer videos. It is accessible to remote unauthenticated users, as well. The device uses the /lua/set-config.lua file to enable this feature. I created a ftp server to test it. The ftp credentials were sent via the GUI and re-sent several times via Burp Suite. I was able to enable it, but it constantly showed as not being properly configured (red instead of green status). I did not notice any network traffic in wireshark on the ftp port of my ftp server. However, I did not have a body-worn camera available to accurately confirm that this feature does not work.

Affected Versions
------
Vulnerable Version(s): 3.1.160322.2252 and possibly all prior versions  
Fixed Version: Version 3.2.160726.1852  
  
Solution
------
Taser stated that they would centrally push out version 3.2.160726.1852 to all Axon Docks on August 8, 2016. If your dock is not updated, try to update the dock manually in the firmware section of the remote console. Contact Taser if you have any complications.  

Timeline
------
July 18-20,2016 - Discovered and validated with multiple exploits.  
July 21, 2016 - My findings and exploits were dislosed to Taser. They immediately acknowledged the issues.  
July 22, 2016 - Taser stated that a fix would be available in 2 weeks.  
July 31, 2016 - CVE-ID was requested from MITRE  
August 1, 2016 - MITRE denied the CVE-ID request  
August 8,2016 - Allegedly, the fix was to be centrally pushed on this day. Although, no docks were updated that were accessible to me.  
August 12,2016 - Received reports that some docks were updated with the fix.  
August 13, 2016 - Taser sent a confirmation email stating that "all" docks have been updated with the fix.  
August 15, 2016 - Public Disclosure.  
