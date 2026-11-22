## Title
Reflected XSS - Mixed Security Parameters
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://settings.pwnedbox.site/
The application accepts user-controlled input through the academy URL parameter. During security testing, a specially crafted input containing quotation marks, HTML characters, and a JavaScript script tag was submitted to check whether the application properly validates and encodes user input.

The test was intended to identify whether the supplied input could be reflected into the webpage without proper output encoding, potentially allowing JavaScript execution in a victim's browser.

<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected URL: https://settings.pwnedbox.site/

Identify the academy parameter in the URL.

Modify the parameter by supplying a test input containing quotation marks, HTML characters, and a script tag.

Submit the modified URL in the browser.

Observe how the application processes and displays the supplied input.

Inspect the page source or HTTP response to determine whether the input is reflected.

Check whether the browser executes the injected JavaScript.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="753" height="156" alt="Screenshot 2026-11-22 225944" src="https://github.com/user-attachments/assets/5bba14e5-a0f9-4663-9377-1b592371ab69" />

<img width="753" height="156" alt="Screenshot 2026-11-22 225944" src="https://github.com/user-attachments/assets/590ef4fb-8fa4-49de-aa41-fe027398c554" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
If the application reflects user-controlled input without proper output encoding and allows JavaScript execution, an attacker could potentially:

Execute arbitrary JavaScript in another user's browser.

Perform actions within the victim's authenticated session.

Modify webpage content and display misleading information.

Access sensitive information exposed to scripts within the same origin.

Conduct phishing attacks through manipulated webpage content.

The actual impact depends on the application's security controls and the context in which the input is reflected.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement context-aware output encoding before displaying user-controlled input.

Validate and sanitize incoming parameters on the server side.

Avoid inserting untrusted input directly into HTML or JavaScript contexts.

Use safe DOM methods such as textContent instead of unsafe HTML insertion methods.

Implement a restrictive Content Security Policy (CSP) as an additional security layer.

Avoid relying exclusively on blacklists or script-tag filtering to prevent XSS.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
