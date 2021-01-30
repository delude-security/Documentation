# Honey Ports

GitHub/.py file: [github.com/adhdproject/honeyports](https://github.com/adhdproject/honeyports)
ADHD: [adhdproject/Annoyance/HoneyPorts.md](https://adhdproject.github.io/#!Tools/Annoyance/HoneyPorts.md)

Definition
   -  This script listens on a port. When a full connection is made to that port Honeyports will create a firewall rule instantly blocking the source IP address. Currently works on Windows, Linux and OS X with the built-in firewalls.

Limitation
   -  Vulnerable to MITM attacks (spoofing an ip address, trying to connect, automatically triggers rule rejecting the spoofed ip). Implement in addition to MITM protection or careful monitoring of created firewall rules. 



# Implimentation

Dependencies:
- Currently works on Windows, Linux and OS X with the built-in firewalls
- Honeyports is a python program: [honeyports.py](https://adhdproject.github.io/#!Tools/Annoyance/HoneyPorts.md)

Installation:
- Install Location: 
    ```sh 
    /opt/honeyports/
    ```

Usage:

- Change to the Honeyports directory and execute the latest version of the script:
    ```sh 
    ~$ cd /opt/honeyports
    /opt/honeyports$ python3 ./honeyports.py
    ```
    
- Monitor a port using HoneyPorts [Example 1](https://adhdproject.github.io/#!Tools/Annoyance/HoneyPorts.md#Example_1:_Monitoring_A_Port_With_HoneyPorts)
   
    - From the honeyports directory, run
    ```sh 
    /opt/honeyports$ sudo python3 ./honeyports.py -p 3389 -h localhost
    ```
    - We can confirm that the listening is taking place with lsof
    ```sh 
    /opt/honeyports$ sudo lsof -i -P | grep python
    ```

- Example of blacklisting in action [Example 2](https://adhdproject.github.io/#!Tools/Annoyance/HoneyPorts.md#Example_2:_Blacklisting_In_Action)


- Example of Spoofing TCP (MITM attack) [Example 3](https://adhdproject.github.io/#!Tools/Annoyance/HoneyPorts.md#Example_3:_Spoofing_TCP_Connect_for_Denial_Of_Service)



