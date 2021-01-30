# Cowrie

Full List of Documentation: [cowrie.readthedocs](https://cowrie.readthedocs.io/en/latest/index.html)
GitHub/Source Code: [github.com/adhdproject/cowrie](https://github.com/adhdproject/cowrie)
ADHD: [adhdproject.github/Annoyance/Cowrie.md](https://adhdproject.github.io/#!Tools/Annoyance/Cowrie.md)

Definition
   -  Fake SSH Server and Telnet honeypot 
   -  Logs brute force attacks and shell interactions performed by attacker
   -  Features:
        - Choose to run as an emulated shell (default)
            - Fake filesystem with the ability to add/remove files. A full fake filesystem resembling a Debian 5.0 installation is included
            - Possibility of adding fake file contents so the attacker can cat files such as /etc/passwd. Only minimal file contents are included
            - Cowrie saves files downloaded with wget/curl or uploaded with SFTP and scp for later inspection
        - Or proxy SSH and telnet to another system
            - Run as a pure telnet and ssh proxy with monitoring
            - Or let Cowrie manage a pool of Qemu emualted servers to provide the systems to login to


# Implimentation

Dependencies:
- Software required:
    - Python 3.5+
    - python-virtualenv
    - Full list of dependencies: [requirements.txt](https://github.com/cowrie/cowrie/blob/master/requirements.txt)

Installation:
- Install Location: 
    ```sh 
   /opt/cowrie
    ```

Usage:

- Cowrie has basically has two parts you need to be aware of:
    - A config file
    - A launch script
- The config file is located at
    ```sh 
    /opt/cowrie/cowrie.cfg
    ```
- By default Cowrie listens on port 2222 and emulates an ssh server
- To run Cowrie, cd into the Cowrie directory and execute
    ```sh 
    ~$ cd /opt/cowrie
    ~$ ./bin/cowrie start
    ```

- Example of Cowrie in action [Example_2:_Cowrie_In_Action](https://adhdproject.github.io/#!Tools/Annoyance/Cowrie.md#Example_2:_Cowrie_In_Action)


- Example of Cowrie's logs [Logging in Cowrie](https://adhdproject.github.io/#!Tools/Annoyance/Cowrie.md#Example_3:_Viewing_Cowrie's_Logs)



