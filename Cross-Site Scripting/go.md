## Title
Reflected XSS - Shopify
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://go.pwnedbox.site/
During security testing, specially crafted HTML and JavaScript input was injected into the returnTo parameter. The application processed the supplied input without properly handling or encoding the injected HTML content.

A mixed-case <ScriPT> tag containing the JavaScript confirm(1) function was used to test script execution. The browser successfully displayed a confirmation dialog containing the value 1.

This indicates that user-controlled input can potentially be used to execute arbitrary JavaScript in the context of the application's origin
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected website: https://go.pwnedbox.site/

Identify the returnTo parameter in the URL.

Inject the following test payload into the parameter:

shri"><><ScriPT>confirm(1);</ScriPT>

Open the modified URL in the browser.

Observe the browser response.

A JavaScript confirmation dialog displaying 1 appears.

Click OK or Cancel to dismiss the dialog.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->
<img width="600" height="272" alt="Screenshot 2026-11-22 231856" src="https://github.com/user-attachments/assets/7f0ee222-459e-4f83-8ebe-f2dcf5f11ddc" />

<img width="600" height="272" alt="Screenshot 2026-11-22 231856" src="https://github.com/user-attachments/assets/540654f2-a312-4bc0-879f-f77d14446e6b" />

## Impact

Execute arbitrary JavaScript in a victim's browser.

Manipulate webpage content and redirect users to malicious websites.

Display fake login forms to capture user credentials.

Perform unauthorized actions using the victim's authenticated session, depending on application permissions.

Access sensitive information exposed to JavaScript within the application's origin.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation

Implement proper context-aware output encoding for all user-controlled input.

Validate and sanitize the returnTo parameter on the server side.

Avoid directly inserting untrusted input into HTML or JavaScript contexts.

Use safe DOM methods such as textContent instead of innerHTML.

Implement a restrictive Content Security Policy (CSP) to reduce the risk of script execution.

Ensure that user-controlled data is treated as text rather than executable HTML or JavaScript.

If returnTo is intended for redirects, validate it against an allowlist of permitted destinations.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
