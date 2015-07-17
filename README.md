# FTCForumTools
Forum Documentation &amp; scripts

As part of a set of server security measures, maintaining a IP blacklist can be the final resort for repeat offenders.

This Blacklist system uses IPTables to provide IP bans. Github is used to ease copying and instalation of the latest list.

The add file contains a line adding each banned IP address, which is run on the server. The drop file is then run to remove the list, before , say, adding a full updated list. 


git clone https://github.com/wrapperband/FTCForumTools

cd IPBlacklist

chmod +x IPBlacklist-add.sh

chmod +x IPBlacklist-drop.sh

sudo ./IPBlacklist-add.sh


For information on the bans you can run :

sudo iptables -L

To clear all IPTables bans, if something went wrong :


