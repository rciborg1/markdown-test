# 1. Target URLS

- url 1 : keikis.noip.me
- url 2 : univ-rennes1.fr
- url 3 : google.com

## 1.1 DNS

### 1 and 2 : IPv4 and Ipv6 addresses sites
The addresses were found with the following command: 
```
nslookup site
```
- keikis.noip.me
<img title="IPv4 and IPv6 addresses of keikis.noip.me" alt="IPv4 and IPv6 addresses of keikis.noip.me" src="/src/keikis.noip.me/1.1.1 et 1.1.2.png">

- univ-rennes1.fr

- google.com
<img title="IPv4 and IPv6 addresses of google.com" alt="IPv4 and IPv6 addresses of google.com" src="/src/google.com/1.1.1 et 1.1.2.png">

### 3 and 4 : Domain's registrar and host : 
They were found with the following command: 
```
whois site
```
- keikis.noip.me
<img title="noip.me's registrar" alt="noip.me's registrar" src="/src/keikis.noip.me/1.1.3.png">
<img title="noip.me's host" alt="noip.me's host" src="/src/keikis.noip.me/1.1.4.png">

- univ-rennes1.fr


- google.com
<img title="google.com's registrar" alt="google.com's registrar" src="/src/google.com/1.1.3.png">
<img title="google.com's host" alt="google.com's host" src="/src/google.com/1.1.4.png">

## 1.2 OSINT

### 1 : Domain’s certificate
We used the following command
```
echo | openssl s_client -servername site -connect site:443 2>/dev/null | openssl x509 -noout -issuer
```
- keikis.noip.me
<img title="noip.me’s certificate" alt="noip.me’s certificate" src="/src/keikis.noip.me/1.2.1.png">

- univ-rennes1.fr

- google.com
<img title="google.com’s certificate" alt="google.com’s certificate" src="/src/google.com/1.2.1.png">

### 2 : Potential security issues with this certificate

- keikis.noip.me

- univ-rennes1.fr

- google.com

### 3 : Google search engine request to find the public facing PDF files sites

- keikis.noip.me
<img title="keikis.noip.me request" alt="keikis.noip.me request" src="/src/keikis.noip.me/1.2.3.png">

- univ-rennes1.fr

- google.com
<img title="google.com request" alt="google.com request" src="/src/google.com/1.2.3.png">

### 4 : List all of the subdomains for sites
We found subdomains by the following command
```
theHarvester -d site -b all
```
As there are many of them, we have captured only a part.

- keikis.noip.me
<img title="subdomains of keikis.noip.me" alt="subdomains of keikis.noip.me" src="/src/keikis.noip.me/1.2.4.png">

- univ-rennes1.fr

- google.com
<img title="subdomains of google.com" alt="subdomains of google.com" src="/src/google.com/1.2.4.png">

### 5 : Are the certificates issued by the same entities

Yes, all certificates are the same, as shown in some of the sub-domains tested.

- keikis.noip.me
<img title="keikis.noip.me" alt="keikis.noip.me" src="/src/keikis.noip.me/1.2.5.png">

- univ-rennes1.fr

- google.com
<img title="google.come" alt="google.com" src="/src/google.com/1.2.5.png">

## 1.3 Mapping

### 1 : Exposed services by the domain
We used the following command
```
nmap site
```
- keikis.noip.me
<img title="noip.me’s opened services" alt="noip.me’s opened services" src="/src/keikis.noip.me/1.3.1.png">

- univ-rennes1.fr

- google.com
<img title="google.com’s opened services" alt="google.com’s opened services" src="/src/google.com/1.3.1.png">

### 2 : Server-side technology or Framework used to serve domains
We used the following command
```
curl -I site
```
- keikis.noip.me
<img title="noip.me’s Server-side technologies" alt="noip.me’s Server-side technologies" src="/src/keikis.noip.me/1.3.2.png">

- univ-rennes1.fr

- google.com
<img title="google.com’s Server-side technologies" alt="google.com’s Server-side technologies" src="/src/google.com/1.3.2.png">

### 2 : Operating system by system
We used the following command
```
command
```
- keikis.noip.me

- univ-rennes1.fr

- google.com

# 2. Root-me.org

