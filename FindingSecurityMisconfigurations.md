Once you have discovered an API and used it as it was intended, you can proceed to perform a baseline vulnerability scan. A good reason to perform your testing in this order is to avoid having any of your scans set off a security control like a WAF that results in your traffic being blocked.


So, we will not use vulnerability scans to determine all of the weaknesses an app has, but instead, we will use the scan results to help guide and focus our testing.

When vulnerability scans are applied generically to web APIs the most common outcome is to receive false-negative results. False-negative results take place when vulnerability scans do not detect or report existing problems. For most organizations, this can result in a false sense of security because the scans came back with no evidence of any present weaknesses.


The current state of many free and paid vulnerability scanners is that they were not designed for web APIs and often do not detect many of the vulnerabilities listed on the OWASP API Security Top 10. These vulnerability scanners, however, do a decent job at detecting API7:2019 Security Misconfiguration.


Security misconfiguration includes missing system patches, unnecessary features enabled, lack of secure transit encryption, weak security headers, verbose error messages, and Cross-Origin Resource Sharing (CORS) policy misconfigurations.


# Nikto

Use Nikto to scan a web app:
- `nikto -h URL`;


# OWASP Zap

Like Nikto, a generic automated OWASP ZAP scan will run into the same problems with false-negative findings. However, you can configure a ZAP scan to better work with web APIs. The first thing that we will do is to run an unauthenticated scan of the attack surface. We can plug in the target URL, but to improve these results and to make sure we hit everything, we can import the **target's API specification file**.

You can do this by selecting import and choosing the relevant specification file (example the "specs.yml" file generated with mitmweb).

You can find the results of the scan under the Alerts tab. 


The next step that you can take to improve the scan results is to perform authenticated scanning. The easiest way to perform authenticated scanning is to use the Manual Explore option.


Set the URL to your target, make sure the HUD is enabled, and choose "Launch Browser".


Once you choose to manually explore, you should see the HUD launch in a browser. Here you can select "Continue to your target". Similar, to the work we did during the "Reverse Engineering APIs" module, we will go through and use the web application as an end-user.
Perform all of those actions again. Sign up for another account, sign in, and use the various features. Make sure to use the HUD to perform certain actions. At the top left of the HUD, you can add your target to the scope of testing. Once you have authenticated to the app and performed a baseline set of actions you can perform an active scan.


On the right-hand side of the HUD, you can set the Attack Mode to On. This will begin scanning and performing authenticated testing of the target. Depending on the scale of the web application that you are targeting, this scan could take a while. 