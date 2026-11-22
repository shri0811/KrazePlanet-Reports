## Title
Reflected XSS - HTML Tag Blacklist Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://board.pwnedbox.site/
The PHP str_ireplace() function is used to remove a predefined list of HTML tag names from the supplied input. The filtering is case-insensitive, meaning it attempts to remove matching tag names regardless of uppercase or lowercase characters.

However, blacklist-based filtering is not a reliable security mechanism because it only blocks predefined patterns and does not guarantee that all potentially malicious HTML or JavaScript input is prevented.

If the filtered input is reflected into the HTML response without proper output encoding, an attacker may be able to bypass the filtering mechanism and execute malicious JavaScript in a victim's browser.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected application: https://board.pwnedbox.site/

Identify the fname and lname GET parameters.

Submit input containing HTML special characters and HTML tag names.

Observe how the application processes the supplied input.

Inspect the HTTP response or page source to identify whether the input is removed, modified, or reflected.

Check whether the filtering mechanism prevents malicious HTML from being interpreted by the browser.

If a bypass is identified, verify JavaScript execution using a harmless proof of concept in the authorised testing environment.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1377" height="302" alt="image" src="https://github.com/user-attachments/assets/9dc01087-40dc-466c-bbcb-deed49140cb6" />

<img width="1117" height="426" alt="image" src="https://github.com/user-attachments/assets/a8d8c275-46ba-4dbb-b9d9-9e2fc3ff3ec6" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
If the blacklist filter can be bypassed and the application reflects untrusted input without proper output encoding, an attacker may be able to execute arbitrary JavaScript in a victim's browser.

Potential impacts include:

Session Hijacking: An attacker may attempt to obtain sensitive session information, depending on cookie security settings.

Account Compromise: Malicious JavaScript could perform unauthorised actions through an authenticated victim's session, subject to application security controls.

Sensitive Information Disclosure: Information accessible to JavaScript within the application's origin could potentially be exposed.

Phishing Attacks: Attackers could modify webpage content or create fake login forms to collect user credentials.

Unauthorised Actions: Malicious scripts could perform actions available to the victim within the application.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Avoid relying on blacklist-based filtering to prevent XSS.

Use htmlspecialchars() with ENT_QUOTES and an explicit UTF-8 encoding when displaying untrusted input in HTML text or appropriate attributes.

Apply context-specific output encoding for HTML, JavaScript, CSS, and URL contexts.

Validate input according to the application's expected format and requirements.

If HTML input is required, use a trusted HTML sanitisation library with an explicit allowlist of permitted elements and attributes.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
