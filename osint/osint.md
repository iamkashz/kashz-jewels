# osint

NOTE: this section is just for my reference and majority of the links I use are saved as bookmarks in browser. If you'd
like me to share it, send a DM.

* [OWASP/Amass](https://github.com/OWASP/Amass) `amass enum -d DOMAIN`

## subdomains osint

* [aboul3la/Sublist3r](https://github.com/aboul3la/Sublist3r) `./sublist3r.py -d DOMAIN`
* [tomnomnom/assetfinder](https://github.com/tomnomnom/assetfinder) `assetfinder [--subs-only] DOMAIN`
* [darkoperator/dnsrecon](https://github.com/darkoperator/dnsrecon) `dnsrecon -t brt -d DOMAIN`
* [samyoyo/Bluto](https://github.com/samyoyo/Bluto)
* [laramies/theHarvester](https://github.com/laramies/theHarvester)

Check for active sub-domains: [tomnomnom/httprobe](https://github.com/tomnomnom/httprobe)

Screenshot tool: [sensepost/gowitness](https://github.com/sensepost/gowitness)

## email osint:

* [Clearbit Connect Chrome Extension](https://chrome.google.com/webstore/detail/clearbit-connect-supercha/pmnhcgfcafcnkbengdcanjablaabjplo?hl=en)

## search engine osint

* [Google Advanced Search](https://www.google.com/advanced_search)

### Search Operators: [google-advanced-search-operators](https://ahrefs.com/blog/google-advanced-search-operators/)

```bash
# *: wildcard
site:*.DOMAIN.com
-<keywordToOmit>
intext:<> | inurl:<> | intitle:<>
filetype: <>
keyword1 AND|OR|* keyword2
"keyword1 keyword2"
```

## social networking osint

### Twitter

* [twintproject/twint](https://github.com/twintproject/twint)

```bash
from:USER
to:USER
@USER
since:YYYY-MM-DD
until:YYYY-MM-DD
geocode:GEO-CODE,<NUMBER>km
```

## leaks osint

* [Radial01/PwnyCorral](https://github.com/Radial01/PwnyCorral) `python pwnycorral.py -h`
* [hmaverickadams/breach-parse](https://github.com/hmaverickadams/breach-parse) `./breach-parse.sh @DOMAIN OUT.txt "PATH-to-BreachCompilationData"`
* [laramies/theHarvester](https://github.com/laramies/theHarvester)

## username osint

* [sherlock-project/sherlock](https://github.com/sherlock-project/sherlock) `python3 sherlock.py USERNAME`

## phone-number osint

* [sundowndev/phoneinfoga](https://github.com/sundowndev/phoneinfoga) `phoneinfoga serve -p 9090`