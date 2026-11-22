## Title
Reflected XSS - String Concatenation Bypass
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://portal.pwnedbox.site/
The application is vulnerable to Reflected Cross-Site Scripting (XSS) through the cat URL parameter. By providing specially crafted input, an attacker can bypass the application's existing filtering mechanism using a string concatenation bypass technique.

The application processes the supplied input without properly sanitizing or encoding it before it is interpreted by the browser. As a result, injected JavaScript executes in the context of the application's domain.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected URL: https://portal.pwnedbox.site/

Navigate to the Reflected XSS - String Concatenation Bypass lab.

Identify the cat parameter in the URL.

Modify the parameter with a crafted XSS payload that uses string concatenation and an event-handler-based execution technique.

Submit the crafted URL in the browser.

Observe that a JavaScript alert popup appears displaying the character K.

This confirms that JavaScript execution was achieved through the supplied input.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1226" height="202" alt="Screenshot 2026-11-22 224002" src="https://github.com/user-attachments/assets/85e6adf7-cc64-4599-87e0-0b83894d6cd1" />

<img width="665" height="312" alt="Screenshot 2026-11-22 224008" src="https://github.com/user-attachments/assets/62b39a1f-1d68-46fb-a7b9-a6a5fc7f073d" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could potentially exploit this vulnerability to:

Execute arbitrary JavaScript in a victim's browser.

Perform actions on behalf of an authenticated user.

Modify webpage content and manipulate the user interface.

Access sensitive information available to the page, depending on application security controls.

Conduct phishing attacks by displaying malicious content.

The actual impact depends on the application's security mechanisms and the privileges of the affected user.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper server-side input validation for all user-controlled parameters.

Apply context-aware output encoding before displaying user-supplied input.

Avoid directly inserting untrusted input into HTML or JavaScript contexts.

Use safe DOM methods such as textContent instead of unsafe HTML insertion methods.

Implement a properly configured Content Security Policy (CSP) as an additional security layer.

Use a trusted HTML sanitization library wherever user-generated HTML is required.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
