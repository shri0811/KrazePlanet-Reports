## Title
Reflected XSS - Script Tag Filter Evasion
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://feedback.pwnedbox.site/
The Feedback website is vulnerable to Reflected Cross-Site Scripting (XSS) through its GET parameter functionality. The application accepts user-controlled input in the First Name and Last Name fields and reflects the submitted input without proper sanitization or output encoding.

As a result, injected JavaScript executes in the user's browser when the form is submitted.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://feedback.pwnedbox.site/.
2. Locate the First Name and Last Name input fields.
3. Enter the following payload in the input fields:
<script>alert(1)</script>
4. Click the Submit button.
5. Observe that a JavaScript alert box displaying 1 appears.
6. This confirms the presence of Reflected XSS through the GET parameter functionality.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1002" height="671" alt="Screenshot 2026-11-19 181806" src="https://github.com/user-attachments/assets/5c1e5722-9f78-4d65-9b59-45274146a683" />


<img width="612" height="287" alt="Screenshot 2026-11-19 181817" src="https://github.com/user-attachments/assets/ab3f2819-5aee-4322-8316-b8137ef5a904" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Arbitrary JavaScript Execution: An attacker could execute malicious JavaScript in a victim's browser.


Phishing Attacks: Attackers could inject fake login forms to trick users into sharing sensitive information.


Session Hijacking Risk: Session information could be exposed if cookies are not properly protected.


Website Manipulation: Attackers could modify webpage content and display misleading information.


Malicious Redirection: Users could be redirected to untrusted websites.


Unauthorized Actions: Malicious scripts could perform actions using the victim's authenticated session.


User Deception: Attackers could create misleading pop-ups or messages to manipulate users.


Reputation Damage: Successful exploitation could reduce user trust in the website.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate all user-supplied inputs, including fname and lname.


Output Encoding: Encode user-controlled data before displaying it in HTML.


Input Sanitization: Prevent unsafe HTML and JavaScript from being processed.


Content Security Policy (CSP): Implement a restrictive CSP to reduce the risk of script execution.


Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.


Cookie Protection: Enable HttpOnly, Secure, and SameSite attributes for session cookies.


Security Testing: Regularly test all GET parameters and input fields for XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
