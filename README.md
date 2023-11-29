# API-Penetration-Testing

**An API (Application Programming Interface) is a set of rules that enables one software application to interact with another, allowing them to share functionality and data. It serves as a bridge for different software systems to communicate and work together.**

##  Passive Reconnaissance

#### Google Dorking Query
- ```intitle:"api" site:"coinbase.com"```
- ```intitle:"/api/v1" site:"microsoft.com"```
- ```intitle:json site site:ebay.com```
- 
- ```inurl:"/wp-json/wp/v2/users"``` Finds all publicly available WordPress API user directories.
- ```intitle:"index.of" intext:"api.txt"```  Finds publicly available API key files.
- ```inurl:"/api/v1" intext:"index of /"``` Finds potentially interesting API directories.
- ```ext:php inurl:"api.php?action="``` Finds all sites with a XenAPI SQL injection vulnerability. (This query was posted in 2016; four years later, there are currently 141,000 results.)
- ```intitle:"index of" api_key OR "api key" OR apiKey -pool``` This is one of my favorite queries. It lists potentially exposed API keys.
#### Github dorking
#### shodan.io
#### wayback machine

## Active Reconnaissance
### Nmap
After starting the docker ``` sudo docker-compose start```
```
nmap -sC -sV 127.0.0.1
```
- -sC: Runs default scripts to gather information.
- -sV: Attempts to determine the version of services on open ports.
```
nmap -p- 127.0.0.1
```
- -p-: Specifies to scan all 65,535 TCP ports. This is an exhaustive scan that checks every possible port for activity.
- Example
``` └─$ nmap -p- 127.0.0.1       
Starting Nmap 7.94SVN ( https://nmap.org ) at 2023-11-29 17:55 +06
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00039s latency).
Not shown: 65531 closed tcp ports (conn-refused)
PORT      STATE SERVICE
8025/tcp  open  ca-audit-da
8443/tcp  open  https-alt
8888/tcp  open  sun-answerbook
35159/tcp open  unknown

```
```
nmap -sV 127.0.0.1 -p 8025 
```
- -p 8025: Specifies the port number to be scanned, in this case, port 8025.


### amass
Amass is an open-source tool used for reconnaissance and information gathering in cybersecurity. It specializes in discovering subdomains and associated network information for a target domain, making it valuable for security professionals and researchers.
```
amass enum -list
```
```
amass enum -active -d microsoft.com | grep api
```
### Gobuster
Gobuster can be used to brute-force URIs and DNS subdomains from the command line. (If you prefer a graphical user interface, check out OWASP’s Dirbuster.) In Gobuster, you can use wordlists for common directories and subdomains to automatically request every item in the wordlist and send them to a web server and filter the interesting server responses. The results generated from Gobuster will provide you with the URL path and the HTTP status response codes. (While you can brute-force URIs with Burp Suite’s Intruder, Burp Community Edition is much slower than Gobuster.)
```
gobuster dir -u http://127.0.0.1:8888 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
