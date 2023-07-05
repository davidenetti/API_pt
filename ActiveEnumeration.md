# Nmap

The Nmap general detection scan uses default scripts (-sC) and service enumeration (-sV) against a target and then saves the output in three formats for later review (-oX for XML, -oN for Nmap, -oG for greppable, or -oA for all three):

- `nmap -sC -sV [target address or network range] -oA nameofoutput`
- `nmap -sV --script=http-enum target -p 80,443,8000,8080`

# Owasp Amass

OWASP Amass is a command-line tool that can map a target’s external network by collecting OSINT from over 55 different sources.
You can set it to perform passive or active scans. If you choose the active option, Amass will collect information directly from the target by requesting its certificate information. Otherwise, it collects data from search engines (such as Google, Bing, and HackerOne), SSL certificate sources (such as GoogleCT, Censys, and FacebookCT), search APIs (such as Shodan, AlienVault, Cloudflare, and GitHub), and the web archive Wayback.

First, we can see which data sources are available for Amass (paid and free) by running:
- `amass enum -list`

Next, we will need to create a config file to add our API keys to.
- `sudo curl https://raw.githubusercontent.com/OWASP/Amass/master/examples/config.ini >~/.config/amass/config.ini`

Simply visit https://censys.io/register and register for a free account. Make sure to use a valid email because you will have to verify for access to your free account. Once you have obtained your API ID and Secret, edit the config.ini file and add the credentials to the file.
- `sudo nano ~/.config/amass/config.ini`

Also, as with any credentials make sure not to share them like I just did. If you did share them then simply use the "Reset My API Secret" button back on Censys.io. You can repeat this process with many free accounts and API keys, then you will make OWASP Amass into a powerhouse for API reconnaissance.

- `amass enum -active -d target-name.com |grep api`

s. Use the intel command to collect SSL certificates, search reverse Whois records, and find ASN IDs associated with your target:

- `amass intel -addr [target IP addresses]`

If this scan is successful, it will provide you with domain names. These domains can then be passed to intel with the whois option to perform a reverse Whois lookup:

- `amass intel -d [target domain] –whois`

Once you have a list of interesting domains, upgrade to the enum subcommand to begin enumerating subdomains. If you specify the -passive option, Amass will refrain from directly interacting with your target:

- `amass enum -passive -d [target domain]`
- `amass enum -active -d [target domain]`

To up your game, add the -brute option to brute-force subdomains, -w to specify the API_superlist wordlist, and then the -dir option to send the output to the directory of your choice:

- `amass enum -active -brute -w /usr/share/wordlists/API_superlist -d [target domain] -dir [directory name]`

# Directory  brute-force with Gobuster

Gobuster can be used to brute-force URIs and DNS subdomains from the command line. In Gobuster, you can use wordlists for common directories and subdomains to automatically request every item in the wordlist and send them to a web server and filter the interesting server responses. The results generated from Gobuster will provide you with the URL path and the HTTP status response codes.

- `gobuster dir -u target-name.com:8000 -w /home/hapihacker/api/wordlists/common_apis_160`
- `gobuster dir -h`
- `gobuster dir -u ://targetaddress/ -w /usr/share/wordlists/api_list/common_apis_160 -x 200,202,301 -b 302`

# Kiterunner

Kiterunner is currently the best tool available for discovering API endpoints and resources. While directory brute force tools like Gobuster/Dirbuster/ work to discover URL paths, it typically relies on standard HTTP GET requests. Kiterunner will not only use all HTTP request methods common with APIs (GET, POST, PUT, and DELETE) but also mimic common API path structures. In other words, instead of requesting GET /api/v1/user/create, Kiterunner will try POST /api/v1/user/create, mimicking a more realistic request.
You can perform a quick scan of your target’s URL or IP address like this:
- `kr scan HTTP://127.0.0.1 -w ~/api/wordlists/data/kiterunner/routes-large.kite`

If you want to use a text wordlist rather than a .kite file, use the brute option with the text file of your choice:
- `kr brute target -w ~/api/wordlists/data/automated/nameofwordlist.txt`

# DevTools

DevTools contains some highly underrated web application hacking tools. The following steps will help you easily and systematically filter through thousands of lines of code in order to find sensitive information in page sources. Begin by opening your target page, and then open DevTools with F12 or ctr-shift-I. Adjust the DevTools window until you have enough space to work with. Select the Network tab and then refresh the page (CTRL+r).


You can use the filter tool to search for any term you would like, such as "API", "v1", or "graphql". This is a quick way to find API endpoints in use. You can also leave the Devtools Network tab open while you perform actions on the web page.