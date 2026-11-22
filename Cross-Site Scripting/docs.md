## Title
Reflected XSS - Page Heading
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://docs.pwnedbox.site/
The application is vulnerable to Reflected Cross-Site Scripting (XSS) through the q URL parameter.

During testing, specially crafted HTML and JavaScript input was supplied through the q parameter. The application processed the input without properly preventing JavaScript execution.

By injecting a mixed-case <ScriPT> tag containing alert(1), JavaScript execution was successfully triggered in the browser.

This vulnerability could allow an attacker to craft a malicious URL and trick other users into opening it, potentially executing unauthorized JavaScript within the context of the vulnerable website.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open the affected website: https://docs.pwnedbox.site/

Identify the q parameter in the URL.

Inject the following test payload into the parameter:

"shri"><> <ScriPT>alert(1)</ScriPT>

Open the modified URL in the browser.

Observe the browser response.

A JavaScript alert dialog displaying 1 appears.

This confirms that the injected JavaScript has successfully executed.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="743" height="222" alt="Screenshot 2026-11-22 231159" src="https://github.com/user-attachments/assets/0e29f88a-0d61-4df3-9be9-b1c124755051" />

<img width="737" height="233" alt="Screenshot 2026-11-22 231205" src="https://github.com/user-attachments/assets/82138462-619f-46c0-9419-c43506168a44" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could potentially exploit this vulnerability to:

Execute arbitrary JavaScript in a victim's browser.

Manipulate the webpage content and redirect users to malicious websites.

Display fake login forms to steal user credentials.

Perform unauthorized actions using the victim's authenticated session, depending on application permissions.

Access sensitive information available to JavaScript within the application's origin.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper context-aware output encoding for all user-controlled input.

Validate and sanitize input received through the q parameter.

Avoid directly inserting untrusted input into HTML elements.

Use safe DOM methods such as textContent instead of innerHTML.

Implement a Content Security Policy (CSP) to restrict unauthorized script execution.

Ensure that user-controlled data is treated as text rather than executable HTML or JavaScript.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
