## Title
Reflected XSS - Multi-Parameter Script Filter Evasion
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://cookbook.pwnedbox.site/
The Cookbook website is vulnerable to Reflected Cross-Site Scripting (XSS) through its GET parameters. The application accepts user-controlled input in the First Name and Last Name fields and reflects the input without proper sanitization or output encoding.
By using script tags with mixed-case characters, JavaScript execution can be demonstrated through the GET parameter functionality.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://cookbook.pwnedbox.site/.
2. Locate the First Name and Last Name input fields.
3. Enter the following payloads:
First Name:
<script>confirm(1)</script>

Last Name:
<script>confirm(2)</script>
4. Click the Submit button.
5. Observe the JavaScript confirmation dialog displaying 2.
6. This confirms that injected JavaScript is executed through the GET parameter reflection
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="873" height="613" alt="Screenshot 2026-11-19 182606" src="https://github.com/user-attachments/assets/250e2539-1f17-4404-8144-c7abde9b46b8" />

<img width="667" height="222" alt="Screenshot 2026-11-19 182617" src="https://github.com/user-attachments/assets/c1639a3e-fc0e-482a-a2a5-762c4c3a1d89" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Arbitrary JavaScript Execution: Attackers could execute malicious JavaScript in a victim's browser.


Filter Evasion: Inadequate script filtering may allow attackers to bypass weak input-handling mechanisms.


Phishing Attacks: Attackers could inject fake login forms to collect user credentials.


Session Exposure: Sensitive session information could be exposed if cookies are not properly secured.


Website Manipulation: Attackers could modify webpage content and display misleading information.


Malicious Redirection: Victims could be redirected to malicious websites.


Unauthorized Actions: Scripts could perform actions using an authenticated victim's session.


User Trust: Successful exploitation could damage the website's reputation.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
1. Input Validation: Validate all user-controlled GET parameters, including fname and lname.
2. Output Encoding: Apply context-aware HTML encoding before displaying user input.
3. Input Sanitization: Do not rely on simple string filtering or case-sensitive script-tag blocking.
4. Content Security Policy (CSP): Implement a restrictive CSP to reduce the impact of XSS.
5. Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.
6. Cookie Protection: Enable HttpOnly, Secure, and SameSite attributes for session cookies.
7. Security Testing: Regularly test all GET parameters against different XSS payload variations
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
