## Title
Reflected XSS - Category Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://shop.pwnedbox.site/
The application is vulnerable to Reflected XSS through the category GET parameter. It does not properly validate or encode user input, allowing injected JavaScript to execute directly in the user's browser. This can affect users visiting a specially crafted URL.
By injecting a JavaScript payload into the URL, an attacker can cause the browser to execute arbitrary JavaScript in the context of the affected website. This could potentially affect users who visit a specially crafted URL.

## Steps to Reproduce
Open https://shop.pwnedbox.site/

Add the following payload to the URL:

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
Affected Parameter: category

Payload:

<script>confirm(1)</script>

Observed Result: A JavaScript confirmation dialog appears, confirming successful script execution through the URL parameter.

Evidence: Screenshots showing the injected URL and confirmation pop-up.

## Impact

Execution of malicious JavaScript in a victim's browser.

Phishing attacks through fake login forms.

Modification of website content.

Potential exposure of sensitive information accessible to JavaScript.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Validate and sanitize user input.

Implement context-specific output encoding.

Avoid inserting untrusted input directly into HTML.

Implement a strong Content Security Policy (CSP).

Conduct regular security testing to prevent XSS vulnerabilities.
