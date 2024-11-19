For set up 3 user roles:
Steps:
 1. Sudo su (be root)
 2. Sudo useradd admin
 3. Sudouseradd developers (editor)
 4. Sudouseradd viewer (quest)
 5. mkdir folder
 6. touch file1
 7. chown admin developer guest file1
 8. chmod 770 file1
 9. chmod u=rwx g=rwx o=r 
 5. vi /etc/sudoers (add admin and developer as sudoers) 


 for Configure iptables rules to restrict SSH access to a specific IP range (10.24.168.2/16) and allow HTTP/HTTPS traffic.
 Steps:
  1. Sudo apt-get install iptables
  2. Sudo apt-get install iptables-persistent
  3. Sudo iptables (options)?
  4. /etc/iptables/rules.v4
  5. /etc/iptables/rules.v6
  6. sudo iptables -L
  its will show: sudo iptables -P INPUT DROP
                 sudo iptables -P Forward DROP
                 sudo iptables -P OUTPUT DROP
  7. sudo iptables -A INPUT -p tcp -s 10.24.168.2/16 --dport 22 -m conntract --ctstate New, ESTABLSHED -j ACCEPT
  8. sudo iptables -A OUTPUT -p tcp --sport 22 -m conntrack --cstate ESTABLSHED -j ACCEPT
  9. sudo iptables -A INPUT -p tcp --dport 80 -m conntract --ctstate New, ESTABLSHED -j ACCEPT
  10. sudo iptables -A OUTPUT -p tcp --sport 80 -m conntrack --cstate ESTABLSHED -j ACCEPT
  11. sudo iptables -A INPUT -p tcp --dport 443 -m conntract --ctstate New, ESTABLSHED -j ACCEPT
  12. sudo iptables -A OUTPUT -p tcp --sport 443 -m conntrack --cstate ESTABLSHED -j ACCEPT
  13. sudo iptables -A INPUT -i lo -j ACCEPT
  14. sudo iptables -A OUTPUT -o lo -j ACCEPT
  15. sudo iptables -A INPUT -p tcp --dport 22 -j DROP
  16. sudo iptables-save > /etc/iptables/rules.v4
  For Set up a cron job and do other things from task, I need:
   Steps:
    1. sudo mkdir -p /backup
    2. sudo chown root:root /backup
    3. sudo chmod 700 /backup
    4. sudo nano /usr/local/bin/backup.sh  -#!/bin/bash (we add this script)
    5. sudo chmod +x /usr/local/bin/backup.sh
    6. sudo crontab -e    02*** /usr/local/bin/backup.sh  save and close
    7. sudo /usr/local/bin/backup.sh    for Verify.