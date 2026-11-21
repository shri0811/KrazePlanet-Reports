## Title
Reflected XSS - Search Filter Bypass
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://kb.pwnedbox.site/
The application is potentially vulnerable to Reflected XSS through its search functionality. During testing, a specially crafted JavaScript payload was entered into the search field. The application failed to properly handle the injected input, resulting in JavaScript execution in the browser.

A browser alert displaying 1 appeared with the domain name kb.pwnedbox.site, confirming that the injected JavaScript was executed in the context of the website.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open https://kb.pwnedbox.site/

Navigate to the search field.

Enter the following payload:

"shri" <><script>alert(1)</script>

Click the Search button.

Observe the JavaScript alert displaying 1.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1346" height="767" alt="Screenshot 2026-11-18 061748" src="https://github.com/user-attachments/assets/2d21a687-9cde-4f6a-bc57-1109f2f4abf6" />

<img width="727" height="317" alt="Screenshot 2026-11-21 224241" src="https://github.com/user-attachments/assets/47526d9c-9073-469c-a45c-f1b4f257cfed" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
JavaScript Execution: Malicious scripts can execute in the browser of users accessing the affected page.

Phishing Attacks: Attackers could display fake login forms to collect user credentials.

Website Manipulation: Page content could be modified to display misleading information.

Information Exposure: Sensitive information accessible to JavaScript could potentially be exposed.

User Trust: Exploitation could affect the reputation and reliability of the website.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate user-supplied search input on the server side.

Output Encoding: Properly encode user input before displaying it in HTML.

Safe DOM Handling: Avoid inserting untrusted input using unsafe methods such as innerHTML.

Content Security Policy: Implement a restrictive CSP to reduce unauthorized script execution.

Secure Coding: Treat all user input as untrusted data.


<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
