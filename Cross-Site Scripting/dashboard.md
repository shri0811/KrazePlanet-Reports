## Title
Reflected XSS - URL Encoding Context
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://dashboard.pwnedbox.site/
The application accepts user-controlled input through the fname and lname GET parameters.

During source code analysis, it was observed that the application uses different encoding functions for these parameters. The fname parameter is processed using PHP's htmlspecialchars() function with the ENT_QUOTES flag, whereas the lname parameter is processed using urlencode().
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to ReproduceOpen the affected application: https://dashboard.pwnedbox.site/

Identify the fname and lname GET parameters.

Submit test input through both parameters.

Observe how the application processes the supplied values.

Inspect the HTTP response and page source.

Compare the encoding behaviour of fname and lname.

Check whether the lname value is reflected into the HTML response.

Verify whether any decoding or unsafe output operation occurs before the value is rendered.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="515" height="253" alt="image" src="https://github.com/user-attachments/assets/56510fa3-0d45-4d32-9a40-ddfb6d2286d5" />

<img width="1031" height="777" alt="image" src="https://github.com/user-attachments/assets/f7e0119f-bd48-4246-89ef-9ef82f57867f" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
If the lname parameter is reflected into an unsafe output context and the encoding is bypassed or reversed, an attacker may be able to execute malicious JavaScript in a victim's browser.

Potential consequences include:

Session Hijacking: Attempting to access sensitive session information, depending on cookie security settings.

Account Compromise: Performing unauthorised actions through an authenticated victim's session, subject to application security controls.

Sensitive Information Disclosure: Accessing information exposed to JavaScript within the application's origin.

Phishing Attacks: Modifying dashboard content or displaying fake login forms to collect credentials.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Use context-appropriate output encoding for all user-controlled data.

Replace urlencode() with htmlspecialchars() when displaying untrusted values in HTML text or appropriate HTML attributes.

Use urlencode() only when constructing URL components.

Avoid decoding untrusted input before inserting it into HTML without proper output encoding.

Apply consistent input validation and output-handling practices.

Implement a Content Security Policy (CSP) as an additional security measure.

Review all locations where fname and lname are displayed to identify unsafe output handling.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
