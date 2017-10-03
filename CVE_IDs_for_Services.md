#CVE IDs for Service Vulnerabilities

This document is meant to organize discussion around this question: **Can CVE IDs be assigned for vulnerabilities that affect services?**

Likely web services, that appear as a single or small number of instances. A vulnerability in such a service is fixed once for all users, users do not have to take action such as updating or patching, users may have to restart a session or browser.

See also: <https://github.com/CVEProject/docs/issues/18> and INC3 in <https://cve.mitre.org/cve/cna/CNA_Rules_v1.1.pdf>

## Use Cases and Sub-Cases
1. Someone wants to talk about a specific service vulnerability.
   a. CVEs help to disambiguate similar issues in a service.
   b. There is a vulnerability at a service/site for some time. A user would want to know the dates, any exploits, impacts, and full description of the problem, to determine their full impact. This information may become available in pieces over time. An identifier helps uniquely tie the pieces of information together.
1. Disclosure
   * A vendor finds and fixes a vulnerability and wishes to disclose it to the public. They typically have a lot of information that should be in a CVE entry: affected dates, impact for a typical customer, number of customers affected.
   * An external researcher finds and wants to disclose a vulnerability without the vendor's help. The researcher may lack critical information about the dates, the full impact to a user, or the full scope to other users. 
1. User needs to take some action to complete the fix, such as clear caches, restart session or browser, change password
1. Forensic investigation. Customer stored sensitive data on the service and wants to know whether there was a potential compromise to that data. User may decide to take actions to protect that data, disclose the breach to their own customers. 
1. Internal software eventually goes public. Having vulns tracked via CVE would make the entire life cycle much easier to manage when things go public.
1. A product has client-side and server-side components (usually via an API). There is value in knowing what services you may want to use have had vulnerabilities.
1. Complex product delivery cases:
  * The affected software is available in both customer-controlled AND vendor-hosted versions. Do you create an ID in both programs and assume it affects both, just the one that was reported, something else?
  * The affected software is offered as vendor-hosted only, but the vendor has allowed a limited number of customer-controlled instances. Same problems as above.
  * The affected software is a hybrid with some client code and some hosted code. It isn't clear which is affected in each case.
  * Many hardware/embedded devices contain software that cannot be changed by the customer (e.g., Iot and appliances). You could argue that this falls into the category of vendor-hosted/controlled since the customer has no way of changing it.
1. The vulnerability may affect multiple sites, is fixed at one, and can be scanned for. (Is this valid? or is this just a regular CVE?)
1. What do we do if we get multiple reports of a service CVE from independent researchers, but no confirmation from the vendor? In this case, Daniel suggested that MITRE could say "we will not assign to services, but anyone who wishes to be a CNA for services (or individual services) can under the Rules"

## Pro
1. Even if a customer cannot take any action to patch the system, the disclosure of the vulnerability affects them in 2 ways:
   1. They can take remediation steps to clean up the data (e.g. locking accounts whose data was compromised, issuing new credit card numbers if they were compromised, informing downstream customers of the breach, etc.)
   2. They can take an action of switching vendors if the disclosure leads them to lose faith in the vendor.

2. The above cases argue for disclosure of vulnerabilities in services. I would argue that whenever you have a disclosure in such a case, the community benefits from having a CVE attached to it. This is for the same reasons that issuing a CVE for any other vulnerability is beneficial. It allows researchers or security practitioners to refer to a common issue.

3. What if there are 3 similar vulnerabilities in a given service during a year? Must a researcher refer to them by disclosure date or by some company advisory disclosure identifier or URL? These things may change over time. A CVE is a fixed, permanent reference point. All vulnerabilities that are significant and enter the realm of public discussion will benefit from having a common identifier attached to them.

4. Vulnerabilities are abstract items. To discuss them, you need to identify them.

5. You can allow for incomplete coverage. Some vendors attach CVEs to their service vulnerability disclosures, using high quality details that make the CVE worth reading. Others choose not to, and that doesn't diminish the CVEs on those that do.

## Con
1. Dilution/counting issues -- flag service IDs so consumers can consider or ignore them?
1. There are often no versions or they are not public -- can maybe use dates?
1. Vulnerabilities in websites would be vague and unverifiable. Hard to know if 2 service CVEs are not the same vuln experienced twice. 
1. An external researcher may have difficulty finding enough details to fully populate a CVE entry. This does not apply to a vendor doing voluntary disclosure, though they may choose to be less than forthcoming, which is still a problem.
1. This could make counting more difficult. But it was widely acknowledged that just counting CVEs is a problematic exercise anyway, fraught with poor conclusions.

## Separate ID Discussion
There were several suggestions about spinning off a separate ID scheme (C\*E) or using some kind of other space partitioning mechanism. Using a field in the CVE was mentioned, as well as carving out a number space (as was done for DWF) for service vulns. A benefit of a separate ID was that people wouldn't mix up the statistics. 

## Specific Examples
Following the advice of Adam Shostack, to "create a zoo" where you can "point at the birds" and "productively debate" real examples, here are some examples of some service-related or vendor-controlled issues that have been disclosed:

1. [Cloudflare]( https://blog.cloudflare.com/incident-report-on-memory-leak-caused-by-cloudflare-parser-bug/) This was mentioned as an example that might require customers to reset passwords and look at third parties who they do business with to swe whether they were affected.
2. [WebEx Browser Extension](https://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-20170717-webex) CVE-2017-6753. This is an example of a cloud-bases service with client-side elements. In this case, the CVE is clearly in the client-side element, and action must be taken by the client to fix or work around it. Customer workarounds include using a different browser, if they choose not to download updated software.
3. [WebEx Meeting Server](https://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-20170118-wms4) CVE-2017-3799. In this case, the service is hosted by Cisco, but the servers for various customers are customized. Thus, they don't all run the same release. Releases are versioned. The fix is a configuration setting. Depending on whether customers have a newer version or not, they can either request that Cisco change the configuration item or (in newer versions) set it themselves in a configuration panel.
4. [WebEx Personal Rooms](https://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-20160526-wmc) CVE-2016-1410. User accounts are subject to enumeration guessing. Names can be exposed in prior meeting invites, because the URL never changes. In many cases, they may be the same as email id's, so they may be easily guessable. Knowledge of these internal names could allow attackers to try to join personal meeting rooms if they are hosted in unlocked personal meeting rooms.
Cisco's fix was to enable logging of these events. A customer could use knowledge of this vulnerability to:
 * Warn their users to always use locked personal meeting rooms (This is a user setting).
 * No longer choose to use personal meeting rooms (there are other meeting room formats available).
5. [WebEx Meeting Access Number Vuln](https://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/Cisco-SA-20150622-CVE-2015-4207) CVE-2015-4207. In this vulnerability, a user might have been able to dial into a web conference call without registering or identifying themselves. While the fix doesn't involve action on a user's part, they may want to take action to secure any information that was disclosed in those meetings. Perhaps URLs or passwords were disclosed that can be changed. 
6. [WebEx Meetings Calendar Download](https://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/Cisco-SA-20150622-CVE-2015-4209). CVE-2015-4209. In this case, .ics (calendar) files for meetings could be accessed by unauthorized users. These could allow attackers into future meetings, some of them perhaps recurring for months. Thus, disclosure to users allows them to cancel the meetings, or to change the access passwords to prevent attacker abuse of those meetings whose details had been disclosed.
