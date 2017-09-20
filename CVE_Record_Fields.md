# Required CVE Fields
Strict/narrow question is: Do required fields change, and if so, how?

Strongly related: Guidance/semantics for field data.

See also: <https://github.com/CVEProject/automation-working-group/blob/master/cve_json_schema/CVE_JSON_4.0_min.schema>

At least one discussion thread:
<http://common-vulnerabilities-and-exposures-cve-board.1128451.n5.nabble.com/Required-information-for-CVE-entry-submissions-td1046.html#none>

## Current
From CNA Rules 1.1, Appendix B <https://cve.mitre.org/cve/cna/CNA_Rules_v1.1.pdf>

\[CVEID]:

\[PRODUCT]: (includes vendor name)\[VERSION]: (affected, not affected)\[PROBLEMTYPE]: (Sometimes CWE)\[REFERENCES]:\[DESCRIPTION]: (Could include attack type/vectors, impact, components)

## Proposal 1
\[CVEID]:

\[PRODUCT]: (includes vendor name)\[VERSION]: (affected, not affected)\[PROBLEMTYPE]: (Sometimes CWE)
<del>[REFERENCES]:</del> (**Removed**)

<del>[DESCRIPTION]: (Could include attack type/vectors, impact, components)</del> (**Removed**)
\[PUBLICATION DATE]: (**Added**, date public, or timeline of events related to publication)

\[ASSIGNING CNA]: (**Added**, or chain of assigning CNAs if there is a Sub-CNA under a Root doing the assignment)

\[IMPACT]: (**Added**)

