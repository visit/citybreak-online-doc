# Domain & Https

## Domain - DNS setup

Add a DNS record with type **CNAME and point to hosted01.citybreak.com**

When this is done Citybreak will connect the subdomain to your Citybreak online.

External testing tool example: 

[nslookup.io](https://www.nslookup.io/) - Check result on the authoritative tab.

or

[dnschecker.org](https://dnschecker.org/all-dns-records-of-domain.php)


## Https - SSL information
We require all CB online implementations to use SSL/HTTPS Certificate.
Citybreak online has implemented [Let’s Encrypt](https://letsencrypt.org) service that enable us to easy add certificates on your sub domains including auto renewal.

We can install your own certificates as a addon service if requested.
_Note this extra service we that we will debit if asked for._
