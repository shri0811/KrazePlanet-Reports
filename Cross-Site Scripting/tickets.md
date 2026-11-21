## Title
Reflected XSS - Event Handler Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://tickets.pwnedbox.site/
The application is vulnerable to Reflected XSS through the First Name and Last Name input fields. It does not properly sanitize or encode user-supplied input, allowing injected JavaScript to execute in the browser after submitting the form.
Therefore, improper handling of user input creates a security risk for users interacting with the affected application.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open https://tickets.pwnedbox.site/

Enter the following payloads in the First Name and Last Name fields:

First Name:

"shri" <><Script>\u0063onfirm(1)</Script>

Last Name:

"shri" <><Script>\u0063onfirm(2)</Script>

Click the Submit button.

Observe the JavaScript confirmation pop-ups displaying 1 and 2.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="782" height="375" alt="Screenshot 2026-11-21 222947" src="https://github.com/user-attachments/assets/8d905610-d312-4242-92c3-3fa98b5b5589" />

<img width="675" height="293" alt="Screenshot 2026-11-21 222957" src="https://github.com/user-attachments/assets/effacf59-9e36-431e-96fd-a77d99f329c9" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Execution of malicious JavaScript in users' browsers.

Possible exposure of sensitive information accessible to JavaScript.

Phishing attacks using fake login forms.

Modification of website content.

Potential unauthorized actions on behalf of authenticated users.

Unauthorized Actions: If a victim is authenticated, injected scripts may perform actions using the victim's existing session, depending on application security controls.

User Trust and Reputation: Successful exploitation could affect user confidence and damage the reputation of the website.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Validate all user-supplied input.

Implement context-specific output encoding.

Avoid directly rendering untrusted input as HTML.

Implement a strong Content Security Policy (CSP).

Secure Cookie Configuration: Set session cookies with Http Only, Secure, and appropriate Same Site attributes to reduce session-related risks.

Regular Security Testing: Conduct periodic vulnerability assessments and penetration testing to identify and fix XSS vulnerabilities.

Use Secure Coding Practices: Treat all user-supplied input as untrusted data and ensure it is safely handled throughout the application.

Perform regular security testing to identify XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
