## Title
Reflected XSS - Path Based
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://path-fetch.pwnedbox.site/
A potential Path-Based Reflected Cross-Site Scripting (XSS) vulnerability was identified in the URL path handling mechanism.

The application extracts the requested URL path using parse_url() and decodes it using urldecode(). Although the fname and lname parameters are protected using htmlspecialchars() with ENT_QUOTES, the extracted $path variable is not HTML-encoded in the provided source code.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Identify that the application processes the URL path.

Navigate to a path containing URL-encoded special characters.

Observe how the application handles and reflects the supplied path.

Inspect the page source or HTTP response to check whether the input is properly encoded.

If executable JavaScript is reflected, verify the behaviour using a harmless JavaScript proof of concept in the authorised testing environment.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="737" height="330" alt="Screenshot 2026-11-22 210540" src="https://github.com/user-attachments/assets/01bd3bd6-1863-4206-b97f-09d4af45811c" />

<img width="1027" height="855" alt="image" src="https://github.com/user-attachments/assets/5590a4a7-0af0-4ed4-899f-c9f3428a63ae" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
If the decoded URL path is reflected into the HTML response without proper output encoding, an attacker may be able to execute malicious JavaScript in a victim's browser.

Potential consequences include:

Manipulation of webpage content.

Performing actions within the victim's authenticated session, subject to application security controls.

Phishing attacks through modified webpage content.

Access to sensitive information exposed to JavaScript in the affected page.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Apply htmlspecialchars() to $path before displaying it in HTML.

Use context-specific output encoding wherever user-controlled data is reflected.

Avoid directly inserting decoded URL paths into HTML.

Validate and sanitise URL path input according to the application's requirements.

Follow secure output-handling practices to prevent Cross-Site Scripting vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
