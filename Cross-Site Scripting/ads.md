## Title
Stored XSS - Twitter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://ads.pwnedbox.site/
A potential Stored Cross-Site Scripting (XSS) vulnerability was identified in the Ads Platform.

The application appears to execute injected JavaScript in the browser, as demonstrated by a JavaScript confirmation dialog displaying HARI1.

This indicates that user-controlled input may be rendered without proper sanitization or output encoding, potentially allowing malicious scripts to execute when users access the affected content.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://ads.pwnedbox.site/.

Navigate to the affected functionality where user input is submitted.

Enter the JavaScript test payload in the affected input field:

<script>confirm("HARI1")</script>

Submit the input.

Navigate to the page displaying the submitted content.

Observe the JavaScript confirmation dialog displaying HARI1.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1060" height="346" alt="Screenshot 2026-11-23 184810" src="https://github.com/user-attachments/assets/09a8224f-c688-4564-932c-5b54c2df5632" />

<img width="717" height="622" alt="Screenshot 2026-11-23 184845" src="https://github.com/user-attachments/assets/cc8625d0-c442-4788-b1e4-90d9c6fd09d4" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could potentially execute arbitrary JavaScript in the browsers of users accessing the affected content.

Potential consequences include:

Unauthorized actions using an authenticated user's session.

Access to sensitive information available to the application.

Manipulation of page content.

Phishing attacks against platform users.

Redirection to malicious websites.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Validate and sanitize all user-controlled input.

Implement context-aware output encoding.

Avoid unsafe DOM manipulation methods such as innerHTML.

Use textContent for displaying plain text.

Implement a restrictive Content Security Policy (CSP).

Ensure stored user-generated content is safely encoded before rendering.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
