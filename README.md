# FTCForumTools
## Forum tools, documentation &amp; scripts

As part of a set of server security measures, maintaining a IP blacklist can be the final resort for repeat offenders.

This Blacklist system uses IPTables to provide IP bans. Github is used to ease copying and installation of the latest list.

It is a simple system to operate, it does not make the bans permanent. If you need to reboot you will have to create your own script or re apply the banlists manually.

The add file contains a line adding each banned IP address, which is run on the server. The drop file is then run to remove the list, before adding a full updated list, for instance. 

##  Using the banlist : 

git clone https://github.com/wrapperband/FTCForumTools   
  
cd ~/FTCForumTools/IPBlocklist  
  
chmod +x IPBlocklist-add.sh  
  
chmod +x IPBlocklist-drop.sh  
  
### To add the bans :  
sudo ./IPBlocklist-add.sh  
  
### To clear the bans :    
sudo ./IPBlocklist-drop.sh  
  
### To update to the latest banlist  
  
cd ~/FTCForumTools/IPBlocklist  
  
sudo ./IPBlocklist-drop.sh  
  
cd ~/FTCForumTools  
  
git remote update  
  
cd ~/FTCForumTools/IPBlocklist  
  
sudo ./IPBlocklist-add.sh  
  
###  For information on the ban's status, you can run :   
  
sudo iptables -L  
  
###  To clear all IPTables bans, if something went wrong :  
  
iptables -F  
iptables -X  
iptables -t nat -F  
iptables -t nat -X  
iptables -t mangle -F  
iptables -t mangle -X  
iptables -P INPUT ACCEPT  
iptables -P FORWARD ACCEPT  
iptables -P OUTPUT ACCEPT  
   
###  To clear stubborn connections :  
  
Sometimes connections that were made, within a range of IPs, will remain after being banned. If there was some connection in that "IP band" already.  
In that case try this to remove stubborn connections ...
  
tcpkill host xxx.xxx.xxx.xxx  
  
###  Other useful IPRules   
  
see FTCForumTools/IPBlocklist/IPRules.txt  
  
### What to do if IPs aren't being blocked?  
  
One reason IPs might be getting through is because the  web server has additional rules in place. For instance to redirect traffic.  
  
With the -A option the rules are appended to iptables, and as other rules already in place could pass the traffic (match the packets), further never will be blocked by the simple rules.   
   
You can do a global replace to modified the IPBlocklist-add so the lines look like this, so the new rules start at 5 .. :  
   
iptables -I INPUT 5 -s xxx.xxx.xxx.xxx -j DROP  
  
This way, using -I, the first 4 lines in the existing iptables are kept, then reject spam IPs as the blocklist is implemented and after that. Then iptables accepts the rest as regular traffic. You can set your own level appropriatly, depending how many other rules are in place.  
  
You can change the -I INPUT 1 -s to -A INPUT -s, if you don't need that flexibility.  
  
