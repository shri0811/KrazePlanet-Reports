## Title
Reflected XSS - HTML Tag Filter Bypass
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://news.pwnedbox.site/
The application was tested for Reflected Cross-Site Scripting (XSS) by supplying specially crafted input through a URL parameter.

During testing, JavaScript execution was observed in the browser, resulting in a confirmation dialog displaying the value 1.

This indicates that user-controlled input may be processed in an unsafe manner, allowing JavaScript code to execute in the context of the application's origin.

If the input is reflected without proper output encoding, an attacker could potentially craft a malicious URL and trick other users into opening it.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected website: https://news.pwnedbox.site/

Identify the user-controlled URL parameter being processed by the application.

Inject a JavaScript test payload into the parameter.

Open the modified URL in the browser.

Observe the browser-generated JavaScript confirmation dialog.

Verify that the dialog originates from news.pwnedbox.site.

Click OK or Cancel to dismiss the dialog.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="593" height="216" alt="Screenshot 2026-11-22 230547" src="https://github.com/user-attachments/assets/f827e5b7-8f80-4c6c-91cf-865cdf7250d6" />

<img width="1288" height="126" alt="Screenshot 2026-11-22 230536" src="https://github.com/user-attachments/assets/160c462e-f11e-46af-b757-9bcf3da306d0" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Execute malicious JavaScript in a victim's browser.

Manipulate webpage content and redirect users to malicious websites.

Perform unauthorized actions using the victim's authenticated session, depending on available application permissions.

Conduct phishing attacks by displaying fake login forms.

Access sensitive information exposed to JavaScript within the application's origin.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement context-aware output encoding for all user-controlled input.

Validate and sanitize user input on the server side.

Avoid directly inserting untrusted data into HTML or JavaScript contexts.

Use safe DOM methods such as textContent instead of innerHTML.

Implement a Content Security Policy (CSP) to restrict unauthorized script execution.

Avoid relying only on blacklist-based filtering to prevent XSS.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
