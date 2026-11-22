## Title
Reflected XSS - Case-Insensitive Filter Bypass
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://directory.pwnedbox.site/
The application is vulnerable to Reflected Cross-Site Scripting (XSS) through the First Name and Last Name input parameters.

During security testing, a specially crafted payload containing a mixed-case HTML script tag was submitted through the input fields. The application failed to properly prevent the execution of the injected JavaScript.

The payload uses a mixed-case <ScRiPt> tag, which may bypass case-sensitive filtering mechanisms that only check for lowercase script tags.

<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected website: https://directory.pwnedbox.site/

Locate the First Name and Last Name input fields.

Enter the following payload into the First Name field:

shri'"><ScRiPt>alert("1");</ScRiPt>

Submit the form.

Observe the browser's response.

A JavaScript alert dialog displaying 1 appears.

Repeat the test in the Last Name field to verify whether it is also vulnerable.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1050" height="440" alt="Screenshot 2026-11-22 232522" src="https://github.com/user-attachments/assets/0cd4a893-56c9-456b-aff1-168eb935bf76" />

<img width="1050" height="440" alt="Screenshot 2026-11-22 232522" src="https://github.com/user-attachments/assets/c497f263-a89e-493c-a619-81dfaf2ca1e8" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
Execute arbitrary JavaScript in a victim's browser.

Manipulate webpage content and redirect users to malicious websites.

Display fake login forms to capture user credentials.

Perform unauthorized actions using a victim's authenticated session, depending on application permissions.

Access sensitive information exposed to JavaScript within the application's origin.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper context-aware output encoding for all user-controlled input.

Avoid relying on case-sensitive keyword filtering or blacklist-based validation.

Validate and sanitize input received through the First Name and Last Name parameters.

Use safe DOM methods such as textContent instead of innerHTML.

Prevent untrusted input from being interpreted as executable HTML or JavaScript.

Implement a restrictive Content Security Policy (CSP) as an additional security layer.

Retest all input fields after implementing the security fixes.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
