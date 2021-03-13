# Wordpot Logging / Log Forwarding

##### HPFEEDS
- The log files generated in log/wordpot.log only show when a new session is started by default
- The only other output in wordpot.log is "hpfeed disabled" 
    - When ENABLE HPFEEDS is set to True in wordpot.conf, the program will not compile
    - Open Issue: [github.com/gbrindisi/wordpot/issues](https://github.com/gbrindisi/wordpot/issues)
    - Currently working on fixing this issue

##### Logs via Stdout Work Around
- Wordpot generates decent logs of any interaction with the site to stdout by default
    - Redirect to log file
         ```
         python3 wordpot.py |& tee -a wordpot_stdout.log &
         ```
##### Rsyslog Forwarding

- Ensure Rsyslog is downloaded on both the client and server
    ```
    apt install rsyslog
    ```
    
- Client
    - Navigate to Rsyslog.d directory    
        ```
        cd /etc/rsyslog.d
        ```
    - Create a .conf file for wordpot logs 
        ```
        vim wordpot-log.conf
        ```
        ```
        $ModLoad imfile
        $InputFilePollInterval 10
        $InputFileName /opt/wordpot/wordpot_stdout.log
        $InputFileTag wordpot-access:
        $InputFileStateFile stat-wordpot-access
        $InputFileSeverity Info
        $InputFileFacility local3
        $InputRunFileMonitor
        local3.* @@<ipaddress>:<port>
        ```
    - Edit the rsyslog.conf file located in /etc
        - Forward logs from all facilities to <ip> on port 514
            ```
            *.* @<server_ipaddress>:514
            ```
   - Confirm the file is configured correctly
        ```
        rsyslogd -f /etc/rsyslog.conf -N1
        ```
    - Restart rsyslog
        ```
        systemctl restart rsyslog
        systemctl start rsyslog
        ```


 - Server
    - Edit the rsyslog.conf file located in /etc    
        ```
        vim /etc/rsyslog.conf
        ```      
        - Ensure UDP and/or TCP reception are enabled
            ```
            $ModLoad imudp
            $UDPServerRun 514
            
            module(load="imtcp")
            input(type="imtcp" port="514")
            ```   
        - Add rules from procesing the remote logs
            ```
            $template remote-incoming-logs,"/var/log/%HOSTNAME%/%PROGRAMNAME%.log"
            *.* ?remote-incoming-logs
            & ~
            ```   
    - Confirm the file is configured correctly
        ```
        rsyslogd -f /etc/rsyslog.conf -N1
        ```
    - Restart rsyslog
        ```
        systemctl restart rsyslog
        systemctl start rsyslog
        ```   
- The logs should now be forwarded to the ip specified as the rsyslog server, and located in the /var/logs folder as "wordpot-access.log"
