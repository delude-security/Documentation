# Recon-ng
[Documentation](https://adhdproject.github.io/#!Tools/Attack/Recon-ng.md)
Recon-ng is a modular framework for passive web reconnaissance. It contains an extensive tool set useful for gathering data that is readily available, but few tools for performing any kind of exploit to get it. 

### Usage
In this usage example, we will look at scraping Google subdomains (*.google.com) from Bing's web search page.  

1. Recon-ng can be invoked directly. With no intervention, Recon-ng will automatically check for updates. If this is undesirable, Recon-ng can be invoked with the `--no-check` flag. 
```
$ ./recon-ng --no-check
[recon-ng][default] >
``` 

2. Using the `help` command, we can view commands to manage the framework instance.
```
Commands (type [help|?] <topic>): 
--------------------------------- 
add Adds records to the database 
back Exits current prompt level 
del Deletes records from the database 
exit Exits current prompt level 
help Displays this menu 
keys Manages framework API keys 
load Loads selected module 
pdb Starts a Python Debugger session 
query Queries the database 
record Records commands to a resource file 
reload Reloads all modules 
resource Executes commands from a resource file 
search Searches available modules 
set Sets module options 
shell Executes shell commands 
show Shows various framework items 
spool Spools output to a file 
unset Unsets module options 
use Loads selected module 
workspaces Manages workspaces
```

3. Let's use the `use` command to load the module `bing_domain_web`, used to scrape domains from the Bing web interface.
```
[recon-ng][default] > use bing_domain_web
[recon-ng][default][bing_domain_web] >
```

4. Next, let's configure the module before we run it. We can view module options with the command `show options`

```
[recon-ng][default][bing_domain_web] > show options

Name    Current Value  Req  Description 
------  -------------  ---  ----------- 
SOURCE  default        yes  source of input (see 'show info' for details)
```

Since we want to search for Google domains, we need to set the SOURCE option to reflect that. Let's set it with the `set` command.

```
[recon-ng][default][bing_domain_web] > set source google.com
    SOURCE => google.com
[recon-ng][default][bing_domain_web] >
```

5. Finally let's run the module using the `run` command.
```
[recon-ng][default][bing_domain_web] > run

----------
GOOGLE.COM
----------
[*] URL: https://www.bing.com/search?first=0&q=domain%3Agoogle.com 
[*] classroom.google.com 
[*] news.google.com 
[*] www.google.com 
[*] helpouts.google.com 
[*] cloud.google.com 
[*] Sleeping to avoid lockout...

------- 
SUMMARY 
------- 
[*] 5 total (2 new) items found.
```

And that's it. As the results show, we located 5 Google domains with our Bing search, and the results database has been updated to save 2 new ones. 

---

This is just one small example of what Recon-ng can do. The arsenal also includes utilities for port scanning, geolocating servers, scraping contact info, scraping encryption certificates, among numerous other things. 

Check out these links to see what modules are available
[Recon-ng Marketplace](https://github.com/lanmaster53/recon-ng-marketplace)
[Additional Compilation of Modules](https://github.com/scumsec/Recon-ng-modules)

Recon-ng also has a considerable number of quality of life features, including a module repository, a builtin SQL database that automatically stores module results, and module searching in the CLI. It can also produce formatted module result reports in HTML 
