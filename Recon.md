# Recon

## 1. **Basic Reconnaissance (Passive OSINT)**

> No interaction with the target, avoids detection.
> 
- **WHOIS & Domain Intelligence**
    - `whois` `Whoxy` 
    - `DomainBigData` `OCCRP Aleph`
    - `Kaferjaeger.gay`
    - Identify registrars, name servers, emails, organization.
- **DNS Enumeration**
    - `dig`, `nslookup`, `dnsrecon`, `fierce`
    - Collect subdomains, mail servers, TXT records (SPF/DMARC).
- **Search Engines**
    - Google Dorking: `site:example.com filetype:pdf`
    - Shodan Dorking
    - Censyus Dorking
    - LinkedIn for employees → spear-phishing usernames.
- **Wayback Machine / Archive.org**
    - Look for old endpoints, forgotten panels, staging environments.
    - Version detection of services
- **Image OSINT**
    
    Google image search : `yandex` `tineye`
    
- **Public Repositories**
    - GitHub/GitLab/Bitbucket leaks: API keys, credentials.
    - Tools: `truffleHog`, `git-secrets`.
        
        Technology Fingerprinting : `wappulyzer`
        
        Source Code
        
- **Media Recon**
    - Stack technology leaks: "We’re hiring a DevOps engineer with AWS, Terraform, Kubernetes experience" = tech stack exposed. ( job postings )
    - Social Media Recon
    - Location recon
    - Satellite images
    - Employee Recon
    - Instagram / Facebook /Twitter /  and all….
        
         `sherlcok`
        
        `whatsapp.checkleaked.cc`
        
