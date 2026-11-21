## Title
Reflected XSS - Script & Img Tag Filter
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://support.pwnedbox.site/
The application is vulnerable to Reflected Cross-Site Scripting (XSS) through the First Name and Last Name input fields. The application accepts user-supplied input containing JavaScript and executes it in the user's browser when the form is submitted.

During testing, JavaScript payloads were entered into both input fields. The application failed to properly sanitize or encode the input, resulting in successful JavaScript execution through browser alert pop-ups.

This vulnerability allows an attacker to inject malicious JavaScript that executes in the context of the affected website.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
1. Open https://support.pwnedbox.site/
2. Enter the following payloads in the First Name and Last Name fields:
 First Name: <SCript>alert(1)</SCript>

Last Name:  <SCript>alert(2)</SCript>

3. Click Submit.
4. Observe two JavaScript alert pop-ups displaying 1 and 2, confirming successful XSS execution.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="695" height="265" alt="Screenshot 2026-11-21 215847" src="https://github.com/user-attachments/assets/2887d71a-47a7-43a7-91d8-5d8cad188446" />

<img width="735" height="241" alt="Screenshot 2026-11-21 215853" src="https://github.com/user-attachments/assets/c9b340e0-59f9-4483-99ad-74588b6d00d3" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->
<img width="932" height="447" alt="Screenshot 2026-11-21 215903" src="https://github.com/user-attachments/assets/025f1ede-e84d-4d13-a6e7-7277f2a9bf5d" />

## Impact
Phishing Attacks: Displaying fake login forms to collect user credentials.

Website Manipulation: Modifying the page content or displaying misleading information.

Unauthorized Actions: Performing actions on behalf of an authenticated user, depending on the application's functionality and security controls.

User Deception: Redirecting users to malicious websites.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate all user-supplied input on the server side.

Output Encoding: Apply context-specific HTML encoding before displaying user input.

Avoid Unsafe HTML Rendering: Do not insert untrusted input directly into HTML using unsafe methods such as innerHTML.

Content Security Policy (CSP): Implement a strong CSP to restrict unauthorized script execution.

Secure Input Handling: Treat all user-supplied data as untrusted and ensure it is safely handled before rendering it in the browser.

Security Testing: Perform regular security testing to identify and fix XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
