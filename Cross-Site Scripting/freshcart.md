## Title
Reflected XSS - FreshCart: Online Grocery Store
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://freshcart.pwnedbox.site/
The FreshCart website is vulnerable to Reflected Cross-Site Scripting (XSS). The vulnerability occurs in the search functionality, where user-supplied input is reflected in the webpage without proper sanitization or output encoding.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://freshcart.pwnedbox.site/.
2. Navigate to the search bar.
3. Enter the following payload:
<script>alert(1)</script>
4. Click on the Search button.
5. Observe that a JavaScript alert box appears, confirming reflected XSS.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="840" height="452" alt="Screenshot 2026-11-19 174722" src="https://github.com/user-attachments/assets/de10e927-5ea1-44ac-a8a9-c1014700c99d" />
<img width="1075" height="305" alt="Screenshot 2026-11-19 174742" src="https://github.com/user-attachments/assets/55b782ac-3550-4bfd-8422-1f5cd202a7c2" />


<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could execute malicious JavaScript in a victim's browser.


It could be used for phishing attacks.


It may lead to unauthorized actions performed through the victim's session.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper input validation and sanitization.


Apply context-aware output encoding.


Implement a strong Content Security Policy (CSP).


Avoid directly inserting untrusted user input into HTML.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