- **Hunting**
    - Fingerprint exposed services globally.
    - Data breaches: `weleakinfo` `pimeyes` `dehashed` `leakcheck` `haveibeenpwned`
    - Emails  credential stuffing targets.
        
        [`Hunter.io`](http://hunter.io/) [`Phonebook.cz`](http://phonebook.cz/) `VoilaNorbert` `rocketreach`
        
        breaches such as : [`intelx.i](http://intelx.io)o` `haveibeenpwnd` `leakradar.io`
        
        Verifying email: `Email Hippo` `Email checker`
        
________________________________________________________________________________________________________________________________________________________________________________________________________
## 2. **Intermediate Reconnaissance (Active, but low-noise)**

> Starts interacting with the target but still stealthy.
> 
- **Subdomain Enumeration**
    - Tools: `subfinder`, `amass`, `assetfinder`, `crt.sh`
    - Bruteforce with wordlists (`dnscan`, `dnsx`)
- **Port Scanning**
    - `nmap -sV -sC -T4 target.com`
    - Service version detection & default scripts.
- **Virtual Host Discovery**
    - Tools: `ffuf -H "Host: FUZZ.example.com" -u http://IP`
    - directory / vhost discovery
- **Directory Bruteforcing**
    - Web path enumeration
    - Directory traversal tests
    - Tools: `gobuster`, `ffuf`, `dirsearch`
    - Wordlists: `SecLists`
    - JS endpoint extraction and link crawling
    - Header-based scanning (`x-forwarded-for`, `x-origin`)
- **SSL/TLS Recon /  Censys lookup**
    - Check certs for SANs (Subject Alt Names).
    - Tools: `sslscan`, `testssl.sh`.
- **Cloud Asset Discovery**
    - AWS S3 Buckets: `aws s3 ls s3://bucket-name`
    - Tools: `cloud_enum`, `s3scanner`.
________________________________________________________________________________________________________________________________________________________________________________________________________
## 3. **Advanced Reconnaissance (Deep Attack Surface Mapping)**

> Involves more aggressive scanning, correlation, and automation.
> 
- **ASN  Records & IP Space Enumeration**
    - Find all IP ranges owned by org.
    - Tools: `amass intel -asn <ASN>`, `bgp.he.net`
    - JS file parsing for endpoints
    - Reverse DNS lookups
    - CORS misconfiguration checks via headers
    - Endpoint wordlist generation using
    - Sitemaps/robots.txt/humans.txt abuse
- **Correlation of Domains & Subs**
    - Tools: `Amass`, `Chaos`, `ProjectDiscovery suite`
    - Combine results, deduplicate.
- **Web Tech Fingerprinting**
    - `wappalyzer`, `httpx`, `whatweb`
    - Identify frameworks, CMS, plugins → known CVEs.
    - WAF and CDN detection
- **Content Discovery Beyond Wordlists**
    - Param guessing: `paramspider`, `arjun`
    - Identify hidden APIs.
    - Content discovery (JS, JSON, config leaks)
- **Git Dorking**
    - Advanced GitHub code search for company leaks.
- **Network-Level Recon**
    - SNMP enumeration (if open): `snmpwalk`
    - SMB shares: `smbclient -L //target`
- **Automated Attack Surface Mapping**
    - Vulnerability scanning with custom Nuclei templates / Nessus
    - Frameworks: `reconFTW`, `BugMap`, `OSINT Framework`, `Nuclei`
    - Daily cronjobs to catch new assets.
________________________________________________________________________________________________________________________________________________________________________________________________________
## 4. **Expert-Level Reconnaissance (Red Team / APT Style)**

> Rarely done by casual hunters, but gold for pentesting.
> 
- **Supply Chain Recon**
    - Third-party vendors → weak links.
    - Identify partner domains, shared infra.
- **Endpoint & API Recon**
    - Decompile mobile apps → API endpoints.
    - Tools: `MobSF`, `apktool`
    - Swagger docs leaks: `/swagger.json`
- **Employee Recon**
    - Password reuse attacks, password spraying.
    - Username harvesting → OWA, VPN, SSO portals.
- **Custom Wordlist Generation**
    - From company docs, GitHub, LinkedIn.
    - Tools: `cewl`, `theHarvester`.
- **Cloud & Container Recon**
    - Kubernetes dashboards, Jenkins, Docker APIs.
- **Advanced Correlation**
    - Use BloodHound-style mapping for external assets.
    - Pivot via DNS records, CDN leaks, forgotten IPs.
 ________________________________________________________________________________________________________________________________________________________________________________________________________



# To Use:
_____________

**ASN records // ip spaces :**

- bgp.he.net
- dnschecker.org
- tracxn.com
___________________
**asnmap**

	$ echo GOOGLE | ./asnmap -silent
	
	$ echo hackerone.com | ./asnmap -json -silent | jq
______________________________________________________________________________________________________________________________

**naabu**

	$ naabu -list ips.txt -p - -s -o open_ports.txt
___________________
**TLSX**

	$ echo 173.0.84.0/24 | tlsx 
	
	$ echo 173.0.84.0/24 | tlsx -san -cn -silent
______________________________________________________________________________________________________________________________

**subfinder** [ Passive subdomain enumeration using multiple sources. ]

*Go to chaos and register an account, get the api key and put in subfinder = 15% more increase enumeration*

	$ subfinder -d example.com -all -silent -o subs.txt | 
___________________
**asset finder** [ Quick subdomain finder ]

	$ assetfinder --subs-only example.com > asset.txt 
______________________________________________________________________________________________________________________________

**amass** [ Powerful subdomain enumeration (passive + active + brute force) ]


	$ amass enum -d example.com -o amass.txt 
______________________________________________________________________________________________________________________________

**feroxbuster** [ fast, recursive content discovery tool ]


	$ feroxbuster -u https://target.com
	
	$ feroxbuster -u https://target.com -x php,txt,html --depth 2 
______________________________________________________________________________________________________________________________

**BBOT** [  Powerful subdomain enumeration  ]

	- Full subdomain enumeration (passive + active):
	$ bbot -t example.com -p subdomain-enum
	
	- Passive sources only:
	$ bbot -t example.com -p subdomain-enum -rf passive
	
	- Subdomains + port scan + web screenshots:
	 $ bbot -t example.com -p subdomain-enum -m naabu gowitness
	
	- Subdomains + web spider for email harvesting:
	 $ bbot -t example.com -p subdomain-enum web-spider
	
	 - $ bbot -t example.com -p subdomain-enum --output-modules json
______________________________________________________________________________________________________________________________

**linkfinder** [ Extract endpoints from JS files]

	$ python3 linkfinder.py -i https://example.com/app.js -o cli 

____________________________________________________________________________
[crawl a web for JS files...]

 - Store both (URLs + endpoints)

	echo "https://example.com" | waybackurls | grep ".js" | while read url; do
	    echo "[+] Processing $url" >> results.txt
	    python3 linkfinder.py -i $url -o cli >> results.txt
	done
______________________________________________________________________________________________________________________________

**waybackurls** [ Fetch archived URLs from Wayback Machine. ]
	
	$ echo "domain.com" | waybackurls | tee urls.txt
	
	$ subfinder -d example.com -all | waybackurls > wayback.txt

______________________________________________________________________________________________________________________________

**arjun** [ Parameter discovery ]
 
	$ arjun -u https://target.com -o arjun.txt
______________________________________________________________________________________________________________________________

**paramspider** [ Crawl and extract GET parameters from URLs. ]

	$ paramspider -d domain.com
	
	$ paramspider -l domains.txt
___________________________________________________

**spiderfoot** [ OSINT automation (subdomains, leaks, IPs, etc.) ]

	$ spiderfoot -s example.com -o spiderfoot.html 
______________________________________________________________________________________________________________________________


**Httpx** [check live hosts]

	$ httpx -l subs.txt -o live.txt 
	
	$ httpx -l subs.txt -silent -o live.txt
	
	$ echo "domain.com" | waybackurls | tee urls.txt | httpx -title -status-code -content-length  -tech-detect | tee results.txt

______________________________________________________________________________________________________________________________

**gf** [- A wrapper around grep that u quickly filter interesting findings from large lists of URLs ]

	$ cat urls.txt | gf xss
___________________________________________________
**XSS findings**

	$ gf xss urls_0.txt | tee xss_0.txt
	
	$ cat urls.txt | gf xss > xss_candidates.txt
___________________________________________________
**redirects**

			$ gf redirect urls_0.txt | tee redirect_0.txt
______________________________________________________________________________________________________________________________

**Gxss** [ Check reflected parameters for potential XSS. ]

	$ cat "domain.txt" | Gxss > reflected_urls.txt
	$ cat xss_candidates.txt | Gxss -p XSS > reflected.txt
___________________________________________________

**dalfox** [ Actively scan/exploit XSS vulnerabilities.]

	$ dalfox file reflected_urls.txt
	$ cat reflected.txt | dalfox pipe -o xss_results.txt
______________________________________________________________________________________________________________________________

**Xss Loader** [ encoding the xss ]

	$ python3 payloader.py
______________________________________________________________________________________________________________________________

**Xss Strike** 

	$ python3 xsstrike.py -u https://example.com/search?q=test
	
	$ python3 xsstrike.py -u https://example.com --crawl
	
	$ python3 xsstrike.py -u https://example.com/search?q=test --skip-waf
___________________________________________________________________________________________________________________________

**exifdata XSS**

	exiftool -ImageDescription='<img src=x onerror=alert(1)>' image.jpg
____________________________________________________________________________

```
		exiftool \
		  -ImageDescription='<img src=x onerror=alert(1)>' \
		  -Artist='<svg onload=alert(2)>' \
		  -UserComment='<details open ontoggle=alert(3)>' \
		  -XPComment='" onmouseover="alert(4)' \
		  -Copyright='<iframe srcdoc="<script>alert(5)</script>"></iframe>' \
		  image.jpg
```
______________________________________________________________________________________________________________________________

**graphql-cop** [ Test common misconfigurations of graphql endpoints ]

	$ python3 graphql-cop.py -t https://mywebsite.com/graphql

__________________________________________________________________________________________________________________________

# rough 

$ cat file1 file2 | sort -u > file3  [ sort out files ] 

*Google dorks*
								site:*<*.target.*

								site:*<-*.target.*

								site:*>*.target.*

								site:*->*.target.*

								site:*<->*.target.*

								site:*<*.target.com intext:"login" | intitle:"login" | inurl:"login" | intext:"username" | intitle:"username" | inurl:"username" | intext:"password" | intitle:"password" | inurl:"password"
________________________________________________________________________________________________
		$ shodan search ssl.cert.subject.CN:"target.com" --fields ip_str | anew shodan.txt
				cat shodan.txt | naabu -top-ports 1000 | anew shodan_ports.txt
_______________________________________________________
- cat subdomains-top1million-50000.txt | ffuf -w -:FUZZ -u http://example.com/ -H 'Host: FUZZ.example.com' -ac

