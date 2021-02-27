# Wordpot

GitHub/SourceCode: [github.com/adhdproject/wordpot](https://github.com/adhdproject/wordpot)
ADHD: [adhdproject.github.io/wordpot](https://adhdproject.github.io/#!Tools/Annoyance/Wordpot.md)
WikiPage: [wordpot/wiki/Plugins](https://github.com/gbrindisi/wordpot/wiki/Plugins)
Project Homepage: [Homepage](http://brindi.si/g/projects/wordpot.html)

Definition
   -  Wordpress honeypot that detects probes for plugins, themes, timthumb and other common files used to fingerprint a wordpress installation
        - Wordpot simulates a full install. Including fake installed themes and plugins

    - Note* Wordpot can be expanded with plugins to improve its behaviour or mimik a particular vulnerability.
        See [wordpot/wiki/Plugins](https://github.com/gbrindisi/wordpot/wiki/Plugins)(beta)
        - A plugin register itself to one or more hooks which are points triggered by incoming requests. When a hook is triggered it puts in execution every plugin attached to it

# Delude Wordpot Implementation

#### Pre-requisite:
- Wordpot can be run within a container for convienence. 
    - Create container within PVE:
        - Click "Create CT"
        - Select "debian-10.0-standard_10.0-1_amd64.tar.gz" from templates
        - Cores: 2
        - Memory: 1024
        - IPv4: DHCP
- Install pre-requisites within wordpot container
    - Update system
    ```sh 
     apt get-update
    ```
    - Install git
    ```sh 
     apt install git 
    ```
    - Install pip3
    ```sh 
     apt install python3-pip 
    ```
    - Navigate into /opt directory
    ```sh 
     cd /opt
    ```
    - Install wordpot
    ```sh 
    git clone https://github.com/adhdproject/wordpot
    ```
    - Install requirements located in requirements.txt in wordpot directory
    ```sh 
    cd wordpot
    pip3 install -r requirements.txt
    ```
    - Install python virtual environment
    ```sh 
     apt-get install python3-venv
    ```
    - Activate virtual environment
    ```sh 
    source venv/bin/activate
    ```
    - If prompted, install flask
    ```sh 
    pip3 install flask
    ```
- You are now able to run your wordpot
   - Ex. Listen on all addresses (default port 80) with title "HelloWorld". Run as background process.
    ```sh 
    python wordpot.py --host=0.0.0.0 --title=HelloWorld &
    '''
#### Usage:

- To run the script, first cd to the wordpot directory.
    ```sh 
    ~$ cd /opt/wordpot
    ```
- And run the application
    ```sh 
    (venv) root@wordpot:/opt/wordpot# python wordpot.py --help
    ```
- This will show you the help dialog.
- - All command line settings (host, port title, theme, spoofed plugins and themes, etc) can be automatically set by editing the wordpot.conf file

# Example

Running A fake Wordpress Install: [Example 1: Running a fake Wordpress install¶](https://adhdproject.github.io/#!Tools/Annoyance/Wordpot.md#Example_1:_Running_a_fake_Wordpress_install)
- Wordpot runs by default without any additional configuration required.
Simply run the script with whatever command line arguments you need for
your situation. With ADHD, by default you should have apache listening
on port 80. So you might need to specify an alternative port number, or
to disable apache for the time that you're running this script.
    ```sh 
    /opt/wordpot$ python ./wordpot.py --port=4444
    ```
- You can view your fancy new fake wordpress install by opening your web
browser and navigating to "http://localhost:4444"

# Full Install Command History
  259  virtualenv
  260  apt install python3-virtualenv
  261  ls
  262  mkdir wordpot_test
  263  cd wordpot_test/
  264  git clone https://github.com/adhdproject/wordpot
  265  cd wordpot/
  266  ls
  267  virtualenv
  268  which virtualenv
  269  find /usr/bin/ | grep virtual
  270  apt install python3-virtualenv
  271  python3-virtualenv
  272  venv
  273  python3 -m venv venv
  274      apt-get install python3-venv
  275  python3 -m venv venv
  276  ls
  277  source venv/bin/activate
  278  ls
  279  pip3
  280  nproc
  281  pip3 -r requirements.txt 
  282  pip3 install -r requirements.txt 
  283  ls
  284  python3 wordpot
  285  python3 wordpot.py 
  286  ip a
  287  python3 wordpot.py 
  288  cat venv/bin/activate
  289  history
  290  history
  291  ss -tulpn
  292  python3 wordpot.py &
  293  ss -tulpn
  294  kill %1
  295  ls
  296  vim wordpot.py 
  297  ip a
  298  python ./wordpot.py --host=0.0.0.0
  299  python ./wordpot.py --host=0.0.0.0 &

# Rsyslog set up resources (will update with documentation later / cmd history)

- https://www.youtube.com/watch?v=nmljOGQOz7c
- https://www.youtube.com/watch?v=mBJ8JfJnlXQ







