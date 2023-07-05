# Google Dorking

- inurl:"/wp-json/wp/v2/users": Finds all publicly available WordPress API user directories;
- intitle:"index.of" intext:"api.txt": Finds publicly available API key files;
- inurl:"/api/v1" intext:"index of /": Finds potentially interesting API directories;
- ext:php inurl:"api.php?action=": Finds all sites with a XenAPI SQL injection vulnerability;
- intitle:"index of" api_key OR "api key" OR apiKey -pool: It lists potentially exposed API keys.

# Git Dorking

Similar to Google Dorking, with GitHub, you can specify parameters like:
- filename:swagger.json
- extension: .json

# TruffleHog

TruffleHog is a great tool for automatically discovering exposed secrets. 
You can simply use the following Docker run to initiate a TruffleHog scan of your target's Github:
`sudo docker run -it -v "$PWD:/pwd" trufflesecurity/trufflehog:latest github --org=target-name`

# API directories

Programmableweb.com is a go-to source for API-related information (https://www.programmableweb.com/apis/directory). 


To learn about APIs, you can use their API University. To gather information about your target, use the API Directory, a searchable database of over 23,000 APIs. Expect to find API endpoints, version information, business logic information, the status of the API, source code, SDKs, articles, API documentation, and a changelog.

# Twilio

Twilio provides a cloud API for voice and SMS communications that leverages existing web development skills, resources and infrastructure. It minimizes the learning curve required to build advanced, reliable voice communications applications that solve critical business needs. The syntax and programming model are focused on making application development as close to the request/response model of web application development as possible. The API uses a RESTful interface and responses are formatted in
HTML, ISON, XML or CSV.

# Shodan

Shodan is the go-to search engine for devices accessible from the internet. Shodan regularly scans the entire IPv4 address space for systems with open ports and makes their collected information public on https://shodan.io. You can use Shodan to discover external-facing APIs and get information about your target’s open ports, making it useful if you have only an IP address or organization’s name to work from. Like with Google dorks, you can search Shodan casually by entering your target’s domain name or IP addresses; alternatively, you can use search parameters like you would when writing Google queries. The following table shows some useful Shodan queries.

- hostname:"targetname.com": Using hostname will perform a basic Shodan search for your target’s domain name. This should be combined with the following queries to get results specific to your target;
- "content-type: application/json": APIs should have their content-type set to JSON or XML. This query will filter results that respond with JSON;
- "content-type: application/xml": This query will filter results that respond with XML;
- "200 OK": You can add "200 OK" to your search queries to get results that have had successful requests. However, if an API does not accept the format of Shodan’s request, it will likely issue a 300 or 400 response;
- "wp-json": This will search for web applications using the WordPress API.

# The Wayback Machine

The Wayback Machine is an archive of various web pages over time. This is great for passive API reconnaissance because this allows you to check out historical changes to your target. If, for example, the target once advertised a partner API on their landing page, but now hides it behind an authenticated portal, then you might be able to spot that change using the Wayback Machine. Another use case would be to see changes to existing API documentation. If the API has not been managed well over time, then there is a chance that you could find retired endpoints that still exist even though the API provider believes them to be retired. These are known as Zombie APIs. Zombie APIs fall under the Improper Assets Management vulnerability on the OWASP API Security Top 10 list. Finding and comparing historical snapshots of API documentation can simplify testing for Improper Assets Management.