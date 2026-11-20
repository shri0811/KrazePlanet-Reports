## Title
Reflected XSS - PUBG
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://assets.pwnedbox.site/
The Assets website is vulnerable to Reflected Cross-Site Scripting (XSS) through its search functionality. The application accepts user-controlled input in the search field and reflects it into the webpage without proper sanitization or output encoding.

By injecting an HTML image element with an onerror event handler, an attacker can trigger JavaScript execution in the browser when the submitted search input is processed.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://assets.pwnedbox.site/.
2. Locate the search bar on the website.
3. Enter the following payload:
<img src=a onerror=alert(1)>
4. Click the Search button.

5. Observe that a JavaScript alert box displaying 1 appears.
6. This confirms successful JavaScript execution through the search functionality.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="707" height="170" alt="Screenshot 2026-11-20 183257" src="https://github.com/user-attachments/assets/b160071d-6f8a-48ef-b226-63727d670500" />

<img width="682" height="245" alt="Screenshot 2026-11-20 183304" src="https://github.com/user-attachments/assets/bbcb8832-d162-44b4-9827-6b1d924becbd" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Vulnerability Type: Reflected Cross-Site Scripting (XSS).

Injection Method: HTML Injection using an Event Handler.

Injection Point: Search Bar.

Payload: <img src=a onerror=alert(1)>

Observed Result: A JavaScript alert box displaying 1 appears in the browser.

Evidence: Screenshots demonstrate the injected payload in the search field and successful JavaScript execution.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate all user-supplied search input on the server side.

Output Encoding: Apply context-aware encoding before displaying user input.

HTML Sanitization: Prevent unsafe HTML elements and event handlers from being executed.

Content Security Policy (CSP): Implement a restrictive CSP to reduce the risk of script execution.

Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.

Cookie Protection: Enable HttpOnly, Secure, and SameSite attributes for session cookies.

Security Testing: Regularly test search functionality against different XSS payloads and HTML event handlers.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
