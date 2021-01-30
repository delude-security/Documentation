# Artillery

GitHub/SourceCode: [github.com/BinaryDefense/artillery](https://github.com/BinaryDefense/artillery)
ADHD: [adhdproject.github/Artillery.md](https://adhdproject.github.io/#!Tools/Annoyance/Artillery.md)
Binary Defense: [binarydefense.com](https://www.binarydefense.com/)


Definition
   -  The purpose of Artillery is to provide a combination of honeypot, file-system monitoring, system hardening, real-time threat intelligence feed, and overall health of a server monitoring-tool; to create a comprehensive way to secure a system
- Project Artillery will monitor the filesystem looking for indicators of change. If one is detected, an email is sent to the server owner.
    - (Linux only) Artillery monitors the folders you specify, by default it checks /var/www and /etc for modifications
- Artillery also listens for rogue connections. If detected, a notification is sent to the server owner, and the offending IP address is banned using a Honey Port
- Monitors the SSH logs and looks for brute force attempts.(linux only)

# Implimentation

Installation:
- Supported Platforms: Windows/Linux


- Install Location: 
    ```sh 
    /var/artillery
    ```
- Config File location
    ```sh 
    /var/artillery/config
    ```
Usage:

- All options are set in the configuration file so there are no command
line arguments for Artillery.
- Be sure to edit the /var/artillery/configon Linux or \Program Files (x86)\Artillery\config on Windows to turn on mail delivery, brute force attempt customizations, and what folders to monitor.


- Run Artillery:
    ```sh 
    /var/artillery$ sudo python3 artillery.py
    ```

- Example - Running Artillery: [Running Artillery](https://adhdproject.github.io/#!Tools/Annoyance/Artillery.md#Example_1:_Running_Artillery)
- Example - Triggering a Honeyport: [Triggering_a_Honeyport](https://adhdproject.github.io/#!Tools/Annoyance/Artillery.md#Example_2:_Triggering_a_Honeyport)
- Example - Adding a File to a Watched Directory: [Adding_a_File_to_a_Watched_Directory](https://adhdproject.github.io/#!Tools/Annoyance/Artillery.md#Example_3:_Adding_a_File_to_a_Watched_Directory)