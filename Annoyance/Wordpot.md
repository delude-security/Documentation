# Wordpot

GitHub/SourceCode: [github.com/adhdproject/wordpot](https://github.com/adhdproject/wordpot)
ADHD: [adhdproject.github.io/wordpot](https://adhdproject.github.io/#!Tools/Annoyance/Wordpot.md)
WikiPage: [wordpot/wiki/Plugins](https://github.com/gbrindisi/wordpot/wiki/Plugins)
Project Homepage: [Homepage](http://brindi.si/g/projects/wordpot.html)

Definition
   -  Wordpress honeypot that detects probes for plugins, themes, timthumb and other common files used to fingerprint a wordpress installation
        - Wordpot simulates a full install. Including fake installed themes and plugins
        - 

    - Note* Wordpot can be expanded with plugins to improve its behaviour or mimik a particular vulnerability.
        See [wordpot/wiki/Plugins](https://github.com/gbrindisi/wordpot/wiki/Plugins)(beta)
        - A plugin register itself to one or more hooks which are points triggered by incoming requests. When a hook is triggered it puts in execution every plugin attached to it

# Implimentation

Installation:
- Install from git:
    ```sh 
     https://github.com/gbrindisi/wordpot/
    ```

- Install Location: 
    ```sh 
    /opt/wordpot/
    ```
Usage:

- To run the script, first cd to the wordpot directory.
    ```sh 
    ~$ cd /opt/wordpot
    ```
- And run the application
    ```sh 
    /opt/wordpot$ sudo python ./wordpot.py --help
    ```
- This will show you the help dialog.
- To configure the honeypot you can edit the config file "wordpot.conf" or provide arguments trough the command line interface as shown above.

Running A fake Wordpress Install: [Example 1: Running a fake Wordpress install¶](https://adhdproject.github.io/#!Tools/Annoyance/Wordpot.md#Example_1:_Running_a_fake_Wordpress_install)
- Wordpot runs by default without any additional configuration required.
Simply run the script with whatever command line arguments you need for
your situation. With ADHD, by default you should have apache listening
on port 80. So you might need to specify an alternative port number, or
to disable apache for the time that you're running this script.
    ```sh 
    /opt/wordpot$ sudo python ./wordpot.py --port=4444
    ```
- You can view your fancy new fake wordpress install by opening your web
browser and navigating to "http://localhost:4444"

