# Wordpot Logging / Log Forwarding

##### HPFEEDS
- The log files generated in log/wordpot.log only show when a new session is started by default

![image](https://user-images.githubusercontent.com/78045843/114895842-d281fe80-9ddd-11eb-8866-344d876a2147.png)

- The only other output in wordpot.log is "hpfeed disabled" 
    - When ENABLE HPFEEDS is set to True in wordpot.conf, the program will not compile
    - Open Issue: [github.com/gbrindisi/wordpot/issues](https://github.com/gbrindisi/wordpot/issues)
    - Currently working on fixing this issue

##### Logs via Stdout Work Around
- Wordpot generates decent logs of any interaction with the site to stdout by default
    - Redirect std to a log file when running wordpot.py
         ```
         python3 wordpot.py |& tee -a wordpot_stdout.log &
         ```
    - This was the temporary work around we used to ensure logs could be collected and forwarded to logstash. It appears that the string are being cut-off early. Additional efforts should be made to enable hpfeeds or allow for more complete logging should wordpot be used in the future. 
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
        - "@@" sends via TCP to the ip of the server with either rsyslogd or logstash listening
        - I first established that logs were recieved by the server running rsyslogd, at which point I disabled rsyslogd to allow logstash to listen for those logs. 
    - Edit the rsyslog.conf file located in /etc
        - Forward logs from all facilities to <ip> on port 5145
            ```
            *.* @<server_ipaddress>:5145
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
    - Note* configuring rsyslogd on the server is a somewhat redundant task, since you will be listening with logstash to send the logs to elastic. However, I initially set this up to verify logs were infact being sent by the rsyslog prior to messing with logstash pipelines
    - Edit the rsyslog.conf file located in /etc    
        ```
        vim /etc/rsyslog.conf
        ```      
        - Ensure UDP and/or TCP reception are enabled
            ```
            $ModLoad imudp
            $UDPServerRun 5145
            
            module(load="imtcp")
            input(type="imtcp" port="5145")
            ```   
            ![image](https://user-images.githubusercontent.com/78045843/114897792-9354ad00-9ddf-11eb-9d2b-321d8377e4d7.png)
        - Add rules from procesing the remote logs
            ```
            $template remote-incoming-logs,"/var/log/%HOSTNAME%/%PROGRAMNAME%.log"
            *.* ?remote-incoming-logs
            & ~
            ```   
            ![image](https://user-images.githubusercontent.com/78045843/114897902-ae272180-9ddf-11eb-93c4-4a6d9a6fc043.png)
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


##### Sending Wordpot logs to Logstash

After verifying that logs were being successfully sent by the wordpot server via rsyslog and recieved over port 5145 by the logstash server running rsyslogd, I turned off rsyslogd to allow logstash to begin listening on port 5145. 
- Initially we attempted to add rules for wordpot to the existing config files (input and output). 
- ![image](https://user-images.githubusercontent.com/78045843/114899303-d8c5aa00-9de0-11eb-8298-3d46e32c4f37.png)
    -   However, we ran into an unknown error where the logs would not send using rules within these config files. When we ran logstash from the command line and used the "-e" flag to hand in input and output rules, the logs were successfully processed as input and sent to output. 
    ```
    /usr/share/logstash/bin/logstash -e 'input { tcp { type => "wordpot" port => 5145 } } output { if [type] == "wordpot" { stdout {} elasticsearch { hosts => ["http://localhost:9200"] index => "wordpot" } } }'
    ```
        - Listen for logs of type "wordpot" on port 5145
        - Output logs to stdout
        - Output logs to elasticsearch with index "wordpot"
        
- Elastic logs were recieved only when handed pipeline rules seperate from the config files in pfelk/conf.d/
    
![image](https://user-images.githubusercontent.com/78045843/114899867-55588880-9de1-11eb-93f1-675e3e394344.png)

##### Pipeline Work Around
- To work around this issue, we created a dedicated wordpot pipeline
    - Create wordpot directory within conf.d 
    ```
    mkdir /etc/pfelk/conf.d/wordpot
    ```
    - Add a single config file with input / output rules to recieve logs over port 5145 and output logs to elasticsearch
    ```
    vim wordpot_simple.conf
    ```
     ![image](https://user-images.githubusercontent.com/78045843/114900955-56d68080-9de2-11eb-89f2-455f95466387.png)

- Edit the pipelines.yml file to create an additional pipeline for wordpot
    ```
    vim /etc/logstash/pipelines.yml
    ```
    ![image](https://user-images.githubusercontent.com/78045843/114901345-b339a000-9de2-11eb-8521-d224bc4fa38e.png)

- Logs should now be sent to elasticsearch with index "wordpot" when starting up logstash normally
    ```
    systemctl restart logstash
    ```
    or
    ```
    /usr/share/logstash/bin/logstash -f /etc/pfelk/conf.d
    ```





    

