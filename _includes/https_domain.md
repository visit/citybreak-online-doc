# Domain & Https

## Domain - DNS setup

Add a DNS record with type **CNAME and point to hosted01.citybreak.com**
**Make sure there is no proxying if you use Cloudflare!**
When this is done Citybreak will connect the subdomain to your Citybreak online.

External testing tool example: 

[nslookup.io](https://www.nslookup.io/) - Check result on the authoritative tab.

or

[dnschecker.org](https://dnschecker.org/all-dns-records-of-domain.php)


## Https - SSL information
We require all CB online implementations to use SSL/HTTPS Certificate.
Citybreak online uses [Let’s Encrypt](https://letsencrypt.org) service, via Cloudflare that enable us to easy add certificates on your sub domains including auto renewal.
