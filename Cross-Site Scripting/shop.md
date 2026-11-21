## Title
Reflected XSS - Category Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://shop.pwnedbox.site/
The application is vulnerable to Reflected XSS through the category GET parameter. The application does not properly sanitize or encode user-supplied input, allowing injected JavaScript to execute in the browser.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open https://shop.pwnedbox.site/

Modify the URL by adding the following payload:

?category=<script>confirm(1)</script>

Press Enter.

Observe the JavaScript confirmation pop-up displaying 1.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1307" height="472" alt="Screenshot 2026-11-18 062137" src="https://github.com/user-attachments/assets/353cd6f4-c00a-4af9-96b7-a19e52181e7b" />

<img width="1197" height="820" alt="Screenshot 2026-11-18 062149" src="https://github.com/user-attachments/assets/55eaddac-e38e-47d5-99ba-31c7da8eaa18" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->
<img width="1392" height="572" alt="Screenshot 2026-11-18 062159" src="https://github.com/user-attachments/assets/e3fdb9e4-152a-483c-96da-63d8321a8ba7" />

## Impact
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->
An attacker could execute malicious JavaScript in a victim's browser.

Phishing attacks through fake login forms.

Modification of website content.

Potential exposure of sensitive information accessible to JavaScript.
## Remediation
Apply proper input validation.

Use context-specific output encoding.

Avoid rendering untrusted input as executable HTML or JavaScript.

Implement a strong Content Security Policy (CSP).

Regularly perform security testing to identify XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
