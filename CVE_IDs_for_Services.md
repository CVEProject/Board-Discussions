# CVE IDs for Service Vulnerabilities

This document is meant to organize discussion around this question: **Can CVE IDs be assigned for vulnerabilities that affect services?**

Likely web services, that appear as a single or small number of instances. A vulnerability in such a service is fixed once for all users, users do not have to take action such as updating or patching, users may have to restart a session or browser.

See also: <https://github.com/CVEProject/docs/issues/18> and INC3 in <https://cve.mitre.org/cve/cna/CNA_Rules_v1.1.pdf>

This document may be updated or superceeded by a draft from @balinsky.

## Use Cases
1. Someone wants to talk about a specific service vulnerability
2. User needs to take some action, restart session or browser, change password
3. Forensic investigation

## Pro
[From @balinsky]:

Even if a customer cannot take any action to patch the system, the disclosure of the vulnerability affects them in 2 ways:

1. They can take remediation steps to clean up the data (e.g. locking accounts whose data was compromised, issuing new credit card numbers if they were compromised, informing downstream customers of the breach, etc.)
2. They can take an action of switching vendors if the disclosure leads them to lose faith in the vendor.

The above cases argue for disclosure of vulnerabilities in services. I would argue that whenever you have a disclosure in such a case, the community benefits from having a CVE attached to it. This is for the same reasons that issuing a CVE for any other vulnerability is beneficial. It allows researchers or security practitioners to refer to a common issue.

What if there are 3 similar vulnerabilities in a given service during a year? Must a researcher refer to them by disclosure date or by some company advisory disclosure identifier or URL? These things may change over time. A CVE is a fixed, permanent reference point. All vulnerabilities that are significant and enter the realm of public discussion will benefit from having a common identifier attached to them.
## Con
1. Dilution/counting issues -- flag service IDs so consumers can consider or ignore them?
2. Versions -- use dates?
