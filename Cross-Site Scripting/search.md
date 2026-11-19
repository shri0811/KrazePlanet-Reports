## Title
Reflected XSS - Global Site Search Portal
The website is vulnerable to Reflected Cross-Site Scripting (XSS) through its GET parameters. The application accepts user-controlled input in the First Name and Last Name fields and reflects the input into the webpage without proper sanitization or output encoding.

JavaScript injected through these parameters gets executed in the browser when the form is submitted.
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://search.pwnedbox.site/
The website is vulnerable to Reflected Cross-Site Scripting (XSS) through its GET parameters. The application accepts user-controlled input in the First Name and Last Name fields and reflects the input into the webpage without proper sanitization or output encoding.

JavaScript injected through these parameters gets executed in the browser when the form is submitted.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://search.pwnedbox.site/.
2. Locate the First Name and Last Name input fields.
3. Enter the following payloads:
First Name:
<script>alert(1)</script>

Last Name:
<script>alert(2)</script>
4. Click the Submit button.
5. Observe that two JavaScript alert boxes appear, displaying 1 and 2.
6. This confirms that both GET parameters are vulnerable to Reflected XSS.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1057" height="571" alt="Screenshot 2026-11-19 175537" src="https://github.com/user-attachments/assets/209a31bc-7925-44dd-9e19-6b0d680ca35c" />

<img width="635" height="267" alt="Screenshot 2026-11-19 175545" src="https://github.com/user-attachments/assets/4529d0f7-6843-4139-bdf5-e28f3a8034a2" />

<img width="596" height="261" alt="Screenshot 2026-11-19 175552" src="https://github.com/user-attachments/assets/a5eb429f-7fb9-4a4c-ba4b-557b0f83674d" />



<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Arbitrary JavaScript Execution: Attackers can execute malicious JavaScript in a victim's browser.


Session Hijacking Risk: Sensitive session information may be exposed if cookies are not properly secured.


Phishing Attacks: Attackers could inject fake login forms to trick users into revealing credentials.


Website Manipulation: Malicious scripts could modify webpage content and display misleading information.


Malicious Redirection: Users could be redirected to untrusted or malicious websites.


Unauthorized Actions: Attackers may perform actions through an authenticated victim's session.


User Trust: Successful exploitation could damage the website's reputation and user confidence.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
1. Input Validation: Validate all user-supplied GET parameters, including fname and lname.
2. Output Encoding: Encode user input before displaying it in HTML.
3. Input Sanitization: Prevent the execution of injected HTML and JavaScript.
4. Content Security Policy: Implement a restrictive CSP to reduce the risk of script execution.
5. Secure DOM Manipulation: Use textContent instead of unsafe methods such as innerHTML.
6. Cookie Protection: Enable HttpOnly, Secure, and SameSite cookie attributes.
7. Security Testing: Regularly test all input fields and GET parameters for XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
