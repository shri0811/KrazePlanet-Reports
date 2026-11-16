## Title
Reflected XSS - PubMed: National Library of Medicine Search Builder
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://pubmed.pwnedbox.site/
The PubMed website is vulnerable to Reflected Cross-Site Scripting (XSS). The vulnerability occurs when user-supplied input is reflected in the webpage without proper sanitization or context-aware output encoding.

An attacker could craft malicious input containing JavaScript and trick a victim into interacting with it. When the application processes and reflects this input, the injected JavaScript executes in the victim's browser under the website's origin.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open the affected website: https://pubmed.pwnedbox.site/
2. Locate the search input field.
3. Enter the following payload:

   `<script>alert(1)</script>`

4. Submit the search query.
5. Observe whether a JavaScript alert box displaying `1` appears.
6. If the alert executes, it confirms the Reflected XSS vulnerability.<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="971" height="225" alt="image" src="https://github.com/user-attachments/assets/d54b028d-68a2-44d6-ba87-73ad844b01fb" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Successful exploitation of this vulnerability could allow an attacker to execute arbitrary JavaScript in a victim's browser within the context of the affected website.

Potential consequences include:

- Manipulation of webpage content and appearance.
- Display of misleading information or phishing content.
- Execution of unauthorized JavaScript in a victim's browser.
- Access to information exposed to JavaScript on the affected page.
- Potential unauthorized actions within the application's context, depending on the victim's privileges and security controls.<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Successful exploitation of this vulnerability could allow an attacker to execute arbitrary JavaScript in a victim's browser within the context of the affected website.

Potential consequences include:

- Manipulation of webpage content and appearance.
- Display of misleading information or phishing content.
- Execution of unauthorized JavaScript in a victim's browser.
- Access to information exposed to JavaScript on the affected page.
- Potential unauthorized actions within the application's context, depending on the victim's privileges and security controls.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
