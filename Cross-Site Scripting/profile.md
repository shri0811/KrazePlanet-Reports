## Title
Reflected XSS - Function Name Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://profile.pwnedbox.site/
The Profile website is vulnerable to Reflected Cross-Site Scripting (XSS) through its GET parameters. The application accepts user-controlled input in the First Name and Last Name fields and reflects the input without proper sanitization or output encoding.

The vulnerability allows JavaScript functions such as prompt() to execute when the submitted input is processed by the application.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://profile.pwnedbox.site/.
2. Locate the First Name and Last Name input fields.
3. Enter the following payloads:
First Name:
<script>prompt(1)</script>

Last Name:
<script>prompt(2)</script>
4. Click the Submit button.
5. Observe that a JavaScript prompt dialog displaying 2 appears.
6. This confirms that injected JavaScript is executed through the GET parameter reflection
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="992" height="548" alt="Screenshot 2026-11-20 182029" src="https://github.com/user-attachments/assets/df7af700-2c9e-4583-9c24-ee4c9d2d1f5d" />

<img width="775" height="332" alt="Screenshot 2026-11-20 182038" src="https://github.com/user-attachments/assets/f5f77806-9833-4c76-80ad-381f5552599a" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Vulnerability Type: Reflected Cross-Site Scripting (XSS).

Injection Method: GET Parameter Injection.

Affected Parameters: fname and lname.

Payload 1: <script>prompt(1)</script>

Payload 2: <script>prompt(2)</script>

Observed Result: A JavaScript prompt dialog displaying 2 appears in the browser.

Evidence: Screenshots demonstrate the injected payloads and successful JavaScript execution
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate all user-controlled inputs, including fname and lname.

Output Encoding: Apply context-aware encoding before displaying user input.

Input Sanitization: Prevent unsafe HTML and JavaScript from being processed.

Content Security Policy (CSP): Implement a restrictive CSP to reduce the risk of script execution.

Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.

Cookie Protection: Enable HttpOnly, Secure, and SameSite attributes for session cookies.

Security Testing: Regularly test all GET parameters with different XSS payloads and JavaScript functions
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
