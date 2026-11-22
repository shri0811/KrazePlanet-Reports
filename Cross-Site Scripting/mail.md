## Title
Reflected XSS - Encoding Bypass Attempts
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://mail.pwnedbox.site/
The application was tested for Reflected Cross-Site Scripting (XSS) through the cat URL parameter. Different encoding and special-character combinations were introduced to check whether the application's input filtering and validation mechanisms could be bypassed.

The testing involved submitting specially crafted input containing encoded characters and HTML-related syntax. The objective was to determine whether the application improperly handles user-controlled input and allows it to be interpreted as executable JavaScript.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected URL: https://mail.pwnedbox.site/

Identify the cat parameter in the URL.

Provide a test value such as riddhi in the parameter.

Modify the parameter using specially crafted encoded characters and XSS-related syntax.

Submit the modified URL in the browser.

Observe how the application processes and handles the supplied input.

Check whether the input is reflected in the webpage and whether JavaScript execution occurs.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1100" height="127" alt="Screenshot 2026-11-22 224742" src="https://github.com/user-attachments/assets/5fd17ec9-ead1-438f-9e06-146492ef0189" />

<img width="602" height="267" alt="Screenshot 2026-11-22 224751 - Copy" src="https://github.com/user-attachments/assets/3160191b-a1ae-4fce-b7c6-27de71092df9" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
If the application allows malicious input to bypass its encoding and filtering mechanisms, an attacker could potentially:

Execute JavaScript in a victim's browser.

Manipulate webpage content.

Perform unauthorized actions using a victim's authenticated session.

Display malicious or misleading content.

Access sensitive information available to the vulnerable page.

These impacts depend on whether script execution is successfully demonstrated and on the application's security controls.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement context-aware output encoding for all user-controlled input.

Validate input on the server side using an appropriate allowlist.

Ensure HTML entities and encoded characters are handled safely.

Avoid inserting untrusted input directly into HTML attributes or JavaScript event handlers.

Use safe DOM methods such as textContent.

Implement a properly configured Content Security Policy (CSP).

Use a maintained HTML sanitization library when accepting user-generated HTML.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
