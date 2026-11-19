## Title
Reflected XSS - FreshCart: Online Grocery Store
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://freshcart.pwnedbox.site/
The FreshCart website is vulnerable to Reflected Cross-Site Scripting (XSS) through its search functionality. The application accepts user input in the search bar and reflects it in the webpage without properly sanitizing or encoding the input. As a result, an attacker can inject malicious JavaScript code that executes in the browser when the search request is processed.
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
JavaScript Execution: An attacker can execute malicious JavaScript in a victim's browser.


Phishing Attacks: Malicious scripts could display fake login forms to steal user credentials.


Session Exposure: Depending on cookie security settings, sensitive session information may be exposed.


Unauthorized Actions: Scripts may perform actions through the victim's authenticated session.


Website Manipulation: Attackers could modify webpage content displayed to users.


User Deception: Victims could be redirected to malicious websites.


Reputation Damage: Successful exploitation could reduce user trust in the FreshCart website.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate search inputs on the server side.


Output Encoding: Properly encode user-controlled data before displaying it in HTML.


Input Sanitization: Remove or neutralize unsafe HTML and JavaScript where rich HTML is not required.


Content Security Policy (CSP): Implement a restrictive CSP to reduce the impact of script injection.


Secure DOM Manipulation: Use textContent instead of innerHTML when displaying search results.


HttpOnly Cookies: Set the HttpOnly flag on session cookies to prevent JavaScript access.


Secure Coding Practices: Follow OWASP XSS prevention guidelines and regularly test search functionality for injection vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
