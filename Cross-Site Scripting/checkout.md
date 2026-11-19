## Title
Reflected XSS - Multi-Parameter Filter Evasion
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://checkout.pwnedbox.site/
The Checkout website is vulnerable to Reflected Cross-Site Scripting (XSS) through its page GET parameter. The application accepts user-controlled input through the URL and reflects it without proper sanitization or output encoding.

By injecting an HTML element with an event handler, JavaScript execution can be triggered in the browser when the parameter is processed.
Affected Parameter: page,id.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://checkout.pwnedbox.site/.
2. Identify the page GET parameter in the URL.
3. Inject the following XSS payload into the parameter:
<img src=x onerror=alert(1)>
4. Submit the modified URL by pressing Enter.
5. Observe that a JavaScript alert box displaying 1 appears.
6. This confirms successful JavaScript execution through the reflected GET parameter.
   
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1355" height="337" alt="Screenshot 2026-11-18 235834" src="https://github.com/user-attachments/assets/147348dc-4380-4c96-8478-120ca22f9951" />

<img width="778" height="485" alt="Screenshot 2026-11-18 235842" src="https://github.com/user-attachments/assets/c281f85f-597e-4a65-b7fd-ed932edb74b7" />


<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Arbitrary JavaScript Execution: An attacker could execute malicious JavaScript in a victim's browser.


Filter Evasion: Weak input filtering may allow HTML event-handler-based payloads to execute.


Phishing Attacks: Attackers could inject fake login forms to collect user credentials.


Session Exposure: Sensitive session information could be at risk if cookies are not properly secured.


Website Manipulation: Attackers could modify webpage content and display misleading information.


Malicious Redirection: Users could be redirected to untrusted websites.


Unauthorized Actions: Malicious scripts could perform actions through an authenticated victim's session.


User Trust: Successful exploitation could damage the website's reputation.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate the page GET parameter on the server side.


Output Encoding: Apply context-aware encoding before displaying user-controlled input.


HTML Sanitization: Prevent unsafe HTML elements and event handlers from being executed.


Content Security Policy (CSP): Implement a restrictive CSP to reduce the risk of script execution.


Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.


Cookie Protection: Enable HttpOnly, Secure, and SameSite attributes for session cookies.


Security Testing: Regularly test URL parameters with different XSS payloads and encoding variations.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
