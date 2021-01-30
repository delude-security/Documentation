# DenyHosts

GitHub/Source Code: [github.com/denyhosts/denyhosts](https://github.com/denyhosts/denyhosts)
ADHD: [adhdproject/Annoyance/DenyHosts.md](https://adhdproject.github.io/#!Tools/Annoyance/DenyHosts.md)
Website: [denyhosts.sourceforge.net/](http://denyhosts.sourceforge.net/)

Definition
   - Script intended to prevents SSH server brute force attacks
   - Upon discovering a repeatedly malicious host, DenyHosts prevents future break-in attempts from that host using iptables, PF firewall, or updating the /etc/hosts.deny file
   - Options to log/notify all suspricious activity / thwarted abuse
     - Tracks non-existent and existing users when login attempt fails
     - Tracks offending hosts / suspicious logins (logins by a host with many failed attempts)
     - Parses /var/log/secure to find all login attempts and filters failed and successful attempts
    - DenyHosts 2.0 introduces synchronization mode which allows DenyHosts daemons to proactively thwart attackers before they strike your ssh server.
        - Since the release of DenyHosts 2.0 (late January) DenyHosts has thwarted over 205,000 hack attempts (39,000 unique) from over 150 countries

# Implimentation


Dependencies:
- The DenyHosts software depends on the "ipaddr" Python module, which is available in most Linux and BSD repositories. Python v2.3 or greater
- sshd server configured with tcp_wrappers support enabled

Installation:
- Additional installation /troubleshooting documentation and source / binary distributions can be found on the [github](https://github.com/denyhosts/denyhosts)

- Install Location: 
    ```sh 
   /opt/denyhosts
   /usr/share/denyhosts/
    ```
- Execute the following or download the [source distribution file](https://github.com/denyhosts/denyhosts)
    ```sh 
   ~$ wget https://github.com/denyhosts/denyhosts/releases/download/v3.1/DenyHosts-3.1.2.tar.gz
   ~$ tar zxvf DenyHosts-3.1.tar.gz
    ```
- The rest of the install process requires elevated privileges. You can either switch to root, or run the following commands with sudo.
    ```sh 
    ~# mv DenyHosts-3.1 /opt
    ~# cd /opt/DenyHosts-3.1
    ~# python3 setup.py install
    ~# cp denyhosts.conf /etc
    ~# cp denyhosts.py /usr/bin
    ```
- To enable DenyHosts, simply start its service.
    ```sh 
   ~$ sudo /opt/denyhosts/daemon-control start
    ```  
    - The /etc/denyhosts.conf file can be edited to configure its behavior.

Usage:
- Option to run in daemon mode (Recommended)
- A majority of DenyHosts’ configurations can be made by editing the configuration file
/etc/denyhosts.conf.
- Example: [Basic DenyHost Configuration](https://adhdproject.github.io/#!Tools/Annoyance/DenyHosts.md)