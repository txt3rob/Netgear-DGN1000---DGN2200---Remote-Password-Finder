Netgear-DGN1000---DGN2200---Remote-Password-Finder
==================================================

PHP to get admin username and password of DGN1000 to DGN2000


put index.php and submit.php in your web directory

Submit a IP of a vunerable router and it will give you the admin password to login.




Unauthenticated command execution on Netgear DGN devices
========================================================
 
[ADVISORY INFORMATION]
Title:    Unauthenticated command execution on Netgear DGN devices
Discovery date: 01/05/2013
Release date:   31/05/2013
Credits:        Roberto Paleari (roberto@greyhats.it, twitter: @rpaleari)
 
[VULNERABILITY INFORMATION]
Class:           Authentication bypass, command execution
 
[AFFECTED PRODUCTS]
This security vulnerability affects the following products and firmware
versions:
   * Netgear DGN1000, firmware version < 1.1.00.48
   * Netgear DGN2200 v1
Other products and firmware versions are probably also vulnerable, but they
were not checked.
 
[VULNERABILITY DETAILS]
Attackers can leverage this vulnerability to bypass existing authentication
mechanisms and execute arbitrary commands on the affected devices, with root
privileges.
 
Briefly, the embedded web server skips authentication checks for some URLs
containing the "currentsetting.htm" substring. As an example, the following URL
can be accessed even by unauthenticated attackers:
 
http://<target-ip-address>/setup.cgi?currentsetting.htm=1
 
Then, the "setup.cgi" page can be abused to execute arbitrary commands. As an
example, to read the /www/.htpasswd local file (containing the clear-text
password for the "admin" user), an attacker can access the following URL:
 
http://<target-ip-address>/setup.cgi?next_file=netgear.cfg&todo=syscmd&cmd=cat+/www/.htpasswd&curpath=/&currentsetting.htm=1
 
Basically this URL leverages the "syscmd" function of the "setup.cgi" script to
execute arbitrary commands. In the example above the command being executed is
"cat /www/.htpasswd", and the output is displayed in the resulting web
page. Slightly variations of this URL can be used to execute arbitrary
commands.
 
[REMEDIATION]
For DGN1000, Netgear included a fix for this issue inside firmware version
1.1.00.48. According to Netgear, DGN2200 v1 is not supported anymore, while v3
and v4 should not be affected by this issue; these versions were not tested by
the author.
 
[DISCLAIMER]
The author is not responsible for the misuse of the information provided in
this security advisory. The advisory is a service to the professional security
community. There are NO WARRANTIES with regard to this information. Any
application or distribution of this information constitutes acceptance AS IS,
at the user's own risk. This information is subject to change without notice.
