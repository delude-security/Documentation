# Bear Traps

GitHub/SourceCode: [github.com/chrisbdaemon/BearTrap](https://github.com/chrisbdaemon/BearTrap)
ADHD: [adhdproject.github.io/#!Tools/Annoyance/BearTrap.md](https://adhdproject.github.io/#!Tools/Annoyance/BearTrap.md)

Definition
   -  Beartrap is a portable network desense utility written entirely in Ruby. It opens "trigger" ports on the host that an attacker would connect to. When the attacker connects and/or performs some interactions with the trigger, an alert is raised and the attacker's ip address is potentially blacklisted. 
   -  ex. When user tries to remotely connect using FTP, beartrap automatically blocks the incoming IP address using iptables



# Implimentation

Dependencies:
- Ruby 1.9.x interpreter
	- Installation varies from system to system.
- getopt ruby gem
	- Install with:
	```sh
    $ gem install getopt
    ```

Installation:
- No installation required.  Simply edit the configuration file, config.yml.  It
should be fairly well documented and/or self-explanatory.  If its not, check
out the support section below.
- Install Location: 
    ```sh 
    /opt/beartrap/
    ```
- Config Location: 
    ```sh 
    /opt/beartrap/config.yml
    ```

Usage:

    $ ruby bear_trap.rb -c config.yml
    
- Running as root is recommended, as most blacklisting tools (pfctl, iptables,
etc) must be ran as root.
- Example of How to Test / Implement: [BearTrap.md#Example_1:_Basic_Usage](https://adhdproject.github.io/#!Tools/Annoyance/BearTrap.md#Example_1:_Basic_Usage)

Support:
- Email "chrisbdaemon@gmail.com" with BearTrap in the subject line




 

