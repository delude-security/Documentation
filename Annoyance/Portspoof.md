# Portspoof
Portspoof Webpage: [portspoof.org](http://portspoof.org/) *Access to this resource is denied
[http://drk1wi.github.io/portspoof/](http://drk1wi.github.io/portspoof/)
Github: [github.com/drk1wi/portspoof](https://github.com/drk1wi/portspoof)
ADHD: [adhdproject.github](https://adhdproject.github.io/#!Tools/Annoyance/Portspoof.md)

Definition
   -  Goal of the program is to make the reconnaissance phase slow and bothersome for your attackers as much it is possible by emulating services
        -   All TCP ports are always open, and emulate a service
            - Portspoof has a huge dynamic service signature database, which will be used to generate responses to your offenders scanning software service probes 
        -   During TCP handshake, when server request is made, Portspoof with return SYN+ACK for every port connection     attempt instead of CLOSED or FILTERED
        - Scanning software usually tries to determine a service that is running on an open port. Portspoof will respond to every service probe with a valid service signature, which is dynamically generated based on a service signature regular expression database.

            - As a result an attacker will not be able to determine which port numbers your system is truly using.



# Implimentation


Installation:

- Install Location: 
    ```sh 
    /usr/local/bin/portspoof
    ```
- Config File Location: 
    ```sh 
    /usr/local/etc/portspoof.conf
    /usr/local/etc/portspoof_signatures
    ```

Usage: [List of Portspoof usage options](https://adhdproject.github.io/#!Tools/Annoyance/Portspoof.md#Usage)

    ~# portspoof -h
    
- Portspoof, when run, listens on a single port by default, port 4444
    
    - Use the following iptables cmd to redirect every packet sent to any port to port 4444
        ```sh 
        ~# iptables -t nat -A PREROUTING -p tcp -m tcp --dport 1:65535 -j REDIRECT --to-ports 4444
        ```
    - Then run Portspoof with no options, which defaults it to "open port" mode. This mode will just return OPEN state for every connection attempt.
        ```sh 
        ~# portspoof
        ```
    - An NMap scan of your system will now show all ports as open
- Example of How to Start Portspoof: [Starting_Portspoof](https://adhdproject.github.io/#!Tools/Annoyance/Portspoof.md#Example_1:_Starting_Portspoof)
- Example of How to Spoof Service Signatures: [Spoofing_Service_Signatures](https://adhdproject.github.io/#!Tools/Annoyance/Portspoof.md#Example_2:_Spoofing_Service_Signatures)
- Example of How to Clean Up and Reset ADHD: [Cleaning_Up](https://adhdproject.github.io/#!Tools/Annoyance/Portspoof.md#Example_3:_Cleaning_Up)



