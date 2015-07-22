# FTCForumTools
Forum tools, documentation &amp; scripts

As part of a set of server security measures, maintaining a IP blacklist can be the final resort for repeat offenders.

This Blacklist system uses IPTables to provide IP bans. Github is used to ease copying and installation of the latest list.

It is a simple system to operate, it does not make the bans permanent. If you need to reboot you will have to create your own script or re apply the banlists manually.

The add file contains a line adding each banned IP address, which is run on the server. The drop file is then run to remove the list, before , say, adding a full updated list. 

##  Using the banlist : 

git clone https://github.com/wrapperband/FTCForumTools   
  
cd ~/FTCForumTools/IPBlacklist  
  
chmod +x IPBlacklist-add.sh  
  
chmod +x IPBlacklist-drop.sh  
  
### To add the bans :  
sudo ./IPBlacklist-add.sh  

### To clear the bans :  
sudo ./IPBlacklist-drop.sh  

##  For information on the ban's status, you can run :

sudo iptables -L


##  To clear all IPTables bans, if something went wrong :  

iptables -F  
iptables -X  
iptables -t nat -F  
iptables -t nat -X  
iptables -t mangle -F  
iptables -t mangle -X  
iptables -P INPUT ACCEPT  
iptables -P FORWARD ACCEPT  
iptables -P OUTPUT ACCEPT  

##  To clear stubborn connections :  

Sometimes connections that were made, within a range of IPs, will remain after being banned. If there was some connection in that "IP band" already.

In that case try this to remove stubborn connections ...

tcpkill host xxx.xxx.xxx.xxx
